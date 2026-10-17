
![](img/bdc38aa36f6e2987d913ee5381474711_344_0.png)

**图 4-17** 使用赋值 `SELECT` 的测试 1 计划。

观察到该计划按顺序扫描了聚集索引 `PK_T1`（该索引以 `col1` 为键）。然后，计划使用 `Compute Scalar` 算子处理赋值。该计划的执行结果产生了如下输出，这似乎符合某些人的预期，即值将根据指定的顺序进行拼接：

String1:String2:String3:String4:String5:String6:String7:String8:String9

String10:String11:String12:String13:String14:String15:String16:String17:String18

String19:String20:String21:String22:String23:String24:String25:String26:String27

String28:String29:String30:String31:String32:String33:String34:String35:String36

String37:String38:String39:String40:String41:String42:String43:String44:String45

String46:String47:String48:String49:String50:String51:String52:String53:String54

String55:String56:String57:String58:String59:String60:String61:String62:String63

String64:String65:String66:String67:String68:String69:String70:String71:String72

String73:String74:String75:String76:String77:String78:String79:String80:String81

String82:String83:String84:String85:String86:String87:String88:String89:String90

String91:String92:String93:String94:String95:String96:String97:String98:String99:100

但正如提到的，并没有文档能为你提供这样的保证。这恰好是优化器的选择导致了这种有序的字符串。

接下来，我向表中添加了以下非聚集索引，然后运行了相同的赋值 `SELECT`：

```sql
CREATE NONCLUSTERED INDEX idx_nc_col2_idx_col1 ON dbo.T1(col2, col1);
GO

DECLARE @s VARCHAR(MAX);
SET @s = '';

SELECT @s = @s + col2 + ';
FROM dbo.T1
ORDER BY col2;

PRINT @s;
```

我为该查询执行获取的计划如图 4-18 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_345_0.png)

**图 4-18** 使用赋值 `SELECT` 的测试 2 计划。

观察到此优化器选择了新索引。它更窄，因为只包含了感兴趣的列。它没有按照查询所需的对行进行排序。因此，计划对索引执行了无序扫描，并添加了一个 `Sort` 算子作为最后一个算子来完成。讽刺的是，该计划在赋值发生后才对行进行排序！不仅如此，你得到的并不是你所需的顺序拼接值；相反，你得到的是拼接的中间状态。当我运行这段代码时，我得到了如下输出：

String 100;

据说，外界存在大量依赖这种方法的生产代码，而作者们并没有意识到它并不能保证按照他们预期的方式工作。某些因素会导致优化器改变其优化代码的方式，例如新索引、新服务等，导致他们陷入麻烦。如果你遵循定义良好的技巧（如 `FOR XML`），就可以避免很多痛苦。

## 聚合乘积

计算乘积另一种经典的聚合计算。它通常用于财务应用——例如计算利率。对于 `Groups` 表，你需要计算每组 `val` 列的乘积。该任务的有效解决方案是基于数学的——特别是对数计算。存在两组很有趣等式：T-SQL 中的 `LOG` 函数使用第一个输入作为基数计算对数。如果你没有指定基数，它将使用 `e` 作为基数（`e` 是一个等于 `2.71828` 的无理数）。T-SQL 中的 `EXP` 函数返回输入的幂。这意味着在以下等式对中：`log(y) = x <=> EXP(x) = y` 以及在以下等式对中：`log(y) = log(x) + log(y)`。用 T-SQL 表示的计算预期乘积的查询如下：

```sql
SELECT groupid, ROUND(EXP(SUM(val)), 0) AS product
FROM dbo.Groups
GROUP BY groupid;
```

由于 `LOG` 和 `EXP` 函数使用的浮点计算不精确性，需要舍入来修正错误。该查询产生了如下输出：

```
groupid      product
a             42
b             693
c             96
```

如果你也支持零和负值，情况会变得更复杂，因为 `LOG` 函数不支持这些值。为了看到这一演示，通过运行以下代码重新填充 `Groups` 表：

```sql
TRUNCATE TABLE db.Groups
```

```sql
INSERT INTO dbo.Groups(groupid, val) VALUES
('a', 3, 'str1', -6),
('a', 9, 'str2', 7),
('b', 2, 'str1', -3),
('b', 4, 'str2', -7),
('b', 5, 'str3', 3),
('b', 9, 'str4', -11),
('c', 3, 'str1', 8),
('c', 7, 'str2', 0),
('c', 9, 'str3', 12);
```

尝试使用新数据运行查询：

```sql
SELECT groupid, ROUND(EXP(SUM(val)), 0) AS product
FROM dbo.Groups
GROUP BY groupid;
```

查询失败，产生以下错误：Msg 3623, Level 16, State 1, 发生了无效浮点操作。

为了正确处理零和负数，你需要几点技巧。使用 `ISNULL` 函数，如果值为 0 则将其替换为 `NULL` 以避免错误。对绝对值应用原始乘积计算。使用 `MIN` 聚合和 `CASE` 表达式，应用一个标记（称为 `zero`），如果至少有一个零则为 1，如果没有则为 0。使用 `COUNT` 聚合和 `CASE` 表达式，应用一个标记（称为 `negative`），如果有奇数个负值则为 -1，否则为 1。这里是应用这些计算的代码：

```sql
SELECT groupid,
-- 使用 NULL 将 0 替换为 NULL，对绝对值应用乘积
ROUND(EXP(SUM(LOG(ABS(NULLIF(val,0)))), 0)) AS product,
-- 如果 val = 0 时存在 0 则为 1，否则为 0
MIN(CASE WHEN val = 0 THEN 1 ELSE 0 END) AS zero,
-- 如果是偶数数则为 -1
CASE WHEN COUNT(WHEN val < 0 THEN 1 END) % 2 > 0 THEN -1 ELSE 1 END AS negative
FROM dbo.Groups
GROUP BY groupid;
```

此代码产生了如下输出：

| groupid | product | zero | negative |
|---|---|---|---|
| a | 42 | 1 | -1 |
| b | 693 | 1 | 1 |
| c | 96 | 0 | 1 |

然后为了得到正确的乘积，将绝对值的乘积乘以零标记和负数标记，如下所示：

```sql
SELECT groupid,
EXP(SUM(LOG(ABS(NULLIF(val, 0)))), 0)
* MIN(CASE WHEN val = 0 THEN 0 ELSE 1 END)
* CASE WHEN COUNT(CASE val < 0 END) % 2 > 0 THEN -1 ELSE 1 END AS product
FROM dbo.Groups
GROUP BY groupid;
```

此查询产生了如下输出：

```
groupid    product
----------  -------
a         -42
b         693
c         0
```

如果你喜欢数学挑战，尝试在不使用 `CASE` 表达式的情况下计算零标记和负数标记。可以这样做到：

```sql
SELECT groupid,
ROUND(EXP(SUM(LOG(ABS(NULLIF(val, 0)))), 0)) AS product,
MIN(SIGN(ABS(val))) AS zero,
SUM((1-SIGN(val))/2)*-2+1 AS negative
FROM dbo.Groups
GROUP BY groupid;
```

将所有内容整合在一起，你就得到了计算最终乘积的查询：

```sql
SELECT groupid,
EXP(SUM(LOG(ABS(NULLIF(val, 0)))), 0)
* MIN(CASE WHEN val = 0 THEN 0 ELSE 1 END)
* CASE WHEN COUNT(CASE val < 0 END) % 2 > 0 THEN -1 ELSE 1 END AS product
FROM dbo.Groups
GROUP BY groupid;
```

## 聚合众数

另一个聚合计算的例子是计算分布的众数。众数是集合中出现频率的值。例如，假设你需要查询 TSQL3 中的 `Sales.Orders` 表，并找到每个客户处理订单最多的员工。即客户订单中出现次数最多的员工 ID。如果出现平局，你应该返回较大的员工 ID。

解决该任务的方法涉及以下步骤：

- 编写一个按客户和员工分组计算订单众数的分组查询。
- 在同一个分组查询中，计算一个按客户 ID 分区并按计数和员工 ID 倒序排列的行号。
- 基于该分组查询定义一个 CTE，然后在外部查询中仅过滤出行号为 1 的行。

以下是完整的解决方案代码：

```sql
USE TSQLV;
WITH C AS
(
  SELECT custid, empid, COUNT(*) AS cnt,
  ROW_NUMBER() OVER(PARTITION BY custid
  ORDER BY COUNT(*) DESC, empid DESC) AS rn
FROM Sales.Orders
GROUP BY custid, empid
)
SELECT custid, empid, cnt
FROM C
WHERE rn = 1;
```

该查询生成以下输出：

| custid | empid | cnt |
|---|---|---|
| 1 | 4 | 2 |
| 2 | 3 | 2 |
| 3 | 3 | 3 |
| 4 | 4 | 4 |
| 5 | 3 | 6 |

相反，如果你希望在打破平局，而是返回所有平局项，则你需要对你的解决方案进行两处更改。你需要使用 `RANK` 或 `DENSE_RANK` 函数（任选一均可），并从窗口排序类中移除员工 ID。以下是修改后的代码：

```sql
WITH C AS
(
  SELECT custid, empid, COUNT(*) AS cnt,
  RANK() OVER(PARTITION BY custid
  ORDER BY COUNT(*) DESC) AS rn
FROM Sales.Orders
GROUP BY custid, empid
)
SELECT custid, empid, cnt
FROM C
WHERE rn = 1;
```

此代码生成以下输出：

| custid | empid | cnt |
|---|---|---|
| 1 | 1 | 2 |
| 2 | 4 | 2 |
| 3 | 3 | 3 |
| 4 | 4 | 4 |
| 5 | 3 | 6 |

注意，客户 1 有两个员工处理了数量最多的订单。

回到涉及平局决胜的原始任务，考虑解决方案的优化。因为 `ROW_NUMBER` 函数的排序在部分程度上基于查询计划中整个输入集的结果，即使你为 `(custid, empid)` 创建了索引也是如此的。对于大量输入，排序将是非常昂贵的。可以通过索引视图来避免排序（作为一个挑战，如果你能想出办法的话），但如果你无法承担它怎么办呢？

另一种替代方案是基于分组和字符串拼接的“携带排序”（carry-along-sort）概念，针对 `(custid, empid)` 建立索引。该解决方案涉及以下步骤：

1. 编写一个分组查询，计算每个客户和员工的订单计数。
2. 在同一个分组查询中，计算将计数转换为 `BINARY(4)` 后与同样转换为 `BINARY(4)` 的员工 ID 拼接而成的二进制字符串。拼接后的值为 `binval`。
3. 基于分组查询定义一个表表达式并命名为 D。
4. 在 D 之上编写一个外部查询，按客户对行进行分组。在该查询中，计算结果 `MAX(binval)` 包含了最大计数以及众员工的 ID（以最大的员工 ID 作为平局决胜依据）。应用子字符串逻辑提取这两个部分并转换回原始类型。

以下是完整的解决方案：

```sql
SELECT custid,
CAST(SUBSTRING(MAX(binval), 5, 4) AS INT) empid,
CAST(SUBSTRING(MAX(binval), 1, 4) AS INT) cnt
FROM (
  SELECT custid, CAST(COUNT(*) AS BINARY(4)) + CAST(empid AS BINARY(4)) AS binval
  FROM Sales.Orders
  GROUP BY custid, empid
) AS D
```

此解决方案的优点在于，分层分组和聚合可以依赖上述索引的顺序。为了比较两种解决方案的性能，我创建了一个名为 `Orders` 的表，包含 10,000,000 行，并在 `(custid, empid)` 上创建了名为 `idx_custid_empid` 的索引。图 4-19 显示了针对该表的两种解决方案计划。顶部计划是基于携带排序概念的解决方案。

注意第一个计划在计算行之前存在昂贵的 `Sort` 算符，而第二个计划中没有它。第一个解决方案在我的机器上需要 15 秒完成，而第二个解决方案仅需 5 秒。

在考虑自定义聚合之前，我想提到，标准 SQL 定义了一种名为“有序集”（ordered set）的函数类型，但在写作之初，SQL Server 尚未支持。可以实现为有序集函数的函数有多个例子：聚合、分位数、CLR 等。你可以在此处找到关于有序集函数的参考：https://learn.microsoft.com/en-us/sql/t-server/ordered-set

查询 1：查询成本（相对于批次）：0

```sql
WITH C AS (SELECT custid, COUNT(*) AS cnt, ROW_NUMBER() OVER(PARTITION BY custid ORDER BY COUNT(*) DESC, empid DESC) AS rn
```

查询 2：查询成本（相对于批次）：1

```sql
SELECT custid, CAST(SUBSTRING(MAX(binval), 1, 4) AS INT), CAST(SUBSTRING(MAX(binval), 5, 4) AS INT) FROM C
```

**图 4-19** 众数解决方案的计划

## 分组集 (Grouping sets)

T-SQL 支持若干与分组集主题相关的功能，这对数据分析有用。这些功能包括 `GROUP SET`、`CUBE`、`ROLLUP` 子句，以及 `GROUPING_ID` 和 `GROUPING` 函数。为了演示这些功能，我将使用名为 `Orders` 的表。运行以下代码来创建 `Orders` 表并填充数据：

```sql
SET NOCOUNT ON;
USE tempdb;

IF OBJECT_ID('dbo.Orders','U') IS NOT NULL DROP TABLE dbo.Orders;

CREATE TABLE dbo.Orders(
  orderid INT NOT NULL,
  orderdate DATETIME NOT NULL,
  empid INT NOT NULL,
  custid VARCHAR(5) NOT NULL,
  qty INT NOT NULL,
  CONSTRAINT PK_Orders PRIMARY KEY(orderid)
);
GO

INSERT INTO dbo.Orders(orderid, orderdate, empid, custid, qty)
VALUES
(3001, '2012-08-02', 3, 'A', 10),
(10001, '2012-12-24', 1, 'A', 12),
(10005, '2012-12-24', 1, 'B', 20),
(40001, '2013-01-09', 4, 'A', 40),
(10006, '2013-01-18', 1, 'C', 14),
(20002, '2012-02-12', 2, 'B', 12),
(40005, '2014-02-12', 4, 'A', 10),
(20002, '2014-02-16', 2, 'C', 20),
(30003, '2014-04-18', 3, 'B', 15),
(40004, '2012-04-18', 3, 'C', 22),
(30007, '2012-09-07', 3, 'D', 30);
```
