
| 7 | 18104.80 | 66689.14 | 56502.05 |
| 1 | 38789.00 | 97533.58 | 65821.13 |
| 4 | 53114.80 | 139477.70 | 57594.95 |
| 5 | 21965.20 | 32595.05 | 21007.50 |
| 2 | 22834.70 | 74958.60 | 79955.96 |
| 8 | 23161.40 | 59776.52 | 50363.11 |

当你完成后，运行以下代码进行清理：

```sql
IF OBJECT_ID(N'dbo.sp_pivot', N'P') IS NOT NULL DROP PROC dbo.sp_pivot;
```

# 动态搜索条件

动态搜索条件（也称为动态过滤）是应用程序中的常见需求。其核心思想是应用程序提供按各种属性过滤数据的接口，由用户每次请求选择要过滤的属性。为了演示处理动态搜索条件的技术，我将在示例中使用名为 `Orders` 的表。运行以下代码在 `tempdb` 中创建 `TSQLV3.Sales.Orders` 的副本 `Orders` 表，并带有几个索引以支持过滤器：

```sql
SET COUNT ON;
USE tempdb;

IF OBJECT_ID(N'dbo.GetOrders', N'P') IS NOT NULL DROP PROC dbo.GetOrders;
IF OBJECT_ID(N'dbo.Orders', N'U') IS NOT NULL DROP TABLE dbo.Orders;
GO
```

```sql
SELECT orderid, customer, empid, orderdate,
CAST('A' AS CHAR(200)) AS filter
INTO dbo.Orders
FROM TSQLV3.Sales.Orders;
```

```sql
CREATE CLUSTERED INDEX idx_orderdate ON dbo.Orders(orderdate);
CREATE UNIQUE INDEX idx_orderid ON dbo.Orders(orderid);
CREATE INDEX idx_custid_empid ON dbo.Orders(custid, empid) INCLUDE(orderid, orderdate, filler);
```

你的任务是创建一个存储过程 `dbo.GetOrders`，它接受四个可选输入，分别为 `@orderid`、`@custid`、`@empid` 和 `@orderdate`。该过程旨在查询 `Orders` 表并根据获取 `NULL` 值的参数过滤行。

该存储过程的以下实现代表了处理此任务最常用的技术之一：

```sql
IF OBJECT_ID('N.dbo.GetOrders', 'P') IS NOT NULL DROP PROC dbo.GetOrders;
GO
CREATE PROC dbo.GetOrders
@orderid AS INT = NULL,
@custid AS INT = NULL,
@empid AS INT = NULL,
@orderdate AS DATE = NULL
AS
```

```sql
SELECT order, custid, empid, orderdate, filler
FROM dbo.Orders
WHERE (orderid = @orderid OR @orderid IS NULL)
AND (custid = @custid OR @custid IS NULL)
AND (empid = @empid OR @empid IS NULL)
AND (orderdate = @orderdate OR @orderdate IS NULL);
GO
```

该过程使用静态查询，对于每个参数，它使用以下谓词的取析（OR 谓词）：`列 = @parameter OR @parameter NULL`。如果没有为参数提供值，则右侧的谓词为真。在谓词取析中，当其中一个操作数为真时，整个表达式即为真；因此对列不会发生任何过滤。如果指定了值，则右侧谓词为假；因此，左侧谓词是确定要过滤哪些行的唯一依据。

这种解决方案简单且易于维护；然而，当元素存在时，它往往会导致查询性能并非最优。原因在于，当你第一次执行该过程时，优化器会对代码的参数化形式进行优化，包含查询中的所有谓词。这意味着谓词既与当前查询执行相关的，也包含了在计划中是不相关的谓词。这种方法用于促进重用行为，以节省每次执行都创建新计划所涉及的时间和资源。此主题将在章节稍后的“编译、重新编译和执行计划的重用”部分进行详细介绍。这种方法确保了如果使用一组不同的相关参数再次调用过程，缓存的计划仍然有效并可以重用。如果计划必须在考虑查询中所有谓词（包括与当前执行无关的谓词）的情况下进行纠正，你会发现这可能是高效的。

例如，运行以下代码以仅为 `@orderdate` 参数提供输入值来执行过程：

```sql
EXEC dbo.GetOrders @orderdate = '20140101';
```

观察图 9-1 所示优化器为该查询创建的计划。

![](img/bdc38aa36f6e2987d913ee5381474711_561_0.png)

图 9-1 使用静态查询解决方案的计划。

计划中有不同的位置应用了不同的谓词，但点在于所有谓词都已考虑在内。如果基于 `orderdate` 列进行过滤，最高效的计划是在聚集索引上执行查找（seek）和范围扫描（range scan）。但你在这里看到的是完全不同的计划，对于这次执行非常无效。

你可以采取几件事来获取高效的计划。如果你愿意强制使用计划重用的用处，可以在查询末尾添加 `OPTION(RECOMPILE)`，这会强制 SQL Server 在每次执行时创建一个新计划。至关重要的是要使用语句级别的 `RECOMPILE` 而不是过程级别的 `RECOMPILE`。对于前者，解析器会执行参数嵌入，它将参数替换为常量，并在传递给优化器之前移除查询的冗余部分。结果是，查询仅优化了与当前执行相关的谓词，因此获得高效计划的概率非常大。

运行以下代码重新创建 `GetOrders` 过程，并在查询中添加 `RECOMPILE` 选项：

```sql
IF OBJECT_ID('n.dbo.GetOrders', 'N') IS NOT NULL DROP proc dbo.GetOrders;
GO
CREATE proc dbo.GetOrders
@orderid AS INT = NULL,
@custid AS INT = NULL,
@empid AS INT = NULL,
@orderdate AS DATE = NULL
```

```sql
SELECT orderid, custid, empid, orderdate, filler
FROM dbo.Orders
WHERE (orderid) = @orderid OR @orderid IS NULL
AND (custid) = @custid OR @custid IS NULL
AND (empid) = @empid OR @empid IS NULL
AND (orderdate) = @orderdate OR @orderdate IS NULL
OPTION (RECOMPILE);
GO
```

运行以下代码以测试基于 `orderdate` 列过滤的过程：

```sql
EXEC dbo.GetOrders @orderdate = '20140101';
```

该执行的计划如图 9-2 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_562_0.png)

图 9-2 使用静态查询解决方案的计划。

```sql
SET sql =
' SELECT orderid, custid, empid, orderdate, filler'
+ N ' /* 27702431-107C-478B-8157-60FCECC148DD */'
+ N ' FROM dbo.Orders'
+ N ' WHERE = 1 \'
+ CASE WHEN @orderid IS NOT NULL THEN
+ N ' AND orderid = @oid ELSE N' END
+ CASE WHEN @custid IS NOT NULL THEN
+ N ' AND custid = @ocid ELSE N' END
+ CASE WHEN @empid IS NOT NULL THEN
+ N ' AND empid = @eid ELSE N' END
+ CASE WHEN @orderdate IS NOT NULL THEN
+ N ' AND orderdate = @dt ELSE N' END;
```

```sql
EXEC sp_executesql
@stmt = @sql,
@params = N'@oid AS INT, @oc AS INT, @eid INT, @dt AS DATE',
@oid = @orderid,
@ocid = @custid,
@eid = @empid,
@dt = @orderdate;
```

观察我在查询注释中放置的 GUID。我是通过调用 `NEWID` 函数创建它的。这样做是为了更容易跟踪由存储过程执行的缓存计划，以便分析计划缓存和重用行为。我将对此演示。

运行以下代码，以执行两次基于 `orderdate` 列过滤的存储过程，但使用两个不同的日期：

```sql
EXEC dbo.GetOrders @orderdate = '20140101';
EXEC dbo.GetOrders @orderdate = '20140102';
```

这些执行操作的计划如图 9 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_564_0.png)

图 9-4 按 `orderdate` 过滤的动态查询的计划。

该计划是高效的，因为优化后的查询仅包含相关的谓词。此外，与使用 `RECOMPILE` 查询不同，这里没有参数嵌入，这在这种情况下是有益的。查询的参数化形式被优化并缓存，允许在存储过程使用相同的参数组合执行时重用计划。在第一次执行基于 `orderdate` 过滤的存储过程时， SQL Server 在缓存中没有找到现有计划，因此它优化了查询并将其缓存。对于第二次执行，它找到了相同字符串的缓存计划，因此重用了它。

再次执行存储过程，这次使用基于 `orderid` 列的过滤：

```sql
EXEC dbo.GetOrders @orderid = 10248;
```

这次构建的查询字符串包含一个基于 `orderid` 的参数化过滤。由于缓存中没有此查询字符串的计划，SQL Server 创建了新计划并将其缓存。图 9-5 显示了 SQL Server 为此查询字符串创建的计划。

![](img/bdc38aa36f6e2987d913ee5381474711_565_0.png)

**图 9-5** 按 `order` 过滤的动态查询的计划。

同样，你为此查询字符串获得了一个高效的计划，其中只有以参数化形式的相关谓词。现在对于存储过程执行的两个唯一查询字符串，你在缓存中有两个计划。使用以下查询来检查缓存计划及其重用行为，仅过滤出代码中提供了 GUID 的查询：

此代码生成以下输出：

```
usecounts                                              text
(@orderid AS INT, @cid AS INT, @eid AS INT, @dt AS DATE)
SELECT orderid, custid, empid, orderdate, filler
/ 27702431-107C-478C-8157-60FECCC148DD %
FROM orders WHERE = 1 AND orderid = @oid
(@orderid AS INT, @cid AS INT, @eid AS INT, @dt AS DATE)
SELECT orderid, custid, empid, orderdate, filler
/ 27702431-107C-478C-8157-60FECCC148DD %
FROM orders WHERE = 1 AND orderdate = @dt
```

注意到创建了两个计划，是因为存在唯一的查询字符串——一个带有 `orderid` 过滤（使用了一次），另一个带有 `orderdate` 过滤（使用了两次）。

第 9 章 可编程对象 541

该解决方案支持高效的计划和高效的计划重用。由于动态代码使用参数而不是注入代码中，因此它不会暴露于 SQL 注入攻击。与多个存储过程的解决方案相比，这种方法容易维护得多。这种解决方案似乎比其他方案具有强大优势。

我的朋友、同时 SQL Server MVP 的 Erland Sommerskog 写了一篇关于动态搜索主题的优秀论文。如果这这对你很重要，请务必查看 Erland 的论文。你可以在他的网站上找到：http://www.sommarskog.se/dyn-search.html。

## 动态排序

与动态搜索条件类似，*动态排序* 是另一个应用需求。例如，假设你需要在 `TSQLV3` 数据库中开发一个名为 `dbo.GetSortedShippers` 的存储过程。该过程接受一个输入参数 `@colname`，并旨在按输入列返回 `Sales.Ships` 表中的行。

完成此任务的首要尝试之一是使用静态 `ORDER BY`，如下：

```sql
ORDER BY
CASE @colname
  WHEN 'shipper' THEN shipper
  WHEN 'companyname' THEN companyname
  WHEN 'phone' THEN phone
END
```

然而，如果你使用这种方法，SQL Server 会尝试将所有操作数转换为相同的数据类型。一种变通方法是为每个输入使用独立的 `CASE` 表达式：

```sql
ORDER BY
CASE WHEN @colname = 'shipper' THEN shipper END,
CASE WHEN @colname = 'companyname' THEN companyname END,
-- 此处省略 phone
```

但这种方式不是 SARGable，优化器无法依赖索引。处理动态排序的正确方法是使用 `RECOMPILE` 选项，如下：

```sql
ORDER BY
CASE WHEN @colname = 'shipper' THEN shipper END,
CASE WHEN @colname = 'companyname' THEN companyname END,
CASE WHEN @colname = 'phone' THEN phone END
OPTION(RECOMPILE)
```

假设用户使用 `'companyname'` 执行存储过程；解析后，`ORDER BY` 变为前者（尽管 `NULL` 常量没有直接出现在 `ORDER BY` 中）：`ORDER BY NULL, companyname, NULL`。只要你有覆盖索引，优化器就可以依靠它并避免显式排序。

为了使存储过程更灵活，你可能还希望支持第二个名为 `@sortdir` 的参数，以指定排序方向（'A' 表示升序，'D' 表示降序）。支持第二个参数将要求你查询中 `CASE` 表达式的数量翻倍。

运行以下代码根据此策略创建 `GetSortedShippers` 存储过程：

```sql
USE TSQLV3;

IF OBJECT_ID(N'dbo.GetSortedShippers', 'P') IS NOT NULL DROP PROC dbo.GetSortedShippers;
GO
CREATE PROC dbo.GetSortedShippers
@colname AS sysname, @sortdir AS CHAR(1) = 'A'
AS

SELECT select, companyname, phone, phone
FROM Sales.Sales
ORDER BY
CASE WHEN @colname = 'shipper' AND @sortdir = 'A' THEN shipper END,
CASE WHEN @colname = 'companyname' AND @sortdir = 'A' THEN companyname END,
CASE WHEN @colname = 'phone' AND @sortdir = 'A' THEN phone END,
CASE WHEN @colname = 'shipper' AND @sortdir = 'D' THEN shipper DESC END,
CASE WHEN @colname = 'companyname' AND @sortdir = 'D' THEN companyname DESC END,
CASE WHEN @colname = 'phone' AND @sortdir = 'D' THEN phone DESC END
OPTION(RECOMPILE);
GO
```

运行以下代码以测试该过程：

解析后，`ORDER BY` 子句导致以下结果：

ORDER BY NULL, NULL, shipper DESC, NULL DESC, NULL DESC

该执行的计划如图 9-6 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_568_0.png)

| SELECT Compute Scalar Cost: 0 % | Clustered Index Scan (Clustered) [Shippers], [Pk_Shippers] Cost: 100% | |
|---|---|---|
| n| > Expr1002 Scalar Operator(NULL) | Ordered | True |
| > Expr1003 Scalar Operator(NULL) | | |
