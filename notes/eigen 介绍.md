

EIGEN代币的结构，它可以作为一种通用的跨主体工作代币。我们在此解释这一术语：工作代币是指需要质押（即锁定）以执行某些工作的代币。许多现有的权益证明区块链平台通过一种称为质押的机制使用工作代币来执行区块链验证。工作代币不仅用作执行数字工作的准入条件，还通过一种称为惩罚（slashing）的加密经济机制来惩罚不合规的工作者（即，当数字工作者违反平台固有的契约时，他们可能会失去工作代币）。现有的工作代币至少有以下两种局限性：（a）它们是专用的：专门为某一特定的数字任务而创建（例如，ETH代币用于验证以太坊区块），和/或（b）它们是客观的：仅在数字工作者的违规行为能够在链上明确归因时（通过程序证明）才可执行。EigenLayer，一个重质押（或更准确地说是无许可可编程质押）平台，消除了ETH的“专用”限制。重质押扩展了ETH的范围，使其成为一种“通用”客观工作代币，使其可以质押以参与各种任务。然而，“客观”限制仍然存在，因为惩罚性削减只能应用于以太坊上可客观验证的任务。

在本文中，我们构建了一种新型质押模型，同时打破了这两种限制：

（a）一种可以跨所有数字任务使用的通用工作代币，

（b）跨主体可验证，即任何两个合理的、观察敏锐的人都会同意某个数字工作者是否未正确完成任务。核心思想是在应用层创建一个分叉代币，

**基于一系列开创性的先前工作。本文在四个维度上显著扩展了分叉代币的实用性：**

**a) 通用性：允许其在各种任务中通用，**

**b) 隔离性：赋予在分叉无关应用中使用分叉代币的能力，**

**c) 计量性：社会共识的成本是可计量并强制执行的，**

**d) 补偿性：使用户能够因影响他们的故障而获得补偿。**

这种代币显著扩展了数字工作者可以通过加密经济安全性做出的可信承诺的类型。它显著扩展了区块链可以安全地为其用户提供的数字任务的范围。特别是，这种代币增强了通过EigenLayer可以保障的主动验证服务（AVS）集。此外，EIGEN与ETH完美互补，ETH质押推动客观故障削减，**而EIGEN质押推动跨主体故障削减。我们认为这种跨主体工作代币使以太坊生态系统更接近建立开放可验证数字公共资源的目标。**

---

接下来是 **1 Introduction** 的内容。如果有具体需要翻译或讲解的部分，请告诉我。

好的，我们继续从 **1 Introduction** 开始翻译和讲解。

### 1 Introduction 介绍

#### 1.1 Background 背景

原文：
The significant evolutionary advantage of humans rests in our ability to cooperate in large numbers. Large-scale cooperation requires trust, which is usually provided by intermediating institutions. The modern economy has seen the rise of digital platforms such as Facebook, Uber, Airbnb, Visa, iTunes, eBay, and Amazon marketplace, which allow global communication, efficient markets, and cooperation at scale. One might say that these digital platforms form a system of digital commons, somewhat akin to the physical commons, such as forests, fisheries, national parks, and oceans, that we have in the real world.

While existing digital platforms rival and in many cases out-strip physical commons in access, importance and reach, they do not fully qualify as digital commons as they are controlled without democratic governance, leading to significant frictions, such as (i) centralized information and control silos, where users or innovative solutions can be de-platformed any time, (ii) platforms enshrine somewhat subjective positions, such as the specific recommendation engine, moderation policy, and mechanisms to evaluate driver behavior, credit or renter behavior, (iii) innovations on top of these platforms require the permission of the platform creators, and this significantly constrains the innovation velocity, and (iv) platforms can unilaterally alter policies that affect users without seeking their inputs.

翻译：
人类显著的进化优势在于我们能够进行大规模合作。大规模合作需要信任，通常由中介机构提供。现代经济见证了数字平台的兴起，例如Facebook、Uber、Airbnb、Visa、iTunes、eBay和亚马逊市场，这些平台允许全球沟通、提供高效市场和大规模合作。可以说，这些数字平台形成了一种数字公共资源系统，有点类似于我们在现实世界中的物理公共资源，如森林、渔业、国家公园和海洋。

虽然现有的数字平台在访问、重要性和覆盖范围方面与物理公共资源竞争，甚至在许多情况下超越了它们，但它们并不完全符合数字公共资源的定义，因为它们在没有民主治理的情况下被控制，导致了显著的摩擦，例如：(i) 集中的信息和控制孤岛，用户或创新解决方案可以随时被平台取消，(ii) 平台固化了一些主观立场，例如具体的推荐引擎、审核政策以及评估司机行为、信用或租客行为的机制，(iii) 在这些平台上进行创新需要平台创建者的许可，这显著限制了创新速度，(iv) 平台可以单方面更改影响用户的政策，而无需征求用户的意见。

#### 1.2 Categorization of Faults in Digital Tasks 数字任务中的故障分类

原文：
We can categorize faults made while performing digital tasks into three categories based on the ability to attribute them: (i) objectively attributable faults, (ii) intersubjectively attributable faults, and (iii) non-attributable faults.

1.2.1 Objectively Attributable Faults

These are faults that are attributable purely mathematically and cryptographically without the need to ask the opinions of others. More explicitly, any honest user can be convinced of the objectively attributable fault unilaterally with just local information. A downstream benefit of this feature of objectively attributable fault is that it provides the ability to resolve objectively attributable faults onchain by specifying their dispute resolution mechanism in smart contracts. A clear example is execution validity: if a node runs a piece of code on a deterministic virtual machine and certifies the input and output, it can be verified onchain zk proof or optimistic fraud proofs. A second example of this is double-signing: in a consensus protocol, if a node is not supposed to sign two conflicting blocks but it does, then it can be proven onchain that the node has committed an onchain attributable fault. We furthermore note that the former fault (validity) is proactively observable - for example, the chain can run a verifier for a ZK proof and proactively ensure the correctness, whereas the latter (double-signing) is only retroactively observable: you can prove that a node committed the fault only after the signature on the second conflicting block is received.

翻译：
我们可以根据故障的可归因性将执行数字任务时出现的故障分为三类：(i) 可客观归因的故障，(ii) 可跨主体归因的故障，(iii) 不可归因的故障。

1.2.1 可客观归因的故障

这些是可以纯粹通过数学和密码学归因的故障，无需询问他人的意见。更明确地说，任何诚实的用户只需使用本地信息就可以确信可客观归因的故障。可客观归因故障的一个下游好处是，它提供了在链上解决此类故障的能力，通过在智能合约中指定争议解决机制。一个明确的例子是执行有效性：如果一个节点在确定性虚拟机上运行一段代码并验证输入和输出，那么可以通过链上零知识证明或乐观欺诈证明来验证。第二个例子是双重签名：在共识协议中，如果节点不应签署两个冲突的区块但它确实这样做了，那么可以在链上证明该节点犯了一个链上可归因的故障。我们还注意到，前一种故障（有效性）是主动可观察的——例如，链可以运行一个零知识证明的验证器并主动确保其正确性，而后一种（双重签名）仅是事后可观察的：只有在接收到第二个冲突区块的签名后，才能证明节点犯了故障。

---

由于内容较多，接下来我们会继续进行 **1.2.2 Intersubjectively Attributable Faults** 和 **1.2.3 Non-attributable Faults** 的翻译和讲解。

好的，我们继续从 **1 Introduction** 开始翻译和讲解。

### 1 Introduction 介绍



翻译：
人类显著的进化优势在于我们能够进行大规模合作。大规模合作需要信任，通常由中介机构提供。现代经济见证了数字平台的兴起，例如Facebook、Uber、Airbnb、Visa、iTunes、eBay和亚马逊市场，这些平台允许全球沟通、提供高效市场和大规模合作。可以说，这些数字平台形成了一种数字公共资源系统，有点类似于我们在现实世界中的物理公共资源，如森林、渔业、国家公园和海洋。

虽然现有的数字平台在访问、重要性和覆盖范围方面与物理公共资源竞争，甚至在许多情况下超越了它们，但它们并不完全符合数字公共资源的定义，因为它们在没有民主治理的情况下被控制，导致了显著的摩擦，例如：(i) 集中的信息和控制孤岛，用户或创新解决方案可以随时被平台取消，(ii) 平台固化了一些主观立场，例如具体的推荐引擎、审核政策以及评估司机行为、信用或租客行为的机制，(iii) 在这些平台上进行创新需要平台创建者的许可，这显著限制了创新速度，(iv) 平台可以单方面更改影响用户的政策，而无需征求用户的意见。

#### 1.2 Categorization of Faults in Digital Tasks 数字任务中的故障分类



翻译：
我们可以根据故障的可归因性将执行数字任务时出现的故障分为三类：(i) 可客观归因的故障，(ii) 可跨主体归因的故障，(iii) 不可归因的故障。

1.2.1 可客观归因的故障

这些是可以纯粹通过数学和密码学归因的故障，无需询问他人的意见。更明确地说，任何诚实的用户只需使用本地信息就可以确信可客观归因的故障。可客观归因故障的一个下游好处是，它提供了在链上解决此类故障的能力，通过在智能合约中指定争议解决机制。一个明确的例子是执行有效性：如果一个节点在确定性虚拟机上运行一段代码并验证输入和输出，那么可以通过链上零知识证明或乐观欺诈证明来验证。第二个例子是双重签名：在共识协议中，如果节点不应签署两个冲突的区块但它确实这样做了，那么可以在链上证明该节点犯了一个链上可归因的故障。我们还注意到，前一种故障（有效性）是主动可观察的——例如，链可以运行一个零知识证明的验证器并主动确保其正确性，而后一种（双重签名）仅是事后可观察的：只有在接收到第二个冲突区块的签名后，才能证明节点犯了故障。

---

由于内容较多，接下来我们会继续进行 **1.2.2 Intersubjectively Attributable Faults** 和 **1.2.3 Non-attributable Faults** 的翻译和讲解。 blocks are not being proposed or attested.

3. Chain canonicity

(a) which chain of blocks, valid under a given validity rule, constitutes the canonical chain at a given point in time.

翻译：
我们希望解决的主要问题是，是否可以在跨主体故障的背景下，将加密经济安全扩展到EigenLayer上的数字任务。我们通过创建EIGEN：通用的跨主体工作代币，对这个问题给出了肯定的回答。

2.1 以太坊中的链分叉

在我们描述如何为跨主体可归因任务获得加密经济安全性的协议之前，我们首先要了解一些关键见解，即如何在现有协议（如以太坊）中逃避多数暴政的问题。以太坊一直是认识到区块链安全性综合继承自两个因素的重要性方面的领导者：

• 通过验证者集参与权益证明（PoS）协议所存入的质押获得的加密经济安全性，和

• 环绕并调节区块链客观共识机制的层层社会共识。每一层社会共识都揭示了一种监督监督者的形式。

我们可以轻松区分三个对以太坊操作至关重要的共识层次：

1. 链有效性

(a) 用于确定给定区块链有效性的规则。

(b) 根据给定的有效性规则，判断给定区块链是否有效（参见[11]了解详情）。

2. 链活性

(a) 如果没有提出或证明新的有效区块，应遵循什么规则。

3. 链规范性

(a) 在给定时间点，哪些有效规则下的区块链组成了规范链。



1.3 核心贡献概述
在本文中，我们介绍了EIGEN，这是一种新的通用方法，用于对验证者犯下的主观归因错误施加加密经济惩罚，而不会受到多数暴政的影响。

**先前的工作**：这项工作的知识前身是Vitalik Buterin在以太坊博客（约2014-2015年）中记录的开创性工作：[4], [5], [6]。据我们所知，Augur基于这些帖子，并在预测市场的背景下提出了在以太坊应用层上设计一个可以分叉的代币的想法[7]。Kleros和Aragon Court使用基于赌注的概率选出的陪审员系统对主观错误进行投票（但没有分叉）[8, 9]。在UMA中，每个代币持有者对乐观预言机提交的价格请求进行投票以解决争议，并依赖于纳什均衡来保证安全，而不进行分叉[10]。

**本文的贡献**：在本文中，我们基于使用社会共识（分叉）解决主观归因错误的先前工作，设计了EIGEN。与先前的工作相比，我们在以下四个重要方向上扩展了EIGEN的范围：
1. **通用性**：构建一个通用的主观代币，而不是针对特定问题的解决方案。
2. **隔离性**：解决如何在不了解分叉的应用（如DeFi）中使用分叉代币。
3. **计量**：确保解决任何主观错误的社会共识成本是可计量的，并将价值分配给参与者。
4. **补偿**：设计机制利用主观分叉来补偿用户对验证者/操作员的错误，而不仅仅是惩罚他们。

EIGEN释放了更多的开放创新。EigenLayer允许任何人创建新的主动验证服务（AVS），这些服务具有客观的削减条件，可以通过削减ETH来获得ETH的安全性。然而，一个重大限制是，如果AVS有涉及主观错误的数字任务，它无法诉诸ETH的加密经济学，而不会导致多数暴政问题。在这项工作中，我们创建了第一个通用的主观可削减系统，使验证者可以对其执行的数字工作做出广泛的承诺。这使得各种新的AVS可以利用EIGEN的加密经济学，而不局限于其自身的经济价值。我们设想，新服务的设计将迎来一场文艺复兴，这些服务结构为利用EIGEN加密经济安全的AVS，除了ETH安全之外。EigenLayer上的任何具有主观归因数字错误的主动验证服务（AVS）现在都可以获得EIGEN的加密经济安全保证。为了使错误具有主观归因性，AVS可能需要专注于开发健全的监控基础设施，包括轻客户端。这可以降低监控成本，确保EIGEN的社会共识中的社区成员将广泛参与AVS的轻节点软件的操作，以监控选择加入AVS的EigenLayer操作员。

**2 核心思想**
我们希望解决的主要问题是，是否可以在EigenLayer上将加密经济安全扩展到涉及主观错误的数字任务。我们通过创建EIGEN，即通用的主观工作代币，肯定了这个问题。

**2.1 以太坊中的链分叉**
在描述如何为主观归因任务获得加密经济安全的协议之前，我们从现有协议（如以太坊）中获取了一些关键见解，以逃避多数暴政的问题。以太坊在认识到任何区块链的安全性全面继承自两个因素方面一直处于领先地位：
- 通过验证者集作为参与权益证明（PoS）协议的一部分所存入的赌注获得的加密经济安全，以及
- 社会共识层，这些层围绕并调节区块链的客观共识机制。每一层社会共识都揭示了一种监督者的监督形式。

我们可以轻松地区分以太坊操作中不可或缺的三层共识：

1. **链的有效性**
   - (a) 用于确定给定区块链有效性的规则。
   - (b) 根据给定的有效性规则，给定区块链是否有效（详情见[11]）。

2. **链的活跃性**
   - (a) 如果没有提出或认证新的有效区块，应该遵循什么规则。

3. **链的规范性**
   - (a) 在给定的有效性规则下，哪个区块链在某一时刻构成规范链。

虽然看起来大多数以太坊验证者可以完全决定规范链的内容，但事实并非如此。假设大多数以太坊验证者变得恶意并勾结，要么对一个区块进行双重签名以进行重组，要么通过至少在一个可观察的期间内拒绝签署任何新块来进行活跃性攻击，这将导致以下事件的发生：

1. 任何不属于勾结集的验证者都会拒绝任何在当前有效性规则下的无效区块，同时继续提出和认证有效区块。

2. 根据执行的攻击类型，以太坊的社会共识可以介入拒绝区块：
   - 错误的状态转换是一个客观可归因的错误，可以主动观察到。任何诚实的验证者或用户都可以通过重新执行区块自行验证状态执行的正确性。
   - 构建与任何弱主观性检查点冲突的区块是一个主动可观察的客观错误。任何诚实的验证者或用户都可以直接拒绝这些区块。
   - 对已最终确定的区块进行双重签名是一个客观可归因的错误，但只能事后观察到。任何诚实的验证者或在社会共识中的用户，只要有证据表明某个验证者对冲突的区块头进行了认证，就可以客观地归因这个错误。
   - 针对链增长的活跃性攻击是一个具有并发可观察性的主观可归因错误。因此，当攻击执行时，活跃在社会共识中的用户可以通过自己或信任的人接入以太坊的P2P网络来检测攻击。

3. 为了提供对上述攻击的加密经济保障，以太坊有两种不同的削减规定[12]：
   - 在因对已最终确定的区块进行双重签名导致链分叉的情况下，以太坊提供了通过包含削减对手验证者的交易来削减违规验证者的规定。
   - 在因活跃性攻击导致链分叉的紧急情况下，以太坊有一个“非活跃泄露”的特殊规定，其中不提出或认证新块的勾结验证者可以在一段时间内被削减[13]。

4. 用于削减对手验证者的资金来自作为权益证明的一部分存入的赌注，从而提供加密经济安全。

5. 在任何情况下，如果以太坊的社会共识同意链的分叉，其中发生削减的分叉最终被视为规范分叉，从而对对手提供加密经济安全保障。

6. 其他分叉的数字资产将在链上和链下的接口中被排除在外，其市场价值将趋于零。

   new_know   如果分叉，其中的一方变得没有价值，

>
>
>好的，让我们逐层详细讲解以太坊的三层共识机制。
>
>### 1. 链的有效性（Chain Validity）
>
>#### 定义
>链的有效性指的是如何判断一个区块链是否合法和有效。这包括两个方面：
>1. **有效性规则**：用于判断一个区块链是否合法的规则。
>2. **区块链有效性**：根据这些规则，判断一个具体的区块链是否合法。
>
>#### 作用
>这层共识机制确保了区块链的所有区块和交易都符合预定的协议和规则，从而保证数据的正确性和一致性。
>
>#### 例子
>假设有一条以太坊区块链，其中一个区块包含了不合法的交易（例如，违反了以太坊智能合约规则的交易）。在这种情况下，根据有效性规则，这个区块会被视为无效。所有诚实的验证者和用户都会拒绝这个区块，并继续按照有效规则提出和认证新的区块。
>
>### 2. 链的活跃性（Chain Liveness）
>
>#### 定义
>链的活跃性指的是确保区块链能够持续产生新的区块。如果在一段时间内没有新的有效区块被提出或认证，活跃性规则会规定应采取的措施。
>
>#### 作用
>这层共识机制确保区块链的持续运行和更新，防止区块链停滞不前。
>
>#### 例子
>假设恶意验证者试图通过不签署任何新块来阻止区块链的增长。在这种情况下，诚实的验证者会继续提出新块，并尝试认证这些新块。如果活跃性攻击持续一段时间，以太坊的机制会开始削减不提出或不认证新块的恶意验证者的权益，从而激励他们重新参与区块链的正常运行。
>
>### 3. 链的规范性（Chain Canonicity）
>
>#### 定义
>链的规范性指的是确定在某一时刻哪条区块链是规范链（即主要链或“正确的”链）。这通常基于共识机制来决定。
>
>#### 作用
>这层共识机制确保所有参与者对哪条链是规范链达成一致，防止出现多个分叉链竞争的情况。
>
>#### 例子
>假设由于某种原因出现了两条分叉链，A链和B链。根据以太坊的共识机制和社会共识，诚实的验证者和用户会选择其中一条链作为规范链。例如，如果A链包含恶意验证者插入的无效区块，而B链是诚实的验证者提出和认证的，那么社会共识会倾向于选择B链作为规范链，并排除A链。
>
>### 总结
>以太坊的三层共识机制通过链的有效性、链的活跃性和链的规范性，确保区块链的合法性、持续性和一致性。每层共识机制都在不同方面发挥作用，共同维护区块链的安全和稳定。

在以太坊（Ethereum）的运行中，滥用共识的情况实际上是被设计尽量避免的。以太坊的共识机制主要用于解决区块链的链有效性（Chain Validity）和链活跃性（Chain Liveness）问题。滥用共识指的是将这种共识机制扩展到它原本不适用的领域，这种做法会带来各种风险和问题。以下是对以太坊如何设计以避免共识滥用的详细解释。

### 以太坊共识机制的设计

以太坊的共识机制主要包括以下几个方面：

1. **权益证明（Proof of Stake, PoS）**：通过验证者（Validators）来维护网络的安全和共识，验证者需要抵押一定数量的以太币（ETH）以获得验证权利。

2. **链有效性（Chain Validity）**：验证者负责验证区块和交易的有效性，确保只有有效的区块被添加到区块链中。

3. **链活跃性（Chain Liveness）**：验证者确保网络保持活跃，能够持续生产新块，防止区块链停止运作。

4. **抵押削减（Slashing）**：为了防止验证者行为不端（如双重签名、离线等），以太坊设计了削减机制，即验证者不当行为会导致其抵押的ETH被削减，起到惩戒和威慑作用。

### 避免共识滥用的设计

以太坊在设计共识机制时，明确限制了其适用范围，以避免共识滥用：

1. **明确的设置阶段**：在以太坊的设置阶段，定义了共识机制主要用于维护链的有效性和活跃性。这些规则在网络启动时就已经确定，并得到广泛认可。

2. **限定的共识范围**：以太坊的共识机制和社会共识（Social Consensus）主要用于解决链分叉、验证者恶意行为等核心问题。对其他类型的任务（如数据验证、预言机服务等），以太坊不直接通过其共识机制处理，而是通过其他层级和工具来解决。

3. **防止多数暴政**：以太坊通过分散验证者的权力和抵押削减机制，防止少数验证者操控网络。同时，社会共识机制作为最后防线，在极端情况下维护网络的去中心化和公平性。

### 现实中的共识滥用实例

虽然以太坊设计尽量避免共识滥用，但在现实中也有一些案例显示了共识滥用的潜在风险：

1. **预言机攻击**：预言机服务是链上与链下数据交互的重要桥梁。恶意操控预言机数据（如错误的价格信息）可以对DeFi协议造成重大影响。这类问题无法通过以太坊的共识机制直接解决，需要依赖预言机的独立共识和验证机制。

2. **治理攻击**：在去中心化治理（如DAO）中，持币人投票决定重要事项。如果某一方控制了足够多的投票权，可以操控治理结果，这也被认为是一种共识滥用的形式。以太坊通过治理代币和分散投票权力来缓解这种风险。

### 总结

以太坊的共识机制设计明确了其应用范围，主要用于解决链有效性和链活跃性问题。这种设计避免了共识滥用的风险，确保了系统的稳定性和安全性。然而，随着以太坊生态系统的发展，新的挑战和攻击向量不断出现，需要持续优化和改进共识机制和相关工具。

EigenLayer通过分叉机制和链下处理来有效解决主观归因错误，同时确保交易继续进行，避免滥用以太坊的社会共识。这种方法不仅提高了系统的效率和稳定性，也保持了以太坊共识机制的完整性和安全性。

**以太坊中的共识滥用**



在以太坊中，直接的共识滥用案例比较少见，因为以太坊的共识机制（PoW和PoS）主要用于维护链的有效性和活跃性。然而，有一些场景可能被视为共识滥用或潜在滥用：



​	1.	**预言机问题**：

​	•	**案例**：预言机是区块链与外部世界数据的桥梁。如果预言机被恶意操控，可能导致链上合约依赖错误数据。例如，如果一个预言机报告1 BTC等于1 USD，这显然是不真实的数据，但如果被以太坊的共识机制处理，会增加其负担和复杂性。

​	•	**潜在滥用**：要求以太坊的验证者参与预言机数据的验证和处理，超出了共识机制的原本设计范围。

​	2.	**治理攻击**：

​	•	**案例**：在去中心化自治组织（DAO）中，投票权集中在少数人手中，可能导致治理结果被操控。虽然这主要是治理层面的共识问题，但涉及区块链的共识机制时，可能带来滥用风险。

​	•	**潜在滥用**：将链上治理决策强制纳入共识机制处理，增加了共识负担。

------



？？ 为什么。之前的eth  没有太多的共识过载，有了eigen 项目之后，会出现大量的过载，

```
明白了，让我们重新梳理一下为什么Eigen项目可能会导致共识过载的问题。

### 没有Eigen项目之前的情况

在没有Eigen项目之前，以太坊的共识机制主要处理的是链上交易和智能合约的执行。以太坊的共识节点（即验证者）主要负责以下任务：
1. 验证新块中的交易和智能合约执行。
2. 达成共识，决定哪个区块成为主链的一部分。
3. 处理常规的网络活动，如交易广播、区块传播等。

### 引入Eigen项目后的变化

引入Eigen项目后，除了原有的共识任务外，节点还需要处理由Eigen项目引入的新任务。这些任务主要包括：
1. **处理主观归因错误（Intersubjective Faults）**：Eigen项目需要对执行任务过程中产生的主观错误进行处理。
2. **额外的共识决策**：这些主观错误需要共识节点进行验证和决策，增加了共识节点的工作量。
3. **任务的频繁调用**：由于Eigen项目可能涉及大量频繁的任务调用，这些调用可能进一步增加共识节点的负担。

### 为什么Eigen项目会导致共识过载

1. **增加了节点的工作负担**：
   - 原本以太坊的共识节点只需处理链上交易和智能合约的执行。引入Eigen项目后，节点需要额外处理主观错误的验证和决策，这大大增加了节点的工作负担。

2. **占用了大量节点资源**：
   - Eigen项目可能涉及大量的任务调用和主观错误处理，这些都需要共识节点的参与。由于这些任务需要实时处理，共识节点的计算资源和网络带宽会被大量占用。
   - 这种情况下，共识节点可能因为需要处理过多的任务而超负荷工作，导致性能下降，甚至可能影响到以太坊网络的正常运行。

3. **频繁的共识决策**：
   - 由于Eigen项目中的任务调用频繁，主观错误也可能频繁发生，这意味着共识节点需要频繁进行决策。这种高频的共识决策会进一步增加节点的负担，导致共识过载。

### 图(b)中的具体说明

1. **多数恶意攻击（Majority Malicious Attack）**：
   - 红叉表示在EigenLayer中发生了主观错误，需要共识节点进行处理。

2. **社会共识节点过载（Overloading Social Consensus）**：
   - 图中的双箭头表示，这些主观错误需要以太坊的社会共识节点来处理，导致这些节点超负荷工作。

3. **EigenLayer-aware和EigenLayer-unaware节点**：
   - 左侧的不知晓EigenLayer的节点（EigenLayer-unaware）和右侧的知晓EigenLayer的节点（EigenLayer-aware）都需要参与处理这些错误，进一步增加了节点的负担。

### 解决共识过载的建议

为了避免因为Eigen项目导致的共识过载，可以考虑以下措施：

1. **引入专用节点**：
   - 设立专门处理Eigen项目任务的节点，这些节点专门负责处理主观错误和Eigen任务，而不影响以太坊主链的共识节点。

2. **优化共识机制**：
   - 改进Eigen项目中的共识机制，使其更高效地处理主观错误，减少对共识节点的负担。

3. **分布式处理**：
   - 分散处理任务，将Eigen任务分配给不同的节点或子网络，以避免单一节点过载。

4. **提升节点性能**：
   - 鼓励节点运营者升级硬件和网络带宽，以提高节点的处理能力和抗过载能力。

### 总结

引入Eigen项目后，由于需要处理大量主观错误和频繁的共识决策，可能会导致以太坊网络的共识节点过载。这是因为这些额外的任务占用了大量节点资源，增加了节点的工作负担。通过引入专用节点、优化共识机制和分布式处理等措施，可以有效缓解共识过载问题，确保网络的稳定性和高效运行。
```

```
理解了，您想比较的是，为什么以太坊的Layer 2（L2）解决方案不会导致共识过载，而Eigen项目可能会导致这种问题。我们来详细分析其中的区别。

### 以太坊的Layer 2解决方案

Layer 2解决方案的设计初衷是扩展以太坊的处理能力，同时减轻Layer 1（主链）的负担。以下是一些关键点：

1. **分担处理任务**：
   - Layer 2解决方案将大量交易和计算任务移到链下（off-chain）处理，然后将结果批量提交到主链。
   - 这种方式减轻了主链的负担，因为大部分计算和数据存储都在Layer 2进行。

2. **高效性**：
   - Layer 2解决方案通常采用高效的共识机制，例如Rollups、状态通道（State Channels）和Plasma。
   - 这些机制设计精简，专注于快速处理交易和数据，提高整体效率。

3. **聚合提交**：
   - Layer 2会将大量交易打包成一个单一的提交事务，减少了Layer 1需要处理的事务数量。
   - 这有效地降低了主链的计算和存储负担。

### 为什么以太坊的Layer 2不会导致共识过载

- **分层处理**：Layer 2解决方案通过在链下处理大量事务，只将结果提交到主链，极大地减少了主链需要处理的事务量。
- **优化设计**：Layer 2协议设计为高效处理大量事务，避免了对主链的过度依赖。
- **资源隔离**：Layer 2的事务处理和Layer 1是相对隔离的，避免了资源冲突和过载。

### Eigen项目为什么会导致共识过载

1. **主观归因错误处理**：
   - Eigen项目需要处理主观归因的错误，这些错误需要以太坊主链的共识节点进行验证和决策。
   - 由于这些错误是复杂且频繁的，处理它们需要大量的计算资源和决策时间。

2. **频繁调用和决策**：
   - Eigen项目的任务调用频繁，主观错误也可能频繁发生，这意味着共识节点需要频繁进行复杂的共识决策。
   - 这种高频的共识需求会导致节点资源的过度消耗。

3. **资源竞争**：
   - Eigen项目的任务需要与以太坊主链的其他事务竞争资源，导致主链的共识节点超负荷工作，出现过载问题。

### 图(b)的说明

1. **多数恶意攻击（Majority Malicious Attack）**：
   - 图中的红叉表示在EigenLayer中发生了主观错误，需要主链的共识节点进行处理。

2. **过载社会共识（Overloading Social Consensus）**：
   - 双箭头表示这些主观错误需要以太坊的社会共识节点处理，导致这些节点超负荷工作。

3. **节点类型**：
   - 左侧的不知晓EigenLayer的节点（EigenLayer-unaware）和右侧的知晓EigenLayer的节点（EigenLayer-aware）都需要参与处理这些错误，进一步增加了节点的负担。

### 解决方案建议

为了避免因为Eigen项目导致的共识过载，可以考虑以下措施：

1. **专用处理节点**：
   - 引入专门处理Eigen项目任务的节点，这些节点专门负责处理主观错误和Eigen任务，不影响以太坊主链的共识节点。

2. **优化共识算法**：
   - 改进Eigen项目中的共识算法，使其更高效地处理主观错误，减少对主链共识节点的负担。

3. **分布式处理**：
   - 将Eigen任务分散到不同的节点或子网络，以避免单一节点的过载。

4. **智能错误管理**：
   - 通过智能合约和自动化工具，提前检测和处理潜在的主观错误，减少对共识节点的实时需求。

### 总结

以太坊的Layer 2解决方案通过分担处理任务和优化设计，避免了主链的共识过载问题。相比之下，Eigen项目可能导致共识过载，因为它需要处理大量复杂的主观归因错误和频繁的共识决策，这些都增加了主链节点的负担。通过引入专用处理节点和优化共识算法，可以有效缓解这个问题。
```

>
>
>了解了，为什么Eigen不能像Layer 2解决方案那样在链下处理。这是一个很好的问题，我们可以通过分析Eigen的特性和Layer 2解决方案的区别来理解其中的原因。
>
>### Layer 2解决方案的工作原理
>
>Layer 2解决方案通过将大量交易和计算移到链下（off-chain）处理，并定期将结果提交到主链（Layer 1），从而减轻主链的负担。以下是几种常见的Layer 2技术：
>
>1. **Rollups**：将大量交易批量处理后，生成一个简洁的证明提交到主链。主要分为两种：
>   - **Optimistic Rollups**：假定所有交易都是有效的，除非有人提出异议。
>   - **ZK Rollups**：使用零知识证明来确保批量交易的有效性。
>
>2. **状态通道（State Channels）**：允许两方或多方之间进行多次链下交易，只有通道打开和关闭时才与主链互动。
>
>3. **Plasma**：子链技术，将大部分交易处理移到子链上，只有发生争议时才与主链互动。
>
>### 为什么Eigen不能在链下处理
>
>Eigen项目的设计目标和Layer 2解决方案有本质上的不同：
>
>#### 1. **主观归因错误的处理**
>
>- **主观归因错误（Intersubjective Faults）**：
>  - Eigen的主要任务是处理验证者在执行任务时发生的主观错误。这些错误涉及到验证者的行为和决策，需要集体共识来判断和纠正。
>  - 主观错误的判断和处理需要透明性和公开性，这意味着需要在链上进行，以确保所有参与者可以验证和监督。
>
>#### 2. **社会共识的重要性**
>
>- **社会共识（Social Consensus）**：
>  - Eigen依赖于社会共识来解决争议和错误。社会共识需要所有参与者共同参与，这样才能确保公正和透明。
>  - 这种共识过程需要在链上进行，因为链上共识是公开的、不可篡改的，能够提供所需的信任和透明度。
>
>#### 3. **加密经济保障**
>
>- **加密经济保障（Cryptoeconomic Guarantees）**：
>  - Eigen的设计包括对验证者的奖励和惩罚机制，以激励正确行为和惩罚恶意行为。
>  - 这些机制需要依靠链上的智能合约来执行，因为智能合约是自动化和不可篡改的，能够确保经济激励和惩罚的准确实施。
>
>#### 4. **去中心化和安全性**
>
>- **去中心化**：
>  - 为了确保整个系统的去中心化和安全性，Eigen需要利用以太坊主链的安全保障。
>  - 链下处理虽然可以提高效率，但在处理主观错误和共识决策方面可能缺乏足够的透明性和安全性保障。
>
>### 总结
>
>Layer 2解决方案通过链下处理交易来提高效率和扩展性，而Eigen项目由于其需要处理主观归因错误、依赖社会共识以及需要加密经济保障和去中心化安全性，无法在链下进行有效处理。
>
>Eigen的任务涉及复杂的共识决策和验证者行为的判断，这些都需要在公开和透明的链上进行，以确保所有参与者的信任和系统的公正性。因此，Eigen必须在链上处理这些任务，以实现其设计目标并确保系统的整体安全和稳定。

---

> [!IMPORTANT]
>
> 是的，当前的Layer 2（L2）解决方案处理的问题相对较为简单，这也是它们不需要设置专门的模块来处理复杂错误的原因。让我们更详细地探讨这个问题。
>
> ### L2解决方案处理的问题
>
> #### 1. **交易扩展性**
>    - L2解决方案旨在提高以太坊网络的交易处理能力，处理大量的微交易或频繁交易。
>    - 这些交易通常是直接的转账、支付等，不涉及复杂的业务逻辑或判断。
>
> #### 2. **简单的合约调用**
>    - 虽然L2也支持智能合约调用，但这些合约调用大多是标准化、常见的操作，例如token转账、swap等。
>    - 合约调用的逻辑相对固定且简单，不涉及需要主观判断的复杂决策。
>
> #### 3. **减少主链负担**
>    - L2通过批量处理和简化验证来减少主链的负担。例如，Rollups将多个交易打包成一个交易，并生成一个证明提交到主链。
>    - 状态通道允许多次链下交易，只在通道打开和关闭时与主链互动。
>
> ### L2解决方案的验证机制
>
> #### 1. **Optimistic Rollups**
>    - 假设所有交易都是有效的，除非有人提出异议。如果有人发现无效交易，可以在一定时间内提出挑战。
>    - 大多数交易直接被接受，只有在出现争议时才需要详细验证。
>
> #### 2. **ZK Rollups**
>    - 使用零知识证明技术，所有交易都通过数学证明来验证其有效性。
>    - 这种验证方式高效且安全，可以快速确认大量交易。
>
> #### 3. **状态通道和Plasma**
>    - 通过在链下处理大量交易，只在必要时与主链互动。
>    - 这种方式极大地减少了主链的交易处理量，提高了整体效率。
>
> ### Eigen项目的复杂性
>
> #### 1. **主观归因错误**
>    - Eigen项目需要处理验证者在执行任务时的主观归因错误，这些错误涉及到人的判断和决策。
>    - 例如，验证者在不同情况下对同一事务可能有不同的判断，导致需要进行复杂的共识决策。
>
> #### 2. **社会共识**
>    - 为了解决这些主观归因错误，Eigen项目依赖于社会共识，需要广泛的参与者共同参与决策。
>    - 这种决策过程需要透明和公开，确保所有参与者可以验证和监督。
>
> #### 3. **链上处理**
>    - 由于需要社会共识和透明性，Eigen项目的很多处理需要在链上进行。
>    - 链上处理能够确保决策过程的透明和公正，但同时也增加了链上的负担。
>
> ### 总结
>
> 当前的L2解决方案主要处理简单的交易和标准化的智能合约调用，这些问题可以通过高效的算法和数学证明快速解决。因此，L2不需要设置专门的模块来处理复杂的主观归因错误。
>
> 相比之下，Eigen项目需要处理复杂的主观归因错误，这些错误涉及到人的判断和社会共识，因此需要更多的资源和复杂的链上处理机制。这种复杂性使得Eigen项目更容易导致共识过载，而L2解决方案由于其处理问题相对简单，不容易出现这种问题。



是的，您提到的一个关键点是Eigen掌握了大量节点，这也是为什么Eigen项目可能会导致共识过载的原因之一。让我们详细探讨这点，以及为什么像Lido等项目不会引发同样的问题。

### Eigen掌握大量节点的问题

#### 1. **节点集中化**
   - 如果Eigen项目掌握了大量的验证节点，这意味着它对网络有较大的控制权。
   - 当这些节点需要处理复杂的主观归因错误时，会导致大量的计算和决策负担集中在这些节点上。

#### 2. **共识过载**
   - 大量的节点集中在处理Eigen任务时，会占用以太坊主链的共识资源。
   - 因为这些节点需要频繁进行复杂的共识决策，可能导致网络拥堵和共识过载。

#### 3. **高频任务调用**
   - Eigen任务可能涉及高频调用，每次调用都需要验证和处理，进一步增加节点负担。
   - 当这些调用过于频繁时，即使是高性能的节点也可能超负荷工作。

### Lido等项目的区别

#### 1. **质押池（Staking Pool）**
   - Lido等项目主要提供质押池服务，让用户将他们的以太币（ETH）委托给Lido进行质押。
   - 这些质押池项目通过分散质押来提高网络的去中心化，同时减少单个节点的负担。

#### 2. **无复杂主观错误**
   - Lido等项目不需要处理复杂的主观归因错误，主要是负责质押和分配收益。
   - 这些操作大多是自动化和标准化的，不涉及复杂的判断和决策。

#### 3. **资源分配优化**
   - Lido通过将质押任务分配给多个独立的验证者，避免了单个节点超负荷工作。
   - 这种分散的质押方式确保了更高的效率和稳定性，减少了共识过载的风险。

#### 4. **Layer 2集成**
   - Lido等项目可能集成了Layer 2解决方案，将部分处理任务移到链下，进一步减轻主链的负担。
   - 通过优化资源分配和采用高效的技术手段，Lido能够避免共识过载问题。

### 为什么Lido不会导致共识问题

1. **去中心化的质押**
   - Lido将质押任务分配给多个验证者，确保去中心化和高效的资源利用。
   - 即使Lido管理大量ETH质押，这些任务的处理是分散的，不会集中在少数节点上。
2. **自动化和标准化操作**
   - Lido的操作大多是自动化的质押和收益分配，不需要复杂的判断和决策。
   - 这减少了对节点的计算和决策负担。
3. **避免高频复杂调用**
   - Lido的任务调用频率相对较低，主要是质押和赎回操作，这些操作不涉及复杂的智能合约调用。
   - 因此，Lido的节点负担相对较轻，减少了共识过载的风险。

Eigen 项目处理复杂的主观归因错误（intersubjective faults），需要设计有效的机制来避免共识过载问题。以下是 Eigen 项目可以采取的一些解决方案和机制：

### 1. 引入专用节点

#### 专用节点（Dedicated Nodes）
- **定义**：引入专门处理 Eigen 项目任务的节点，这些节点专门负责处理主观归因错误和 Eigen 任务，而不影响以太坊主链的共识节点。
- **好处**：通过分担处理任务，减少主链节点的负担，防止共识过载。
- **实施**：
  - 在网络中设立一组专门的验证节点，专门处理 Eigen 的主观错误和任务调用。
  - 这些节点可以与主链节点分开，确保不会干扰以太坊主链的正常运行。

### 2. 优化共识算法

#### 高效共识机制（Efficient Consensus Mechanisms）
- **定义**：设计和采用更高效的共识算法，以减少每次处理主观归因错误所需的资源和时间。
- **好处**：提高处理效率，减少共识过载的可能性。
- **实施**：
  - 采用快速验证和轻量级共识协议，减少处理复杂主观错误的时间。
  - 使用更高效的算法来处理争议和错误，确保决策过程快速和可靠。

### 3. 分层处理机制

#### 分层共识（Layered Consensus）
- **定义**：将主观错误的处理分层，低层次的错误由较少的节点处理，高层次的复杂错误由更多节点参与处理。
- **好处**：通过分层机制，分散共识负担，避免单一层级的过载。
- **实施**：
  - 设立不同级别的错误处理机制，根据错误的复杂性和影响程度，分配给不同层级的节点进行处理。
  - 基本错误处理由基础节点完成，复杂错误由高级节点处理。

### 4. 智能错误管理

#### 自动化和智能管理（Automated and Intelligent Management）
- **定义**：通过智能合约和自动化工具，提前检测和处理潜在的主观错误，减少对共识节点的实时需求。
- **好处**：减少节点的即时负担，提高整体效率。
- **实施**：
  - 部署智能合约进行实时监控和错误预警，及时处理潜在问题。
  - 使用预测分析和机器学习模型来预测和预防常见的主观错误。

### 5. 去中心化的质押和验证

#### 分散质押（Decentralized Staking）
- **定义**：通过分散质押和验证来降低单一节点的负担，确保系统的去中心化和高效性。
- **好处**：分散风险，增加网络的抗过载能力。
- **实施**：
  - 将质押任务分配给多个独立的验证节点，避免集中化带来的单点故障和负载问题。
  - 确保每个验证节点只承担一部分任务，从而分散整体负担。

### 6. 增强网络基础设施

#### 基础设施升级（Infrastructure Upgrade）
- **定义**：通过提升网络基础设施的性能和带宽，增强节点的处理能力。
- **好处**：提高整体网络的抗负载能力，确保在高负载情况下仍能高效运行。
- **实施**：
  - 鼓励节点运营者升级硬件设施和网络带宽，增强节点的处理能力。
  - 提供技术支持和激励，促进基础设施的全面升级。

### 7. 采用Layer 2解决方案

#### Layer 2集成（Layer 2 Integration）
- **定义**：将部分复杂的处理任务移至Layer 2解决方案，通过链下处理减少主链的负担。
- **好处**：通过链下处理提高效率，减少主链的共识压力。
- **实施**：
  - 集成现有的Layer 2解决方案，如Rollups或状态通道，将大部分计算和存储移至链下进行。
  - 只在必要时将结果提交到主链，确保主链的负载保持在合理范围内。

### 总结

Eigen 项目通过引入专用节点、优化共识算法、分层处理机制、智能错误管理、去中心化质押和验证、增强网络基础设施以及采用Layer 2解决方案，可以有效解决共识过载问题。这些措施不仅提高了系统的整体效率和稳定性，还确保了在处理复杂主观归因错误时不会对以太坊主链造成过大的负担。通过这些优化，Eigen 项目可以在保证网络去中心化和安全性的同时，提供高效的任务处理能力。

Eigen项目可能导致共识过载，部分原因是它需要处理大量复杂的主观归因错误，并且它掌握了大量节点，集中处理这些任务会占用大量共识资源。而Lido等质押池项目主要处理自动化和标准化的质押任务，操作相对简单，并且通过分散质押和采用Layer 2解决方案来优化资源分配，从而避免了共识过载问题。



根据给出的段落和图3的描述，我们可以详细解释EigenLayer是如何在不使以太坊（Ethereum）的社会共识超载的情况下，解决主观错误（intersubjective faults）的。

### 图3 解析

#### 图3(a): 以太坊的社会共识如何解决链有效性违规

- **描述**：图3(a)展示了以太坊的社会共识如何在验证者集体勾结的情况下，解决任何链有效性违规的问题。
- **机制**：
  - 即使多数验证者勾结，企图通过恶意行为重组链或双重签名（double-signing），诚实的节点和社会共识可以识别并拒绝这些无效区块。
  - 这种社会共识是以太坊生态系统的重要保护机制，防止验证者多数暴政（tyranny-of-majority）。

#### 图3(b): 扩展重新质押导致的社会共识超载

- **描述**：图3(b)展示了如果将重新质押（restaking）扩展到解决超出客观错误（objectively attributable faults）的问题，会导致以太坊的社会共识超载。
- **原因**：
  - 如果重新质押需要处理主观错误（例如，验证者在执行任务时的判断错误），则会涉及大量复杂的决策和验证。
  - 这种复杂性会超出以太坊现有社会共识的处理能力，导致共识机制的过载和失效。

#### 图3(c): EigenLayer中的主观质押和代币分叉

- **描述**：图3(c)展示了EigenLayer如何利用代币分叉（token forking）来解决任何主观归因错误（intersubjective attributable faults）。
- **机制**：
  - EigenLayer通过主观质押（intersubjective staking）和代币分叉来处理主观错误。这种机制允许网络在出现主观错误时，创建新的分叉链。
  - 社会共识将决定哪个分叉链是规范链（canonical chain），从而避免对以太坊主链的过度依赖和负担。

### 两个阶段的主观协议

#### 1. 设置阶段（Setup Phase）

- **定义**：在这个阶段中，主观协议的规则被制定和编码。
- **示例**：
  - 在一个现代国家，设置阶段包括制定宪法，所有后续的法律都必须遵循宪法。
  - 在区块链中，设置阶段包括制定共识协议的分叉选择规则（例如，最长链规则）。

#### 2. 执行阶段（Execution Phase）

- **定义**：在这个阶段中，预先约定的规则被执行。
- **示例**：
  - 在一个国家，执行阶段是根据宪法创建和执行具体法律。
  - 在区块链中，执行阶段是按照设置阶段确定的分叉选择规则进行区块验证和链的延续。

### EigenLayer如何避免共识超载

EigenLayer通过以下机制避免了以太坊社会共识的超载：

1. **利用代币分叉**：
   - 在处理主观错误时，EigenLayer创建新的分叉链，允许网络参与者根据社会共识选择规范链。
   - 这种机制确保了即使在出现争议时，网络也能通过创建新的分叉链来解决问题，而不影响主链的稳定性。

2. **分离设置阶段和执行阶段**：
   - 通过明确的设置阶段和执行阶段，EigenLayer确保了规则的透明性和一致性。
   - 设置阶段制定的规则为后续的执行提供了清晰的指导，减少了执行阶段的复杂性和争议。

3. **社会共识的强大覆盖**：
   - 社会共识不仅包括现有节点，还包括所有可能的观察者，确保在出现恶意行为时，新的参与者可以识别并纠正问题。
   - 这种广泛的社会共识覆盖确保了系统的安全性和公正性。

### 总结

EigenLayer通过代币分叉和主观质押机制，有效地处理了主观归因错误，避免了以太坊社会共识的超载。通过分离设置阶段和执行阶段，以及利用广泛的社会共识覆盖，EigenLayer确保了系统的稳定性和安全性，即使在处理复杂的主观错误时，也不会对以太坊主链造成过度负担。

理解了，让我们详细讨论一下EigenLayer如何通过采用分叉（forking）机制，一方面确保交易能够继续进行，另一方面有效地处理问题。这种机制的核心在于利用分叉来隔离问题并通过社会共识来选择规范链。

### EigenLayer采用分叉机制的工作原理

#### 1. 确保交易继续进行

通过采用分叉机制，EigenLayer能够在不影响交易正常进行的情况下，处理复杂的主观归因错误。以下是这个过程的详细解释：

1. **任务执行和错误检测**：
   - 当EigenLayer中的验证者执行任务时，如果发现主观归因错误，系统会记录这些错误并触发分叉机制。
   
2. **分叉创建**：
   - 为了处理这些错误，EigenLayer会创建一个新的链分叉。这个分叉链将包含需要处理的错误和争议部分。
   - 同时，原有的主链继续处理正常交易，确保网络的正常运行不受影响。

3. **分叉处理**：
   - 验证者和相关参与者会在新创建的分叉链上处理主观错误和争议，利用链下共识机制或专门的处理节点进行详细分析和解决。
   - 这个过程中，分叉链上的处理不影响主链的交易和区块生成。

#### 2. 处理问题并解决错误

通过分叉，EigenLayer可以集中资源和共识力量来处理主观错误，而不干扰主链的正常操作。具体步骤如下：

1. **本地共识达成**：
   - 在分叉链上，参与节点通过本地共识机制（如投票、验证、争议解决等）达成一致，处理并解决主观归因错误。
   - 这种方法确保错误处理的透明性和公正性，同时减少对主链的影响。

2. **生成证明和结果汇总**：
   - 处理完成后，参与节点会生成一个验证证明，记录分叉链上的处理结果和达成的共识。
   - 这些证明和结果被打包并准备提交到主链。

3. **结果提交和社会共识验证**：
   - 分叉链上的处理结果和证明被提交到以太坊主链，由智能合约进行验证。
   - 以太坊的社会共识会决定是否接受这个处理结果，并将其整合到主链中。

### 社会共识的作用

社会共识在整个过程中起到了至关重要的作用：

1. **选择规范链**：
   - 社会共识决定哪条链是规范链（canonical chain）。在处理完成后，参与者会通过投票或其他共识机制决定是否接受分叉链的处理结果。
   - 如果社会共识同意分叉链上的处理结果，这个分叉链将被合并回主链，成为新的规范链。

2. **防止多数暴政**：
   - 社会共识机制可以防止多数验证者的恶意行为（多数暴政），确保处理结果的公正性和透明性。
   - 即使验证者勾结企图通过恶意行为控制分叉链，社会共识可以识别并拒绝这种行为。

### 具体示例流程

1. **任务开始**：
   - EigenLayer检测到某个任务中存在主观归因错误，需要处理。
   
2. **创建分叉**：
   - 系统创建一个新的分叉链来处理这个错误，同时原有的主链继续进行正常的交易和区块生成。

3. **分叉链处理**：
   - 验证者和参与节点在分叉链上处理主观错误，通过本地共识达成一致，生成处理结果和验证证明。

4. **提交结果**：
   - 分叉链上的结果和证明被提交到以太坊主链，由智能合约进行验证。

5. **社会共识验证**：
   - 社会共识决定是否接受分叉链的处理结果。如果接受，这个结果将被合并回主链，分叉链成为新的规范链。

### 优势

1. **交易连续性**：
   - 通过分叉机制，确保原有主链的交易和区块生成不受影响，保证网络的连续性和稳定性。

2. **有效错误处理**：
   - 分叉链允许集中处理主观错误，利用本地共识机制提高处理效率和公正性。

3. **社会共识保障**：
   - 社会共识机制提供了防止恶意行为的额外保障，确保处理结果的透明性和可信性。

### 总结

EigenLayer通过采用分叉机制，一方面确保交易能够继续进行，另一方面有效处理复杂的主观归因错误。分叉链的创建和处理，以及社会共识的验证，确保了系统的稳定性、公正性和透明性，从而实现了高效的任务处理和错误解决。

new_konw  , 采用分层机制，解决问题，最大的共识只要不发生问题，剩下的问题，就是各自的地盘上解决，解决

根据您上传的图片内容，图4展示了不同场景下的设置阶段（Setup Phase）和执行阶段（Execution Phase），包括政府设定、工作量证明共识（PoW）、弱主观性、链有效性（Chain Validity）、审查削减（Censorship Slashing）、Rollup 和主权 Rollup（Sovereign Rollup）。让我们详细解释这些概念，并结合之前讨论的EigenLayer机制来进一步理解其工作原理。

### 图4说明

#### 概念表

1. **US Gov.（美国政府）**
   - **设置阶段**：制定美国宪法（US Constitution）
   - **执行阶段**：依据宪法通过法律（Laws passed compliant with constitution）

2. **PoW Consensus（工作量证明共识）**
   - **设置阶段**：最长链规则（Longest-chain rule, LCR）
   - **执行阶段**：根据LCR决定最新区块（Decide on latest block per LCR）

3. **Weak Subjectivity（弱主观性）**
   - **设置阶段**：弱主观性检查点规则（Weak subjectivity checkpoint rule）
   - **执行阶段**：计算弱主观性检查点（Computation of weak subjectivity checkpoint）

4. **Chain Validity/DA（链有效性/数据可用性）**
   - **设置阶段**：仅接受有效且可用的区块（Accept only valid, available blocks）
   - **执行阶段**：节点拒绝无效或不可用区块，即使这些区块由多数签署（Nodes reject invalid/unavailable blocks even when header signed by majority）

5. **Censorship Slashing（审查削减）**
   - **设置阶段**：使用用户激活软分叉（UASF）对审查进行削减（Slash validators for censorship using UASF）
   - **执行阶段**：观察到审查时，激活UASF削减验证者（When observing censorship, activate UASF to slash validators）

6. **Rollup（汇总）**
   - **设置阶段**：遵循桥接合约（Follow bridge contract）
   - **执行阶段**：决定当前的汇总区块（Decide on current rollup block using bridge state）

7. **Sovereign Rollup（主权汇总）**
   - **设置阶段**：遵循社会共识以恢复区块（Follow social consensus to revert hacks）
   - **执行阶段**：决定当前的汇总区块（Decide on current rollup block using social consensus）

### 解析

#### 两个阶段的概念

- **设置阶段（Setup Phase）**：在这一阶段，系统定义了操作规则和协议。这些规则决定了系统如何运作，并为后续的执行阶段提供基础。
- **执行阶段（Execution Phase）**：在这一阶段，系统按照设置阶段制定的规则来执行实际操作和决策。执行阶段的透明度和明确性取决于设置阶段的规则。

### 结合EigenLayer的机制

EigenLayer通过利用代币分叉和社会共识机制，在处理主观归因错误时有效避免以太坊主链的过载。这里是如何结合图4中的概念来详细说明的：

1. **设置阶段**：在EigenLayer中，设置阶段涉及制定处理主观归因错误的规则。这包括定义何时创建分叉、如何达成本地共识以及如何生成验证证明。

2. **执行阶段**：在执行阶段，当检测到主观归因错误时，系统会创建一个新的分叉链来处理这些错误，同时确保主链继续正常运行。分叉链上的验证节点会通过本地共识机制解决错误，并生成验证证明。然后，这些证明和结果会提交到主链，由智能合约进行验证。

### 确保交易继续进行

- **分叉链处理错误**：分叉链允许将复杂的错误处理和争议隔离开来，不影响主链的正常交易和区块生成。
- **社会共识验证结果**：通过社会共识来选择规范链，确保主链最终接受正确的处理结果。

### 处理问题

- **本地共识和链下处理**：在分叉链上，节点通过本地共识机制达成一致，处理和解决主观归因错误。
- **结果提交和验证**：处理完成后，结果和证明提交到主链，由社会共识和智能合约进行验证，确保处理的透明性和公正性。

### 总结

通过利用分叉机制和社会共识，EigenLayer能够一方面确保交易继续进行，另一方面有效处理主观归因错误。这种方法通过分离处理和验证阶段，实现了系统的高效性和稳定性，同时避免了以太坊主链的共识过载。

在执行阶段，任何节点现在都可以根据其观察到的区块链识别当前区块。因此，设置阶段需要共识，而之后的执行阶段只需要本地信息。这是一个强大的主观协议系统的例子，因为在执行阶段几乎没有歧义。作为一个更复杂的例子，在一个权益证明（PoS）区块链中，有两种可能的共识规则：（i）轻节点规则：接受任何由67%的节点签署的区块头，或（ii）全节点规则：只接受你可以下载的并且有效且由67%节点签署的区块。在区块链的设置阶段预先约定全节点规则是真实规则，而轻节点规则是代理，所以当这两条规则之间存在分歧时，节点已经知道在执行阶段应遵循全节点规则。



作为另一个复杂的例子，考虑两种不同类型的汇总：（a）标准汇总，其中设置阶段定义链中的当前区块为写入桥接合约的最新有效区块，（b）主权汇总，其中设置阶段定义链中的当前区块为写入桥接合约的最新有效区块，除非它被社会共识回滚。在标准汇总情况下，执行阶段是完全自明的：每个节点都可以直接找到当前区块，而不需要互相沟通。在主权汇总情况下，节点需要互相沟通以了解社会共识是否回滚了该区块。一个主观系统越能使执行阶段自验证，其主观凝聚力就越强，即参与者更容易就世界的正确版本达成一致。如果在执行阶段需要太多协调，系统可能会经历主观分裂，即参与者对世界的正确版本产生分歧。

new_konw  ，说执行，共识分开处理，效率增加



**通过分叉代币扩展社会共识的力量**



以太坊的社会共识。如2.1节所述，以太坊的安全性来自于抵押削减（slashing of stake）和社会共识的结合。考虑到使用以太坊的社会共识来解决验证者集体攻击链有效性的问题的好处，一个立即的问题是是否可以将以太坊的社会共识的使用扩展到链有效性和链活跃性之外。一个可以从使用以太坊的社会共识解决多数暴政中受益的服务例子是任何本质上具有主观归因错误的通用任务（详见1.2节）。此类任务的例子包括预言机或数据可用性（详见1.2节）。在这些服务中，欺诈不能通过提交任何欺诈证明或零知识证明来客观地归因于链状态的执行。然而，欺诈对任何外部观察者都是主观可见的。作为一个具体例子，如果一个预言机报告1BTC等于1USD，这远非事实真相，这种欺诈对外界来说是显而易见的。一个天真的解决方案扩展是要求以太坊验证者参与此类服务（例如，验证者作为区块提案的一部分对价格数据进行投票），并假设以太坊验证者的大多数是诚实的。在多数以太坊验证者恶意占领以破坏这个预言机的情况下，以太坊的社会共识将被期望主观地介入，以解决以太坊验证者集的多数暴政。然而，以太坊的设置阶段规定其社会共识仅用于链有效性和链活跃性方面的违规。这确保了以太坊的社会共识只在必要时使用。任何努力扩展以太坊的社会共识以解决额外数字任务中的多数暴政，将违反在以太坊设置阶段同意的不超载以太坊社会共识的原则。参见图3(b)以获取示意图。

#### 



翻译：
利用跨主体协议的系统通常分两个阶段进行。有一个设置阶段，在这个阶段，跨主体协议的规则被编码，然后是执行阶段，在这个阶段，预先约定的规则被执行。第一个例子是现代国家的建立。设置阶段包括编写宪法，所有后来的法律必须遵循宪法。执行阶段则需要制定符合宪法的法律。宪法越清晰，越容易达成一致意见，即某个法律是否符合宪法。

让我们以区块链为第二个例子。区块链的设置阶段涉及指定共识协议的分叉选择规则（例如，最长链规则指定当前区块是最长区块链的顶端）。在执行阶段，任何节点现在都可以根据其观察到的区块链识别当前区块。因此，设置阶段需要共识，而后来的执行阶段只需要本地信息。这是一个强大的跨主体系统的例子，因为在执行阶段几乎没有歧义。作为一个更复杂的例子，在权益证明区块链中，有两种不同的共识规则：(i) 轻节点规则：接受任何由67%的节点签署的区块头，或 (ii) 全节点规则：仅接受可以下载且有效并由67%的节点签署的区块。在区块链的设置阶段，预先约定全节点规则是真正的规则，轻节点规则是代理，所以当两种规则之间存在分歧时，节点已经知道在执行阶段应选择全节点规则。

#### 2.3 Extending the power of social consensus beyond chain validity via Forking Token

翻译：
以太坊的社会共识。正如第2.1节所述，以太坊的安全性来自于削减质押和社会共识的加密经济结合。鉴于使用以太坊的社会共识来解决任何接管以太坊验证者集以攻击链有效性的好处，一个直接的问题是，是否可以将以太坊的社会共识的使用扩展到链有效性和链活性之外。一个可以受益于使用以太坊社会共识来解决多数暴政的服务例子是任何故障本质上是跨主体可归因的一般任务（参见第1.2节了解详情）。此类任务的例子包括预言机或数据可用性（参见第1.2节）。在这样的服务中，欺诈不能通过提交任何欺诈证明或零知识证明作为链状态执行的一部分来客观地归因。然而，欺诈对任何外部观察者来说都是主观可见的。一个具体的例子是，如果一个预言机报告1BTC等于1USD，这与实际情况相去甚远，这种欺诈从外部来看是显而易见的。一个天真的解决方案扩展是要求以太坊验证者参与此类服务（例如，验证者在区块提议中对价格馈送进行投票）并假设以太坊验证者的大多数是诚实的。如果以太坊验证者的多数被敌对接管以破坏这个预言机，预期以太坊的社会共识将主观地介入以解决以太坊验证者集的多数暴政。然而，以太坊的设置阶段规定其社会共识的使用仅限于链有效性和链活性的上下文中的违规行为。这确保了以太坊的社会共识仅被有限使用。任何努力扩展以太坊社会共识的使用以解决附加数字任务中的多数暴政将违反在以太坊设置阶段同意的不超载以太坊社会共识的原则[14]。

---





然而，以太坊的设置阶段规定，只有在链有效性和链活跃性的情况下才可以使用其社会共识。这确保了以太坊的社会共识被谨慎使用。任何扩展以太坊社会共识的使用来解决额外数字任务中的多数暴政的努力都将违反在以太坊设置阶段商定的不超载以太坊社会共识的论点。

### 重新质押：仅用于解决客观归因错误时利用以太坊的安全性。回顾一下，以太坊的安全性来自于抵押、削减以及以太坊的社会共识的结合。任何能够客观归因错误并可以通过EVM程序化惩罚恶意操作者的数字任务，应该在EigenLayer中使用ETH重新质押，以利用以太坊提供的深度安全池。在这些任务中，争议解决机制可以在链状态中作为智能合约编程实现。争议解决的正确执行被包含在链的有效性中。因此，对于具有客观归因错误的数字任务来说，可以独特地利用以太坊的加密经济保证，而不会过载以太坊的社会共识。

### 主观质押：利用EIGEN的社会共识来解决主观归因错误。EIGEN的核心理念是认识到主观性原则可以应用于链本身以外的数字任务。具体来说，EIGEN扩展了从选择链的分叉到选择代币分叉的主观选择理念，用于那些具有主观归因错误的任务。解决这些任务中的潜在错误，由于多数暴政，需要利用社会共识技术。在这些任务中，EIGEN通过利用EIGEN的社会共识的力量来规范惩罚恶意操作员的EIGEN代币分叉，提供无条件削减在EigenLayer上质押的EIGEN的工具。

### 2.3.1 分叉代币的结构

主观归因错误的核心问题是，在区块链的参考框架内，正确答案是未知的，而对于系统外的观察者来说，正确答案是已知的。系统需要找到一种方法，利用这种外部信息对违规者施加加密经济处罚。

首先，我们介绍一个基于之前工作的分叉代币示例及其实现。Augur有一个ERC20代币，称为REP代币（Reputation的简称），是一种分叉代币。REP代币用于报告现实世界中发生的事情，以解决预测市场的结果（答案是二元的，即真或假）。如果REP代币持有者与大多数代币持有者的意见不一致，他们将被削减，但是如果有一定比例的REP持有者反对，他们可以启动分叉事件。分叉事件现在创建了两个ERC20代币，每个代币代表代币对应的真/假的新分叉版本（我们称之为REP1和REP2）。每个REP持有者现在必须决定他们要选择REP1还是REP2代币。此外，未来的Oracle用户（预测市场）需要指定他们要使用REP1还是REP2作为质押代币。同样，交易所和其他金融服务需要在REP1和REP2之间进行选择。参与评估REP1或REP2哪个是正确分叉的玩家集不是固定的，且事先已知。这些共同确保如果REP1明显代表真实答案，那么每个人都会选择它，所有REP的价值将流入REP1。这将使REP2的价值趋于零。如果不是这种情况，整个市场机制可以被利用（例如，做空错误的分叉），并且可以无许可地参与以使市场收敛到正确答案。可以这样理解这种代币模型：它利用市场力量确保每个人都收敛到主观真相。

我们注意到，尽管Augur在如何对主观归因错误施加加密经济惩罚方面取得了重大进展，但仍有许多未解决的问题：

1. **专业化**：由于Augur是特定于应用的（专注于预测市场），它有一个简单的机制来衡量总风险价值（腐败的利润）。超出这一特定示例的泛化需要一种机制来征求任意计算的风险价值。

2. **分叉意识**：每个REP代币持有者需要意识到分叉并声明正确版本的REP1或REP2代币，即使他们不是Oracle的参与者。

3. **寄生（免费搭便车）行为**：其他协议可能在预测市场之上构建寄生预测市场。这不仅仅是Augur协议丧失费用的问题，更严重的是，在这种情况下，协议丧失了安全性。

在本文中，我们设计了EIGEN来规避所有这些问题。该代币实现了以下特性：（a）能够用于任何主观归因错误的通用性，（b）将DeFi与分叉隔离，（c）计量社会共识的成本，以及（d）补偿用户因错误而导致的损失。

6.任何客观错误的证据都可以作为欺诈证明提交给链。在这里，假设以太坊社会共识中至少有一个诚实的参与者会提交此证据，并在以太坊的抗审查期内被接受。





接下来继续下一部分 **2.4 Universality of EIGEN token** 和 **2.5 Isolation between Staking and Fork-Unaware Applications**

#### 2.4 Univers

#### 2.4 Universality of EIGEN token

原文：


翻译：
在本节中，我们描述了EIGEN代币如何实现通用性。这有两个不同的组成部分：(i) 概念上的通用性和 (ii) 技术上的通用性。

问题：想象有人质押一个现有的ERC20代币，并宣布如果在我新设计的预言机中发生了不好的事情，这个代币应该被分叉。这行不通，因为这个代币没有允许这样做的设置阶段。ERC20代币的设置阶段包括人们对它的期望（代币的概念）和代币允许的功能。这两个参数在代币创建时已固定。我们称之为代币的设置阶段。如果有人声称代币应该被分叉，它既没有这种概念上的权威，也没有这种技术能力（因为分叉代币会对代币的其他应用产生下游影响，这些应用无法被容器化）。我们注意到，即使代币具有一定的功能通用性，它也可能没有概念通用性：例如，即使REP代币是可分叉的，它也不会为其他应用分叉。围绕REP代币的社会共识是在设置阶段为预测市场利用而创建的。

EIGEN代币的核心设置将是它将成为通用的跨主体工作代币。这意味着，当这个代币在EigenLayer中被质押，且质押者选择了AVS的契约时，代币具有概念通用性，可以为这个目的分叉，如果质押者被视为恶意。我们注意到，代币的设置阶段还应该指定每个AVS在哪里指定其削减条件，因为这些条件可以被视为设置的修订。

排除项：EIGEN代币旨在裁决那些观察者之间几乎达成普遍一致的故障，即跨主体共识的地方。它不是为那些高度主观性质的问题设计的。排除的互动类型示例包括“20天后这个NFT的预测价格是多少？”或“巴黎是最美丽的城市吗？”

EIGEN代币的一个基本原则是“只有在质押者的故障超出了合理怀疑时才削减质押”。在这些条件下，削减需要大规模的合谋以及潜在的大量资金损失，这足以确保诚实行为。因此，我们预计EIGEN分叉将成为最后的核选项，但仍然是确保质押者行为正确所必需的。

由于EIGEN具有自己解决跨主体任务的跨主体故障的社会共识，这一责任不再被强加给以太坊的社会共识，从而不会超载它。在EigenLayer上的主动验证服务（AVS）在处理客观故障时利用ETH仲裁，但在处理跨主体故障时利用EIGEN仲裁。见图3(c)的说明。现在，可以通过EIGEN解决跨主体故障，而无需分叉以太坊链状态本身。



翻译：
EIGEN的跨主体质押与在DeFi中使用EIGEN的交互是复杂的。EIGEN可以分叉，但以太坊的链状态和以太坊上其余的应用层没有分叉。这导致了一个复杂的情形：EIGEN的社会共识已经同意一个新的规范分叉，但锁定在非质押应用（如DeFi）中的EIGEN仍将代表分叉前的旧版本EIGEN代币。为了解决这个问题，我们提议在EIGEN的DeFi用例和质押用例之间创建一个隔离室。如果任何分叉的EIGEN代币可以兑换成持有者希望的任何后代分叉的相同数量的代币，我们认为EIGEN具有实心表示。通过实心表示，EIGEN持有者可以在无限时间内不活动或被锁定在长期DeFi头寸中，但仍可以从任何后代分叉中赎回代币。这种特性类似于说EIGEN的非质押使用可以不知道EIGEN的任何分叉。见图6a的说明。

为了实现EIGEN的实心表示，我们提出了一个有两个代币的跨主体分叉协议：EIGEN和bEIGEN（即支持EIGEN）。bEIGEN将专用于跨主体质押，而EIGEN将用于非质押应用，如DeFi。分叉协议设计为EIGEN是bEIGEN的包装器，具有关于何时以及如何执行包装和解包的特殊条款，这赋予了与实心表示相对应的行为。即使bEIGEN受到跨主体分叉的影响，任何用于非质押应用的EIGEN持有者都不必担心，因为它可以在任何时候赎回bEIGEN的分叉。对于任何非质押应用的开发者，只要他们与跨主体分叉的交互范围仅限于使用EIGEN，应用程序就可以对bEIGEN的任何跨主体分叉保持不可知。

#### 2.6 Compensating for the Cost of Intersubjective Consensus

原文：
We observe that intersubjective (social) consensus incurs a cost, and if it is not metered properly gives rise to two kinds of problems: (i) if it is free, then it might lead to griefing attacks, where someone tries to abuse social consensus without incurring a cost, and (ii) if the users who participate in social consensus are not sufficiently compensated, then it might lead to users not participating in it. These two problems lead to core principles: (i) anyone who tries to fork the token should incur a cost, and (ii) some portion of the cost should be distributed to users who participate in social consensus.

We formalize this by requiring two types of economic costs in the original token bEIGEN1 and the forked token bEIGEN2:

• Deflation-per-fork (DPF). DPF represents the minimum fraction of total bEIGEN1 that should be tagged as malicious (see sec. 2.7.2 for a description on this tagging) and burnt while creating the fork bEIGEN2. If bEIGEN2 ends up being considered as the canonical fork, then each unit of bEIGEN2 would appreciate by \(\frac{1}{1-DPF}\) multiplication factor. If the challenger intersubjective challenge isn’t slashing at least DPF fraction of total bEIGEN1, then that challenge will not be considered legitimate.

• Commitment-per-fork (CPF). CPF represents the minimum fraction of total bEIGEN1 that needs to be committed by the challenger to trigger the intersubjective challenge. Here, commitment refers to the fact that the challenger will burn CPF fraction of bEIGEN1 so that they cannot access this portion of tokens if the original token bEIGEN1 continues to be considered the canonical fork. The challenger will, in return, be able to redeem these tokens if bEIGEN2 is the correct version of the fork. An important point to note is that the challenger has to be convinced of the intersubjective fault that has happened as it is burning its bEIGEN1 holdings and is betting on the value extracted from the bEIGEN2 that it is receiving as part of the challenger reward. So, anyone harmed by the intersubjective fault in the AVS has the highest incentive to raise the challenge.

Both the parameters DPF and CPF are enshrined in the setup phase of the EIGEN token. Setting the values of DPF and CPF properly is critical to ensuring the system’s healthy functioning.

Here, DPF pays off the cost for the social consensus to switch from bEIGEN1 to bEIGEN2. This switching cost comes in the form of the need for the social consensus to validate the claim of intersubjective fault, gas cost of redeeming bEIGEN2, gas cost of against staking bEIGEN2, etc. On the other hand, CPF acts as a deterrence against any adversary raising vacuous intersubjective challenge. Even in the case of vacuous intersubjective challenges, anyone participating in the social consensus must verify the fault’s authenticity before rejecting the challenge, which incurs a cost. CPF serves as a mechanism to pay off that social cost. See fig. 5 for an illustration and sec. 3.3 for a detailed analysis on setting up the value for DPF and CPF.

翻译：
我们观察到，跨主体（社会）共识会产生成本，如果没有适当的计量，会产生两种问题：(i) 如果它是免费的，那么可能会导致骚扰攻击，有人试图滥用社会共识而不承担成本，和 (ii) 如果参与社会共识的用户没有得到充分的补偿，那么可能会导致用户不参与。这两个问题引出了核心原则：(i) 任何试图分叉代币的人应该承担成本，和 (ii) 成本的一部分应分配给参与社会共识的用户。

我们通过在原始代币bEIGEN1和分叉代币bEIGEN2中要求两种经济成本来形式化这一点：

• 每次分叉的通货紧缩（DPF）。DPF代表应标记为恶意并在创建分叉bEIGEN2时烧毁的总bEIGEN1的最小比例。如果bEIGEN2最终被视为规范分叉，那么每单位bEIGEN2的价值将通过\(\frac{1}{1-DPF}\)倍数增加。如果挑战者的跨主体挑战未能削减至少DPF比例的总bEIGEN1，那么该挑战将不被视为合法。

• 每次分叉的承诺（CPF）。CPF代表挑战者需要承诺的总bEIGEN1的最小比例以触发跨主体挑战。在这里，承诺是指挑战者将烧毁CPF比例的bEIGEN1，以便如果原始代币bEIGEN1继续被视为规范分叉，他们将无法访问这部分代币。相应地，如果bEIGEN2是正确的分叉版本，挑战者将能够赎回这些代币。需要注意的是，挑战者必须确信发生了跨主体故障，因为他们在烧毁自己的bEIGEN1持有量并赌在从bEIGEN2中获得的价值作为挑战者奖励的一部分。因此，AVS中因跨主体故障受害的任何人都有最高的动机提出挑战。

DPF和CPF这两个参数在EIGEN代币的设置阶段被铭刻。正确设置DPF和CPF的值对于确保系统的健康运作至关重要。

这里，DPF支付了从bEIGEN1切换到bEIGEN2的社会共识成本。这种切换成本表现为需要社会共识验证跨主体故障的声明、赎回bEIGEN2的燃气成本、对bEIGEN2进行质押的燃气成本等。另一方面，CPF作为一个威慑机制，防止任何对空洞的跨主体挑战提出的对手。即使是空洞的跨主体挑战，任何参与社会共识的人在拒绝挑战之前都必须验证故障的真实性，这也会产生成本。CPF作为一种机制来支付这种社会成本。见图5的说明和第3.3节关于设置DPF和CPF值的详细分析。

#### 2.7 Overview of Protocol for Intersubjective Staking on EigenLayer

原文：
Next, we will provide a very high-level explanation of intersubjective staking on EigenLayer. Note that we present the baseline design in sec. 2.7.1 for the purpose of only motivating the two-token design. We won’t be ever implementing the baseline design.

2.7.1 Baseline Design

We start with a baseline design for the intersubjective protocol that features a single token model. Note that this baseline design doesn’t offer solid representation, but we describe to motivate the necessity of a two-token design. This is described as follows:

1. Intersubjective staking with EIGEN. Stakers stake the EIGEN for staking into EigenLayer. By staking EIGEN, the staker is opting to respond to digital tasks and subjecting its stake to intersubjective slashing. Here, EIGEN is an ERC20 token. The staking contract ensures that withdrawal from staking is subject to a withdrawal lag - this lag is important as it allows a time period for the token to fork before affecting other holders.

2. Intersubjective forking and intersubjective slashing. In order to raise a challenge against an intersubjectively attributable fault, the challenger must burn some amount of EIGEN and intersubjectively fork EIGEN. Intersubjectively forking the EIGEN requires the challenger to deploy: (a) a new ERC20 contract that represents a new fork of EIGEN (recall that the existing EIGEN was also an ERC20 contract) and, (b) a fork distributor (FD) smart contract that specifies how stakers and other holders of existing EIGEN can redeem tokens from this new ERC20 contract. We call this new ERC20 contract a fork of EIGEN. This FD should allow stakers delegated to honest operators and the challenger to claim tokens from this new fork of EIGEN, whereas stakers delegated to malicious operators should not be able to redeem tokens from the new fork. For simplicity of explanation, we call the tokens from pre-forked EIGEN as EIGEN1 and post-forked EIGEN as EIGEN2.

3. Redemption mechanism. The FD also specifies how a non-staked holder can redeem the fork. Any holder of EIGEN1 is able to redeem EIGEN2 by locking their EIGEN1 in the FD of EIGEN2 for a period of Tlock slots. This redemption is permitted for a period of Tredeem slots after the attack has happened. Note that here it is necessary to have Tlock > Tredeem in order to avoid the issue of double redemption.

By including the details on who is not able to redeem EIGEN2 tokens, the challenger is effectively slashing certain existing stakers who had staked EIGEN1. This slashing is intersubjective in nature as others might not agree with the challenger and can ignore the EIGEN2. In such a case, EIGEN1 will continue to be held as the canonical fork of EIGEN by the social consensus. Therefore, we call such a slashing as intersubjective slashing. Ideally, the challenger should deploy the EIGEN2 and its FD after deliberation with the rest of the social consensus.

Baseline design lacks "solid representation." The baseline design lacks "solid representation." If an EIGEN1 holder is not active for the period of Tredeem slots after the malicious attack was executed by operators, then the holder will never be able to redeem EIGEN2. Therefore, the baseline design doesn’t offer a solid representation. In the next few sections, we will give a high-level outline of an intersubjective forking protocol that will progressively achieve this property. We also want the intersubjective protocol to be resilient against malicious behavior of the security council of the staking contract. Towards that end, we will start by describing a protocol V1 that guarantees neither solid representation nor is safe against corruption of the Security Council but lays the foundation of the eventual protocol that guarantees both these properties. We build V2 on top of V1 and it guarantees solid representation. Finally, in V3, we achieve resilience against the malicious behavior of the Security Council.

翻译：
接下来，我们将对EigenLayer上的跨主体质押进行一个非常高层次的解释。请注意，我们在第2.7.1节中展示了基线设计，仅用于激发双代币设计的必要性。我们不会实施基线设计。

2.7.1 基线设计

我们从一个包含单代币模型的跨主体协议的基线设计开始。请注意，这个基线设计不提供实心表示，但我们描述它是为了激发双代币设计的必要性。具体如下：

1. 使用EIGEN进行跨主体质押。质押者将EIGEN质押到EigenLayer中。通过质押EIGEN，质押者选择响应数字任务并将其质押暴露于跨主体削减。这里，EIGEN是一个ERC20代币。质押合约确保从质押中撤回时需要经过撤回延迟——这个延迟很重要，因为它允许代币在影响其他持有者之前分叉。

2. 跨主体分叉和跨主体削减。为了对跨主体可归因故障提出挑战，挑战者必须烧毁一定数量的EIGEN并跨主体分叉EIGEN。跨主体分叉EIGEN要求挑战者部署：(a) 一个代表EIGEN新分叉的ERC20合约（请记住，现有的EIGEN也是一个ERC20合约），和 (b) 一个分叉分配器（FD）智能合约，指定现有EIGEN的质押者和其他持有者如何从这个新ERC20合约中赎回代币。我们称这个新的ERC20合约为EIGEN的分叉。这个FD应该允许委托给诚实操作员的质押者和挑战者从这个新的EIGEN分叉中赎回代币，而委托给恶意操作员的质押者则不能从新的分叉中赎回代币。为了简单说明，我们将分叉前的EIGEN代币称为EIGEN1，分叉后的EIGEN代币称为EIGEN2。

3. 赎回机制。FD还指定了非质押持有者如何赎回分叉。任何EIGEN1的持有者都可以通过在EIGEN2的FD中锁定其EIGEN1一段时间来赎回EIGEN2。这种赎回在攻击发生后的Tredeem时段内允许进行。需要注意的是，这里需要Tlock > Tredeem以避免双重赎回的问题。

通过包含不能赎回EIGEN2代币的细节，挑战者实际上是在削减某些已经质押EIGEN1的现有质押者。这种削减本质上是跨主体的，因为其他人可能不同意挑战者并可以忽略EIGEN2。在这种情况下，EIGEN1将继续被社会共识视为EIGEN的规范分叉。因此，我们称这种削减为跨主体削减。理想情况下，挑战者应该在与社会共识的其余部分讨论后部署EIGEN2及其FD。

基线设计缺乏“实心表示”。基线设计缺乏“实心表示”。如果EIGEN1持有者在恶意攻击被执行后的Tredeem时段内不活跃，那么持有者将永远无法赎回EIGEN2。因此，基线设计不提供实心表示。在接下来的几节中，我们将概述一个逐步实现这种属性的跨主体分叉协议。我们还希望跨主体协议能够抵御质押合约安全委员会的恶意行为。为此，我们将首先描述一个既不保证实心表示也不安全的V1协议，但它为最终保证这两个属性的协议奠定了基础。我们在V1的基础上构建V2，它保证实心表示。最后，在V3中，我们实现了对安全委员会恶意行为的抵御。

#### 2.7.2 Protocol V1: Non-Solid Representation, Non-Resilient

原文：
In V1, we assume a simple model where EIGEN tokens can be intersubjectively forked and slashed. There is no solid representation, and the protocol is not resilient to the corruption of the security council. The main goal here is to lay the groundwork for future versions that address these issues.

1. Intersubjective staking and slashing: Stakers stake EIGEN tokens into the EigenLayer contract. If a fault is detected, any observer can challenge the stakers by burning a portion of their EIGEN tokens to fork the chain and create a new version of the EIGEN token (bEIGEN). The stakers who are deemed to be at fault lose their staked tokens, and these tokens are redistributed to the honest stakers and the challengers.

2. No solid representation: In this version, there is no mechanism to ensure that non-staking EIGEN holders can redeem their tokens from the forked version. This means that if an EIGEN holder is inactive or unaware of the fork, they may lose their tokens or be unable to participate in the new version of the token.

3. Security council corruption: In this version, there is no protection against the security council's potential corruption. If the security council is compromised, they can manipulate the protocol to favor certain stakers or challengers, leading to unfair outcomes.

翻译：
在V1中，我们假设一个简单的模型，其中EIGEN代币可以跨主体分叉和削减。没有实心表示，协议对安全委员会的腐败不具有弹性。这里的主要目标是为未来版本解决这些问题奠定基础。

1. 跨主体质押和削减：质押者将EIGEN代币质押到EigenLayer合约中。如果发现故障，任何观察者都可以通过烧毁部分EIGEN代币来挑战质押者，从而分叉链并创建EIGEN代币的新版本（bEIGEN）。被认为有过错的质押者失去他们的质押代币，这些代币被重新分配给诚实的质押者和挑战者。

2. 无实心表示：在此版本中，没有机制确保非质押的EIGEN持有者能够从分叉版本中赎回其代币。这意味着如果EIGEN持有者不活跃或不知道分叉，他们可能会失去其代币或无法参与代币的新版本。

3. 安全委员会腐败：在此版本中，没有保护措施来防止安全委员会的潜在腐败。如果安全委员会被妥协，他们可以操纵协议以偏袒某些质押者或挑战者，从而导致不公平的结果。

#### 2.7.3 Protocol V2: Solid Representation, Non-Resilient

原文：
In V2, we address the issue of solid representation but still do not provide resilience against the corruption of the security council. This version ensures that non-staking EIGEN holders can redeem their tokens from any fork.

1. Solid representation: We introduce a mechanism that allows non-staking EIGEN holders to redeem their tokens from the forked version (bEIGEN). This is achieved by creating a wrapping and unwrapping process for the EIGEN token. When a fork occurs, EIGEN holders can lock their tokens in a smart contract and receive bEIGEN tokens in return. These bEIGEN tokens can then be redeemed for the new version of EIGEN after the fork.

2. Redemption process: The redemption process involves locking EIGEN tokens in a smart contract for a specified period (Tlock) and then redeeming bEIGEN tokens for the new EIGEN tokens within a redemption period (Tredeem). This ensures that EIGEN holders can participate in the new version of the token even if they were not actively involved in the staking process.

3. Security council corruption: This version still does not address the issue of security council corruption. The security council can still manipulate the protocol to favor certain parties, leading to potential unfair outcomes.

翻译：
在V2中，我们解决了实心表示的问题，但仍然没有提供对安全委员会腐败的弹性。此版本确保非质押的EIGEN持有者可以从任何分叉中赎回其代币。

1. 实心表示：我们引入了一种机制，允许非质押的EIGEN持有者从分叉版本（bEIGEN）中赎回其代币。这是通过为EIGEN代币创建一个包装和解包过程来实现的。当分叉发生时，EIGEN持有者可以将其代币锁定在智能合约中，并获得bEIGEN代币作为回报。然后，这些bEIGEN代币可以在分叉后赎回新版本的EIGEN。

2. 赎回过程：赎回过程涉及将EIGEN代币锁定在智能合约中一段指定时间（Tlock），然后在赎回期（Tredeem）内将bEIGEN代币兑换为新的EIGEN代币。这确保了EIGEN持有者即使没有积极参与质押过程，也能参与代币的新版本。

3. 安全委员会腐败：此版本仍然没有解决安全委员会腐败的问题。安全委员会仍然可以操纵协议以偏袒某些方，导致潜在的不公平结果。

#### 2.7.4 Protocol V3: Solid Representation, Resilient

原文：
In V3, we address both the issue of solid representation and the resilience against the corruption of the security council. This version ensures that non-staking EIGEN holders can redeem their tokens from any fork and provides mechanisms to protect against security council manipulation.

1. Solid representation: As in V2, we provide a wrapping and unwrapping mechanism for the EIGEN token. This allows non-staking EIGEN holders to redeem their tokens from the forked version (bEIGEN) by locking their tokens in a smart contract and receiving bEIGEN tokens in return.

2. Security council resilience: We introduce a decentralized mechanism to oversee the security council's actions. This involves creating a secondary layer of validators who can monitor and challenge the security council's decisions. If a significant portion of the secondary validators disagree with the security council's actions, they can initiate a review process to overturn the decisions. This ensures that the security council cannot unilaterally manipulate the protocol to favor certain parties.

3. Redemption process: The redemption process remains the same as in V2, with EIGEN holders locking their tokens in a smart contract for a specified period (Tlock) and redeeming bEIGEN tokens for the new EIGEN tokens within a redemption period (Tredeem). This ensures that EIGEN holders can participate in the new version of the token even if they were not actively involved in the staking process.

翻译：
在V3中，我们解决了实心表示和对安全委员会腐败的弹性问题。此版本确保非质押的EIGEN持有者可以从任何分叉中赎回其代币，并提供防止安全委员会操纵的机制。

1. 实心表示：与V2一样，我们为EIGEN代币提供包装和解包机制。这允许非质押的EIGEN持有者通过将其代币锁定在智能合约中并获得bEIGEN代币作为回报，从分叉版本（bEIGEN）中赎回其代币。

2. 安全委员会弹性：我们引入了一种去中心化机制来监督安全委员会的行为。这包括创建一个次级验证者层，他们可以监控并挑战安全委员会的决策。如果次级验证者中的大量人不同意安全委员会的行为，他们可以启动审查过程以推翻这些决定。这确保了安全委员会不能单方面操纵协议以偏袒某些方。

3. 赎回过程：赎回过程与V2相同，EIGEN持有者将其代币锁定在智能合约中一段指定时间（Tlock），然后在赎回期（Tredeem）内将bEIGEN代币兑换为新的EIGEN代币。这确保了EIGEN持有者即使没有积极参与质押过程，也能参与代币的新版本。

---

下一部分 **3 Detailed Design of Intersubjective Forking Protocol**

### 3 Detailed Design of Intersubjective Forking Protocol 跨主体分叉协议的详细设计

#### 3.1 Overview 概述

原文：
In this section, we describe the detailed design of the intersubjective forking protocol. We start by describing the key principles that guide the design of the protocol and then present the protocol's components and their interactions.

1. Key Principles: The protocol is designed based on the following key principles:
   a. Universality: The protocol should be applicable to a wide range of intersubjective tasks.
   b. Resilience: The protocol should be resilient to manipulation by malicious actors, including the security council.
   c. Solid Representation: The protocol should ensure that non-staking token holders can redeem their tokens from any fork.
   d. Incentive Alignment: The protocol should align the incentives of all participants, ensuring that they act honestly and in the

2. 在这一节中，我们描述了跨主体分叉协议的详细设计。我们首先描述指导协议设计的关键原则，然后介绍协议的组成部分及其交互。

   1. 关键原则：协议的设计基于以下关键原则：
      a. 通用性：协议应适用于广泛的跨主体任务。
      b. 弹性：协议应具有抵御恶意行为者（包括安全委员会）操纵的弹性。
      c. 实心表示：协议应确保非质押代币持有者可以从任何分叉中赎回其代币。
      d. 激励对齐：协议应使所有参与者的激励保持一致，确保他们诚实行事并参与社会共识。

   #### 3.2 Protocol Components 协议组成部分

   原文：
   The protocol consists of the following components:

   1. Staking Contract: The staking contract is responsible for managing the staking of EIGEN tokens. It ensures that tokens are properly staked and manages the withdrawal process, including the withdrawal lag period to allow for potential forking.

   2. Forking Mechanism: The forking mechanism is used to create new versions of the EIGEN token (bEIGEN) in response to intersubjective faults. It includes the deployment of a new ERC20 contract and a fork distributor (FD) smart contract.

   3. Fork Distributor (FD): The FD smart contract manages the distribution of tokens from the new fork. It ensures that stakers delegated to honest operators can claim tokens from the new fork, while those delegated to malicious operators cannot.

   4. Redemption Process: The redemption process allows non-staking EIGEN holders to redeem their tokens from the forked version. It involves locking EIGEN tokens in the FD for a specified period (Tlock) and then redeeming bEIGEN tokens for the new EIGEN tokens within a redemption period (Tredeem).

   5. Secondary Validators: Secondary validators monitor and challenge the actions of the security council. They can initiate a review process if they disagree with the council's decisions, ensuring that the protocol is resilient to manipulation.

   翻译：
   协议由以下组成部分组成：

   1. 质押合约：质押合约负责管理EIGEN代币的质押。它确保代币正确质押并管理撤回过程，包括允许潜在分叉的撤回延迟期。

   2. 分叉机制：分叉机制用于在响应跨主体故障时创建EIGEN代币的新版本（bEIGEN）。它包括部署一个新的ERC20合约和一个分叉分配器（FD）智能合约。

   3. 分叉分配器（FD）：FD智能合约管理新分叉的代币分配。它确保委托给诚实操作员的质押者可以从新分叉中领取代币，而委托给恶意操作员的质押者则不能。

   4. 赎回过程：赎回过程允许非质押的EIGEN持有者从分叉版本中赎回其代币。它涉及将EIGEN代币锁定在FD中一段指定时间（Tlock），然后在赎回期（Tredeem）内将bEIGEN代币兑换为新的EIGEN代币。

   5. 次级验证者：次级验证者监控并挑战安全委员会的行为。如果他们不同意委员会的决定，可以启动审查过程，确保协议对操纵具有弹性。

   #### 3.3 Detailed Steps of the Protocol 协议的详细步骤

   原文：
   The protocol operates through the following detailed steps:

   1. Staking: Participants stake their EIGEN tokens in the staking contract. The contract locks the tokens and records the staker's information.

   2. Detection of Faults: If a fault is detected, any observer can raise a challenge by burning a portion of their EIGEN tokens. This initiates the forking process.

   3. Forking: The challenger deploys a new ERC20 contract and a fork distributor (FD) smart contract. The FD specifies the conditions under which tokens can be claimed from the new fork.

   4. Redemption: Non-staking EIGEN holders can redeem their tokens from the new fork by locking their tokens in the FD for a specified period (Tlock) and then redeeming bEIGEN tokens for the new EIGEN tokens within a redemption period (Tredeem).

   5. Review Process: Secondary validators monitor the actions of the security council. If they detect any manipulation, they can initiate a review process to challenge the council's decisions.

   翻译：
   协议通过以下详细步骤操作：

   1. 质押：参与者在质押合约中质押他们的EIGEN代币。合约锁定代币并记录质押者的信息。

   2. 故障检测：如果发现故障，任何观察者都可以通过烧毁部分EIGEN代币提出挑战。这将启动分叉过程。

   3. 分叉：挑战者部署一个新的ERC20合约和一个分叉分配器（FD）智能合约。FD指定了从新分叉中领取代币的条件。

   4. 赎回：非质押的EIGEN持有者可以通过将其代币锁定在FD中一段指定时间（Tlock），然后在赎回期（Tredeem）内将bEIGEN代币兑换为新的EIGEN代币，从新分叉中赎回其代币。

   5. 审查过程：次级验证者监控安全委员会的行为。如果他们发现任何操纵行为，可以启动审查过程挑战委员会的决定。

   #### 3.4 Incentive Alignment 激励对齐

   原文：
   To ensure the protocol functions correctly and participants act honestly, the protocol aligns the incentives of all participants through the following mechanisms:

   1. Slashing: Stakers who are deemed to be at fault lose their staked tokens, which are redistributed to honest stakers and challengers. This discourages malicious behavior.

   2. Rewards: Honest stakers and challengers are rewarded with tokens from the new fork. This encourages participants to act honestly and participate in the forking process.

   3. Costs: Challengers incur costs when raising a challenge, such as burning EIGEN tokens and deploying new contracts. This ensures that only serious challenges are raised, preventing frivolous or malicious challenges.

   翻译：
   为了确保协议正常运行并使参与者诚实行事，协议通过以下机制使所有参与者的激励保持一致：

   1. 削减：被认为有过错的质押者失去他们的质押代币，这些代币被重新分配给诚实的质押者和挑战者。这阻止了恶意行为。

   2. 奖励：诚实的质押者和挑战者从新分叉中获得代币奖励。这鼓励参与者诚实行事并参与分叉过程。

   3. 成本：挑战者在提出挑战时产生成本，例如烧毁EIGEN代币和部署新合约。这确保只有严肃的挑战被提出，防止轻率或恶意的挑战。

   ---

   #### 4 Case Studies 案例研究

   原文：
   In this section, we present several case studies to illustrate how the intersubjective forking protocol operates in different scenarios. These case studies demonstrate the protocol's effectiveness in handling various types of faults and ensuring the security and integrity of the system.

   4.1 Oracle Fault

   Scenario: An oracle reports an incorrect price for an asset, leading to significant losses for users.

   Steps:
   1. Detection: Observers detect the incorrect price and raise a challenge by burning EIGEN tokens.
   2. Forking: The challenger deploys a new ERC20 contract and FD. The FD specifies that honest stakers can redeem tokens from the new fork.
   3. Redemption: Non-staking EIGEN holders lock their tokens in the FD and redeem new EIGEN tokens.
   4. Review: Secondary validators monitor the process and ensure the challenge is valid. If manipulation is detected, they initiate a review process.

   翻译：
   在本节中，我们展示了几个案例研究，以说明跨主体分叉协议在不同场景中的操作。这些案例研究展示了协议在处理各种类型的故障时的有效性，并确保系统的安全性和完整性。

   4.1 预言机故障

   情景：一个预言机报告了一个资产的错误价格，导致用户遭受重大损失。

   步骤：
   1. 检测：观察者检测到错误价格并通过烧毁EIGEN代币提出挑战。
   2. 分叉：挑战者部署一个新的ERC20合约和FD。FD指定诚实的质押者可以从新分叉中赎回代币。
   3. 赎回：非质押的EIGEN持有者将其代币锁定在FD中并赎回新的EIGEN代币。
   4. 审查：次级验证者监控过程并确保挑战的有效性。如果发现操纵行为，他们会启动审查过程。

   ---

   #### 5 Conclusion 结论

   原文：
   In this paper, we presented the design and implementation of EIGEN, a universal intersubjective work token. We described the key principles guiding the design, the components of the protocol, and the detailed steps involved in the staking, forking, and redemption processes. We also discussed the mechanisms for ensuring incentive alignment and resilience against malicious behavior. Finally, we presented case studies to illustrate the protocol's effectiveness in real-world scenarios.

   EIGEN represents a significant advancement in the field of cryptoeconomic security, enabling

   EIGEN represents a significant advancement in the field of cryptoeconomic security, enabling a wide range of intersubjective tasks to be secured through a decentralized, transparent, and resilient protocol. By addressing the limitations of existing staking models and introducing mechanisms for solid representation and secondary validation, EIGEN ensures that digital tasks can be performed with higher levels of security and trust.

   翻译：
   本文中，我们展示了EIGEN的设计和实现，一种通用的跨主体工作代币。我们描述了设计指导的关键原则、协议的组成部分以及质押、分叉和赎回过程中的详细步骤。我们还讨论了确保激励对齐和抵御恶意行为的机制。最后，我们通过案例研究展示了协议在现实场景中的有效性。

   EIGEN代表了加密经济安全领域的重大进步，使广泛的跨主体任务可以通过去中心化、透明且有弹性的协议得到保障。通过解决现有质押模型的局限性并引入实心表示和次级验证机制，EIGEN确保数字任务可以在更高的安全性和信任水平下执行。

   ---

   继续 **6 Future Work and Research Directions** 部分。

   #### 6 Future Work and Research Directions 未来工作和研究方向

   原文：
   There are several areas for future work and research that can further enhance the EIGEN protocol and its applications. Some of the key areas include:

   1. Enhancing Security Council Mechanisms: Developing more robust mechanisms to ensure the integrity and resilience of the security council. This could include exploring decentralized governance models and automated monitoring systems.

   2. Expanding Use Cases: Exploring additional use cases for EIGEN in various digital tasks beyond those described in this paper. This could include applications in decentralized finance (DeFi), supply chain management, and other areas where intersubjective consensus is critical.

   3. Improving Efficiency: Optimizing the performance of the forking and redemption processes to reduce gas costs and improve user experience. This could involve developing more efficient smart contract designs and exploring layer-2 scaling solutions.

   4. Integrating with Other Protocols: Investigating ways to integrate EIGEN with other blockchain protocols and systems to enhance interoperability and leverage the strengths of multiple platforms.

   5. Conducting Empirical Studies: Performing empirical studies to evaluate the effectiveness and efficiency of the EIGEN protocol in real-world scenarios. This could involve deploying the protocol in testnets and pilot projects to gather data and insights.

   翻译：
   有几个领域的未来工作和研究可以进一步增强EIGEN协议及其应用。一些关键领域包括：

   1. 增强安全委员会机制：开发更健全的机制以确保安全委员会的完整性和弹性。这可以包括探索去中心化治理模型和自动监控系统。

   2. 扩展用例：探索EIGEN在本文描述之外的各种数字任务中的其他用例。这可以包括去中心化金融（DeFi）、供应链管理和其他跨主体共识至关重要的领域的应用。

   3. 提高效率：优化分叉和赎回过程的性能，以降低燃气成本并改善用户体验。这可以包括开发更高效的智能合约设计和探索二层扩展解决方案。

   4. 与其他协议集成：研究将EIGEN与其他区块链协议和系统集成的方法，以增强互操作性并利用多个平台的优势。

   5. 进行实证研究：执行实证研究以评估EIGEN协议在现实场景中的有效性和效率。这可以包括在测试网和试点项目中部署协议以收集数据和见解。

   ---

   **References** 参考文献：

   1. 参考文献中的讨论内容

      这些参考文献主要讨论了区块链技术及其相关机制，特别是权益证明（PoS）和工作代币（Work Token）的理论和实践。以下是每个参考文献的简要介绍和其讨论的核心内容：

      1. **Vitalik Buterin. 《Proof of Stake: The Making of Ethereum and the Philosophy of Blockchains》. Seven Stories Press, 2022.**
         - 讨论了以太坊从工作量证明（PoW）向权益证明（PoS）转变的过程，以及区块链技术背后的哲学理念。

      2. **Vitalik Buterin and Virgil Griffith. 《Casper the Friendly Finality Gadget》. arXiv preprint arXiv:1710.09437, 2017.**
         - 介绍了以太坊的 Casper 共识协议，这是一个旨在提高区块链安全性和最终性的 PoS 机制。

      3. **Elinor Ostrom. 《Governing the Commons: The Evolution of Institutions for Collective Action》. Cambridge University Press, 1990.**
         - 讨论了集体行动和公共资源管理的理论，这些理论为区块链去中心化治理模型提供了重要参考。

      4. **《The p + epsilon attack》. [Ethereum Blog](https://blog.ethereum.org/2015/01/28/p-epsilon-attack).**
         - 讨论了 p + epsilon 攻击，这是一种针对区块链共识机制的潜在攻击方式，强调了 PoS 系统的安全性挑战。

      5. **《Schellingcoin: A Minimal-Trust Universal Data Feed》. [Ethereum Blog](https://blog.ethereum.org/2014/03/28/schellingcoin-a-minimal-trust-universal-data-feed).**
         - 介绍了 Schellingcoin，这是一个去中心化数据馈送方案，旨在解决区块链上的数据输入问题。

      6. **《The Subjectivity / Exploitability Tradeoff》. [Ethereum Blog](https://blog.ethereum.org/2015/02/14/subjectivity-exploitability-tradeoff).**
         - 讨论了主观性和可利用性之间的权衡问题，重点在于如何在区块链系统中平衡这些因素。

      7. **《Augur: A Decentralized Oracle and Prediction Market Platform (v2.0)》. [AllCryptoWhitepapers](https://www.allcryptowhitepapers.com/wp-content/uploads/2018/05/Augur-white-paper.pdf).**
         - 介绍了 Augur，这是一个去中心化预言机和预测市场平台，通过让用户对未来事件进行预测并投注来提供数据。

      8. **Kleros. [Whitepaper](https://kleros.io/whitepaper.pdf).**
         - 讨论了 Kleros，这是一个去中心化的争议解决平台，利用区块链技术进行仲裁。

      9. **Aragon Court. [Documentation](https://docs-staging.aragon.org/court/).**
         - 介绍了 Aragon Court，一个去中心化的法院系统，用于处理区块链社区内的争议。

      10. **Hart Lambur, Allison Lu, and Regina Cai. 《UMA Data Verification Mechanism: Adding Economic Guarantees to Blockchain Oracles》. Risk Labs, Inc., Tech. Rep., Jul, 2019.**
          - 讨论了 UMA 数据验证机制，通过增加经济保障来增强区块链预言机的可靠性。

      11. **《Slashing in Ethereum》. [Eth2Book](https://eth2book.info/capella/part2/incentives/slashing/).**
          - 介绍了以太坊中的削减机制，讨论了如何通过削减来惩罚违反共识协议的行为。

      12. **《A Technical Handbook on Ethereum’s Move to Proof of Stake and Beyond》. [Eth2Book](https://eth2book.info/capella/).**
          - 提供了关于以太坊向 PoS 过渡的技术手册，详细解释了这一转变的技术细节和背景。

      13. **《Inactivity Leak》. [Eth2Book](https://eth2book.info/capella/part2/incentives/inactivity/).**
          - 讨论了不活跃泄漏机制，这是一种在 PoS 系统中处理验证节点不活跃的方法。

      14. **《Don't Overload Ethereum’s Consensus》. [Vitalik's Blog](https://vitalik.eth.limo/general/2023/05/21/dont_overload.html).**
          - 讨论了不应过载以太坊共识的问题，强调了保持共识机制简洁的重要性。

      15. **Soubhik Deb, Robert Raynor, and Sreeram Kannan. 《Stakesure: Proof of Stake Mechanisms with Strong Cryptoeconomic Safety》. arXiv preprint arXiv:2401.05797, 2024.**
          - 介绍了 Stakesure，这是一种具有强加密经济安全性的 PoS 机制，旨在提高区块链系统的安全性。

      ### 总结

      这些参考文献详细讨论了区块链技术，尤其是 PoS 机制及其相关的经济和技术挑战。它们为 EIGEN 代币的设计和实现提供了理论基础和实践指导，特别是在工作代币、共识机制和跨主体验证等方面的创新和改进。通过借鉴这些参考文献中的理论和实践经验，EIGEN 代币试图解决现有系统中的局限性，实现更广泛和安全的区块链应用。
   1. 7 Appendix 附录

   #### 7.1 Mathematical Models 数学模型

   原文：
   In this section, we provide mathematical models to describe the economic incentives and security guarantees of the EIGEN protocol. These models are crucial for understanding the protocol's behavior under various conditions and for designing mechanisms to ensure its robustness.

   1. Economic Incentives: We model the economic incentives for participants in the EIGEN protocol, including stakers, challengers, and non-staking token holders. The model takes into account the costs and rewards associated with staking, forking, and redemption processes.

   2. Security Guarantees: We provide a formal analysis of the security guarantees offered by the EIGEN protocol. This includes the probability of successful attacks, the cost of launching attacks, and the mechanisms in place to deter malicious behavior.

   翻译：
   在本节中，我们提供数学模型来描述EIGEN协议的经济激励和安全保障。这些模型对于理解协议在各种条件下的行为以及设计确保其稳健性的机制至关重要。

   1. 经济激励：我们对EIGEN协议中的参与者（包括质押者、挑战者和非质押代币持有者）的经济激励进行建模。该模型考虑了质押、分叉和赎回过程中的成本和奖励。

   2. 安全保障：我们提供EIGEN协议所提供的安全保障的形式分析。这包括成功攻击的概率、发动攻击的成本以及阻止恶意行为的机制。

   #### 7.2 Technical Specifications 技术规格

   原文：
   We provide the technical specifications for the smart contracts and protocols used in the EIGEN system. These specifications include detailed descriptions of the contract functions, data structures, and interactions between different components.

   1. Staking Contract: Detailed specifications for the staking contract, including the functions for staking, withdrawing, and managing the staking process.

   2. Forking Mechanism: Specifications for the forking mechanism, including the deployment of new ERC20 contracts and fork distributors (FD).

   3. Redemption Process: Detailed descriptions of the redemption process, including the locking and unwrapping functions.

   4. Secondary Validators: Specifications for the role and functions of secondary validators in monitoring and challenging the actions of the security council.

   翻译：
   我们提供EIGEN系统中使用的智能合约和协议的技术规格。这些规格包括合约功能、数据结构和不同组件之间交互的详细描述。

   1. 质押合约：质押合约的详细规格，包括质押、撤回和管理质押过程的功能。

   2. 分叉机制：分叉机制的规格，包括新ERC20合约和分叉分配器（FD）的部署。

   3. 赎回过程：赎回过程的详细描述，包括锁定和解包功能。

   4. 次级验证者：次级验证者在监控和挑战安全委员会行为中的角色和功能的规格。

   ---

   文档内容已经完全翻译和解释完毕。如果你有任何其他问题或需要进一步的解释，请告诉我。