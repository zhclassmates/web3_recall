```
/**
 *Submitted for verification at Etherscan.io on 2024-03-19
*/

// SPDX-License-Identifier: MIT
/*
Website: https://fomonetwork.io
Telegram: https://t.me/FOMONetwork
Twitter: https://twitter.com/FOMO_Network
*/

pragma solidity ^0.8.1;  // 设置 Solidity 编译器版本要求

// 地址操作库
library Address {
    // 判断地址是否为合约地址
    function isContract(address account) internal view returns (bool) {
        // 通过检查代码长度来判断
        // 如果是合约，地址的代码长度大于 0
        return account.code.length > 0;
    }

    // 向指定地址转账
    function sendValue(address payable recipient, uint256 amount) internal {
        require(address(this).balance >= amount, "Address: insufficient balance");  // 确保合约有足够余额

        (bool success, ) = recipient.call{value: amount}("");  // 执行转账操作
        require(success, "Address: unable to send value, recipient may have reverted");  // 确保转账成功
    }

    // 调用合约方法
    function functionCall(address target, bytes memory data) internal returns (bytes memory) {
        return functionCallWithValue(target, data, 0, "Address: low-level call failed");  // 默认不传值
    }
    
    function functionCall(address target, bytes memory data, string memory errorMessage) internal returns (bytes memory) {
        return functionCallWithValue(target, data, 0, errorMessage);  // 带自定义错误消息
    }

    // 带 value 的调用合约方法
    function functionCallWithValue(address target, bytes memory data, uint256 value) internal returns (bytes memory) {
        return functionCallWithValue(target, data, value, "Address: low-level call with value failed");  // 默认错误消息
    }

    function functionCallWithValue(address target, bytes memory data, uint256 value, string memory errorMessage) internal returns (bytes memory) {
        require(address(this).balance >= value, "Address: insufficient balance for call");  // 确保合约有足够的余额

        (bool success, bytes memory returndata) = target.call{value: value}(data);  // 执行调用

        return verifyCallResultFromTarget(target, success, returndata, errorMessage);  // 验证调用结果
    }

    // 静态调用（读取操作，不修改状态）
    function functionStaticCall(address target, bytes memory data) internal view returns (bytes memory) {
        return functionStaticCall(target, data, "Address: low-level static call failed");
    }

    function functionStaticCall(address target, bytes memory data, string memory errorMessage) internal view returns (bytes memory) {
        (bool success, bytes memory returndata) = target.staticcall(data);  // 执行静态调用
        return verifyCallResultFromTarget(target, success, returndata, errorMessage);
    }

    // 委托调用
    function functionDelegateCall(address target, bytes memory data) internal returns (bytes memory) {
        return functionDelegateCall(target, data, "Address: low-level delegate call failed");
    }

    function functionDelegateCall(address target, bytes memory data, string memory errorMessage) internal returns (bytes memory) {
        (bool success, bytes memory returndata) = target.delegatecall(data);  // 执行委托调用
        return verifyCallResultFromTarget(target, success, returndata, errorMessage);
    }

    // 验证调用结果
    function verifyCallResultFromTarget(
        address target,
        bool success,
        bytes memory returndata,
        string memory errorMessage
    ) internal view returns (bytes memory) {
        if (success) {
            if (returndata.length == 0) {
                // 如果没有返回数据且调用成功，确保目标地址是合约地址
                require(isContract(target), "Address: call to non-contract");
            }
            return returndata;
        } else {
            _revert(returndata, errorMessage);  // 如果调用失败，回退错误信息
        }
    }

    function verifyCallResult(
        bool success,
        bytes memory returndata,
        string memory errorMessage
    ) internal pure returns (bytes memory) {
        if (success) {
            return returndata;
        } else {
            _revert(returndata, errorMessage);
        }
    }

    // 处理回退错误
    function _revert(bytes memory returndata, string memory errorMessage) private pure {
        if (returndata.length > 0) {
            // 如果返回数据不为空，则回退错误信息
            /// @solidity memory-safe-assembly
            assembly {
                let returndata_size := mload(returndata)
                revert(add(32, returndata), returndata_size)
            }
        } else {
            revert(errorMessage);  // 否则使用自定义错误消息
        }
    }
}

pragma solidity ^0.8.0;

// ERC20 接口，定义了 ERC20 标准的基本操作
interface IERC20 {
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    function totalSupply() external view returns (uint256);  // 查询总供应量
    function balanceOf(address account) external view returns (uint256);  // 查询余额
    function transfer(address to, uint256 amount) external returns (bool);  // 转账
    function allowance(address owner, address spender) external view returns (uint256);  // 查询批准的额度
    function approve(address spender, uint256 amount) external returns (bool);  // 批准额度
    function transferFrom(address from, address to, uint256 amount) external returns (bool);  // 执行从一个地址转账
}

interface IERC20Metadata is IERC20 {
    function name() external view returns (string memory);  // 查询代币名称
    function symbol() external view returns (string memory);  // 查询代币符号
    function decimals() external view returns (uint8);  // 查询代币小数位数
}

// ERC20 合约的实现，继承了 Context、IERC20 和 IERC20Metadata 接口
abstract contract Context {
    function _msgSender() internal view virtual returns (address) {
        return msg.sender;  // 返回发送消息的地址
    }

    function _msgData() internal view virtual returns (bytes calldata) {
        return msg.data;  // 返回消息数据
    }
}

// 实现 ERC20 的主要合约
contract ERC20 is Context, IERC20, IERC20Metadata {
    mapping(address => uint256) private _balances;  // 余额映射
    mapping(address => mapping(address => uint256)) private _allowances;  // 批准额度映射

    uint256 private _totalSupply;  // 总供应量

    string private _name;  // 代币名称
    string private _symbol;  // 代币符号

    // 构造函数，初始化代币名称和符号
    constructor(string memory name_, string memory symbol_) {
        _name = name_;
        _symbol = symbol_;
    }

    // 查询代币名称
    function name() public view virtual override returns (string memory) {
        return _name;
    }

    // 查询代币符号
    function symbol() public view virtual override returns (string memory) {
        return _symbol;
    }

    // 查询代币的小数位数（默认为18）
    function decimals() public view virtual override returns (uint8) {
        return 18;
    }

    // 查询总供应量
    function totalSupply() public view virtual override returns (uint256) {
        return _totalSupply;
    }

    // 查询指定账户的余额
    function balanceOf(address account) public view virtual override returns (uint256) {
        return _balances[account];
    }

    // 转账
    function transfer(address to, uint256 amount) public virtual override returns (bool) {
        address owner = _msgSender();
        _transfer(owner, to, amount);
        return true;
    }

    // 查询指定地址的批准额度
    function allowance(address owner, address spender) public view virtual override returns (uint256) {
        return _allowances[owner][spender];
    }

    // 批准转账额度
    function approve(address spender, uint256 amount) public virtual override returns (bool) {
        address owner = _msgSender();
        _approve(owner, spender, amount);
        return true;
    }

    // 执行转账
    function transferFrom(address from, address to, uint256 amount) public virtual override returns (bool) {
        address spender = _msgSender();
        _spendAllowance(from, spender, amount);
        _transfer(from, to, amount);
        return true;
    }

    // 增加批准额度
    function increaseAllowance(address spender, uint256 addedValue) public virtual returns (bool) {
        address owner = _msgSender();
        _approve(owner, spender, allowance(owner, spender) + addedValue);
        return true;
    }

    // 减少批准额度
    function decreaseAllowance(address spender, uint256 subtractedValue) public virtual returns (bool) {
        address owner = _msgSender();
        uint256 currentAllowance = allowance(owner, spender);
        require(currentAllowance >= subtractedValue, "ERC20: decreased allowance below zero");
        unchecked {
            _approve(owner, spender, currentAllowance - subtractedValue);
        }
        return true;
    }

    // 转账内部实现
    function _transfer(address from, address to, uint256 amount) internal virtual {
        require(from != address(0), "ERC20: transfer from the zero address");
        require(to != address(0), "ERC20: transfer to the zero address");

        _beforeTokenTransfer(from, to, amount);

        uint256 fromBalance = _balances[from];
        require(fromBalance >= amount, "ERC20: transfer amount exceeds balance");
        unchecked {
            _balances[from] = fromBalance - amount;
            _balances[to] += amount;
        }

        emit Transfer(from, to, amount);

        _afterTokenTransfer(from, to, amount);
    }

    // 内部铸币函数
    function _mint(address account, uint256 amount) internal virtual {
        require(account != address(0), "ERC20: mint to the zero address");

        _beforeTokenTransfer(address(0), account, amount);

        _totalSupply += amount;
        unchecked {
            _balances[account] += amount;
        }
        emit Transfer(address(0), account, amount);

        _afterTokenTransfer(address(0), account, amount);
    }

    // 内部销毁函数
    function _burn(address account, uint256 amount) internal virtual {
        require(account != address(0), "ERC20: burn from the zero address");

        _beforeTokenTransfer(account, address(0), amount);

        uint256 accountBalance = _balances[account];
        require(accountBalance >= amount, "ERC20: burn amount exceeds balance");
        unchecked {
            _balances[account] = accountBalance - amount;
            _totalSupply -= amount;
        }

        emit Transfer(account, address(0), amount);

        _afterTokenTransfer(account, address(0), amount);
    }

    // 批准额度内部实现
    function _approve(address owner, address spender, uint256 amount) internal virtual {
        require(owner != address(0), "ERC20: approve from the zero address");
        require(spender != address(0), "ERC20: approve to the zero address");

        _allowances[owner][spender] = amount;
        emit Approval(owner, spender, amount);
    }

    // 支出批准额度
    function _spendAllowance(address owner, address spender, uint256 amount) internal virtual {
        uint256 currentAllowance = allowance(owner, spender);
        if (currentAllowance != type(uint256).max) {
            require(currentAllowance >= amount, "ERC20: insufficient allowance");
            unchecked {
                _approve(owner, spender, currentAllowance - amount);
            }
        }
    }

    // 执行 token 转移前的钩子
    function _beforeTokenTransfer(address from, address to, uint256 amount) internal virtual {}

    // 执行 token 转移后的钩子
    function _afterTokenTransfer(address from, address to, uint256 amount) internal virtual {}
}

abstract contract Ownable is Context {
    address private _owner;

    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

    constructor() {
        _transferOwnership(_msgSender());
    }

    modifier onlyOwner() {
        _checkOwner();
        _;
    }

    function owner() public view virtual returns (address) {
        return _owner;
    }

    function _checkOwner() internal view virtual {
        require(owner() == _msgSender(), "Ownable: caller is not the owner");
    }

    function renounceOwnership() public virtual onlyOwner {
        _transferOwnership(address(0));
    }

    function transferOwnership(address newOwner) public virtual onlyOwner {
        require(newOwner != address(0), "Ownable: new owner is the zero address");
        _transferOwnership(newOwner);
    }

    function _transferOwnership(address newOwner) internal virtual {
        address oldOwner = _owner;
        _owner = newOwner;
        emit OwnershipTransferred(oldOwner, newOwner);
    }
}

```

