
要看到这一效果，需要一个分区表，并进行一些设置。以下代码在 `tempdb` 中创建一个分区函数、一个分区方案和一个表：

```sql
USE tempdb;
GO

CREATE PARTITION FUNCTION pf_1 (INT)
AS RANGE FOR VALUES
(
25000, 50000, 75000, 100000,
125000, 150000, 175000, 200000,
225000, 250000, 275000, 300000,
325000, 350000, 375000, 400000,
425000, 450000, 475000, 500000,
525000, 550000, 575000, 600000,
625000, 650000, 675000, 700000,
725000, 750000, 775000, 800000,
825000, 850000, 875000, 900000,
925000, 950000, 975000, 1000000
);

CREATE PARTITION SCHEME ps_1
AS PARTITION pf_1
ALL TO ([PRIMARY]);

CREATE TABLE partitioned_table (
  col1 INT NOT NULL,
  col2 INT NOT NULL,
  some_stuff CHAR(200) NULL
) ON ps_1;

CREATE UNIQUE CLUSTERED INDEX ix_col1 ON partitioned_table(col1) ON ps_1;

GO
```

考虑以下 `SELECT INTO` 查询：

```sql
WITH
n1 AS (SELECT 1 UNION ALL SELECT 1),
n2 AS (SELECT 1 FROM n1, n1 c),
n3 AS (SELECT 1 FROM n2, n2 c),
n4 AS (SELECT 1 FROM n3, n3 c),
n5 AS (SELECT 1 FROM n4, n4 c),
n6 AS (SELECT 1 FROM n5, n5 c)
SELECT TOP (100000000)
  col1,
  ROW_NUMBER() OVER
  (
    ORDER BY
      (SELECT NULL)
  ) AS coll,
  CHECKSUM(NEWID()) AS col2
INTO #test_table
FROM n6;
```

该查询向名为 `#test_table` 的临时表插入了 10,000,000 行。图 2-8 显示了该查询在 SQL Server 2012 实例上运行时的执行计划片段。

| 表 (insert #test_table) | 标量计算 (Compute Scalar) | 顶部 (Top) | 序列投影 (标量计算) | 分段 (Segment) | 并行 (汇聚流) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 成本: 70 % | 成本: 0 % | 成本: 0 % | 成本: 0 % | 成本: 0 % | 成本: 1 % |

图 2-8 在 SQL Server 2012 中，`SELECT INTO` 在单个线程上进行写入。

尽管此查询使用了并行处理，但在计算行号之前，并行流会进行聚集。计算完行号后，数据将通过单串行流写入临时表。

在 SQL Server 2014 实例上运行相同的查询会生成图 2-82 所示的计划片段。

| 并行 (汇聚流) | 表 (insert #test_table) | 标量计算 (Compute Scalar) | 并行 (分发流) | 顶部 (Top) | 序列投影 (标量计算) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 成本: 5 % | 成本: 37 % | 成本: 0 % | 成本: 19 % | 成本: 1 % | 成本: 1 % |

图 2-82 在 SQL Server 2014 中，`SELECT INTO` 可以是多线程的。

在 SQL Server 2014 中，行号是在串行线程中生成的。然而，一旦计算完成，行就会分布到多个线程（在本例中，使用轮询方案），然后从多个并发的流写入目标表。

这种改进带来的性能收益可能是惊人的：在一台同时安装了 SQL Server 2012 和 SQL Server 2014 的测试服务器上，在磁盘系统和内存分配相同的情况下，查询在 SQL Server 2012 中运行了 10 秒，而在 SQL Server 2014 中仅运行了 4 秒。

# 并行与查询优化

在查询处理器能够执行并行查询计划之前，查询优化器必须生成该计划。所使用的过程比串行查询计划的要复杂且细微，作为一名处理并行查询的开发者，你需要了解发生的情况，以便在问题发生时有效地处理它们。

查询计划中使用或不用并行处理的决定大部分是在查询处理器参与查询执行之前做出的。此决定基于实例级（或资源生成器组级）设置与所涉及查询的结合。实际运行计划的执行引擎对于是否使用并行处理几乎没有多少发言权，且当 SQL Server 实例处于极端资源压力时，它将否决使用并行处理。

# 并行设置

有四个影响并行处理的实例级设置。这些设置可以在 `sys.configurations` 目录视图中查看，并可以使用 `sp_configure` 系统存储过程进行配置。设置如下：

- **亲和性映射 (Affinity Map)**：此设置控制服务器的哪些逻辑处理器将映射到 SQL 调度器。并行查询需要多个 SQL 调度器，因此，如果亲和性映射被设置为只有一个处理器，则查询优化器将不会尝试生成并行查询计划。也就是说，鉴于当今服务器中众多的处理器，看到单调度器的 SQL Server 实例是非常罕见的。此设置的默认值为 0，表示所有逻辑处理器都应映射到 SQLOS 调度器。

- **最大并行度 (Max Degree of Parallelism)**：最大并行度是并行查询使用的默认值，用于确定为每个并行单元分配多少工作线程（之前讨论过的 `DOP`）。可以使用查询级别的 `MAXDOP` 提示来覆盖此设置——无论是增加还是减少。此设置名称中的“最大”一词以及查询提示有一点误导性；如果并行查询使用了并行处理，它将使用在查询级别指定、通过设置或通过本节稍后描述的资源生成器设置所确定的任何 `DOP`。对于给定的查询，关于“正确”的 `DOP` 应该是多少，既没有查询优化器的决定，也没有运行时查询处理器的决定。此设置的默认值为 0，意味着并行计划的每个区域可以使用与在线 SQLOS 调度器数量相等的线程，最多为 64 个。

- **并行处理的成本阈值 (Cost Threshold for Parallelism)**：在优化查询时，查询优化器会经历多个阶段，每个阶段都会为过程增加时间和开销。优化器的核心目标之一是在短时间内生成良好的计划，此设置通过帮助其实现该目标（如果查询计划的串行版本成本不高，不值得进一步处理，它将退出查询优化过程）。此设置的默认值为 5，这意味着只有当成本超过 5 时，才会考虑并行处理。

例如，SQL Server 与 IIS 实例共享一个服务器，而管理员希望为每个进程分配其自己的预留 CPU。这种情况是有意义的，但在当今世界，服务器虚拟化技术通常是处理此类情况更好的方法。

最大工作线程数（`Max Workers Threads`）被设计为自动维护，通常只有在极端情况下（特别是极其沉重的并行负载以及对线程池耗尽有特定需求时）才需要调整。这些情况通常需要产品支持的能力，让支持人员决定如何解决这种情况可能是明智的。

查询成本（`Query cost`）是一个最早在 1998 年 SQL Server 7.0 中引入的指标。现在，16 年后（截至本文结构体编写时），计算机行业已经发生了巨大变化，但查询成本仍然使用基本结构。一个成本为 5 的查询（并行度阈值 `Cost Threshold Of Parallelism` 的默认值）在 1998 年是非常庞大的，但在如今的海量数据库中则相对较小。因此，建议对大多数 SQL 实例更改此数字。对于今天典型的硬件和数据规模，值在 30 到 50 之间是合理的。如果你发现查询（针对你的环境）正在使用并行计划，可以考虑将其设置得更高。

与并行度成本类似，最大并行度（`Max Degree Of Parallelism`）也有一个令人遗憾的默认值。此设置应该针对特定实例进行调整，以平衡查询响应时间与允许许多查询并发运行之间的目标。如果最大并行度太低，查询将变慢；如果太高，并发查询将强制竞争处理器时间并产生负面影响。

最大并行度的通用指南取决于工作负载。对于 OLTP 系统，其倾向于具有高比例的小型串行查询，此外还有许多轻量级查询，可能建议较小的最大并行度——低至 2。

另一方面，对于 OLAP 工作负载，典型情况是少量的大型查询，较高的最大并行度通常是一个好主意。在四插槽服务器上，明智的做法是设置为每个 NUMA 节点的处理器数量（通常与每个插槽的处理器数量相同），或者在双插槽服务器上取其的一半。这为每个查询提供了可用 CPU 算力的很大一部分，同时允许并发查询运行而互不干扰。

如果启用了超线程（`Hyper-Threading`），建议将最大并行度设置为不超过比每个节点物理处理器数量多 50%。换句话说，如果每个节点有 6 个物理处理器和 12 个逻辑处理器（由于超线程），通常建议将最大并行度设为不超过 9。这有助于防止查询执行压过超线程提供的额外加速。

## 并行抑制因素

除了核心查询优化和处理决策外，几个查询功能可以以一种方式抑制并行性：要么在原本并行的查询计划中强制执行串行区域，要么完全禁用给定查询的并行性。

以下是导致并行查询计划中出现串行区域的常见原因列表：

- **多语句 T-SQL UDF**：多语句 UDF 通过表变量返回表值。用户定义函数 (`UDF`) 中的逻辑将在串行区域中进行处理，尽管计划的其他部分可能使用并行处理。

- **递归 CTE**：递归通用表表达式在串行区域中处理，下游算符 (`operators`) 可能会使用并行处理。

- **反向扫描**：SQL Server 中的索引使用链表，可以按正向或反向方向扫描。只有正向扫描符合前述的并行扫描。反向扫描将被限制在串行中执行。

- **非分区的 TOP、聚合和窗口函数**：`TOP` 运算符、聚合和窗口函数的使用涉及创建行组。如果必须在计划的给定阶段通过分析整个输入行集来确定组，则查询优化器将不得不使用串行示例。示例包括相关表表达式之外的未分组聚合（也称为标量聚合）以及不使用分区的窗口函数。

以下列表包含了会完全禁用给定计划并行性的常见功能：

- **标量 T-SQL UDF**：在查询中使用任何标量 T-SQL `UDF` 都会导致该查询无法使用并行性。对于任何考虑使用 T-SQL `UDF` 的开发者来说，这应该是一个重大的警示信号。内联表达式或 CLR 标量 `UDF` 是更好的选择。

- **表变量的修改**：在大多数情况下，当使用表进行插入、更新或删除行时，在实际数据修改之前的查询部分可以在串行区域中处理，并行的 `SELECT INTO` 除外。表变量将打破这一惯例；如果修改了表变量中的行，整个计划将串行运行。请注意，如果表变量仅用于计划中不涉及修改的某些部分，则并非如此。

- **标记为 `DataAccessKind.Read` 的 CLR UDF**，这意味着它有权在托管数据库中运行查询。

- **内存优化表 (`Memory-optimized tables`)**：内存优化表不能参与并行查询计划。

要查看这些功能之一的影响，首先考虑以下查询，其计划如图 2-85 所示：

```sql
SELECT TOP(1000)
OrderQty
FROM Sales.SalesOrderDetail
ORDER BY
OrderQty DESC;
```

| SELECT | Top | 并行 (Gather Streams) | 排序 | 聚集索引扫描 (Cluste...) |
| --- | --- | --- | --- | --- |
| Cost: 0 | Cost: 0 | Cost: 1 | Cost: 70 % | Cost: 29 % |

**2-85** 并行计划。

尽管这可能是可以编写的最简单的 `UDF`，但它对查询计划的影响是巨大的，如图 2-86 所示。首先创建 `UDF`：

```sql
CREATE FUNCTION ReturnInput(@input INT)
RETURNS INT
AS
BEGIN
RETURN(@input)
END
```

一旦创建了 `UDF`，就可以在查询中使用：

```sql
SELECT TOP(1000)
ReturnInput(OrderQty)
FROM Sales.SalesOrderDetail
ORDER BY
OrderQty DESC;
```

| SELECT | 计算标量 | 计算标量 | 排序 (Top N Sort) | 聚集索引扫描 (Cluste...) |
| --- | --- | --- | --- | --- |
| Cost: 0 | Cost: 0 | Cost: 0 | Cost: 90 % | Cost: 10 % |

**2-86** 不再是并行计划。

如果你试图确定选择是否是因为抑制因素而不并行，请检查 `SELECT` 算符的属性。图 2-87 突出了 `NonParallelReason` 属性，它可以帮助你理解限制并行性的原因。

| MemoryGrantInfo | CouldNotGenerateParallelPlan |
|---|---|
| SELECT Cost:0% | NonParallelReason |
| Optimization Level | FULL |

**2-87** `NonParallelReason` 节点显示存在抑制因素。

接下来，这里有一个事务次数比标准版本多 504 倍的：

```sql
SELECT
th.ProductID + x.v AS ProductID,
th.ActualCost,
th.TransactionDate
INTO #bigger_transactions
FROM Production.TransactionHistory AS th
  CROSS JOIN
  (
    SELECT
      (NTILE(5) OVER (ORDER BY p.ProductID) - 1) * 1000
    FROM Production.Product AS p
) AS x(v);
CREATE CLUSTERED INDEX i_ProductID
ON #bigger_transactions (ProductID);
```

该表通过将 `Production.TransactionHistory` 中的 113,443 条交易与来自 `Production.Product` 派生的 504 行进行交叉连接而创建。使用 `NTILE` 函数是为了创建五组行，这些行对应于创建 `#bigger_products` 表时使用的 5 行。结果集包含 57,175,272 行，并且在 `ProductID` 列上进行了聚集。之所以选择该列是因为查询将使用该列来连接这两个表。

场景如下：用户想知道每个产品销售出的前 10 个最高价格（包括相同价格）以及相应的交易日期。以下查询回答了该问题：

```sql
SELECT
p.Name,
x.TransactionDate,
x.ActualCost
FROM
(
  SELECT
    th.ProductID,
    th.TransactionDate,
    th.ActualCost,
    ROW_NUMBER() OVER (
      PARTITION BY
        th.ProductID
      ORDER BY
        th.ActualCost DESC
    ) AS rn
  FROM #bigger_transactions AS th
) AS x
INNER JOIN #bigger_products p ON p.ProductID = x.ProductID
WHERE x.rn <= 10;
```

该查询通过在派生表 `x` 中计算行号来实现，按 `ProductID` 分区并按 `ActualCost` 降序排序。在查询的外部，对行进行过滤以仅返回每个产品的前 10 条，并与 `#bigger_products` 进行连接以获取每个产品的名称。图 2-88 显示了为了适应本书而编辑过的计划版本。

![](img/bdc38aa36f6e2987d913ee5381474711_207_0.png)

**图 2-88** 查找前 10 个最贵交易的查询计划。

此查询计划使用了并行性，但存在几个可以在不修改索引或表结构的情况下解决的潜在瓶颈。

第一个瓶颈是 `Hash Join` 算符探针侧（`probe side`）的排序。正如前面提到的，排序（`Sort`）并不是线性扩展的，而且在这种情况下，输入行数很大。由于这是一个并行计划，集合将被拆分，但规模的减少将受到计划 `DOP`（并行度）的限制。将集合拆分成更小的工作子集可能会产生更大的收益。此外，较小的子集需要的内存更少，内存耗尽并溢出到 `tempdb` 的机会也较低。

第二个瓶颈是在 `Hash Join` 算符探针侧并行扫描下游使用的 `Repartition Streams`（重新分区流）。该算符使用 `Hash` 分布方法根据 `ProductID` 将行分发到线程之间。这样做是为了让每个产品的行被正确地排序在一起。遗憾的是，这种分区在计划的如此早阶段就是必要的，它将移动扫描产生的每一行——全部 57,175,272 行。这是大量的数据移动。

# 并行嵌套循环

这两个瓶颈的解决方案是重新思考数据流通过这种大型计划的方式，并想出一种消除单体操作的方法，转而执行更多更小的操作。可以实现这一点的查询计划工具是 `Nested Loops`（嵌套循环）算符。

在任何查询计划中，无论是串行的还是并行的，`Nested Loops` 算符都会为每个外部行调用一次内部侧算符。`Nested Loops` 通常与相关子查询或表表达式，用作对每个必要的行评估相关表达式。
