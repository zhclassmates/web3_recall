goat  币安上有合约，

`

```
from solana.rpc.api import Client
import pandas as pd
from solana.publickey import PublicKey

# 配置 RPC 客户端，使用你的 QuickNode URL 或其他 RPC 端点
client = Client("https://ultra-intensive-general.solana-mainnet.quiknode.pro/8ffff402c51f466cf31709de9c4e42ca3aec2b94")

# 替换为 Pump 代币的 mint 地址
token_mint_address = "CzLSujWBLFsSjncfkh59rUFqvafWcY5tzedWJSuypump"

def get_token_holders(token_mint_address):
    holders = []
    # 使用 Solana Token Program 的地址
    token_program_id = PublicKey("TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA")

    # 查询代币的所有持有地址
    response = client._provider.make_request(
        "getProgramAccounts",
        str(token_program_id),
        {
            "encoding": "jsonParsed",
            "filters": [
                {"dataSize": 165},  # Token account的固定大小
                {"memcmp": {"offset": 0, "bytes": token_mint_address}}  # 过滤条件：匹配mint地址
            ]
        }
    )

    if 'result' in response and response['result']:
        for account in response['result']:
            owner = account['account']['data']['parsed']['info']['owner']
            balance = account['account']['data']['parsed']['info']['tokenAmount']['uiAmount']
            holders.append({"address": owner, "balance": balance})
    
    return holders

# 获取代币的持有地址
holders = get_token_holders(token_mint_address)

# 检查是否获取到持有者数据
if holders:
    # 使用 pandas 导出到 CSV 文件
    df = pd.DataFrame(holders)
    df.to_csv("goat_token_holders.csv", index=False)
    print("Token holders data saved to pump_token_holders.csv")
else:
    print("No holders found or error in response.")

```

`
