
| > Expr1004 Scalar Operator(NULL) | | |
| > Expr1005 Scalar Operator(shippend) | | |
| > Expr1006 Scalar Operator(NULL) | | |
| > Expr1007 Scalar Operator(NULL) | | |

**图 9-6** 带有多个 CASE 表达式且重新编译的查询计划

注意到该计划对 `shipper` 上的聚集索引执行了顺序扫描，避免了显式排序的需求。

这种解决方案产生了高效的计划。因为它使用了静态查询，所以不会受到 SQL 注入攻击的影响。然而，它有两个缺点。首先，根据定义，它不重用查询计划。其次，它不支持多个列作为输入；你将得到许多 CASE 表达式。

具有这些缺点的解决方案是基于动态 SQL 的。你通过注入排序列方向构造带有 `ORDER BY` 子句的查询字符串。该解决方案显而易见的挑战是 SQL 注入。然后，在表中包含一个测试，以确保列名出现在你从表中想要支持的硬编码排序列集中。如果列名不在集合中，你将中止查询，怀疑是尝试进行 SQL 注入。如果支持的排序列集需要更改，你只需更新过程定义。很可能，更改的频率足够低，足以使这种方法可行。

使用以下代码通过此策略重新创建该过程：

```
IF OBJECT_ID('N''dbo.GetSortedShippers'', N'P') IS NOT NULL DROP PROC dbo.GetSortedShippers;
GO
CREATE PROC dbo.GetSortedShippers
@colname as sysname, @sortdir AS CHAR(1) = 'A'
AS
IF @colname NOT IN('shippid', N'companyname', N'phone')
THROW 50001, 'Column name not supported. Possibly a SQL injection attempt.', 1;
```

*下*

```
DECLARE @sql AS NVARCHAR(1000);
```

```
SET @sql = 'SELECT shiperid, companyname
FROM Sales.Shippers
ORDER BY 
  + QUOTENAME(@colname) + CASE @sortdir WHEN ''D'' THEN '' DESC'' ELSE '' ASC'' END + ';
```

```
EXEC sys.sp_executesql @stmt = @sql;
GO
```

`QUOTENAME` 函数用于用方括号定界排序列名。在我们特定的示例中，不需要定界符，但万一你需要支持被视为不规则标识符的列名，你将需要定界符。

使用以下代码测试该过程：

该执行的计划如图 9-7 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_569_0.png)

**图 9-7** 动态查询的计划。

这是一个依赖于索引顺序的高效计划。与之前的解决方案不同，如果你需要支持多个输入排序，也可以轻松地扩展，包括之前缓存的计划。此解决方案还可以重用以下演示：

```
IF OBJECT_ID('N''dbo.GetSortedShippers'', 'N''P') IS NOT NULL DROP PROC dbo.GetSortedShippers;
GO
CREATE PROC dbo.GetSortedShippers
@colname1 AS sysname, @sortdir1 CHAR(1) = 'A',
@colname2 AS sysname = NULL, @sortdir2 AS CHAR(1) = 'A',
@colname3 AS sysname = NULL, @sortdir3 CHAR(1) = 'A'
```

```
IF @colname1 NOT IN('N''shiperid', 'N''companyname', 'N''phone')
OR @colname2 IS NOT NULL AND @colname2 NOT IN('N''shiperid', 'N''companyname', 'N''phone')
OR @colname3 IS NOT NULL AND @colname3 NOT IN('N''shiperid', 'N''companyname', 'N''phone')
THROW 50001, 'Column name not supported. Possibly a SQL injection attempt.', 1;
```

```
DECLARE @sql AS NVARCHAR(1000);
```

```
EXEC sys.sp_executesql @stmt = @sql;
GO
```

关于安全性，重要的是，要知道通常情况下执行存储过程的用户需要具有运行动态执行代码的权限。如果你不想授予此类权限，可以使用 `EXEC AS` 子句来确保子句中指定用户的安全性。你可以在在线书籍（Books Online）中找到有关如何执行此的细节：http://msdn.microsoft.com/en-us/library/ms18834.aspx。

作为额外资源，你可以在此处找到动态 SQL 的精彩介绍：Erland Somkog 的 [The Curse and Blessings of Dynamic SQL](http://www.sommarskog.se/dynamic_sql.html)。

## 定义函数

定义函数（UDF）提供了强大的封装和重用性，因为它们可以方便地嵌入查询中。然而，你需要意识到存在某些性能开销。出于这个目的，我指的是 T-SQL UDF 和多表值函数（TVFs）。内联 TVFs 根据定义是内联的，因此不会产生性能开销。本节涵盖了 T-SQL UDF。后续章节涵盖 CLR UDF。

## 标量 UDF

标量 UDF 接受参数并返回标量值。它们可以使用在查询、约束和计算列。T-SQL UDF 有两种主要的实现方式。在第一种情况下，它调用单个表达式；在另一种情况下，它调用多个语句并最终返回标量结果。无论如何，你需要意识到使用 UDF 与性能相关的关联。我将从一个基于单个表达式的示例开始，比较直接包含表达式的查询与将其封装在 UDF 中的查询的性能。

以下查询过滤出在最后一天下单的订单：

```
USE PerformanceV3;

SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
WHERE orderdate = DATEADD(year, DIFF(year, '19001231', orderdate), '1900231');
```

如果你不熟悉计算年份最后一天的方法，可以在第 7 章“处理日期和时间”中找到细节。

在我的系统中，此查询获得了如图 9-8 所示的执行计划。

![](img/bdc38aa36f6e2987d913ee5381474711_571_0.png)

**图 9-8** 无函数的查询计划

注意到该计划使用了并行扫描，主要使用多个线程处理过滤器。为了检查并行性的影响，我通过指定提示 `MAXDOP 1` 强制执行串行计划，如下：

```
SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
WHERE orderdate = DATEADD(year, DIFF(year, '19001231', orderdate), '1900231')
OPTION(MAXDOP 1);
```

这次，查询花费了 511 毫秒完成，并且使用了 704 毫秒的 CPU 时间。

当在缓存中热运行此查询时，查询花费了 281 毫秒完成。所以，在我的系统中，并行计划的执行时间是串行执行时间的一半。

毫无疑问，从编程的角度来看，将计算年底日期的表达式封装在标量 UDF 中是有益的。这种封装有助于隐藏复杂性并实现重用性。运行以下代码将表达式封装在 `EndYear` 中。

```
IF OBJECT_ID(N'dbo.EndYear') IS NOT NULL DROP FUNCTION dbo.EndYear;
GO
CREATE FUNCTION dbo.EndYear(@dt DATE) RETURNS DATE
AS
BEGIN
    RETURN DATEADD(year, DATEDIFF(year, '19001231', @dt), '19001231');
END
GO
```

现在，将直接表达式替换为对 UDF（用户定义函数）的调用并运行查询，如下：

```
SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
WHERE orderdate = dbo.EndYear(orderdate);
```

与不使用 UDF 相比，在这里获得的编程优势是不言而疑的。代码更加清晰、简洁。然而，使用 UDF 对性能的影响非常严重。请观察图 9-9 中该查询的计划。

![](img/bdc38aa36f6e2987d913ee5381474711_572_0.png)

**图 9-9** 使用标量 UDF 的查询计划。

遗憾的是，即使 UDF 基于单个表达式，SQL Server 也不会对其进行内联。这意味着 UDF 会针对底层表中的每一行被调用一次，正如我们在案例的 Filter 算子的谓词（Predicate）属性中所看到的，该 UDF 被调用了 1,000,000 次。每次调用都有开销，而百万次调用产生的开销是相当巨大的。此外，请注意查询计划是串行的。任何对 T-SQL 标量 UDF 的使用都会阻止并行。

该查询在我的系统上花费了四多秒才完成，总 CPU 成本超过四秒。大约是不带 UDF（使用默认并行）查询的 16 倍，是我强制使用串行计划的 8 倍。无论如何，如你所见，使用 UDF 的代价非常高。

奇的是，有一种通通方法可以让你将逻辑封装在函数中，而不会产生性能损失。不要使用标量 UDF，而是使用内联 TVF（表值函数）。困难的之处在于内联 TVF 必须返回一个查询。因此，在 FROM-SELECT 查询中指定表达式以及列别名，并从函数返回该查询。以下是删除标量 UDF 并改用内联 TVF 的代码：

```
IF OBJECT_ID(N'dbo.EndOfYear') IS NOT NULL DROP FUNCTION dbo.EndOfYear;
GO
CREATE FUNCTION dbo.EndOfYear(@dt DATE) RETURNS TABLE
AS
RETURN
SELECT DATEADD(year, DATEDIFF(year, '19001231', @dt), '19001231') AS endofyear;
GO
```

要在查询中调用函数并将外部表的列作为输入，你需要使用 APPLY 算子或在子查询中实现它。以下是隐式形式的示例：

```
SELECT orderid, custid, empid, shipper, orderdate, filler
FROM dbo.Orders
WHERE orderdate = (SELECT endofyear FROM dbo.EndOfYear(orderdate));
```

这一次，函数中的表达式被内联了。SQL Server 创建的计划与我之前在图 9-8 中所示的无 UDF 原始查询计划相同。使用内联 TVF 没有性能损失。

与基于多个语句的标量 UDF 不同，这些通常用于实现迭代逻辑。正如本书第 2 章“查询调优”中所讨论的，使用了 T-SQL 迭代。因此，特别是当你需要应用多次迭代时，你会倾向于使用 CLR UDF 而不是 T-SQL UDF。此外，只要 CLR UDF 没有被标记为访问（accessing），它就不会阻止并行。

使用迭代逻辑的 T-SQL UDF 示例，考虑以下 `RemoveChars` UDF 的定义：

```
USE TSQLV3;
IF OBJECT_ID(N'dbo.RemoveChars', 'N'FN') IS NOT NULL DROP FUNCTION dbo.RemoveChars;
GO
CREATE FUNCTION dbo.RemoveChars(@string NVARCHAR(4000), @pattern AS NVARCHAR(4000))
RETURNS NVARCHAR(4000)
AS
BEGIN
DECLARE @pos AS INT;
SET @pos = PATINDEX(@pattern, @string);

WHILE @pos > 0
BEGIN
SET @string = STUFF(@string, @pos, 1, N'');
SET @pos = PATINDEX(@pattern, @string);
END

RETURN @string;
END;
GO
```

该函数接受两个参数作为输入。一个是 `@string`，代表输入字符串。另一个是 `@pattern`，代表单个字符的模式。UDF 的目的是返回一个字符串，代表删除所有输入字符模式后的字符串。

函数代码首先使用 `PATINDEX` 函数找到字符模式在 `@string` 中的第一个出现位置，并将其存储在 `@pos` 中。然后代码进入一个循环，只要字符串中仍有字符模式的出现，循环就会继续运行。在每次迭代中，代码使用 `STUFF` 函数从字符串中删除第一个出现的位置，并寻找下一次出现的位置。循环完成后，代码返回 `@string` 中剩余的内容。

以下是在针对 `Sales.Customers` 表查询中使用 UDF 以返回干净电话号码（通过删除所有非字符）的示例：

```
SELECT custid, phone, dbo.RemoveChars(phone, N'[^0-9]') AS cleanphone
FROM Sales.Customers;
```

该函数返回以下输出：

| custid | cleanphone |
|---|---|
| 1 | 030-456789 |
| 2 | 789-0123 |
| 3 | 123-4567 |
| 4 | 171-4567890 |
| 5 | 0921-678901 |
| 6 | 0621-6890 |
| 7 | 6789-0123 |
| 8 | 91-3456789 |
| 9 | 23-456789 |
| 10 | 604-9212345 |

你将在“SQL 编程”章节找到 CLR UDF。

## 多语句 TVF (Multistatement TVFs)

多语句 TVF 内部包含多个语句，并返回一个表变量作为输出。返回的变量在函数头部定义。当查询此类函数时，SQL Server 声明表变量，运行填充数据，然后交给调用查询。为了演示多语句 TVF，我将使用以下代码创建并填充表：

```
SET NOCOUNT ON;
USE tempdb;
GO
IF OBJECT_ID(N'dbo.Employees', 'U') IS NOT NULL TABLE dbo.Employees;
GO
CREATE TABLE dbo.Employees
(
  empid INT NOT NULL PRIMARY KEY,
  mgrid INT NOT NULL REFERENCES dbo.Employees,
  empname VARCHAR(25) NOT NULL,
  salary MONEY NOT NULL,
  CHECK (empid <> mgrid)
);

INSERT INTO dbo.Employees(empid, mgrid, empname, salary)
VALUES(1, NULL, 'David', 10000.00),
(2, 1, 'Eitan', 7000.00),
(3, 1, 'Ina', 7500.00),
(4, 2, 'Seraph', 5000.00),
(5, 2, 'Zira', 5000.00),
(6, 2, 'Steve', 4500.00),
(7, 3, 'Aaron', 5000.00),
(8, 5, 'Lilach', 3500.00),
(9, 7, 'Rita', 3000.00),
(10, 5, 'Sean', 3000.00),
(11, 7, 'Gabriel', 3000.00),
(12, 9, 'Emilia', 2000.00),
(13, 9, 'Michael', 2000.00),
(14, 9, 'Didi', 1500.00);
```

遵循名为 `GetSubtree` 的函数定义：
