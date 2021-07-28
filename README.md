# FEED

## 数据集
该数据集主要包含了五种类型的金融事件：股权回购(ER)，股权冻结(EF)，股权减持(EU)，股权增持(EO)，股权质押(EP)。每种事件类型的数据量如下表所示：
|Event Type|Train|Dev|Test|
|:--:|:--:|:--:|:--:|
|ER|2942|360|365|
|EF|938|120|110|
|EU|4453|560|580|
|EO|4622|580|585|
|EP|12443|1555|1535|
|Total|25398|3175|3175|

在构建该数据集时，主要包含两个步骤：知识库构建和远程监督标注。
### 知识库构建
知识库的构建可以分成三个步骤：数据预处理，候选集生成和弱监督分类。  
在数据预处理过程中，使用pdfminer将PDF格式的财务公告转换为HTML格式，并将所有公告输入Fonduer。PDF格式的数据负责提供可视化信息，HTML格式的数据负责提供文本和结构化信息。Fonduer系统首先对HTML格式数据进行解析，识别段落、句子、表格等，然后将解析后的内容转换为Fonduer中定义的数据模型。Fonduer中的数据模型是一个有向无环图(DAG)，它可以清楚地描述文档上下文之间的层次结构。图中的每个节点代表一个上下文。DAG的根节点是相应的文档。一份文件可分为几章。章节包括文本、表格和图片。文章按段落划分，每个段落由不同的句子组成。对于表格数据，行、列和标题属性可以分段。注意，声明数据不包含图像内容。使用Fonduer数据模型的优势在于，它可以从文档的不同上下文中提取事件参数，并形成候选事件。  
在得到候选事件后，我们通过命名实体识别工具和正则表达式提取事件中的一些事件元素，包括人名，机构名，数量等。由于不同实体的组合会形成一个新的候选事件，这可能会导致候选事件的数量呈指数级增长。因此，在生成的候选事件中存在大量的负面例子。我们通过以下规则来筛选候选事件:1.如果多个事件参数有相同的值，其余的可以被过滤掉；2.如果任何键事件参数的值为空，则可以将其过滤掉；3.如果一个事件参数在表结构中，那么其他事件参数也应该在同一表的同一行，否则它会被过滤掉。  
在弱监督分类中，用户首先通过标注函数为数据提供弱监督标签，然后使用分类模型从人工标注的数据中学习潜在的关系，使用测试数据验证模型的性能，最后用户通过观察模型的性能来调整标记功能。这样的过程是反复的。最终会训练出性能更好的分类模型。利用该模型对所有候选事件进行标记后，可以得到一个结构化的事件知识库。这里的标记函数是一个数据编程范例，它是以一种程序化的方式标记候选事件，即将候选事件标记为正/负示例或跳过标记。
### 远程监督标注
经过上述步骤得到金融事件知识库之后，我们采用远程监督的方式对爬取的文档数据进行标注。首先清洗文本数据。数据清理是对转换后的文本进行标准化，主要包括过滤乱码和根据特殊符号对句子进行分割。然后，我们根据文档ID从知识库中检索文档中的结构化事件，并使用BIO格式标记事件参数。通过两个条件过滤标注结果:(1)事件必须包含事件本体定义的关键角色(如个人或公司)，(2)文档和事件本体具有相同数量的事件角色。最后，我们获得了五类事件的标记数据:股权冻结(EF)、股权回购(ER)、股权减持(EU)、股权增持(EO)和股权质押(EP)。其中，每个事件类型由不同的事件元素组成，如下表所示：
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
