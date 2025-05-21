
## 字段解释
id: 帖子的唯一标识符。
cardType: 帖子的类型，这里是 "BUZZ_SHORT"。
contentType: 内容类型，1 表示文本内容。
title: 帖子的标题，这里为空。
subTitle: 帖子的副标题，这里为空。
webLink: 帖子的网页链接。
shareLink: 帖子的分享链接。
date: 帖子发布的时间戳（Unix 时间）。
handWork: 手动操作相关信息。
contentStatus: 内容状态，2 表示已发布。
squareAuthorId: 作者的唯一标识符。
needTranslate: 是否需要翻译，这里为 false。
needAutoTranslate: 是否需要自动翻译，这里为 true。
isFeatured: 是否为精选内容，这里为空。
featuredLink: 精选内容的链接，这里为空。
topFlagInHashtagDetailPage: 在话题详情页是否置顶，false 表示否。
topFlagForProjectLatestContent: 在项目最新内容中是否置顶，false 表示否。
translatedData: 翻译后的数据，这里为空。
redEnvelop: 红包信息，这里为空。
isAssociateRedEnvelop: 是否关联红包，false 表示否。
portfolioPerformance: 组合表现，这里为空。
tradingSignal: 交易信号，这里为空。
isStickyToTop: 是否置顶，false 表示否。
badgeInfos: 徽章信息，这里为空。
hyperlinkList: 超链接列表，这里为空。
mentionUserVOs: 提到的用户信息列表，这里为空。
extraFeature: 额外特性，这里为 "NO_FEATURE"。
quoteContent: 引用的内容，这里为空。
content: 帖子的正文内容，包含对多个山寨币的分析和推荐。
images: 图片列表，这里为空。
authorName: 作者的名字，这里是 "T先生"。
authorAvatar: 作者的头像链接。
authorVerificationType: 作者的认证类型，这里为 0。
authorRole: 作者的角色，这里为 11。
likeCount: 点赞数，这里为 4。
shareCount: 分享数，这里为 0。
viewCount: 查看数，这里为 1155。
commentCount: 评论数，这里为 0。
quoteCount: 引用数，这里为 0。
isLiked: 是否已点赞，false 表示否。
isFollowed: 是否已关注，false 表示否。
followsYou: 作者是否关注你，false 表示否。
hashtagList: 话题标签列表，这里包含 "#ETH" 和 "#BTC"。
sourceType: 来源类型，这里为 5。
quotedContentWebLink: 引用内容的网页链接。
tradingPairs: 交易对信息列表，包含市场类型、桥接货币、代码、符号和标志 URL。
coinPairList: 帖子中提到的币对列表。
tradingPairsV2: 第二版交易对信息列表，结构与 tradingPairs 相同。
tendency: 趋势，这里为 0。
imageMetaList: 图片元数据列表，这里为空。
coverMeta: 封面元数据，这里为空。
totalReactionCount: 总反应数，这里为 4。
reactionCount: 反应类型和数量列表。
isReaction: 是否有反应，这里为空。
liveStatusVO: 实时状态信息，这里为空。
username: 作者的用户名，这里是 "tyy991202"。




## 关键字段及其分析用途

id:

用于唯一标识每条记录，确保数据的完整性。
content:

用于文本分析，包括情感分析、关键词提取、主题建模等。
authorName:

分析作者的影响力、发帖频率和受欢迎程度。
likeCount:

衡量帖子受欢迎程度，分析受欢迎帖子的特征。
viewCount:

分析帖子被查看的次数，评估帖子的传播范围。
hashtagList:

提取和分析话题标签，识别流行话题和趋势。
tradingPairs:

分析提到的交易对，研究哪些交易对受到关注。
date:

时间戳，用于时间序列分析，观察发帖时间和频率。
