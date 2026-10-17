
SET NOCOUNT ON;

USE tempdb;

```sql
IF OBJECT_ID('dbo.Arrays', 'U') IS NOT NULL DROP TABLE dbo.Arrays;
```

```sql
CREATE TABLE dbo.Arrays(
  id VARCHAR(10) NOT NULL PRIMARY KEY,
  arr VARCHAR(8000) NOT NULL
);
GO
```

```sql
INSERT INTO dbo.Arrays VALUES('A', '20,223,2544,25567,14');
INSERT INTO dbo.Arrays VALUES('B', '30,-23433,28');
INSERT INTO dbo.Arrays VALUES('C', '12,10,8099,12,1200,13,12,14,10,9');
INSERT INTO dbo.Arrays VALUES('D', '-4,-6,-45678,-2');
```

挑战在于给出一个高效的 T-SQL 解决方案，将每个字符串拆分为单独元素，并以单独行返回，带有 `id`、位置和元素本身。期望的结果所示。

| id | pos | element |
| :--- | :--- | :--- |
| A | 1 | 20 |
| A | 2 | 223 |
| A | 3 | 2544 |
| A | 4 | 25567 |
| A | 5 | 14 |
| B | 1 | 30 |
| B | 2 | -23433 |
| B | 3 | 28 |

注意，此任务可以使用 .NET 比 T-SQL 更高效地解决——可以通过使用 `System.String.Split` 方法，或者实现你自己的迭代解决方案。然而，我们的挑战是使用 T-SQL 实现一个高效的解决方案。

一种直观的方法是实现一个迭代解决方案，作为一个表函数，以单个字符串和分隔符作为输入并返回一个表变量。该函数将在每次迭代中提取一个元素并插入结果变量中。这种方法的问题是，T-SQL 中的迭代解决方案通常效率较低。

因此，挑战在于找到一个使用 T-SQL 的高效的基于集合（set-based）的解决方案。要实现这样的解决方案，你需要将任务分为三个步骤：

1. 生成副本。
2. 提取元素。
3. 计算位置。

第一步是从原始行生成副本——副本的数量等于字符串中元素的数量。第二步是从每个副本中提取相关元素。第三步是计算元素在字符串中的序数位置。

对于第一步，你会发现 TSQLV3 数据库中的辅助表 `Nums` 非常好用。该表有一个名为 `n` 的列，它存储了一组从 1 开始的整数。你可以将这些数字理解为字符串中的字符位置。$n=1$ 代表位置为 1 的字符，$n=2$ 代表位置为 2 的字符，依此类推。为了生成副本，你对 `Arrays` 和 `Nums` 进行连接。使用以下表达式作为连接谓词，它表示第 $n$ 个字符是：`SUBSTRING(arr, n, 1) = ','`。为了避免提取字符串末尾之后的字符，使用谓词 $n \le LEN(arr)$ 将数字限制为字符串的长度。以下是实现此逻辑的代码：

```sql
SELECT id, arr, n
FROM dbo.Arrays
INNER JOIN TSQLV3.Nums
ON n <= LEN(arr)
AND SUBSTRING(arr, n, 1) = ',';
```

此代码生成以下输出：

```
id arr n
-- -- --
A 20,223,2544,2567,14 3
A 20,223,2544,2567,14 7
A 20,223,2544,2567,14 12
A 20,223,2544,2567,14 18
B 30,-2433,28 3
B 30,-2433,28 10
```

观察发现输出中缺少了每个字符串的副本。原因是，对于一个包含 $X$ 个元素的字符串，如果你将 $X-I$ 个分隔符考虑为元素之前的分隔符，那么缺失的就是第一个元素之前的分隔符。为了解决这个问题，只需在字符串开头放置一个分隔符，并将结果作为第一个输入传递给 `SUBSTRING` 函数。此外，确保将你提取的字符长度增加一，以考虑到这个额外的字符。在进行这两个修改后，查询如下：

```sql
SELECT id, arr, n
FROM dbo.Arrays
INNER JOIN TSQLV3.dbo.Nums
ON n <= LEN(arr) + 1
AND SUBSTRING(',' + arr, n, 1) = ',';
```

此查询生成以下输出：

```
id arr n
-- -- --
A 20,223,2544,2567,14 1
A 20,223,2544,2567,14 4
A 20,223,2544,2567,14 8
A 20,223,2544,2567,14 13
A 20,223,2544,2567,14 19
B 30,-2433,28 1
B 30,-2433,28 4
B 30,-2433,28 11
```

这一次，你得到了正确数量的副本。此外，观察到查询的修改使得发现分隔符的位置增加了一，因为整个字符串向右移动了一个字符。这种效果实际上对我们非常方便，因为相对于原始字符串（不包含开头的分隔符），$n$ 实际上代表了元素的起始位置。该任务的解决方案的第一步已经完成。

第二步是提取当前副本所代表的元素。为了这一点，你将使用 `SUBSTRING` 函数。你需要将字符串、起始位置和要提取的长度作为输入。你知道元素从位置 $n$ 开始。对于长度，你需要找到下一个分隔符的位置，并从中减去 $n$。你可以使用 `CHARINDEX` 函数来实现此目的。前两个输入是你正在查找的分隔符以及你要查找它的字符串。作为第三个输入，指定 $n$ 为查找的起始位置。

## UNION ALL 和 UNION 运算符

`UNION` 运算符合并来自两个输入中的行。图 3-24 形象地展示了该操作符的作用。它用深色背景显示了该操作符的结果。

![](img/bdc38aa36f6e2987d913ee5381474711_274_0.png)

T-SQL 支持 `UNION` 运算符的两种变体：`UNION`（隐含的 `DISTINCT`）和 `UNION ALL`。两者都会合并两个输入中的行，但只有前者会从结果中删除重复；后者则不会。标准 SQL 实际上支持前者使用显式 `DISTINCT` 形式，但 T-SQL 仅支持隐式形式。

作为 `UNION` 的示例，以下代码返回了唯一的合并后的员工和客户位置：

```sql
USE TSQLV;
SELECT country, region, city FROM HR.Employees
UNION
SELECT country, region, city FROM Sales.Customers;
```

此查询返回了 71 个不同的地点。

如果你想保留重复项，请使用 `UNION ALL` 变体，如下所示：

```sql
SELECT country, region, city FROM HR.Employees
UNION ALL
SELECT country, region, city FROM Sales.Customers;
```

此查询返回了 100 行，因为它合并了 9 行员工数据和 91 行客户数据。通常情况下，返回带有重复项的结果是没有意义的，但你可能需要对结果应用某些进一步逻辑。例如，假设你需要统计每个地点有多少个员工和客户。为了这一点，你可以根据基于 `UNION` 运算符的代码定义一个表表达式，并在外部查询中执行所有的分组和聚合。

在性能方面，`UNION` 通常比 `UNION ALL` 更昂贵，因为它包含一个删除重复项的额外步骤。图 3-25 显示了最后 `UNION` 和 `UNION ALL` 查询的计划，证明了这一点。

![](img/bdc38aa36f6e2987d913ee5381474711_275_0.png)

查询 1: 查询成本（相对于批处理）：72%
`SELECT country, region, city FROM HR.Employees UNION SELECT country, region, city FROM Sales.Customers`

![](img/bdc38aa36f6e2987d913ee5381474711_275_1.png)

查询 2: 查询成本（相对于批处理）：28%
`SELECT country, region, city FROM HR.Employees UNION SELECT country, region, city FROM Sales.Customers`

![](img/bdc38aa36f6e2987d913ee5381474711_275_2.png)

## 图 3-25 UNION 与 UNION ALL。

`UNION` 查询的计划使用 `Sort`（去重排序）操作符来删除重复项。另一个选项是为此使用哈希算法。无论何种方式，你都可以看到涉及的工作比 `UNION ALL` 查询更多。

当你合并不相交的输入时（例如包含日期列的不同年份数据），`UNION` 和 `UNION ALL` 在逻辑上是等价的。遗憾的是，在这种情况下你可能会使用 `UNION` 运算符，是因为代码的按键次数较少，而没有意识到正在进行不必要的工作。因此，将 `UNION ALL` 作为默认值，并将 `UNION` 运算符保留给结果可能存在重复项且你需要删除它们的情况是非常重要的。

有趣的是，如果你使用 `UNION` 合并表行，而这些表具有定义不相交间隔的检查约束，优化器可以检测此并帮助你避免删除重复项的额外工作。例如，以下代码创建了单独表来存储不同年份的数据，并 `CHECK` 约束强制执行不相交的年份间隔：

```sql
USE tempdb;
IF OBJECT_ID(N'dbo.T2014', N'U') IS NOT NULL DROP TABLE dbo.T2014;
IF OBJECT_ID(N'dbo.T2015', N'U') IS NOT NULL DROP TABLE dbo.T2015;
GO
CREATE TABLE dbo.T2014
(
  keycol INT NOT NULL CONSTRAINT PK_T2014 PRIMARY KEY,
  dt DATE NOT NULL CONSTRAINT CHK_T2014_dt CHECK (dt >= '20140101' AND dt < '20150101')
);
CREATE TABLE dbo.T2015
(
  keycol INT NOT NULL CONSTRAINT PK_T2015 PRIMARY KEY,
  dt DATE NOT NULL CONSTRAINT CHK_T2015_dt CHECK (dt >= '20150101' AND dt < '20160101')
);
```

在忽略最佳实践的情况下，你使用以下代码通过 `UNION` 运算符合并表行：

```sql
SELECT keycol, dt FROM dbo.T2014
UNION
SELECT keycol, dt FROM dbo.T2015;
```

幸运的是，得益于约束的存在，优化器发现结果中不存在重复项，因此像处理 `UNION ALL` 一样优化此查询。该查询的计划如图 3-26 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_276_0.png)

**图 3-26** UNION 和 CHECK 约束。

建议遵循最佳实践并坚持将 `UNION ALL` 作为默认值。

## INTERSECT 运算符

`INTERSECT` 运算符返回两个输入共同的行。图 27 形象地展示了它的返回的内容。

![](img/bdc38aa36f6e2987d913ee5381474711_277_0.png)

图 27 INTERSECT 运算符。

作为一个示例，以下代码返回共同的员工和客户位置：

```sql
SELECT country, region, city FROM HR.Employees
INTERSECT
SELECT country, region, city FROM Sales.Customers;
```

此查询生成以下输出：

| country | region | city |
|---|---|---|
| UK | NULL | London |
| USA | WA | Kirkland |
| USA | WA | Seattle |

如果你想保留重复项，使用 `INTERSECT ALL` 变体，如下：

```sql
SELECT country, region, city FROM HR.Employees
INTERSECT ALL
SELECT country, region, city FROM Sales.Customers;
```

此查询返回 10 行，因为它合并了 9 行员工和 91 行客户。通常，返回带有重复项的结果是没有意义的，但你可能对结果应用某些进一步逻辑。例如，假设你需要统计每个地点有多少个员工和客户。为了这一点，你基于 `INTERSECT` 运算符的代码定义一个表表达式，并在外部查询中执行分组和聚合。

在性能方面，`INTERSECT` 通常比 `INTERSECT ALL` 更昂贵，因为它包含一个删除重复项的额外步骤。图 28 显示了 `INTERSECT` 和 `INTERSECT ALL` 查询的计划，证明了这一点。

![](img/bdc38aa36f6e2987d913ee5381474711_278_0.png)

查询 1: 查询成本（相对于批处理）：72%
`SELECT country, region, city FROM HR.Employees INTERSECT SELECT country, region, city FROM Sales.Customers`

![](img/bdc38aa36f6e2987d913ee5381474711_278_1.png)

查询 2: 查询成本（相对于批处理）：28%
`SELECT country, region, city FROM HR.Employees INTERSECT SELECT country, region, city FROM Sales.Customers`

![](img/bdc38aa36f6e2987d913ee5381474711_278_2.png)

## 图 3-28 INTERSECT 与 INTERSECT ALL。

`INTERSECT` 查询的计划使用 `Sort`（去重排序）操作符来删除重复项。另一个选项为此使用哈希算法。无论何种方式，你都可以看到涉及的工作比 `INTERSECT ALL` 查询更多。

当你合并不相交的输入时（例如包含日期列的不同年份数据），`INTERSECT` 和 `INTERSECT ALL` 在逻辑上是等价的。遗憾的是，在这种情况下你可能会使用 `INTERSECT` 运算符，是因为代码的按键次数较少，而没有意识到正在进行不必要的工作。因此，将 `INTERSECT ALL` 作为默认值并将 `INTERSECT` 运算符保留给结果可能存在重复项且你需要删除它们的情况是非常重要的。

有趣的是，如果你使用 `INTERSECT` 合并表行，而这些表具有定义不相交间隔的检查约束，优化器可以检测此并帮助你避免删除重复项的额外工作。例如，以下代码创建了单独表存储不同年份的数据，用 `CHECK` 约束强制执行不相交的年份间隔：

```sql
USE tempdb;
IF OBJECT_ID(N'dbo.T2014', N'U') IS NOT NULL DROP TABLE dbo.T2014;
IF OBJECT_ID(N'dbo.T2015', N'U') IS NOT NULL DROP TABLE dbo.T2015;
GO
CREATE TABLE dbo.T2014
(
  keycol INT NOT NULL CONSTRAINT PK_T2014 PRIMARY KEY,
  dt DATE NOT NULL CONSTRAINT CHK_T2014_dt CHECK (dt >= '20140101' AND dt < '20150101')
);
CREATE TABLE dbo.T2015
(
  keycol INT NOT NULL CONSTRAINT PK_T2015 PRIMARY KEY,
  dt DATE NOT NULL CONSTRAINT CHK_T2015_dt CHECK (dt >= '20150101' AND dt < '20160101')
);
```

在忽略最佳实践的情况下，你使用以下代码通过 `INTERSECT` 运算符合并表行：

```sql
SELECT keycol, dt FROM dbo.T2014
INTERSECT
SELECT keycol, dt FROM dbo.T2015;
```

幸运的是，得益于约束的存在，优化器发现结果中不存在重复项，因此像处理 `INTERSECT ALL` 一样优化此查询。该查询的计划如图 3-26 所示。

## EXCEPT 运算符

`EXCEPT` 运算符只返回出现在第一个输入中但不在第二个输入中的行。图 3-28 形象地展示了该操作符返回的内容。

![](img/bdc38aa36f6e2987d913ee5381474711_279_0.png)

图 3-28 EXCEPT 运算符。

作为一个示例，以下代码返回了不是客户位置的唯一员工位置：

```sql
SELECT country, region, city FROM HR.Employees
EXCEPT
SELECT country, region, city FROM Sales.Customers;
```
