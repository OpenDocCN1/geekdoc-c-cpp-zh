
关于并非分区开始的帧的优化之处在于，你会预期优化器会创建一个将所有帧写入窗口并进行聚合的计划。在示例中，这意味着 100 × 2,000,000 = 2,000,000,000 行。然而，优化器在某些条件下可以使用一种技巧来避免这种工作。如果帧超过四行且聚合是累积聚合（如 `SUM`、`COUNT` 或 `AVG`），优化器会创建一个带有两个快速通道运行计算的计划：从分区开始到所需帧最后一行的计算（称为 `CumulativeBottom`），另一个从分区开始到所需帧开始之前的一行的计算（称为 `CumulativeTop`）。然后它通过计算两者之间的值得出最终聚合结果。你可以在图 4-7 显示的最后一个查询的计划中看到这种策略。

该查询在我的系统上花费了 12 秒完成。考虑到替代方案，这并不差。

![](img/bdc38aa36f6e29f)
![](img/bdc38aa36f6e29f)
![](img/bdc38aa36f6e29f)
![](img/bdc38aa36f6e29f)

因此，对于员工 9，您应该得到以下输出：

| empid | ordermon qty | sum3month |
|---|---|---|
| 9 | 2013-07-01 294 | 294 |
| 9 | 2013-10-01 256 | 256 |
| 9 | 2013-12-01 25 | 281 |
| 9 | 2014-01-01 74 | 99 |
| 9 | 2014-03-01 137 | 211 |
| 9 | 2014-04-01 52 | 189 |
| 9 | 2014-05-01 8 | 197 |
| 9 | 2014-06-01 161 | 221 |
| 9 | 2014-07-01 4 | 173 |
| 9 | 2014-08-01 98 | 263 |

遗憾的是，SQL Server 缺少两个可以实现此类查询的功能：第一，SQL Server 缺少 `INTERVAL` 功能；第二，SQL Server 在 `RANGE` 单元上仅支持 `UNBOUNDED` 和 `CURRENT ROW` 作为界符。

要在 SQL Server 中实现此任务，您有几种选择。一种是对缺失的员工和月份条目进行填充，然后使用 `ROWS` 选项，如下：

```sql
DECLARE
@frommonth AS DATE = '20130701',
@tommonth AS DATE = '20150501';
WITH M AS
(
SELECT DATEADD(month, N.n, @frommonth) AS ordermon
FROM TSQLV3.dbo.GetNums(0, DATEDIFF(month, @frommonth, @tommonth)) AS N
),
R AS
(
SELECT E.empid, M.ordermon, EO.qty,
SUM(EO.qty) OVER(PARTITION BY E.empid ORDER BY M.ordermon ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS sum3month
FROM TSQLV3.HR.Employees AS E CROSS JOIN M
LEFT OUTER JOIN dbo.EmpOrders AS EO
ON E.empid = EO.empid AND M.ordermon = EO.ordermon
)
SELECT empid, ordermon, qty, sum3month
FROM R
WHERE qty IS NOT NULL;
```

另一种选项是使用连接（join）和分组的查询，就像我之前为运行总费用展示的那样：

```sql
SELECT O1.empid, O1.ordermonth, O1.qty,
SUM(O2.qty) AS summonth
FROM dbo.EmpOrders AS O1
INNER JOIN dbo.EmpOrders AS O2
ON O2.empid = O1.empid
AND O2.ordermonth BETWEEN DATEADD(month, -2, O1.ordermonth) AND O1.ordermonth
GROUP BY O1.empid, O1.ordermonth, O1.qty
ORDER BY O1.empid, O1.ordermonth;
```

问题在于，为什么只支持以 `UNBOUNDED` 和 `CURRENT ROW` 作为界符的 `RANGE` 呢？事实证明，当使用相同的框架规范时，`ROWS` 和 `RANGE` 之间存在细微差异。这种差异在排序值不同时不会表现出来。`ROWS` 选项不包含相同值（排序值中的 peers），而 `RANGE` 则包含。考虑以下查询示例：

```sql
SELECT orderdate, val,
SUM(val) OVER(ORDER BY orderdate ROWS UNBOUNDED PRECEDING) AS sumrows,
SUM(val) OVER(ORDER BY orderdate RANGE UNBOUNDED PRECEDING) AS sumrange
FROM dbo.orderValues;
```

该查询生成了以下输出：

| orderid | orderdate | val | sumrows | sumrange |
|---|---|---|---|---|
| 10248 | 2013-07-04 | 440.00 | 440.00 | 440.00 |
| 10249 | 2013-07-05 | 1863.40 | 2303.40 | 2303.40 |
| 10250 | 2013-07-08 | 1552.60 | 3856.00 | 4510.00 |
| 10251 | 2013-07-08 | 654.06 | 4510.00 | 4510.00 |
| 10252 | 2013-07-09 | 3597.90 | 8107.96 | 8107.96 |
| 11070 | 2015-05-05 | 1629.98 | 125712.06 | 126304.56 |
| 11071 | 2015-05-05 | 484.50 | 125746.56 | 126304.56 |
| 11072 | 2015-05-05 | 5218.00 | 126271.56 | 126304.56 |
| 11073 | 2015-05-05 | 300.00 | 126304.56 | 126304.56 |
| 11074 | 2015-05-06 | 232.09 | 126342.65 | 126793.22 |
| 11075 | 2015-05-06 | 374.75 | 126374.75 | 126793.23 |
| 11076 | 2015-05-06 | 484.50 | 125746.56 | 126304.56 |

注意到客户 10 在 2014 年 1 月 10 日下了两个订单，计算结果在两行中产生了相同的 YTD（年初至今）值，这是符合预期的。

如果你需要每个唯一的客户和日期只返回一行，你首先需要根据这两项对行进行分组，然后对分组后的结果应用 `SUM` 函数。由于分区元素和排序元素的组合是唯一的，你应该使用 `ROWS` 函数。以下是完整的查询：

```sql
SELECT custid, orderdate,
SUM(val) OVER(PARTITION BY custid, YEAR(orderdate) ORDER BY orderdate ROWS UNBOUNDED PRECEDING) AS YTD_val
FROM dbo.OrderValues
GROUP BY custid, orderdate;
```

此查询生成了以下输出：

| custid | orderdate | YTD_val |
|---|---|---|
| 1 | 2014-08-25 | 814.50 |
| 1 | 2014-10-03 | 1692.50 |
| 1 | 2014-10-13 | 2022.50 |
| 1 | 2015-01-15 | 845.80 |
| 1 | 2015-03-16 | 1317.00 |
| 1 | 2015-04-09 | 2250.50 |
| ... | ... | ... |
| 10 | 2013-12-22 | 1832.80 |
| 10 | 2014-01-10 | 1768.80 |
| 10 | 2014-01-30 | 3661.05 |
| 10 | 2014-04-01 | 4512.25 |
| 10 | 2014-11-14 | 7630.25 |

注意，每个唯一的客户和日期只有一行，例如客户 10 在 2014 年 1 月 10 日的情况。

## 排名窗口函数

排名计算在 T-SQL 中是以窗口函数实现的。当你对一个值进行排名时，你并不是孤立地进行排名，而是根据特定的顺序相对于一组值进行排名。窗口化概念非常适用于这种计算。该集合由 `OVER` 子句定义。如果没有窗口分区子句（partition clause），你将当前行的值与底层查询结果集中的所有行进行排名。如果有分区子句，你将在同一窗口分区内的行之间进行排名。强制性的窗口排序子句定义了排名的顺序。

为了演示排名窗口函数，我将使用以下表。

```sql
SET NOCOUNT ON;
USE tempdb;
IF OBJECT_ID('dbo.Orders', 'U') IS NOT NULL DROP TABLE dbo.Orders;
CREATE TABLE dbo.Orders
(
  orderid INT NOT NULL,
  orderdate DATE NOT NULL,
  empid INT NOT NULL,
  custid VARCHAR(5) NOT NULL,
  qty INT NOT NULL,
  CONSTRAINT PK_Orders PRIMARY KEY (orderid)
);
GO
INSERT INTO dbo.Orders(orderid, orderdate, empid, custid, qty)
VALUES(30001,'20130802', '3', 'B', 10),
(10001,'20131224', '1', 'C', 10),
(10005,'20131224', '1', 'A', 30),
(40001,'20140109', '4', 'A', 40),
(10006,'20140118', '1', 'C', 10),
(20001,'20140212', '2', 'B', 20),
(40005,'20140212', '4', 'A', 10),
(20002,'20140216', '2', 'C', 20),
(30003,'20140418', '3', 'B', 15),
(40004,'20140418', '3', 'B', 20),
(30007,'20140907', '3', 'C', 30);
```

T-SQL 支持四个排名函数，分别称为 `ROW_NUMBER`、`RANK`、`DENSE_RANK` 和 `NTILE`。以下是在 `Orders` 表上演示这四种函数的查询，没有分区子句，并按 `qty` 列排序：

```sql
SELECT orderid, qty,
ROW_NUMBER() OVER(ORDER BY qty) AS rownum,
RANK() OVER(ORDER BY qty) AS rnk,
DENSE_RANK() OVER(ORDER BY qty) AS densrank,
NTILE(4) OVER(ORDER BY qty) AS ntile
FROM dbo.Orders;
```

此查询生成了以下结果：

| orderid | qty | rownum | rnk | ntile |
|---|---|---|---|---|
| 10001 | 10 | 1 | 1 | 1 |
| 10006 | 10 | 2 | 1 | 1 |
| 10005 | 30 | 3 | 3 | 1 |
| 40005 | 10 | 4 | 1 | 2 |
| 30003 | 15 | 5 | 2 | 2 |
| 20001 | 20 | 6 | 3 | 2 |
| 40004 | 20 | 7 | 3 | 3 |
| 20002 | 20 | 8 | 3 | 3 |
| 30007 | 30 | 9 | 4 | 3 |
| 40001 | 40 | 10 | 5 | 4 |

`ROW_NUMBER` 函数是四个函数中最常用的。它根据指定的顺序在分区（在本例中为查询结果）中计算增量整数。当分区内的排序不唯一（如示例所示），计算是非确定性的。这意味着如果你再次运行查询，无法保证结果是重复的。例如，数量为 20 的三行得到了行号 6、7 和 8。

在某些情况下，你需要保证确定性（重复的结果）。例如，`ROW_NUMBER` 可用于分页（如我在第 5 章中演示的“TOP 和 OFFSET”）。当数据变化时，为了强制行号计算具有确定性，可以在排序子句中添加一个决胜因素。在示例中，扩展到 `qty` 使排序变为唯一，从而使计算具有确定性。

`RANK` 和 `DENSE_RANK` 与 `ROW_NUMBER` 的不同在于，它们对排序相同的行产生相同的值。`RANK` 和 `DENSE_RANK` 的区别在于，前者计算小于当前值的行数，而后者计算小于当前值的不同值的数量。例如，行号 6、7 和 8 的行得到了排名值 6（1 + 5 行小于 20）和密集排名值 3（1 + 2 个不同的值小于 20）。因此，排名值之间存在间隙。最后，`NTILE` 函数根据指定的桶数和排序将行分配到分区中。在本例中，请求的桶数为 4，排序基于 `qty` 列。根据数量排序，结果中的前几行分配到桶 1，后续是 2，依此类推。如果行数不能被桶数整除（假设余数为 R），则前 R 个桶将获得额外的一行。在本例中，我们有 11 行，桶大小为 2，余数为 3。因此前三个桶有三行而不是二行。`NTILE` 计算是四个排名中最不常用的，它的主要用途是数据统计分析。

分区子句适用于所有窗口函数。以下是一个按 `custid` 分区并按 `orderid` 排序的计算示例：

```sql
SELECT custid, orderid, qty,
ROW_NUMBER() OVER(PARTITION BY custid ORDER BY orderid) AS rownum
FROM dbo.Orders
ORDER BY custid, orderid;
```

此查询生成了以下输出，你可以看到每个客户的行号是独立的：

| custid | orderid | qty | rownum |
|---|---|---|---|
| A | 10005 | 30 | 1 |
| A | 40001 | 40 | 2 |
| A | 40005 | 10 | 3 |
| B | 20001 | 20 | 1 |
| B | 30001 | 10 | 2 |
| B | 30003 | 15 | 3 |
| B | 40004 | 20 | 4 |
| C | 10001 | 10 | 1 |
| C | 10006 | 10 | 2 |
| C | 20002 | 20 | 3 |
| C | 30007 | 30 | 4 |

查询通过 `custid`, `orderid` 定义了输出顺序。记住，如果没有 `ORDER BY` 子句，输出顺序是不保证的。

从优化的角度来看，就像窗口聚合函数一样，带有 `ROW_NUMBER` 等排名函数的查询的理想索引是 POC 索引（覆盖索引）。图 4-10 显示了不存在 POC 索引时的查询计划。

![](img/bdc38aa36f6e2987d913ee5381474711_308_0.png)

| Output List |
|---|
| [tempdb].[Orders].orderid, [tempdb].[dbo].[Orders].custid, [tempdb].[dbo].[Orders].qty |
| Order By |
| [tempdb].[Orders].custid Ascending, [tempdb].[Orders].orderid Ascending |

# 图 4-10 无 POC 索引的 ROW_NUMBER 优化。

由于案例中不存在 POC 索引，优化器选择了 `Order False` 的聚簇索引扫描。它应用 `Sort` 算符来按 `custid`, `orderid` 对数据进行排序。这种顺序支持 `ROW_NUMBER` 函数的计算以及输出顺序，后者恰好是对齐的。`Segment` 算符在新段（分区）开始时标记 `Sequence Project` 算符。反过来，后者在行是分区内的第一行时返回 1，否则在前一个值上加 1。

如果你想对 `oid` 进行排序，你需要创建一个 POC 索引，如下：

```sql
CREATE UNIQUE INDEX idx_cust_oid_1_qty ON dbo.Orders(custid, orderid) INCLUDE(qty);
```
