
# 子查询优化与 EXISTS 谓词

该计划对代表 `Orders` 表实例 `O1`（查询中的外部实例）的 POC 索引进行全扫描。然后对于每一行 `O1`，计划在代表 `Orders` 表实例 `O2`（查询中的内部实例）的 POC 索引中执行查找。查找到达索引叶片中当前客户部分的开头，并扫描一行以收集键。然后计划过滤来自 `O1` 的行，其 `O1` 键等于 `O2` 键。

该计划中存在某种可以优化的低效之处，即 `Index Seek` 算子大约执行了多少次。每个订单执行一次查找，但你实际上只需要每个客户的一行。更高效的策略是每个客户执行一次查找。`custid` 列越密集，这种策略需要的查找越少。为了使性能更具体，假设数据有 10,000 个客户，平均每个客户有 1,000 个订单。现有的计划执行了 10,000,000 次查找。如果 B 树有三层，这将转化为 60,000 次随机读取。这是极其低效的。如果你能得出更高效的子查询计划，你将只需要 10,000 次查找。目前，我将解决方案限制在使用子查询，因为这是本节的重点。

```
![](img/bdc38aa36f6e2987d913ee5381474711_217_0.png)
```

图 3-2 每个客户一次查找的计划。

除了解决方案的第一步（检索符合条件的键）描述的工作外，该计划还在表中执行了 10,000 次查找，以获取目标订单的属性。随后进行了排序以优化查找。此计划增加了 10,000 次查找，总共 20,000 次查找，导致 60,000 次随机读取。与之前的解决方案相比，这提高了 500 倍！

完成后，运行以下代码进行清理：

```sql
DROP INDEX idx_poc_on ON Sales.Orders;
```

## EXISTS 谓词

`EXISTS` 谓词接受子查询并根据子查询返回非空集或空集分别返回真或假。作为一个基础示例，以下查询返回了订单了客户：

```sql
SELECT custid, customername
FROM Sales.Customers AS C
WHERE EXISTS (SELECT * FROM Sales.Orders AS O
WHERE O.custid = C.custid);
```

该谓词非常自然，因为它允许你用 SQL 表达上述请求的方式与你在口语中表达它们的方式相似。

`EXISTS` 的奇特之处在于，与 SQL 中的大多数谓词不同，它使用二值逻辑。它只返回真或假。它不会返回未知，因为不存在它不知道查询是返回了至少一行还是没有返回的情况。请原谅这种三重否定形式的最后一句，出于本章的目的，你需要练习这种逻辑。如果内部查询包含过滤器，则由于 `NULL` 的存在导致过滤器评估结果为未知的行将被丢弃。尽管如此，`EXISTS` 谓词总是能够确定地判断结果集是否为空。与 `EXISTS` 相反，例如 `IN` 谓词使用的是三值逻辑。因此，当你对谓词取反且数据中存在 `NULL` 时，使用 `EXISTS` 的查询与使用 `IN` 的查询逻辑含义可能不同。我将在稍后演示这一点。

关于 `EXISTS` 的另一点，是从索引选择的角度来看，优化器忽略了 `SELECT` 列表。例如，`Orders` 表有一个由 `custid` 列定义的索引 `idx_nc_custid`，且没有包含列。观察图 3-4 所示的 `EXISTS` 查询的执行计划。

```
![](img/bdc38aa36f6e2987d913ee5381474711_219_0.png)
```

图 3-4 使用 `SELECT *` 的 `EXISTS` 计划。

注意，尽管子查询使用了 `SELECT *`，但计划从 `Orders` 表中使用的唯一索引是 `idx_nc_custid`。换句话说，对于此查询，该索引被视为覆盖索引。这证明为了索引选择，`SELECT` 列表被忽略了。

接下来我将演示可以使用 `EXISTS` 谓词处理的经典任务。我将使用表 `T1`，你可以通过运行以下代码创建并填充该表：

```sql
SET NOCOUNT ON;
USE tempdb;
IF OBJECT_ID('dbo.T1') IS NOT NULL DROP TABLE dbo.T1;
CREATE TABLE dbo.T1(col1 INT NOT NULL CONSTRAINT PK_T1 PRIMARY KEY);
INSERT INTO dbo.T1(col1) VALUES(1), (2), (3), (7), (8), (9), (10), (11), (15), (16), (17), (28);
```

表中的键列是 `col1`。假设你有一个键生成器，它生成从 1 开始的连续键，但由于删除操作，存在间隙。一个经典的挑战是识别缺失的值。为了测试你解决方案的正确性，你可以使用后续代码生成的这组样本数据。为了性能考虑，你想向表中填充一个更大的集合。使用以下代码填充 10,000,000 行：

```sql
TRUNCATE TABLE dbo.T1;
INSERT INTO dbo.T1 WITH (TABLOCK) (col1)
SELECT n FROM TSQLV.dbo.GetNums(1, 10000000) As N n % 10000 <> %
OPTION(MAXD 1);
```

# 第 3 章 多表查询

你可以使用 `CASE` 表达式，如果 1 不已经存在于表中，则返回 1。更棘手的部分是在当 1 已经存在时识别最小值。实现此目标的一种方法是使用以下查询：

```sql
SELECT MIN(A.col) + 1 AS missingval
FROM dbo.T1 AS A
WHERE NOT EXISTS
(SELECT *
FROM dbo.T1 AS B
WHERE B.col = A.col + 1);
```

这段代码的第一步是过滤 `T1`（别名为 `A`）中的行，使得 `A` 中的值出现在缺失值之前。然后，你就知道 `A` 中的值出现在缺失值之前，因为你无法在 `T1`（别名为 `B`）中找到另一个 `B` 值比 `A` 大 1 的值。然后，从 `A` 的所有剩余值中返回最小的一个。也许你预期查询会立即完成；毕竟，在 `col1` 上有一个索引（`PK_T1`）。理论上，你应该能够按顺序扫描索引，并在发现缺失值之前的第一个点时立即短路工作。但在大型样本数据集上，需要几秒钟才能完成。在我的系统上，花费了五秒钟。要理解为什么查询很慢，请检查图 3-5 所示的执行计划。

```
![](img/bdc38aa36f6e2987d913ee5381474711_220_0.png)
```

**图 3-5** 最小缺失值的计划，第一次尝试。

注意 `col1` 上的索引被扫描了两次。使用了 `Merge Join` 算子来应用右半连接以检测不匹配项。`Stream Aggregate` 算子识别了最小值。关键在于，由于输入被扫描了两次，该计划效率低下。尽管扫描是有序的，但并没有短路。

优化查询的一种尝试是使用 `TOP` 过滤器代替 `MIN` 聚合，如下所示：

```sql
SELECT TOP (1) A.col + 1 AS missingval
FROM dbo.T1 AS A
WHERE NOT EXISTS
(SELECT *
FROM dbo.T1 AS B
WHERE B.col = A.col + 1)
ORDER BY A.col;
```

但查询被“杀死”了。检查图 3-6 所示的该查询的执行计划。

```
![](img/bdc38aa36f6e2987d913ee5381474711_221_0.png)
```

图 3-6 最小缺失值的计划，第二次尝试。

`Merge Join` 谓词认为 `A` 输入是按 `A.col` 排序的，`B` 输入也是排序的。由于外部查询按 `A.col` 排序而不是 `A.col + 1` 排序，优化器没有意识到行已经是排序的，并添加了一个消耗整个输入的 `Sort (Top N)` 算子。要修复此，只需将外部查询的 `ORDER BY` 改为 `A.col + 1`，如下：

```sql
SELECT TOP (1) A.col + 1 AS missing
FROM dbo.T1 AS A
WHERE EXISTS (
SELECT *
FROM dbo.T1 AS B
WHERE B.col = A.col + 1)
ORDER BY A.col+1;
```

观察图 3-7 所示的计划。

```
![](img/bdc38aa36f6e2987d913ee5381474711_221_1.png)
```

图 3-7 缺失值的计划，第三次尝试。

优化器意识到 `Merge Join` 算子返回行的方式与 `TOP` 过滤器相同，因此可以在找到第一个匹配行时短路。查询在亚秒内完成。或者，如果将内部查询的 `B.col = A.col + 1` 改为 `A.col - 1`，你也会得到一个最优计划，如下：

```sql
SELECT TOP (1) A.col + 1 AS missingval
FROM dbo.T1 AS A
WHERE EXISTS
(SELECT *
FROM dbo.T1 AS B
WHERE B.col = A.col - 1)
ORDER BY A.col;
```

现在添加 `CASE` 表达式逻辑，当不存在时返回 1，否则返回子查询的结果（高效解决方案之一）。你得到：

```sql
SELECT CASE
WHEN NOT EXISTS (SELECT * FROM dbo.T1 WHERE col = 1) THEN 1
ELSE (SELECT TOP (1) A.col + 1
FROM dbo.T1 AS A
WHERE EXISTS (...省略省略...))
```

另一个涉及序列的经典任务是识别所有缺失值的范围。在我们的情况下，我们将查找最小和最大值之间的缺失值。此任务通常被称为识别间隙。与最小值任务不同，这里没有短路可能。作为第一步，可以使用之前相同的查询查找间隙之前的所有值：

```sql
SELECT col
FROM dbo_T1 AS A
WHERE NOT EXISTS
(SELECT *
FROM dbo_T1 AS B
WHERE B.col = A.col + 1);
```

在小数据集上你得到以下输出：

```
col
----
3
9
11
17
28
```

注意你也得到了表中的最大值（28），因为该值加 1 不存在。但这个值并不是你想返回的间隙。为了从输出中排除它，为外部查询的过滤器添加谓词：

```sql
AND col < (SELECT MAX(col) FROM dbo_1)
```

现在你只剩下间隙之前的值，你需要为每个当前值识别间隙之后的相关值。你可以在外部查询的 `SELECT` 列表中使用以下子查询，它为每个值返回比当前值的最小值：

```sql
(SELECT MIN(B.col1)
FROM dbo.T1 AS B
WHERE B.col1 > A.col1)
```

你可能认为在此别名 `B` 以及检查值加 1 是否存在的子查询有点奇怪。但由于两个子查询具有独立的作用域，这没有问题。最后，将间隙之前的值加 1，并将间隙之后的值减 1，以获取实际间隙信息。将所有内容整合在一起，这是完整的解决方案：

```sql
SELECT col1 + 1 AS range_from,
(SELECT MIN(B.col1)
FROM dbo.T1 AS B
WHERE B.col1 > A.col1) - 1 range_to
FROM dbo.T1 AS A
WHERE NOT EXISTS (
SELECT
FROM dbo.T1 AS B
WHERE B.col1 = A.col1 + 1)
AND col1 < (SELECT MAX(col1) FROM dbo.T1);
```

此查询生成了内容：

| range_from | range_to |
| ---------- | -------- |
| 4          | 6        |
| 10         | 10       |
| 12         | 14       |
| 18         | 27       |

该解决方案的执行计划如图 3-8 所示。上分支中最右的三个算子处理表中最大 `col1` 值的计算。该值是从索引尾部获得的，因此工作忽略不计。中间部分使用 `Merge Join`（右反半连接）算子来识别间隙之前的值。算法在索引 `col1` 的两次有序扫描上运行。这种策略比另一种方案（对序列中的每个值应用索引查找）高效得多。最后，底部分支对每个过滤后的值（间隙之前的值）应用索引查找，以识别间隙之后的相应值。在这里重要的是，你获得的是每个过滤值（即每个间隙）的索引查找，而不是原始值。因此，特别是当间隙数量很少时，你会获得少量的查找。例如，大型样本数据集有 10,000,000 行和 1,000 个间隙。使用这些样本数据，查询在五秒内完成。

```
![](img/bdc38aa36f6e2987d913ee5381474711_222_0.png)
```

## 针对间隙查询的计划 3-8。

完成后，请运行以下代码：

```sql
IF OBJECT_ID('dbo.T1', 'U') IS NOT NULL DROP dbo.T1;
```

T-SQL 查询任务的有趣之处之一在于，对于任何给定的问题，通常有许多可能的解决方案。通常，不同的解决方案会导致不同的执行计划。因此，培养以不同方式编写查询的技能，并仔细观察优化器在每种情况下是如何处理的，至关重要。之后，当你调整查询并需要对计划实现某些效果时——例如，比较 SQL Server 如何处理基于子查询的解决方案与基于连接的解决方案，如何处理使用聚合的解决方案与使用 `TOP` 过滤的解决方案等等。另一种不同方法的示例是应用正逻辑与负逻辑。例如，回想本章开头提到的，识别出所有员工都处理过订单的客户。我为该任务提供的解决方案使用了正逻辑：

### SELECTSQL3

```sql
SELECT custid
FROM Sales.Orders
GROUP BY custid
HAVING COUNT(DISTINCT empid) = (SELECT COUNT(*) FROM HR.Employees);
```

另一种方法是应用负逻辑，因为你追求的是正向结果——即员工处理过订单的客户——你需要两个否定才能得到相同的含义。这就像说“常见”等同于说“不常见”。在我们的情况下，说“所有员工都处理过订单的客户”就像是说“没有员工没有处理过订单的客户”。这翻译为带有两个嵌套的 `NOT EXISTS` 谓词的查询：

```sql
SELECT custid, companyname
FROM Sales.Customers AS C
WHERE NOT EXISTS
(SELECT * FROM HR.Employees AS E
WHERE NOT EXISTS
(SELECT * FROM Sales.Orders AS O
WHERE O.custid = C.custid
AND O.empid = E.empid);
```

也许双重否定的形式最初并不直观，但好消息是，这种思维可以通过练习得到提高。

现在你可以检查并比较正逻辑解决方案与负逻辑解决方案的计划，以学习优化器在不同情况下是如何处理的。不过注意，TSQLV3 数据库中的表非常小，因此你实际上无法对它们进行任何性能测试。你需要更大的表来进行适当的性能分析和优化。我在文章[在序列中识别子序列，部分 2](http://sqlmag.com/t-sql-identifying-subsequence-in-sequence-part-2) 中展示了一个大数据量量的示例，其中双重否定方法实现了一种非常高效的解决方案。

发现双重否定方法在许多其他情况下也适用。例如，假设你有一个字符串列 `sn`（序列号），它应该只允许数字。你想用 `CHECK` 约束来强制执行此规则。你可以赞美基于正逻辑的谓词，但我发现在这种情况下，双重否定的形式是最优雅且经济的。正向规则说是：列中的每个字符都是数字。双重否定的形式是：列中没有任何一个字符不是数字。在 T-SQL 中，该规则翻译为以下谓词：

```sql
sn NOT LIKE '%[^0-9]'
```

简单明了！

## 异常的子查询

有些常见任务是通过子查询处理的，如果它们不遵循最佳实践，你很容易陷入 Bug 的困扰。我将描述两个问题：一个涉及子查询列名的替换错误，另一个是子查询中对 `NULL` 的不直观处理。我还将提供最佳实践，如果遵循这些原则，可以帮助你避免此类麻烦。

考虑 `T1` 和 `T2` 表及其填充的示例数据：

```sql
IF OBJECT_ID('dbo.T1') IS NOT NULL DROP TABLE dbo.T1;
IF OBJECT_ID('dbo.T2') IS NOT NULL DROP TABLE dbo.T2;
GO
CREATE TABLE dbo.T1(col1 INT NOT NULL);
CREATE TABLE dbo.T2(col2 INT NOT NULL);
INSERT INTO dbo.T1(col1) VALUES(1);
INSERT INTO dbo.T1(col1) VALUES(2);
INSERT INTO dbo.T1(col1) VALUES(3);
INSERT INTO dbo.T2(col2) VALUES(2);
```

假设你需要返回 `T1` 中也出现在 `T2` 值集中的值。以下查询（但不要运行它）：

```sql
SELECT col1 FROM dbo.T1 WHERE col1 IN(SELECT col1 FROM dbo.T2);
```

在执行此查询之前，检查两个表中的值并回答问题：你期望在结果中看到哪些值？自然地，你期望在结果中只看到值 2。执行查询。得到以下输出：

```
col1
-----
1
2
3
```

你能解释为什么你得到了 `T1` 的所有值而不是只有 2 吗？

仔细检查表定义和查询代码会发现，针对 `T2` 的子查询错误地引用了 `col1`，而不是 `col2`。现在问题是，为什么代码没有报错？SQL Server 在解析表列时，首先在紧邻查询的表中查找该列。如果找不到（如我们的案例中所示），它就会在外部查询的表中查找。

忽略它们。你可以通过几种方式实现这种行为。一种方法是在内部查询中通过添加过滤器 `WHERE col1 IS NOT NULL` 来显式移除 `NULL` 值，如下：

```sql
```
