# FEED

## 数据集
该数据集主要包含了五种类型的金融事件：股权回购(ER)，股权冻结(EF)，股权减持(EU)，股权增持(EO)，股权质押(EP)
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

在构建该数据集时，主要包含两个步骤：知识库构建和远程监督标注
### 知识库构建

### 远程监督标注
