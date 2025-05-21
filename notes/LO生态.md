####  cosmos

1. 投资回本率，想象空间
2. ![image-20240201160818539](LO生态.assets/image-20240201160818539.png)
3. ![image-20240201160856525](LO生态.assets/image-20240201160856525.png)
4. d
5. d
6. # Fuel：执行层的并行交易
7. https://www.aixinzhijie.com/media/6812110
8. ![image-20240204225119698](LO生态.assets/image-20240204225119698.png)
9. ![image-20240204225044918](LO生态.assets/image-20240204225044918.png)

#### Celestia 

1. 就是说像 ETH 这样的链大家都知道它是在一条链上面把执行层、结算层还有共识，包括数据的存储这些东西，它都打包在一起了，我们把称为整体的链或者是集成的链，它每一条链都有完整的端到端功能，包括 ETH 也好，像什么 AVAX 这些对吧，它都是这样一种形态的。

2. 以太坊设想了一个以 Rollup 为中心的未来，Rollup 往往比 L1 更昂贵且灵活性更低，但可以彼此共享安全性。相比之下，Cosmos 是一个由称为区域的可互操作主权 L1 组成的生态系统。Cosmos 比 Rollups 更便宜、更灵活，但它们不能彼此共享完全的安全性。

   Celestia 结合了这两个项目的精华，其愿景是将 Cosmos 的主权互操作区域与以 Rollup 为中心并具有共享安全性的以太坊结合起来，提供一个更灵活、更安全、更便宜的公链。

![图像](LO生态.assets/GEmUKYna8AAlHfu.png)

+ 区块链可以分为四个部分： 

  - **执行**：交易执行 
  - **结算**：解决/欺诈证明/其他执行层之间的桥梁 
  - **共识**：就交易顺序达成一致 
  - **数据可用性**：为所有网络参与者提供可访问的数据 

  简单来说，执行就是计算最终分数的地方。新交易被上传，并且这个新状态被广播。解决是纠纷发生的地方。任何与交易有效性相关的分歧都可以在这里解决。正是在这里，[汇总](https://www.coingecko.com/learn/optimistic-vs-zero-knowledge-rollups)之间的大部分变化变得可见：乐观汇总使用欺诈证明，而 ZKrollups 使用有效性证明。共识是对交易顺序的安排和约定。数据可用性是指提供允许任何人验证交易的数据。 

  Celestia 专注于共识和数据可用性，两者齐头并进。数据可用性需要达成共识才能对数据进行排列和排序；否则，历史就无法确定。 

+ Cosmos 共识机制，传输协议， 共识 模块 跨链。
+ Celestia  数据共识网络  这种架构使 Celestia 能够专注于成为可扩展的数据可用性层
+ 他们建立了 Tendermint 和 Cosmos SDK，使人们建立区块链的软件编写变得简单。对于 2，他们建立了 Interchain 标准，如 IBC 和 Interchain 账户，使跨链变得简单。

## 没有 Celestia，以太坊就无法扩展 Rollup https://www.bi123.co/article/3861

以下是解决方案的类型： 

- **侧链**：[侧链](https://ethereum.org/en/developers/docs/scaling/sidechains/)是通过桥连接到以太坊的[EVM兼容区块链。](https://ethereum.org/en/developers/docs/evm/)他们有自己的共识协议和区块参数。
- **Rollups**：[Rollups](https://ethereum.org/en/developers/docs/scaling/layer-2-rollups/)在主以太坊区块链之外执行交易，并将交易数据发送回主以太坊网络。
- **状态通道**：[状态通道](https://ethereum.org/en/developers/docs/scaling/state-channels/)使用多重签名通道来结算各方之间主链上的交易，并将状态发送到主区块链。这些非常安全，但有特定的用例。
- **Plasma**：[Plasma](https://ethereum.org/en/developers/docs/scaling/plasma/)是一个框架，其中有锚定到主以太坊区块链的侧链，它们通过根合约连接到以太坊区块链；该合约记录了当前状态并规定了子链的规则。

***

+ Cosmos 以生态系统为中性来促进区块链协作，强调独立区块链之间的互联性，并使用 Tendermint 整合了共识和执行，提供了一个有凝聚力的环境，这带来的直观负面影响是失去了自身灵活性。通过 Celestia 的模块化方法提供了增强的可扩展性和开发灵活性，并为满足不同应用需求提供了定制解决方案，甚有呼声称 Celestia+Cosmos 才是未来应用链的终极形态。
+ ![img](LO生态.assets/7170434_watermarknone.jpeg)

#### [Celestia：以太坊DA 最大的竞争对手](https://www.coinlive.com/zh/news/celestia-ethereum-da-s-biggest-competitor) https://www.coinlive.com/zh/news/celestia-ethereum-da-s-biggest-competitor

***

在以太坊、Celestia和EigenDA之外，DA市场还有一个被大家忽视的玩家：Covalent。cqt  Oneone 说的项目。

私以为，坎昆升级后模块化公链将成为公链主流范式，而DA层将成为模块化堆栈中竞争最激烈的领域，DA War将如火如荼地上演。而模块化堆栈中的诸协议，将成为24年的一大投资主线。



# Sequencers in Ethereum 以太坊中的排序器 https://blog.bingx.com/blockchain-en/what-are-sequencers-in-ethereum-network/

这里存在一个悖论，DA能力放弃以太坊选低成本的Celestia还容易理解，若layer2把最核心的Sequencer收税权利交给外包，手续费该怎么收，生态项目该怎么激励扶持，会存在一系列后续运维难题https://twitter.com/tmel0211/status/1752523889513791644

espresso、Astria如果发空投的话，会是哪个方向？atom质押者

+ 用户将事务发送到汇总服务器（例如 RPC 服务）
+ 汇总将事务连同该汇总的标识符转发到定序器节点。

- 以太坊 Rollup 网络的采用在 2022 年激增，但仍存在一些有待改进之处。

#### 排序器https://www.aicoin.com/article/342554.html

负责对用户提交的交易进行排序。目前，几乎所有的 Rollup 都依赖于一个单独的排序器。鉴于 Rollup 通过欺诈或有效性证明受益于以太坊的安全性，中心化排序不会造成重大问题。尽管如此，去中心化排序最终还是更优解，因为中心化排序器可能在 MEV 提取或审查方面存在风险。

- 本文将介绍各种去中心化排序器项目，包括：Espresso Sequencer、SUAVE、Polygon PoE、EigenLayer 和 Cosmos ICS。

，中心化排序是几乎所有 L2 网络的规范。甚至两个最大的 Rollup 网络 Optimism 和 Arbitrum 也运行单个排序器来决定所有交易的顺序。中

尽管大多数 L2 项目最终都计划将排序器去中心化，但这需要引入一种新的交易排序共识机制。为多个排序器纳入共识机制不可避免地会损害可扩展性，这违背了 Rollup 的初衷。但是，基于区块链精神去中心化排序确有优势，必然是追求的最终方向。本文探讨了最近为去中心化排序器所做的尝试和努力

本文考察了 Rollup 去中心化的不同思路：Polygon 的 PoE 共识算法直接在 Rollup 网络层面实现去中心化排序，Espresso Systems 的 Espresso Sequencer 和 Flashbots 的 SUAVE 绕道另一层解决问题，EigenLayer 和 Cosmos 的 ICS 利用已经构建了强大安全性的网络验证器集。由于 排序器的去中心化至关重要，来自 Celestia 的 Alex Beckett 在 2022 年 6 月就此主题发表了文章。我想通过简要概述 Alex 的解决方案来结束本文。

第一个是「带领导者选举的无许可 PoS」。在这种方法下，任何人都可以作为 Rollup 排序器参与网络，通过抵押代币并通过领导者选举过程来决定网络的区块生产顺序。如上所述，Espresso Sequencer、EigenLayer 和 Cosmos ICS 都采用了这种方法。

第二个是「通过 MEV 拍卖的无许可 PoS」。不是像上面那样使用领导者选举过程来确定哪个定排序器将创建下一个区块，而是在拍卖过程中出价最高的排序器负责生成区块。Flashbots 的 SUAVE 或前面讨论的 Polygon zkEVM 的 PoE 共识算法采用了类似的方法。

最后，「执行公平排序的许可排序器集」。由于上面讨论的两种解决方案都是无需许可的，任何人只要满足一定的条件就可以参与到排序过程中。另一方面，涉及许可排序器的解决方案是指与受信任的实体以私有方式创建一组排序器。您可以将其视为排序器，收集交易并根据先到先得的方式公平公正地决定订单。然而，这种方法需要信任，不能被视为真正的 Rollup 排序器去中心化解决方案。

尽管 Rollup 网络在 2022 年获得了极大关注，但仍存在相关的重大风险，而去中心化排序器通常被认为是低优先级的风险。尽管如此，实现去中心化排序对于解决审查问题和提高 MEV 提取效率至关重要。随着 2022 年 Rollup 网络的广泛采用，他们处理着越来越庞大的资金，这增加了对提高网络安全性和公平性的需求。希望未来排序器去中心化会有所改进，让用户可以使用更安全、更公平的 Rollup 网络。

***

Rollup路线能杀出重围恰恰因为其既能沿用以太坊DA的安全性，又足够灵活提升TPS的上限，关键是主网Rollup合约可由主网Validators做验证，Layer2的用户还有发起挑战撤回资金的权益。尽管在实际践行过程中部分环节不尽人意，但理论上Rollup方案也算获得了主流的市场共识。

有意思，dAPI预言机服务商 

[@API3DAO](https://twitter.com/API3DAO)

  宣布基于Polygon CDK构建了一条ZK layer2公链 OEV Network。 OEV即预言机可提取价值，意思是清算人在监控到dApps用户仓位临近liquidity清算时，可以参与dAPI3 网络的拍卖，出价最高者即可获得下一个预言机数据Update更新权，从而获得参与清算的MEV利润。 OEV原本类似于Flashbot是针对清算人对dApps用户进行精准清算套利的服务，OEV Network这条layer2公链则要把dApps清算获得的利润返还给dApps协议和协议上的用户，从为小众服务的MEV工具升级成为大众逃避MEV的layer2公链，可算把OEV这种清算机制的“格局”打开了。 似乎，Flashbot 2.0 SUAVE也在规划做类似的事，还是让API3通过模块化的Rollup 发链方式捷足先登了。

***

链下环节包括Sequencer收集并batch交易，会生成ZK SNARK证明和Merkle树等打包同步到主网Calldata，然后链下会把ZK SNARK证明经过Prover系统的验证，将最终的State diff上传到主网，**主网根据State root根再结合Calldata中的区块数据，验证数据的完整性和一致性，最终完成Finality状态确认。**

【Api3相关信息】官推：https://twitter.com/API3DAO

官网：https://api3.org/API3

白皮书：https://drive.google.com/file/d/1b8QsGPCJJC1pQOcg83-knD1IAOIgCtZZ/viewOEV 

litepaper ：https://drive.google.com/file/d/1wuSWSI8WY9ChChu2hvRgByJSyQlv_8SO/editmedium：https://medium.com/@api3

联合创始人medium：https://medium.com/@bbenligiray

融资信息：https://medium.com/api3/api3-closes-seed-round-with-six-major-funds-67677b82ed8b

代币分发情况：https://medium.com/api3/api3-public-token-distribution-event-1acb3b6d94

\- API3的L2有什么特别之处？可以帮助协议DApp们捕获Oracle Extractable Value (OEV)，即“预言机可提取价值”，并将其返回给DApp和用户。- 什么是预言机可提取价值 Oracle Extractable Value (OEV)？MEV的一种。 OEV是预言机由于其作为数据源的特权地位而可以从交易中提取的利润。如在一个借贷协议的清算时刻，预言机可以抢跑，这部分利润API3可以帮协议提前捕获并且返还给协议本身。- 支持什么链上的应用/协议？支持所有API3覆盖的16条链，包括Ethereum、Polygon、Polygon zkEVM、BNB Chain、Optimism、Arbitrum、Avalanche、Base、Kava、Linea、Mantle、Gnosis Chain、Moonriver、Moonbeam、Fantom、Rootstock。- $API3在预言机赛道估值相对较低：3.6 亿美元
官宣文章及OVE介绍：

1.官宣发布OVE网络 https://medium.com/api3/announcing-oev-network-the-zk-rollup-to-capture-all-oracle-extractable-value-b9df4168d1362.Polygon

关于api3使用起cdk的文章 https://polygon.technology/blog/api3-to-launch-a-zk-layer-2-chain-powered-by-polygon-cdk?utm_source=twitter&utm_medium=social&utm_content=api3-cdk-blog3.2022年

发布关于OVE的文章 https://medium.com/api3/oracle-extractable-value-oev-13c1b6d53c5b4.api3

质押信息 https://tracker.api3.org/(staking rewards tracker - note that rewards auto-compound so APY is higher than APR)

5.关于预言机部分，

api优势 https://www.chaincatcher.com/article/20595016.ed

区块日记对Api3的理解 https://twitter.com/Ed_x0101/status/17523501596511113757.



日月小楚对Api3的理解 https://www.theblockbeats.info/news/50449?search=1
测试网络：> Network name: OEV Network Sepolia testnet> 

RPC URL: https://oev-network-sepolia-testnet-rpc.eu-north-2.gateway.fm

> Chain ID: 736160594> Currency symbol: testETH>
>
>  Block explorer URL: https://oev-network-sepolia-testnet-blockscout.eu-north-2.gateway.fm> 
>
> Bridge URL: https://oev-network-sepolia-testnet-bridge.eu-north-2.gateway.fm
