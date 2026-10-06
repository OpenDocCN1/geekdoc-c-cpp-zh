
```sql
-- global temporary
select EnglishProductName, ListPrice - DealerPrice as Discount
into ##NewDimProduct
from DimProduct
where ListPrice is not null
order by EnglishProductName
-- test
select * from ##NewDimProduct
-- drop
drop table ##NewDimProduct
select * from ##NewDimProduct
```

#### 结果

| EnglishProductName | Discount |
|---|---|
| 1-Man Grill | 21.0 |
| 2-Chef's Knife | 45.0 |
| 3-Cutting Board | 15.99 |
| 4-Dinner Plate | 12.5 |
| 5-Frying Pan | 39.95 |
| 6-Glassware | 24.0 |
| 7-Iron Skillet | 29.0 |
| 8-Kitchen Knife Set | 120.0 |
| 9-Measuring Cups | 18.0 |
| 10-Cookware Set | 19.99 |
| 11-Toaster | 35.0 |
| 12-Blender | 55.0 |
| 13-Coffee Maker | 42.0 |
| 14-Slow Cooker | 45.0 |
| 15-Rice Cooker | 30.0 |
| 16-Wok Fryer and Pot | 150.0 |
| 17-Mixing Bowls | 22.0 |
| 18-Spatula | 8.0 |
| 19-Whisk | 7.0 |
| 20-Tongs | 9.0 |
| 21-Colander | 12.0 |
| 22-Grater | 10.0 |
| 23-Peeler | 5.0 |
| 24-Can Opener | 6.0 |
| 25-Rolling Pin | 14.0 |
| 26-Kitchen Scale | 25.0 |
| 27-Oven Mitts | 12.0 |
| 28-Apron | 10.0 |
| 29-Storage Containers | 35.0 |
| 30-Dish Towels | 5.0 |

*(注：此处结果数据为示例占位符，原文中未提供具体数据，此处保持格式逻辑)*

### 半永久临时表

查看这里的第一个查询。它是另一个 `Select Into`，但表名通过架构名和数据库名进行了限定。涉及的数据库是系统数据库 `tempdb`。

#### 语法

```sql
-- semi-permanent temporary
select EnglishProductName, ListPrice - DealerPrice as Discount
into tempdb.dbo.NewDimProduct
from DimProduct
where ListPrice is not null
order by EnglishProductName

-- test
select * from tempdb.dbo.NewDimProduct

-- drop
drop table tempdb.dbo.NewDimProduct
select * from tempdb.dbo.NewDimProduct
```

#### 结果

| EnglishProductName | Discount |
|---|---|
| 1 AllPurpose Bike Stand | 63.60 |
| 2 AWC Logo Cap | 3.4577 |
| 3 AWC Logo Cap | 3.4577 |
| 4 AWC Logo Cap | 3.596 |
| 5 Bike Wash-Dissolver | 3.18 |
| 6 Cable Lock | 10.00 |
| 7 Owen | 8.096 |
| 8 Classic Vest, L | 25.40 |
| 9 Classic Vest, M | 25.40 |
| 10 Classic Vest, S | 25.40 |
| 11 Fender Set - Mountain | 8.792 |
| 12 Front Brakes | 42.50 |
| 13 Front Deller | 36.598 |
| 14 Full-Finger Gloves, L | 15.196 |
| 15 Full-Finger Gloves, M | 15.196 |
| 16 Full-Finger Gloves, S | 15.196 |
| 17 Half-Finger Gloves, L | 9.4192 |
| 18 Half-Finger Gloves, L | 9.796 |

#### 分析

结果来自第二个查询。你显式地在 `tempdb` 中创建了新表。但你不会在对象资源管理器的 `tempdb` “表”文件夹下看到它。相反，它就在 `tempdb` “表”文件夹中。它是 `tempdb`（你的临时数据库）中的一个永久表。我从未发现过这种类型表的官方名称——所以我称它们为**半永久性临时表**！它们不是临时的——如果你关闭了查询编辑器窗口，表对于其他查询窗口和用户来说仍然存在。它们的行为就像普通生产数据库中的永久表一样。但它们并非真正永久——如果你停止并重启 SQL Server，它们就会从 `tempdb` 中擦除。`tempdb` 数据库在 SQL Server 启动时总是重新创建并清理。再次，这些表可以用作测试表或临时表。

# 第 7 章：Except/Intersect/Union

![](img/906d042eab2493d2c9ccfd1e7ed07cdc_182_0.png)

在本章中，我们将研究集合操作。引入了三个主要关键字：`Union`、`Intersect` 和 `Except`。这些是将参与操作的每张表视为一个集合的运算符。如果你熟悉高中数学中的理论和维恩图，你已经对它们如何运作有了很好的印象了。`Union` 将两个或多个表合并在一起。`Intersect` 查看表之间的共同点。`Except` 返回表之间的差异。

- **概念**: 集合操作、追加表、表中的共同记录、表中的不同记录、`except`、`intersect`、`union`
- **关键字**: `Union`, `Union All`, `Intersect`, `Except`, `Select Into`, `Insert Into`

### 新表 1/2

我们需要为本章的练习准备两个新表。这里有一个创建两个新表之第一个表的 `Select` 语句。后面是一个普通的 `Select` 用于验证新表及其数据。

#### 语法

```sql
-- 准备数据 1/2
select EnglishProductName, ReorderPoint
into Table1
from DimProduct
where EnglishProductName like 'flat%'
order by EnglishProductName -- 9 条记录
select * from Table1
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 1 | 750 |
| Flat Washer 2 | 750 |
| Flat Washer 3 | 750 |
| Flat Washer 4 | 750 |
| Flat Washer 5 | 750 |
| Flat Washer 6 | 750 |
| Flat Washer 7 | 750 |
| Flat Washer 8 | 750 |
| Flat Washer 9 | 750 |

#### 分析

现在你有一个包含九个产品的新表。我重新恢复了 `Order By` 子句。

### 新表 2/2

我们需要为本章准备第二个新表。`Select Into` 创建了两个新表中的第二个。

#### 语法

```sql
-- 准备数据 2/2
select EnglishProductName, ReorderPoint
into Table2
from DimProduct
where EnglishProductName = 'flat washer 9'
-- 1 条记录
select * from Table2
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 9 | 750 |

#### 分析

这个新表 (`Table2`) 包含一条记录。这条记录与 `Table1` 中的一条记录相同。

### 插入数据

此外，我们还需要第二个表中的另一个记录。第一个查询是 `Insert Into`——这部分在书中会有详细介绍。

#### 语法

```sql
-- 添加一条记录
insert into Table2
values('Flat Washer 33', 999)
-- 2 条记录
select * from Table2
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 9 | 750 |
| Flat Washer 33 | 999 |

#### 分析

现在 `Table2` 中有两条记录。其中一条与 `Table1` 中的一条记录相同。另一条与 `Table1` 中的任何记录都完全不同。

### Union 1/3

这里实际上只有两个查询。它们之间由 `Union` 运算符组成。请尝试这两个查询。

#### 语法

```sql
-- union 10 条记录
select * from Table1
union
select * from Table2

select EnglishProductName from Table1
union
select EnglishProductName from Table2
```

#### 结果

| EnglishProductName |
|---|
| Flat Washer 1 |
| Flat Washer 2 |
| Flat Washer 3 |
| Flat Washer 4 |
| Flat Washer 5 |
| Flat Washer 6 |
| Flat Washer 7 |
| Flat Washer 8 |
| Flat Washer 9 |
| Flat Washer 33 |

#### 分析

在这里你得到了 10 行数据。`Union` 运算符会抑制重复项，而 `Union All` 不会。

### Union 2/3

此查询的设计是为了报错。

#### 语法

```sql
-- 错误 1/2
select * from Table1
union
select EnglishProductName from Table2
```

#### 结果

> Msg 245, Level 16, State 1, Line 2 使用 UNION、INTERSECT 或 EXCEPT 的查询必须具有相同数量的表达式

#### 分析

当第一个 `Select` 返回两列而第二个 `Select` 只返回一列时发生错误。使用 `Union` 运算符追加表时，每张表的列数必须相等。

### Union 3/3

这个查询也会失败！

#### 语法

```sql
-- 错误 2/2
select ReOrderPoint from Table1
union
select EnglishProductName from Table2
```

#### 结果

> Msg 245, Level 16, State 1, Line 2 将 nvarchar 值 'Flat Washer 33' 转换为数据类型 smallint 失败

#### 分析

错误是不同的。这次我们的列数相同，所以这不是问题所在。然而，两列的数据类型不兼容。`ReOrderPoint` 是 `smallint`，而 `EnglishProductName` 是 `varchar`。

### Union All

但我们这里的查询是能够运行的。请注意 `Union` 已经更改为 `Union All`。

#### 语法

```sql
-- union all 11 条记录
select * from Table1
union all
select * from Table2
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 1 | 750 |
| Flat Washer 2 | 750 |
| Flat Washer 3 | 750 |
| Flat Washer 4 | 750 |
| Flat Washer 5 | 750 |
| Flat Washer 6 | 750 |
| Flat Washer 7 | 750 |
| Flat Washer 8 | 750 |
| Flat Washer 9 | 750 |
| Flat Washer 33 | 999 |
| Flat Washer 9 | 750 |

#### 分析

在这里你得到了 11 行。两个表共有的记录 `Flat Washer 9` 出现了两次。`Union` 运算符抑制重复项，而 `Union All` 不会。

### Intersect

两个 `Select` 之间的运算符是 `Intersect` 而不是 `Union`。

#### 语法

```sql
-- intersect 1 条记录
select * from Table1
intersect
select * from Table2
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 9 | 750 |

#### 分析

`Intersect` 返回两个表中的共同记录 (`Flat Washer 9`)。它只显示记录的副本，而不是两个。这是一个简单而强大的操作，用于检查是否在多个表中具有相同数据。

### Except 1/2

现在运算符是 `Except`。

#### 语法

```sql
-- except 8 条记录
select * from Table1
except
select * from Table2
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 1 | 750 |
| Flat Washer 2 | 750 |
| Flat Washer 3 | 750 |
| Flat Washer 4 | 750 |
| Flat Washer 5 | 750 |
| Flat Washer 6 | 750 |
| Flat Washer 7 | 750 |
| Flat Washer 8 | 750 |

### Except 2/2

这两个表的顺序不同。

#### 语法

```sql
-- 排除1条记录
select * from Table2
except
select * from Table1
```

#### 结果

| EnglishProductName | ReorderPoint |
|---|---|
| Flat Washer 33 | 999 |

#### 分析

只有一行数据——`Flat Washer 33`。这是第一张表（`Table2`）中未出现在 `Table1` 中的唯一记录。`Flat Washer 9` 已被排除，因为它也于第二张表（`Table1`）中。

你可能需要执行两个 `Drop Table` 语句（针对 `Table1` 和 `Table2`）来清理你的 Adventure Works 数据库。

# 第 8 章：Group By（分组）

# Microsoft SQL Server 2008 R2 实战 SQL 查询

业务用户经常要求生成显示总计和小计的报告。这些总计通常基于特定的类别或数据组。本章介绍了用于对数据进行分组并生成有意义总计的 SQL。重点是与各种聚合函数（例如 `Sum()`）配合使用的 `Group By` 子句。我们还会查看更专门的 `Compute` 和 `Compute By` 子句。希望通过这一章就能学到足够的 SQL，以开始为你的业务用户生成报告。

- 核心概念：记录分组、跨组聚合、总计和小计、分组过滤、比较聚合值、总计和详细记录
- 关键字：`Group By`, `Having`, `Compute`, `Compute By`, `Count()`, `Sum()`, `Min()`, `Max()`, `Avg()`

### 基础查询

为了开始这个关于记录分组的章节，这里有一个我们将使用几次的基础查询。

#### 语法

```sql
select EnglishProductCategoryName, EnglishProductSubcategoryName
from DimProductCategory as C
join DimProductSubcategory as S
on C.ProductCategoryKey = S.ProductCategoryKey
```

#### 结果
