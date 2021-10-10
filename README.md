# FEED: Chines Financial Event Extraction Dataset Benchmark

## 1. Abstract

We release a large-scale Chinese financial event extraction dataset FEED, consisting of 31,748 documents on five financial event types derived from the Chinese financial portals, which considers the case of event arguments scattered in multiple sentences. In order to construct FEED dataset, we first extract candidate events from financial announcements by Fonduer. Then we build an event knowledge base using weakly supervised classification, and finally label events via distant supervision. We also verify the usability  of FEED and the distinguishability between baseline models. Empirical results show that FEED is challenging for existing event extraction methods, which indicates that Chinese financial event extraction remains an open problem and requires further efforts.

### 2. Introduction

In order to efficiently build a large-scale Chinese financial EE dataset from massive financial announcements, we propose an approach based on distant supervision. The overview of this approach is illustrated in Figure \ref{overview}. We first extract candidate events from preprocessed data by Fonduer \cite{wu2018fonduer}. Second, an event knowledge base is built using weakly supervised classification method. Finally, we label the events via distant supervision to obtain the FEED dataset.

### 远程监督标注
经过上述步骤得到金融事件知识库之后，我们采用远程监督的方式对爬取的文档数据进行标注。如下图所示：
![ds label](https://github.com/seukgcode/FEED/blob/main/IMG/ds%20label.jpg)
首先清洗文本数据。数据清理是对转换后的文本进行标准化，主要包括过滤乱码和根据特殊符号对句子进行分割。然后，我们根据文档ID从知识库中检索文档中的结构化事件，并使用BIO格式标记事件参数。通过两个条件过滤标注结果:(1)事件必须包含事件本体定义的关键角色(如个人或公司)，(2)文档和事件本体具有相同数量的事件角色。最后，我们获得了五类事件的标记数据:股权冻结(EF)、股权回购(ER)、股权减持(EU)、股权增持(EO)和股权质押(EP)。其中，每个事件类型由不同的事件元素组成，如下表所示：
|EquityRepurchase (ER)|EquityFreeze (EF)|EquityUnderweight (EU)|EquityOverweight (EO)|EquityPledge (EP)|
|:--:|:--:|:--:|:--:|:--:|
|CompanyName|EquityHolder|EquityHolder|EquityHolder|EquityHolder|
|RepurchasedShares|FrozeShares|TradedShares|TradedShares|PledgedShares|
|HighestTradingPrice|LegalInstitution|StartDate|StartDate|Pledgee|
|LowestTradingPrice|StartDate|EndDate|EndDate|StartDate|
|ClosingDate|EndDate|AveragePrice|AveragePrice|EndDate|
|RepurchaseAmount|UnfrozeDate|LaterHoldingShares|LaterHoldingShares|ReleasedDate|
|-|TotalHoldingShares|-|-|TotalPledgedShares|
|-|TotalHoldingRatio|-|-|TotalHoldingShares|
|-|-|-|-|TotalHoldingRatio|
