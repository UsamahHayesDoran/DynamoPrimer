# 词典
Dynamo 2.0 引入了将词典数据类型与列表数据类型进行分隔的概念。此更改可能会对您在工作流中创建和使用数据的方式作出一些重大改变。在 2.0 之前，词典和列表已组合为一种数据类型。简而言之，列表实际上是带有整数键的词典。

* #### 什么是词典？
词典是由一组键值对组成的数据类型，其中每个键在每个集合中是唯一的。词典没有顺序，基本上您可以使用键而不是类似列表的索引值来“查找”内容。*在 Dynamo 2.0 中，键只能是字符串。

* #### 什么是列表？
列表是由有序值集合组成的数据类型。在 Dynamo 中，列表使用整数作为索引值。

* #### 为什么要进行此更改？为什么我应该关心此更改？
词典与列表之间的分离将词典作为“一等公民”，您可以使用它们快速、轻松地存储和查找值，无需记住索引值或在整个工作流中保持严格的列表结构。在用户测试期间，当使用词典而不是多个 ```GetItemAtIndex``` 节点时，我们看到图形大小显著减小。

* #### 会产生哪些变化？
  * *语法*已发生更改，改变了初始化以及使用代码块中的词典和列表的方式。
    * 词典使用以下语法 ```{key:value}```
    * 列表使用以下语法 ```[value,value,value]```
  * 库中引入了*新节点*，以帮助您创建、修改和查询词典。
  * 加载脚本时，在 1.x 代码块中创建的列表将自动迁移为使用方括号 `[ ]` 而不是大括号 `{ }` 的新列表语法
![IMAGE](images/9-1/DYN20_Dictionary.png)

* #### 我为什么应该关心？您会将它们用于什么？
在计算机科学中，词典（如列表）是对象集合。虽然列表按特定顺序排列，但词典是*无序*集合。它们并不依赖于顺序编号（索引），而是使用*键*。

在下图中，我们演示了词典的潜在使用案例。通常，词典用于关联两个可能没有直接相关性的数据。在本例中，我们将单词的西班牙语版本连接到英文版本，供以后查找。
![IMAGE](images/9-1/9-1_dictionaryExample.png)
