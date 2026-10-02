
我的机器上有 8 个逻辑 CPU。根据 SQL Server 的成本公式，在有许多 CPU 的情况下，针对具有 1,000,000 行的表并过滤掉 100,000 行的查询应该获得一个并行计划。这就是为什么第一个查询的计划使用了并行扫描。然而，由于反向扫描无法通过并行方式处理，第二个查询的计划使用了串行计划。

当你尝试使用跟踪标志 8649 强制第二个查询使用并行处理时，观察优化器的做法很有趣，如下所示：

```sql
SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
WHERE orderid <= 100000
ORDER BY orderid DESC
OPTION(QUERYTRACEON 8649);
```

此查询的计划如图 2-49 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_141_0.png)

**图 2-49** 强制并行的计划。

由于无法使用并行反向序扫描，优化器选择了一个使用并行无序扫描紧跟一个显式排序操作的计划。显然，这是一个非常低效的计划。如果你发现并行是查询性能的关键因素，你可以安排一个降序索引。当然，如果微软在以后某时刻引入了对并行反向扫描的支持，你就不再需要为此目的使用降序索引了。

另一个降序索引有用的奇案例是同时具有窗口分区子 (`PARTITION BY`) 和排序子 (`ORDER BY`) 的窗口函数。考虑以下查询：

```sql
-- Query 1
SELECT orderid, custid, empid, shipperid, orderdate, filler, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate ASC) AS rownum
FROM dbo.Orders;
```

```sql
-- Query 2
SELECT orderid, custid, empid, shipperid, orderdate, filler, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate DESC) AS rownum
FROM dbo.Orders;
```

```sql
-- Query 3
SELECT orderid, custid, empid, shipperid, orderdate, filler, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate DESC) AS rownum
FROM dbo.Orders;
```

目前，表上有一个名为 `idx_nc_sid_od` 的覆盖索引，它从分区列开始并以排序列继续。检查图 2-50 中的执行计划。

查询 1：查询成本（相对于批处理）：100%

SELECT orderid, custid, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate ASC) AS rownum

| Sequence (Compute Scalar) | Segment | Index Scan (Clustered) |
| :--- | :--- | :--- |
| Cost: 0% | | Cost: 2% |

查询 2：查询成本（相对于批处理）：100%

SELECT orderid, custid, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate DESC) AS rownum

| Sequence (Compute Scalar) | Segment | Parallelize (Gather Streams) | Sort | Index Scan (Clustered) |
| :--- | :--- | :--- | :--- | :--- |
| Cost: 0% | Cost: 0% | Cost: 19% | Cost: 71% | Cost: 10% |

查询 3：查询成本（相对于批处理）：100%

SELECT orderid, custid, ROW_NUMBER() OVER (PARTITION BY shipperid ORDER BY orderdate DESC) AS rownum

| Sequence (Compute Scalar) | Segment | Index Scan (Clustered) |
| :--- | :--- | :--- |
| Cost: 0% | Cost: 2% | Cost: 98% |

图 2-50 窗口函数的计划。

查询 1 的计划显示，有一个覆盖索引，其键从升序分区列开始并以排序列继续，优化器选择了索引的序扫描并避免了显式排序操作。

在查询 2 中，窗口函数的规范与查询 1 相似，但排序列为降序。理论上，优化器可以选择按降序扫描索引的计划。但是，由于缺少 `ORDER BY` 子句，SQL Server 似乎想按窗口分区元素的升序处理行，因此它添加了显式排序操作。

奇怪的是，正如查询 3 的计划所示，如果你添加了按 `shipperid` 列降序的 `ORDER BY` 子句，优化器突然发现可以使用反向扫描来计算窗口函数并支持所需的表示。索引的另一个用是二十年前，在 SQL Server 2000 发布后不久，Wayne Snyder 发现了我在 SQL Server 中见过的最惊人的漏洞之一。如果你创建一个以 `col1 DESC` 为键的聚集索引，并执行带有过滤器 `col1 > @n` 的 `DELETE` 语句，SQL Server 会删除所有 `col1 < @n` 的行。这个漏洞存在于 SQL Server 2000 RTM 中，当然，在 Service Pack 1 中被修复了。

# 包含列 (Included columns)

当你定义非聚聚集索引时，你会指定一个列向量作为键列表，以确定索引中行的顺序。SQL Server 可以根据此键列表执行有序扫描和范围扫描，以支持排序、过滤、分组和连接等操作。然而，如果你需要为了覆盖性（避免回查）而向索引中添加列，且这些列不具有任何排序相关的用途，则你可以在指定的 `INCLUDE` 子句中添加这些列。

与键列不同，包含列仅出现在索引的叶节点行中。此外，SQL Server 对此的限制较少。例如，键列表不能超过 16 列，而包含列可以包含任意数量。键列表的大小不能超过 900 字节，而包含列可以使用 XML 和其他大对象（LOB）特殊类型。当你更新表中的某行时，SQL Server 自然需要更新所有相应的列。如果索引键列的值发生变化，行的排序位置可能会发生变化，此时 SQL Server 需要重新定位该行。如果包含列的值发生变化，排序位置保持不变，更新可以在原处完成（假设行没有扩展）。

作为 `INCLUDE` 子句用法的示例，考虑以下查询：

```sql
SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
WHERE custid = 'C0000000001'
```

我在之前讨论访问方法（即“无序非聚聚集索引扫描 + 回查”）时展示过此查询，并在图 2-1 中提供了其执行计划。目前，该查询没有最优索引。该计划扫描了某个非覆盖非聚聚集索引的整个叶节点层，该索引包含 `custid` 列作为非前导键，然后对匹配的案例应用回查。该计划的执行在我的机器上执行了 406 次逻辑操作。

更优的索引是使用以 `custid` 定义的键列来支持过滤，并将所有剩余列定义为包含列以避免回查，如下：

```sql
CREATE INDEX idx_nc_c1_oid_eid_sid_od_fl ON dbo.Orders(custid)
INCLUDE(orderid, empid, shipperid, orderdate, filler);
```

再次运行查询：

```sql
SELECT orderid, custid, empid, orderdate, filler
FROM dbo.Orders
WHERE custid = 'C0000000001'
```

该查询的执行计划如图 2-51 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_143_0.png)

**图 2-51** 使用包含列索引的执行计划。

我发现该查询仅报告了 5 次逻辑读取。

完成后，运行以下代码进行清理：

`DROP INDEX dbo.Orders.idx_nc_cid_old_eid_sid_od_fl;`

# 过滤索引和统计信息 (Filtered indexes and statistics)

过滤索引是根据谓词对底层表的行子集创建的索引。你在索引定义中通过 `WHERE` 子句指定谓词。与非过滤索引相比，过滤索引的创建和维护成本更低，因为只有对相关行子集的修改才会反映在索引中。此外，过滤分布统计信息（直方图）比非过滤统计信息更准确。这是因为直方图中的最大步数为 200，而使用过滤统计信息时，该数字用于表示更小的行集。此外，由于直方图是针对满足索引条件的行子集的索引前导键创建的，你实际上获得了等同于拥有多列直方图的的估算质量。

在索引本身并不重要但统计信息很重要的情况下，你也可以创建过滤统计信息。你可以使用 `CREATE STATISTICS` 命令并在 `WHERE` 子句中指定谓词来实现。

作为过滤索引的示例，假设你经常查询发货国家为美国（USA）且处于特定日期范围（从本周、本月、本年初开始）的订单。你可能不会频繁地对其他发货国家执行类似的查询。你需要专门针对美国加速查询。你创建了一个带有谓词 `shipcountry = 'USA'` 过滤的索引，并将 `orderdate` 指定为键。如果避免回查对你来说很重要，你将希望将查询中的所有剩余列指定为包含列。运行以下代码创建此类过滤索引：

```sql
CREATE NONCLUSTERED INDEX idx_USA_orderdate
On Sales.Orders(orderdate)
INCLUDE(orderid, custid, requireddate)
WHERE shipcountry = 'USA'
```

接如下所示查询将从新索引中受益：

```sql
SELECT orderid, custid, orderdate, requireddate
FROM Sales.Orders
WHERE shipcountry = 'USA'
AND orderdate >= '20140101'
```

该查询的执行计划如图 2-52 所示。

| 实际行数 | 99 |
| 估计行数 | 678 |

![](img/bdc38aa36f6e2987d913ee5381474711_145_0.png)

**图 2-52** 使用过滤索引的计划，优化器认为该索引可能有用，且基数估算存在不准确之处。

由于索引匹配查询过滤器，优化器认为该索引可能有用。

## 列存储索引

列存储技术是数据库领域的一个游戏规则改变者。它最初在 SQL Server 2012 中引入，并在 SQL Server 2014 中得到了显著改进。该技术主要针对数据仓库负载。请考虑图 2-54 所示的数据仓库经典星型体系模型。

![](img/bdc38aa36f6e2987d913ee5381474711_147_0.png)

图 2-54 星型模型。

你拥有维度表，用于跟踪分析数据的维度，如客户、员工、产品和时间。每个维度表都有一个代理键。大部分数据存储在事实表（Fact table）中。该表包含每个维度表代理键列，以及代表数量和金额等指标的列。在引入列存储技术之前，SQL Server 中数据的传统的内部表示是基于行存储（rowstore）技术的。这意味着数据是以行模式进行存储和处理的。随着近年来数据仓库中数据量的不断增长，行存储技术在许多层面上往往效率低下，而列存储技术解决了这些低效问题。

要理解为什么行存储在大型数据仓库环境中效率低下，请考虑典型的数据仓库查询（也称为星型连接查询）。它们通常将事实表与某些维度表连接，并进行过滤、分组和聚合。以下是我们 PerformanceV3 数据库中典型数据仓库查询的示例：

```sql
USE PerformanceV3;
SET STATISTICS IO, TIME ON; -- 开启性能统计

SELECT D1.attr1 AS x, D2.attr1 AS y, D3.attr1 AS z,
COUNT(*) AS cnt, SUM(F.measure1) AS total
FROM dbo.Fact AS F
INNER JOIN dbo.Dim1 AS D1
ON F.key1 = D1.key1
INNER JOIN dbo.Dim2 AS D2
ON F.key2 = D2.key2
INNER JOIN dbo.Dim3 AS D3
ON F.key3 = D3.key3
WHERE D1.attr1 <= 10
AND D2.attr1 <= 15
AND D3.attr1 <= 10
GROUP BY D1.attr1, D2.attr1, D3.attr1;
```

该查询的执行计划如图 2-55 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_148_0.png)

图 2-55 使用行存储进行星型连接查询的计划。

我在系统中对该查询获取了以下性能统计：

Table 'Fact'. Scan count 122, logical reads 29300

CPU time = 890 ms, elapsed time = 490 ms.

示例数据库中的事实表只有 2,500,000 行。通常情况下，现在的表要大得多。不过，我们的表已经大到足以支持并行计划并允许我说明行存储和列存储技术之间的差异。表越大，使用列存储技术的优势越明显，因此请记住，你看到的差异将比我在示例中看到的大得多。

如所述，行存储技术有许多缺点。在索引方面有许多可能性，导致你花费大量的时间和精力在建立索引上。如果你在系统中有很多查询，那么为事实表查询创建完美的索引将非常不利。你最终会得到太多的索引。为了限制创建的索引数量，你会优先对某些查询进行调优，并合并具有相似索引要求的多个查询。例如，如果你有多个查询可以从相同的键列表获益，但包含不同的包含列表，你可能会创建一个包含这些包含列的超集的索引。结果是，许多查询将没有真正支持它们的索引，而且每个查询最终都可能使用包含比其相关列更多的的索引。正如你所意识到的，这意味着查询执行的读取次数多于最优数量。

在行存储中，数据默认是不压缩的；你很少需要显式地使用行压缩或页压缩。即使你这样做了，由于数据是逐行存储的，SQL Server 实现的压缩水平远无法达到列存储所能达到的水平。

行存储技术的另一个缺点是，目前的执行模型是行执行模型。这意味着查询计划中的不同算符都被限制为一次处理一行。你可以从图 2-55 中示例查询的执行计划中看到这一点。计划中的所有算符都将显示执行模式为 Row（行）（我高亮了针对事实表的聚集索引查找以及一个哈希连接的此属性）。由于算符一次处理一行，浪费了大量的 CPU 周期。算符评估所需的任何内部信息都是按行评估的。

列存储技术发生了非常的变化。请注意，SQL Server 2012 仅限于非聚集、不可更新的列存储索引。SQL Server 2014 增加了对聚集、可更新索引的支持，使得该技术变得更易用。

使用以下代码在我们的事实表上创建一个非聚集列存储索引：

```sql
CREATE NONCLUSTERED COLUMNSTORE INDEX idx_nc_cs
ON db.Fact(key1, key2, key3, measure1, measure2, measure3);
```

你列出的顺序并不重要。与行存储不同，列存储中没有排序的概念。图 2-56 阐了数据在列存储中的组织方式。

![](img/bdc38aa36f6e2987d913ee5381474711_150_0.png)

| Segment | Segment | Segment | Segment |
|---|---|---|---|---|
| Rowgroup 1 | | | | |
| Rowgroup 2 | | | | |
| Rowgroup 3 | | | | |
| Rowgroup 4 | | | | |

![](img/bdc38aa36f6e2987d913ee5381474711_150_1.png)

数据以称为行组（rowgroups）的单位存储。每个行组最多包含 1,000 行。你可以在视图 `columnstore_rowgroups` 中找到关于行组的信息。每个行组被划分为列段（column segments）。你可以在视图 `columnstore_segments` 中找到关于列段的信息。SQL Server 在内部记录每个列段的最小值和最大值。如果你的查询按特定列进行过滤，且过滤后的值落在列段覆盖的范围之外，整个行组将被排除。这种能力被称为段消除（segment elimination）。

你可以在视图 `columnstore_dictionaries` 中找到关于字典的信息。SQL Server 将字典用于字符串，有时也用于其他类型。列存储技术也受益于并行处理。每个行组都以高压缩格式存储。你可以在视图 `columnstore_rowgroups` 中找到关于行组的信息。

列存储技术的另外两个方面倾向于减少 I/O 成本。如所述，微软通过列存储实现的压缩水平远高于行存储。此外，请记住 SQL Server 将数据安排在字典中。而且，SQL Server 仅从相关列构造结果集的这一事实，与行存储相比，显著减少了 I/O 成本。

## 查询调优

*   注意：
