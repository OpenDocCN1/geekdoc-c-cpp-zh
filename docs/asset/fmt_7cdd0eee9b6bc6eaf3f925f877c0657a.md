
检查图 2-15 所示的该查询的执行计划。

![](img/bdc38aa36f6e2987d913ee5381474711_85_1.png)

图 2-15 包含聚集键的索引。

观察发现，对于该查询，`PK_Orders` 索引仍然被视为覆盖索引。问题是，当索引显式定义在 `orderid` 列上作为键时，为什么会这样？答案是表有一个按 `orderdate` 列定义的聚集索引。正如你可能记得的，SQL Server 在非聚集索引中使用聚集索引作为行定位器。因此，尽管你显式地在 `orderid` 列上定义了 `PK_Orders`，SQL Server 在内部将其包含了 `orderid` 和 `orderdate` 列。无论 SQL Server 是否添加 `orderdate` 列作为行定位器——一旦在那里，它就可以用于查询处理。

# 有序聚集索引扫描 (Ordered clustered index scan)

聚集索引扫描是对聚集索引叶级的完全扫描，保证数据按顺序返回给下一个算子。例如，以下按 `orderdate` 排序的查询将得到这种方法：

```sql
SELECT orderid, custid, empid, shipperid, orderdate, filler
FROM dbo.Orders
ORDER BY orderdate;
```

图 2-11 显示了优化器为该查询生成的执行计划。注意，聚集索引扫描算子的 `Ordered` 属性显示为 `False`。图 2-12 展示了存储引擎执行此方法的两种方式。

图 2-11 B 树扫描（执行计划）。

![](img/bdc38aa36f6e2987d913ee5381474711_83_0.png)

**图 2-12** B 树扫描（存储引擎）。

SQL Server 报告在我的系统上对该查询执行了 25,073 次逻辑读取。

同样，在这里发现计划在物理操作和逻辑操作属性中显示相同的值也让我困惑。这一次，两个属性都显示为聚集索引扫描。对我来说，逻辑操作仍然是表格扫描，而物理操作是聚集索引扫描。

聚集索引扫描算子的 `Ordered` 属性显示为 `False`，这说明从关系顺序的角度来看，数据不需要按键从算子返回。这并不意味着按顺序返回就是问题；相反，它意味着任何顺序都可以。这为存储引擎留出了一些操作空间，意味着它可以自由地在两种扫描类型之间进行选择：索引顺序扫描（遵循链表进行索引扫描）和分配顺序扫描（基于 IAM 页的扫描）。存储引擎在选择采用哪种扫描类型时考虑的因素包括性能和数据一致性。

![](img/bdc38aa36f6e2987d913ee5381474711_88_0.png)

图 2-19 有序覆盖非聚集索引扫描（存储引擎）。

注意执行计划，索引扫描（Index Scan）算子的 `Ordered` 属性显示为 `True`。

有序索引扫描不仅用于你显式请求排序数据的情况，还用于计划使用了可以从排序输入数据中获益的算子的情况。这发生在处理 `GROUP BY`、`DISTINCT`、连接以及其他请求时。这种情况也可能发生在较不明显的情况下。例如，查看图 2-20 所示的以下查询的执行计划：

```sql
SELECT orderid, empid, orderdate
FROM dbo.Orders AS O01
WHERE orderid =
    (SELECT MAX(orderid)
     FROM dbo.Orders AS O02
     WHERE O02.orderid = O01.orderdate);
```

| 实际行数 | 1490 |
|---|---|
| SELECT 成本: % 0 | Top 成本: % 0 | Segment 成本: % 2 | 扫描（非聚集）[Orders].[idx_unc_od_od_1_cid_eid] [O01] 成本: % 98 |

图 2-20 带有分段的有序覆盖非聚集索引扫描。

`Segment` 算子将数据分组，并一次发送一个组到下一个算子（在本例中为 `Top`）。我们的查询请求每个 `orderdate` 具有最大 `orderid` 的订单。幸运的是，我们为该任务有一个覆盖索引（`idx_unc_od_od_cid_eid`），其键列 (`orderid`, `orderdate`) 和包含的非键列 (`custid`, `empid`)。我将在本章稍后详细介绍包含的非键列。我们讨论的关键点是，`Segment` 算子按 `order` 值的组对数据进行组织，并一次发送一组数据，其中每组的最后一行是组内最大的 `orderid`；因为 `orderid` 是紧随 `orderdate` 之后的第二列。因此，计划不需要对数据进行排序；而是通过对覆盖索引进行有序扫描来收集数据，该索引已经按照 `orderdate` 和 `orderid` 排序。`Top` 算子的任务很简单，即收集最后一行（`TOP 1 descending`），这正是该组所关注的行。`Top` 算子报告的行数为 1490，这是唯一组（`orderdate` 值）的数量，每个组都从算子获取了单行。

由于我们的非聚集索引通过在叶节点级包含查询中提到的所有其他列（`custid`, `empid`）来覆盖查询，因此不需要回表查找数据行；仅通过索引数据即可满足查询。

# 存储引擎对扫描的处理

在继续介绍其他访问方法之前，我将解释存储引擎如何处理关系引擎发出的执行扫描的指令。关系引擎类似于 SQL Server 的大脑；它包含了优化器，优化器负责为查询生成执行计划。存储引擎类似于 SQL Server 的肌肉；它需要执行关系引擎在执行计划中提供的指令，并执行实际的行操作。有时，优化器的指令会给存储引擎留出一些操作空间，此时存储引擎会根据性能和一致性等因素在多个可能的选项中决定最佳的一个。

## 分配顺序扫描与索引顺序扫描

当计划显示 `Table Scan` 算子时，存储引擎只有一个选项：使用分配顺序扫描（allocation order scan）。当计划显示具有 `Ordered: True` 属性的 `Index Scan` 算子（聚集或非聚集）时，存储引擎只能使用索引顺序扫描。

当计划显示 `Ordered: False` 的 `Index Scan` 算子时，关系引擎并不关心行的顺序。在这种情况下，有两种扫描数据的选项：分配顺序扫描和索引顺序扫描。使用哪种取决于存储引擎。遗憾的是，存储引擎的实际选择没有在执行计划（或任何地方）中标示出来。我将解释存储引擎的决策过程，但重要的是，要理解计划所显示的是关系引擎的指令，而不是存储引擎的实际操作。

分配顺序扫描的性能不受索引中逻辑顺序的影响，因为无论如何它都是文件顺序。然而，涉及物理读取的索引顺序扫描的性能会受到碎片的影响——碎片越高，扫描越慢。因此，从性能角度来看，存储引擎认为分配顺序扫描是优选方案。例外是索引非常小（最多 64 页）。在这种情况下，解释 IAM 页的成本相对于其他工作变得显著，存储引擎认为索引顺序扫描更优。除小表外，执行分配顺序扫描被认为是更优的。

然而，性能并不是存储引擎需要考虑的唯一因素；它还需要根据有效的隔离级别考虑对数据一致性的预期。当有多个选项可以执行某个请求时，存储引擎会选择满足一致性要求的最快选项。

在某些情况下，扫描可能会导致行的多次出现，甚至跳过行。分配顺序扫描比索引顺序扫描更容易发生这种行为。我将描述这种现象如何在分配顺序扫描中发生以及在什么情况下发生。我将解释它在索引顺序扫描中是如何发生的。

### 分配顺序扫描

图 2-21 通过三个步骤演示了分配顺序扫描如何返回行的多次出现。

分配顺序扫描：获取多次出现的行。

分配顺序扫描，第一步：
![](img/bdc38aa36f6e2987d913ee5381474711_88_0.png)
输出：

分配顺序扫描，第二步：
![](img/bdc38aa36f6e2987d913ee5381474711_88_0.png)
输出：

分配顺序扫描，第三步：
![](img/bdc38aa36f6e2987d913ee5381474711_88_0.png)
输出：

图 2-21 分配顺序扫描：获取多次出现的行。

在类别方面，存储引擎也选择了分配顺序扫描（allocation order scans），其隔离级别比“未提交读取”（Read Uncommitted）高，且这种扫描在不牺牲读取一致性的情况下（至少在页拆分方面）是安全的。例如，当你通过 `TABLOCK` 运行查询时，存储引擎知道在读取进行期间没有人可以更改数据。因此，使用分配顺序扫描是安全的。当然，这意味着在读取期间，其他会话的尝试将被阻塞。另一个存储引擎认为可以采用分配顺序扫描的例子是索引位于只读文件组或数据库中。总而言之，当索引大小大于 64 页且数据是只读的（由于只读文件组或数据库）时，存储引擎将使用安全类别的顺序扫描。

请记住，逻辑碎片会影响索引顺序扫描的性能，但不会影响分配顺序扫描的性能。根据上述信息，你应该意识到存储引擎利用索引顺序扫描（index order scans）来处理具有 `Ordered: False` 属性的索引扫描（Index Scan）。

下一节将演示不安全和安全的分配顺序扫描。

运行以下代码来创建一个名为 T1 的表：

```sql
SET NOCOUNT ON;
USE tempdb;
GO
-- Create table T1
IF OBJECT_ID(N'dbo.T1', N'U') IS NOT NULL DROP TABLE dbo.T1;
CREATE TABLE dbo.T1
(
    clcl UNIQUEIDENTIFIER NOT NULL DEFAULT(NEWID()),
    filler CHAR(2000) NOT NULL DEFAULT('a')
);
GO
CREATE UNIQUE CLUSTERED INDEX idx_clcl ON dbo.T1(clcl);
```

在 `clcl` 上创建了一个唯一索引，它将由默认表达式 `NEWID()` 填充随机 GUID。用随机 GUID 填充索引键会导致大量的拆分，这又会导致索引中产生高程度的逻辑碎片。

运行以下代码使用无限循环向表中插入行，并在几秒后停止它（假设 5 秒，以允许表包含超过 64 页的数据）：

```sql
SET NOCOUNT ON;
USE tempdb;
TRUNCATE TABLE dbo.T1;
WHILE 1 = 1
    INSERT INTO dbo.T1 DEFAULT VALUES;
```

运行以下代码检查索引的碎片程度：

```sql
SELECT avg_fragmentation_in_percent FROM sys.dm_db_index_physical_stats
(
    DB_ID(N'tempdb'),
    OBJECT_ID(N'dbo.T1'),
    1,
    NULL,
    NULL
);
```

当我在系统上运行此代码时，我得到了超过 99% 的碎片，这显然非常高。如果你需要更多证据来支持链表中页的顺序与其在文件中的顺序不同的事实，可以使用未记录的 `DBCC IND` 命令，它可以提供索引的 B 树布局：

```sql
DBCC IND(N'tempdb', N'dbo.T1', 0);
```

我准备了以下代码，以避免你通过浏览 `DBCC IND` 的输出来试图找出叶节点布局：

```sql
CREATE TABLE #DBCCIND(
    PageID INT,
    PageID INT,
    IAMID INT,
    ObjectID INT,
    IndexID INT,
    Partition BIGINT,
    PartitionID BIGINT,
    iamType VARCHAR(100),
    PageType INT,
    IndexLevel INT,
    NextPageID INT,
    NextPageID INT,
    PrevPageID INT
);
INSERT INTO #DBCCIND
EXEC DBCC IND(N'tempdb', N'dbo.T1', 0);
CREATE CLUSTERED INDEX idx_cl_prevpage ON #DBCCIND(PrevPageID, PageID);
WITH LinkedList AS
(
    SELECT CurLevel.RowNum + 1, CurLevel.PageID
    FROM #DBCCIND AS CurLevel
    JOIN #DBCCIND AS NextLevel ON CurLevel.PrevPageID = NextLevel.PageID
)
SELECT CAST(PageID AS VARCHAR(MAX)) + ' '
    + CAST(PageID AS VARCHAR(MAX)) + ' ' AS text
FROM LinkedList
FOR XML PATH('')), OPTION (MAXRECURSION 0);
DROP TABLE #DBCCIND;
```

代码将 `DBCC IND` 的输出存储在临时表中，然后使用递归查询从头部跟踪链表，最后使用 `FOR XML PATH` 技术将叶节点地址连接成字符串。我在我的系统上得到了以下输出：132098 111372 133098 125591 113756 111898... 在这里观察逻辑碎片很容易。例如，页 132098 指向文件中较早的页 111372。

接下来，运行以下代码查询 T1：

```sql
SELECT SUBSTRING(CAST(clcol AS BINARY(16)), 1, 6) AS segment1, *
FROM dbo.T1;
```

使用 `SUBSTRING` 函数提取最后的 6 个字节以查看行是否按索引返回。此查询的执行计划是一个聚集索引扫描（Clustered Index Scan），顺序为 False。然而，由于环境是只读的且隔离级别是默认，存储引擎使用了索引扫描。在这里是我系统上的输出：

| segment1 | clcol | filler |
|---|---|---|
| 0000ED8A0E6 | 5F75CA42-8786-4176-8BDC-00ED8A0E6 | |
| 000627711D | 7B3D64F2-9197-487E-A354-0026771FD | |
| 00EEAF4130 | 7D4A61D3-8BF3-4837-831C-00EE4130 | |
| 00093E50A08 | 2A70C2C3-5459-4056-90CE-0039E53008 | |
| 0004B9604D2 | 40C1BD2-B8C7-40D9-A5F4-004B960A4D2 | |
| 0005E9B1ED3 | 0EF78B3A-40F1-4097-B138-00E1A2C5D3 | |
| 000670D63977 | B4C951D3-01E7-4745-B573-00670D63977 | |
| 0007B8D21817 | 15F7F2E9-A27E-4795-850F-7B87BD1817 | |
| 0007BC02C1C | 93ED4A5C-3AAD-4686-B4A1-0007BC02C1C | |
| 0007E73BEBF8 | 732E07E2-A267-483A-B2CF-0007E73BF8 | |

再次带有 `NOLOCK` 提示查询表：

```sql
SELECT SUBSTRING(CAST(clcol AS BINARY(16)), 1, 6) AS segment1, *
FROM dbo.T1 WITH (NOLOCK);
```

这次，存储引擎采用了不安全的分配顺序。这是我从这段代码得到的输出：

| segment1 | clcol |
|---|---|
| 0x03D5CA4A3F8AE | 7E2A282E-8712-47F1-A553-03D5CA4F8AE |
| 0x42D6FD0DBD | 003FE4B-180E-4A8D-86E1-C260DB8D3 |
| 0x42D6A3FF2C | 9239BF31-9AA2-47F0-8B50-426DA3FF2C |
| 0x42AE5E69673AD | 2FA0A98B-247E-42C2-A22E-426ES973AD |
| 0x5EEBC295A844 | 374327C-07C2-48BC-A6B5-52EC295A844 |
| 0x97A52864AE1D | 131BDF97-B0F1-488-97A528641D |
| 0x78D967590DBC | 7AA0F5BF-08D1-46B9-78D967590BC |
| 0x78DA17132327 | 7AF0C88F-FC08-4534-842C-78DA1713227 |
| 0x78DACE8159E | 90EBE771-301F-4A6B-A39B-78DACE819E |
| 0x20C225A8A10D | 54B7D0D9-7804-4969-8A7F-20C225A810D |

注意这些行并不是按索引顺序返回的。如果在读取期间发生了拆分，这种读取可能会返回多次。作为分配顺序的一个例子，运行带有 `TABLOCK` 提示的查询：

```sql
SELECT SUBSTRING(CAST(clcol AS BINARY(16)), 1, 6) AS segment1, *
FROM dbo.T1 WITH (TABLOCK);
```
