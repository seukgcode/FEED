# FEED

## 数据集
该数据集的构建主要分为两个部分：知识库构建和远程监督标注

### 知识库构建

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
