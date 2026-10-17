
```sql
WITH LastDay AS (
  SELECT
    GROUPING_ID(custid, empid, YEAR(orderdate), MONTH(orderdate), DAY(orderdate)) AS grp_id,
    custid, empid,
    YEAR(orderdate) AS orderyear,
    MONTH(orderdate) AS ordermonth,
    DAY(orderdate) AS orderday,
    SUM(qty) AS qty
  FROM dbo.orders
  WHERE orderdate = '20140419'
  GROUP BY
    CUBE(custid, empid),
    ROLLUP(orderdate), MONTH(orderdate), DAY(orderdate)
)
MERGE dbo.GroupingSets AS TGT
USING LastDay AS SRC
ON EXISTS (
  SELECT SRC.grp_id, SRC.orderdate, SRC.ordermonth, SRC.orderday, SRC.custid, SRC.empid
  INTERSECT
  SELECT TGT.grp_id, TGT.orderdate, TGT.ordermonth, TGT.orderday, TGT.custid, TGT.empid
)
WHEN MATCHED THEN
  UPDATE SET TGT.qty = SRC.qty
WHEN NOT MATCHED THEN
  INSERT (grp_id, custid, empid, orderyear, ordermonth, orderday, qty)
  VALUES (SRC.grp_id, SRC.custid, SRC.empid, SRC.orderyear, SRC.ordermonth, SRC.orderday, SRC.qty);
```

## 结论

本章涵盖了大量关于数据分析的内容。它从深度的窗口函数开始，描述了不同类型，以及处理间隙和孤岛问题（`gaps and islands problems`）的实际用途。接着涵盖了处理透视（`pivoting`）和逆透视（`unpivoting`）任务的技术，展示了基于标准的方法以及基于专有的 `PIVOT` 和 `UNPIVOT` 算子的解决方案。随后，本章介绍了处理自定义聚合计算（如字符串拼接和乘积）的不同方法。最后，本章介绍了你可以用于在同一查询中为多个分组集计算聚合的若干功能。

## 第 5 章

# TOP 和 OFFSET-FETCH

SQL 中的经典筛选器（如 `ON`、`WHERE` 和 `HAVING`）是基于谓词的。`TOP` 和 `OFFSET-FETCH` 是基于不同概念的筛选器：你指定顺序以及根据该顺序过滤的行数。许多过滤任务是定义在顺序和所需的行数上的。在 T-SQL 中拥有语言支持，允许你以接近你思考任务的方式来表述请求，这无疑是一件好事。

本章从筛选器的逻辑设计方面开始，然后使用分页场景来演示优化。本章还涵盖了在修改语句中使用 `TOP`。最后，本章演示了使用 `TOP` 和 `OFFSET-FETCH` 来解决实际问题：每组前 N 和中位数。

## TOP 和 OFFSET-FETCH 筛选器

你使用 `TOP` 和 `OFFSET-FETCH` 筛选器以直观的方式实现查询中的过滤需求。`TOP` 筛选器是 T-SQL 的专用功能，而 `OFFSET-FETCH` 筛选器是一个标准功能。T-SQL 从 Microsoft SQL Server 2012 开始支持 `OFFSET-FETCH`。截至 SQL Server 2014，T-SQL 中的 `OFFSET-FETCH` 实现仍然缺少标准元素——有趣的是，这些元素在 `TOP` 中是可用的。根据目前的实现，每个筛选器都拥有对方不支持的功能。

我将先开始描述 `TOP` 的逻辑设计方面，然后介绍 `OFFSET-FETCH` 的相关内容。

# TOP 筛选器

`TOP` 筛选器是 T-SQL 中常用的构造结构。它的流行可能归功于其设计与许多表达出来的过滤需求非常契合——例如，“返回最近的三个订单”。在这一请求中，筛选顺序是基于 `orderdate` 降序，且要根据顺序过滤的行数是 3。

你在 `SELECT` 列表中指定 `TOP` 选项并输入一个如 `BIGINT` 的值，表示你想过滤的行数。你在经典的 `ORDER BY` 子句中提供排序规范。例如，你使用以下查询获取最近的三个订单。

```sql
USE TSQLV3;

SELECT TOP (3) orderid, orderdate, custid, empid
FROM Sales.Orders
ORDER BY orderdate DESC;
```

我从此查询中得到了以下输出：

| orderid | orderdate | custid | empid |
|---|---|---|---|
| 11077 | 2015-05-06 | 65 | 1 |
| 11076 | 2015-05-06 | 9 | 4 |
| 11075 | 2015-05-06 | 68 | 8 |

与其指定你想过滤的行数，不如使用 `TOP` 来指定百分比（查询结果的总行数）。你通过提供 0 到 100 范围内的值（类型为 `FLOAT`）并添加 `PERCENT` 关键字来实现此。例如，在以下查询中，你请求过滤百分之一的行：

```sql
SELECT TOP (1) PERCENT orderid, orderdate, custid, empid
FROM Sales.Orders
ORDER BY orderdate DESC;
```

SQL Server 对根据输入的百分比计算的行数向上取整。例如，应用于 `Orders` 表中 830 行的 1% 结果是 8.3。将此数字向上取整，你得到 9。这是我为此查询得到的输出：

| orderid | orderdate | custid | empid |
|---|---|---|---|
| 11074 | 2015-05-06 | 73 | 7 |
| 11075 | 2015-05-06 | 68 | 8 |
| 11076 | 2015-05-06 | 9 | 4 |
| 11077 | 2015-05-06 | 65 | 1 |
| 11070 | 2015-05-05 | 44 | 2 |
| 11071 | 2015-05-05 | 46 | 1 |
| 11072 | 2015-05-05 | 20 | 4 |
| 11073 | 2015-05-05 | 58 | 2 |
| 11067 | 2015-05-04 | 17 | 1 |

> **注意**：要将输入的百分比转换为行数，SQL Server 必须先确定查询结果的行数，这通常需要额外的工作。

有趣的是，排序规范对于 `TOP` 筛选器是可选的。例如，考虑以下查询：

```sql
SELECT TOP (3) orderid, orderdate, custid, empid
FROM Sales.Orders;
```

为了提供呈现排序保证，你必须在外部查询中指定 `ORDER BY` 子句，例如：

```sql
SELECT orderid, orderdate, custid, empid
FROM (
  SELECT TOP (3) orderid, orderdate, custid, empid
  FROM Sales.Orders
  ORDER BY orderdate DESC, orderid DESC
) AS D
ORDER BY orderdate DESC, orderid DESC;
```

## OFFSET-FETCH 过滤器

`OFFSET-FETCH` 过滤器是一个与 `TOP` 设计类似的标准功能，但它多了一个元素。你可以在指定要过滤哪些行之前，指定要跳过多少行。

正如你所料到的，此功能在实现分页解决方案时非常有用——即当完整结果过长，无法在一个屏幕或网页上完全显示时，根据请求每次向用户返回分块结果。

`OFFSET-FETCH` 过滤器要求存在 `ORDER BY` 子句，并且紧跟在其后指定。你首先通过 `OFFSET` 子句指定要跳过的行数，然后通过 `FETCH` 子句指定要过滤的行数数量。例如，根据指定的顺序，以下查询将跳过前 50 行并过滤接下来的 25 行：

```sql
SELECT orderid, orderdate, custid, empid
FROM Sales.Orders
ORDER BY orderdate DESC, orderid DESC
OFFSET 50 ROWS FETCH NEXT 25 ROWS ONLY;
```

换句话说，查询过滤了第 51 到 75 行。在分页术语中，假设页面大小为 25 行，此查询返回了第三页。

为了允许自然的声明式语言，如果你喜欢，可以使用 `FIRST` 替代 `NEXT`，尽管它们的含义相同。如果你不跳过任何行，使用 `FIRST` 可能会更直观。如果你不想跳过任何行，T-SQL 仍然强制要求指定 `OFFSET` 子句（使用 `0 ROWS`）以避免解析歧义。同样，你不需要使用关键字 `ROWS` 的复数形式，可以在 `OFFSET` 和 `FETCH` 子句中都使用单数形式 `ROW`。如果你只需要跳过或过滤一行，这样会更自然。

如果你对关键字 `ONLY` 的用途感到好奇，它意味着不包含相同值（ties）。标准 SQL 定义了替代方案 `WITH TIES`；但 T-SQL 不支持它。同样，标准 SQL 定义了 `PERCENT` 选项，但 T-SQL 目前也不支持。这些缺失的选项在 `TOP` 过滤器中可用。

如所述，`OFFSET-FETCH` 过滤器需要 `ORDER BY` 子句。如果你想使用任意顺序（类似于不带 `ORDER BY` 子句的 `TOP`），你可以使用 `ORDER BY (SELECT NULL)` 技巧，如下：

```sql
SELECT orderid, orderdate, custid, empid
FROM Sales.Orders
ORDER BY (SELECT NULL)
OFFSET 0 ROWS FETCH NEXT 3 ROWS;
```

`FETCH` 子句是可选的。如果你想跳过某些行但不限制返回的行数，只需不使用 `FETCH` 子句即可。例如，以下查询跳过了 50 行，但不限制返回的行数：

```sql
SELECT orderid, orderdate, custid, empid
FROM Sales.Orders
ORDER BY orderdate DESC, orderid
OFFSET 50 ROWS;
```

关于呈现排序，其行为与 `TOP` 过滤器相同；即，使用 `OFFSET-FETCH` 时，只有当最外层查询具有 `ORDER BY` 时，才能保证呈现排序。

## 通过分页演示过滤器的优化

到目前，我描述了 `TOP` 和 `OFFSET-FETCH` 过滤器的逻辑设计方面。在本节，我将涵盖优化方面。我将通过查看不同的分页解决方案来实现。我将描述两种使用 `TOP` 过滤器的分页解决方案、一个使用 `OFFSET-FETCH` 过滤器的解决方案，以及一个使用 `ROW_NUMBER` 函数的解决方案。

在所有情况下，无论你为分页解决方案使用何种过滤选项，排序元素上的索引对于良好的性能都是至关重要的。通常，即使索引不是覆盖索引，也能获得良好的性能。奇怪的是，有时当索引没有覆盖时你反而会获得更好的性能。我将在具体的实现中提供细节。

我将在示例中使用 `PerformanceV3` 数据库中的 `Orders` 表。假设你需要实现一个分页解决方案，根据 `orderid` 键每次返回一页订单。该表有一个名为 `PK_Orders` 的非聚集索引，以 `orderid` 为键。对于我将要演示的分页查询，该索引并不是覆盖索引。

## TOP 的优化

你可以使用几种策略来实现基于 `TOP` 的分页解决方案。一种是基于锚点（anchor-based）的策略，另一种是 `TOP OVER`（嵌套 `TOP` 查询）。

基于锚点的策略允许用户逐步访问页面。你定义一个存储过程，当上一页最后一行的排序键存在时，它返回下一页。以下是此类过程的实现：

```sql
USE PerformanceV3;
IF OBJECT_ID('dbo.GetPage', 'P') IS NOT NULL DROP PROC dbo.GetPage;
GO
CREATE PROC dbo.GetPage
  @orderid AS INT = 0, -- anchor sort key
  @pagesize AS BIGINT = 25
AS
SELECT TOP (@pagesize) orderid, orderdate, custid, empid
FROM dbo.orders
WHERE orderid > @orderid
ORDER BY orderid;
GO
```

在这里我假设支持可能的 `order ID`。当然，你可以使用 `CHECK` 约束来实现一个完整性规则。查询使用 `WHERE` 子句仅过滤大于 `@orderid` 的行。在剩余的行中，使用 `TOP` 过滤出第一页。

要请求第一页，请使用以下代码：

```sql
EXEC dbo.GetPage @orderid = 0, @pagesize = 25;
```

我得到了以下结果（但由于示例数据中的随机性，你的结果可能不同）：

要请求第二页，传递 25 作为输入：

```sql
EXEC dbo.GetPage @orderid = 25, @pagesize = 25;
```

要请求第三页，传递 50 作为输入：

```sql
EXEC dbo.GetPage @orderid = 50, @pagesize = 25;
```

`Index Seek` 算符中的范围扫描不仅被缩减到 `TOP` 的行数目标（`Top Expression` 属性），查询优化器还需要根据该行数目标调整受影响算符的成本。优化的这一方面在 Paul White 的一篇优秀文章中进行了详细描述：“The Optimizer: Row Goals In”。你可以在此处找到该文章：http://sqlblog.com/blogs/paul_white/archive/2010/08/18/inside-the-optimizer-row-goals-in-depth.aspx。

执行查询计划涉及的 I/O 成本由以下项管理：

- 叶子节点查找：3 次读取（索引有三层）
- 25 行范围扫描：0–1 次读取（每页数百行）
- 用于优化查找的嵌套循环预取（`Nested Loops prefetch`）：9 次读取（通过跟踪标志 8744 禁用预取来测量）
- 25 次键查找：75 次读取

处理此查询总共报告了 87 次逻辑读取。这不算坏。可以更好也可以更糟？两方面都是。你可以通过创建覆盖索引来获得更好的性能。这样，你就消除了预取和查找的成本，导致总共只有 3–4 次逻辑读取。如果你没有以排序列作为前导键的良好索引——甚至没有非覆盖索引，性能可能会糟糕得多。这会导致计划对数据进行全扫描，不仅如此。这是一个非常昂贵的计划，特别是考虑到你为用户请求的每一页都要付出代价。
