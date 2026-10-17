
| 7 | Mountain Bike Socks, M | 9.50 |
| 8 | Mountain Bike Socks, L | 9.50 |
| 9 | Mountain Bottle Cap | 9.99 |
| 10 | Tights: Battery-Powered | 12.99 |
| 11 | Minarump | 19.99 |
| 12 | Chain | 20.24 |
| 13 | LL Road Tree | 21.49 |
| 14 | Fender Set - Mountain | 21.98 |
| 15 | Half-Finger Gloves, S | 23.5481 |
| 16 | Half-Finger Gloves, M | 23.5481 |
| 17 | Half-Finger Gloves, L | 23.5481 |
| 18 | Half-Finger Gloves, L | 24.45 |

#### 分析

这是一个很难破译的查询。它要求列出价格大于子查询中任何平均价格的产品列表。换句话说，它显示了所有 `ListPrice` 超过 7.95 的产品。

#### 子查询 All 1/2

`Any` 关键字被 `All` 关键字取代了。

#### 语法

```sql
-- all with nulls
select EnglishProductName, ListPrice from DimProduct
where ListPrice > all(select avg(ListPrice) from DimProduct
group by ProductSubcategoryKey
order by ListPrice asc)
```

#### 结果

| EnglishProductName | ListPrice |
|---|---|

#### 分析

该查询没有返回任何记录。它在寻找价格大于子查询中所有平均价格的产品。换句话说，它在寻找所有价格高于子分类平均价格最高值的产品。

那个数字大约是 1742——这是两个查询前的结果。但其中有一个平均价格（两个查询前）包含一个空值（null）。如果你愿意的话，空值是不确定的——因此无法保证 1742 这个数字确实是最大值。由于最大值未知，因此外部查询无法显示任何记录。

#### 子查询 All 2/2

我在子查询中添加了一个 `Having` 子句——这将消除所有带有空值的平均价格记录。

#### 语法

```sql
-- all without nulls
select EnglishProductName, ListPrice from DimProduct
where ListPrice > all(select avg(ListPrice) from DimProduct group by
ProductSubcategoryKey having avg(ListPrice) is not null)
order by ListPrice asc
```

#### 结果

| EnglishProductName | ListPrice |
|---|---|
| 1 | Mountain-200 Black, 36 | 2049.0982 |
| 2 | Mountain-200 Black, 46 | 2049.0982 |
| 3 | Mountain-200 Black, 42 | 2049.0982 |
| 4 | Mountain-200 Silver, 46 | 2071.4196 |
| 5 | Mountain-200 Silver, 38 | 2071.4196 |
| 6 | Mountain-200 Silver, 42 | 2071.4196 |
| 7 | Road-250 Red, 58 | 2181.5625 |
| 8 | Road-250 Black, 44 | 2181.5625 |
| 9 | Road-250 Black, 46 | 2181.5625 |
| 10 | Road-250 Black, 52 | 2181.5625 |
| 11 | Road-250 Black, 58 | 2181.5625 |
| 12 | Mountain-200 Black, 42 | 2294.99 |
| 13 | Mountain-200 Black, 38 | 2294.99 |
| 14 | Mountain-200 Black, 46 | 2294.99 |
| 15 | Mountain-200 Silver, 46 | 2319.99 |
| 16 | Mountain-200 Silver, 42 | 2319.99 |
| 17 | Mountain-200 Silver, 38 | 2319.99 |
| 18 | Touring-1000 Yellow, 46 | 2384.07 |

#### 分析

从子查询中删除了空平均价格后，任何子分类的最大平均价格肯定在 1742 之后。外部查询现在可以返回所有高于该最大平均价格的产品。这些产品的 `ListPrice` 从大约 2049 开始上升到 3578。

## 第 10 章：子查询

## 第 11 章：删除/插入/更新

![](img/906d042eab2493d2c9ccfd1e7ed07cdc_244_0.png)

### 用于 Microsoft SQL Server 2008 R2 的实用 SQL 查询

其他任何章节都涉及从表格和数据库中提取数据——即大量的 `Select` 语句。当然，这假设数据已经存在并且是你所需的格式。相比之下，本章专门用于从零开始输入和维护数据。没有良好的数据，你的 `Select` 语句将无任何返回。在这里，我们学习使用 `Insert` 语句进行数据输入，并使用 `Update` 语句维护数据准确性。此外，你将学习如何使用 `Delete` 语句删除过时或不需要的数据。还有示例查询展示了如何处理 `identity`（自动编号）列。

- 核心概念：插入记录、更新记录、删除记录、清空表、删除表、处理标识列
- 关键字：`Insert Into ... Select`, `Insert Into ... Values`, `Select Into`, `Update ... Set`, `Delete`, `Truncate Table`, `DBCC Checkident()`, `Set Identity_Insert`, `Drop Table`

#### Select Into

我们在本章中的第一个查询基于名为 `DimScenario` 的现有表创建一个新表 `Scenario`。有第二个 `Select` 来测试这个新表。该新表稍后用于练习。第一个查询还演示了 `Select Into`，这是将数据放入表的方法之一（多种方法之一）。

#### 语法

```sql
-- base table select into
select *
into Scenario
from DimScenario
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Actual |
| 2 | Budget |
| 3 | Forecast |

#### 分析

我们在本章中的第一个查询基于名为 `DimScenario` 的现有表创建了一个新表 `Scenario`。有第二个 `Select` 来测试这个新表。该新表稍后将用于练习。第一个查询还演示了 `Select Into`，这是将数据放入表的方法之一（多种方法之一）。

#### Truncate Table

表已经存在，因此 `Select Into` 失败。

```sql
-- error
select *
into Scenario
from DimScenario
```

Msg 2714, Level 16, State 4: 'Scenario'

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 4 | Actual |
| 5 | Budget |
| 6 | Forecast |
| 7 | Actual |
| 8 | Budget |
| 9 | Forecast |

#### 分析

如果你到为止完全遵循了这些步骤，你应该有六行。三条记录是由上一个查询插入的，另外三条是由此查询插入的。但如果你仔细观察，标识列 `ScenarioKey` 现在从 4 开始了！

#### 清空带标识列的表

在执行下一次 `Insert Into ... Select` 之前，让我们用 `Truncate Table` 清空表。

#### 语法

```sql
-- identities!
truncate table Scenario
---
insert into Scenario (ScenarioName)
select ScenarioName from DimScenario
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Actual |
| 2 | Budget |
| 3 | Forecast |

#### 分析

`ScenarioKey` 列现在从 1 开始。`Truncate Table` 重置了标识列，使其能够再次从头开始自动编号。

### 带标识列的删除 1/2

这次，我们在重新填充 `Scenario` 表之前，将使用 `Delete` 而不是 `Truncate Table`。

#### 语法

```sql
-- delete again
delete Scenario
-- delete from Scenario also occurs
--
insert into Scenario (ScenarioName)
select ScenarioName from DimScenario
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 4 | Actual |
| 5 | Budget |
| 6 | Forecast |

#### 分析

现在 `ScenarioKey` 从 4 开始。它从上次计数停止的地方继续向下计数。`Delete`（与 `Truncate Table` 不同）不会重置标识列。

### 带标识列的删除 2/2

那么，在 `Delete` 之后如何重置标识列呢？这里的第二个查询使用了 `DBCC Checkident()`。

#### 语法

```sql
-- delete with identities
delete Scenario
-- reseed
dbcc checkident(Scenario, reseed, 0)
--
insert into Scenario (ScenarioName)
select ScenarioName from DimScenario
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Actual |
| 2 | Budget |
| 3 | Forecast |

#### 分析

你的 `ScenarioKey` 应该再次从 1 开始。`DBCC Checkident()` 接受表名、Reseed 键和 reseed 值。这这一切有点复杂，为什么要费这个劲呢？

`Truncate Table` 会删除表中的所有记录。`Delete`（不带 `Where` 子句）执行相同的操作。`Truncate Table` 重置标识列，而 `Delete` 不会。然而，如果 `Truncate Table` 没有记录，它是危险的。无论如何，如果表涉及引用完整性关系，它将无法工作。你可能更喜欢或被迫使用 `Delete` 来清空表。但为什么要担心在 `Delete` 之后用 `DBCC Checkident` 重置标识列呢？好吧，如果它再次从 1 开始看起来会好一些。但更重要的是，你可能会用光数字，而后续的插入将不会。你用光数字的点取决于标识列的数据类型。`Tinyint` 限制为几百，`smallint` 的限制仅略高于 3 万，而 `int` 的限制约为二十亿。在性能和存储空间方面，`tinyint` 优于 `smallint`，而 `smallint` 又优于 `int`。你将在性能和数字限制之间面临权衡。`DBCC Checkident()` 重置标识列可以帮助你避免这种权衡。

### 带 Where 的删除

如果一切顺利，你应该在新的 `Scenario` 表中拥有三条记录，标识列从 1 开始。到目前，`Truncate Table` 和 `Delete` 每次都成功删除了所有记录。`Truncate Table` 和 `Delete` 可能非常危险！如果你有日志（通过恢复模型），`Delete` 更安全——它很容易撤销。为 `Delete` 添加一个 `Where` 子句要安全得多（`Truncate Table` 不支持该）。

#### 语法

```sql
-- delete with where
delete Scenario
where ScenarioName = 'Budget'
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Actual |
| 2 | Forecast |

#### 分析

你应该拥有两条完整的记录。由于 `Delete` 有一个 `Where` 子句，这意味着只有一条记录被删除了。

### 重新创建基础表

在进入另一个主题 `Update` 之前，让我们重新创建 `Scenario` 表。

#### 语法

```sql
-- reset
truncate table Scenario
--
insert into Scenario (ScenarioName)
select ScenarioName from DimScenario
--
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Actual |
| 2 | Budget |
| 3 | Forecast |

#### 分析

你回到了三行。

### 更新

这是 `Update ...` 语法。正如你预期的那样，`Update` 会更改现有数据。

#### 语法

```sql
-- update one column
update Scenario
set ScenarioName = 'forecast'
select * from Scenario
```

#### 结果

| ScenarioKey | ScenarioName |
|---|---|
| 1 | Revised forecast |
| 2 | Revised forecast |
| 3 | Revised forecast |

#### 分析

哎呀，我忘记使用 `Where` 子句了！现在所有 `ScenarioName` 列都有相同的数据。

### 带 Where 的更新 1/2

在上一查询中，我们在 `Update` 中带了一个 `Where` 子句。

#### 语法
