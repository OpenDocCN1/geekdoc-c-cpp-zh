
![](img/bdc38aa36f6e2987d913ee5381474711_261_0.png)

图 3-18 茂密计划。

观察到计划中实现了预期的茂密布局。

## 半连接与反半连接

通常情况下，连接会匹配两个表中的行并返回双方的元素。半连接的特点在于你只返回其中一侧的元素。你返回元素的一侧决定了它是左半连接还是右半连接。

例如，考虑请求返回下过订单的客户 ID 和公司名称。只要在 `Orders` 表中找到匹配的行，你就仅从 `Customers` 表中返回信息。将 `Customers` 视为左表，该操作就是半连接。实现此任务有很多方法。其中一种是使用内连接并应用 `DISTINCT` 子句来删除重复的客户，如下：

```sql
SELECT DISTINCT C.custid, C.companyname
FROM Sales.Customers AS C
INNER JOIN Sales.Orders AS O
ON O.custid = C.custid;
```

另一种是使用 `EXISTS` 谓词，如下：

```sql
SELECT custid, companyname
FROM Sales.Customers AS C
WHERE EXISTS (
    SELECT *
    FROM Sales.Orders AS O
    WHERE O.custid = C.custid
);
```

这两个查询会获得相同的计划。当然，还有其他方法可以实现该任务。

反半连接是指如果在相关表中无法找到匹配的行，则从其中一个表中返回元素。同样，取决于你返回来自左表还是右表的信息，该连接是左反半连接或右反半连接。例如，返回未下订单的客户的请求可以通过左反半连接操作完成。

实现这种反半连接有许多经典方法。一种是在 `Customers` 和 `Orders` 之间使用左外连接并仅过滤外部行，如下：

```sql
SELECT custid, C.companyname
FROM Sales.Customers AS C
LEFT OUTER JOIN Sales.Orders AS O
ON O.custid = C.custid
WHERE O.orderid IS NULL;
```

另一种是使用 `NOT EXISTS` 谓词，如：

```sql
SELECT custid, companyname
FROM Sales.Customers AS C
WHERE NOT EXISTS (
    SELECT *
    FROM Sales.Orders AS O
    WHERE O.custid = C.custid
);
```

奇怪的是，目前优化器似乎没有检测到外连接为应用反半连接的逻辑，但在使用 `NOT EXISTS` 解决方案时可以。这可以在图 3-19 所示的这些查询执行计划中看到。

查询 1：查询成本（相对于批处理）：52%
```sql
SELECT custid, C.companyname
FROM Sales.Customers AS C
LEFT OUTER JOIN Sales.Orders AS O
ON O.custid = C.custid
```
![](img/bdc38aa36f6e2987d913ee5381474711_262_0.png)

查询 2：查询成本（相对于批处理）：48%
```sql
SELECT custid, companyname
FROM Sales.Customers AS C
WHERE NOT EXISTS (
    SELECT *
    FROM Sales.Orders AS O
    WHERE O.custid = C.custid
)
```
![](img/bdc38aa36f6e2987d913ee5381474711_262_1.png)

**图 3-19** 反半连接解决方案的计划。

当然，还有许多实现反半连接的其他方法。我展示的是两种经典方法。

## 连接算法

连接算法是 SQL Server 用于处理连接的物理连接策略。SQL Server 支持三种连接算法：嵌套循环、合并和哈希。嵌套循环是这三种算法中最古老的，也是当其他算法无法使用时的回退方案。例如，交叉连接只能通过嵌套循环进行处理。合并和哈希要求连接是等值连接，或者更准确地说，至少有一个基于等值运算符的连接谓词。

在图形化查询计划中，每个算法的连接操作符都有不同的图标。此外，`Physical Operation` 属性标识连接算法（`Nested Loops`、`Hash Match`、`Merge Join`），而 `Logical Operation` 属性标识逻辑连接类型（`Inner Join`、`Left Outer Join`、`Left Anti Semi Join` 等）。此外，物理算法名称出现在操作符正下方，逻辑连接类型出现在算法名称的括号内。

接下来的章节将描述各个连接算法、它们可能高效的情况，以及支持它们的索引指南。

## 嵌套循环

嵌套循环算法非常直观。它只执行一次外部（顶部）输入，并使用循环为外部循环的每一行执行一次内部（底部）输入以识别匹配项。

当外部输入较小且内部输入具有基于键列表（基于连接列以及任何额外的列，如果相关的话）的索引时，嵌套循环性能良好。索引是否必须是覆盖索引取决于你获取到多少匹配项。如果总匹配数很少，几次查找的开销并不大，索引不需要是覆盖索引。如果匹配数量很大，查找将变得昂贵，此时考虑通过使索引成为覆盖索引来避免查找变得至关重要。

例如，考虑以下查询：

```sql
SELECT C.custid, O.orderid, O.empid, O.shippid, O.orderdate
FROM dbo.Customers AS C
INNER JOIN dbo.Orders AS O
ON O.custid = C.custid
```

（注：此处原文后续部分存在逻辑混乱和重复，翻译已根据语意进行平滑处理）

在最坏情况下，表会被全扫描。然而，如果你想避免对 `Customers` 表进行全扫描，可以在 `custname` 上准备一个索引并包含 `custid` 列以覆盖。考虑在循环的单次迭代中涉及的工作。由于你有一个等值谓词和一个范围谓词，在这里创建一个基于 `custid` 和 `orderdate` 的理想索引是非常简单的，并包含剩余列（`orderid`、`empid`、`shipper`）。记住，当你同时拥有等值谓词和范围谓词时，需要先等值列定义键列表。这样，匹配行将连续地出现在索引中。运行以下代码为你的查询创建优化索引：

```sql
CREATE INDEX idx_nc_id ON dbo.Customers(custname) INCLUDE (custid);
CREATE INDEX idx_nc_cid_od_oid ON dbo.Orders(custid, orderdate) INCLUDE(orderid, empid, shipper);
```

现在运行查询并检查图 20 所示的查询计划。

![](img/bdc38aa36f6e2987d913ee5381474711_264_0.png)

**图 20** 使用嵌套循环算法的计划。

如你所示，优化器选择了使用较小表 `Customers` 作为外部输入、较大表作为内部输入的嵌套循环算法。计划在 `Customers` 覆盖索引上执行查找和范围扫描以检索匹配的客户（有 1 个）。然后，通过循环在 `Orders` 索引上执行查找和范围扫描以检索当前客户的订单（总共 3 个订单）。

接下来，我将讨论查询的不同更改对优化的影响。正如前面提到的，如果总匹配数很少，内部表索引是覆盖索引并不是至关重要的。你可以通过在查询的 `SELECT` 列表中添加 `O.filler` 来测试这种情况。计划仍将使用嵌套循环算法，但由于该列不是 `index_nc_cid_od_oid` 的一部分，它将添加键查找。在测试时，应用下一个更改之前从查询中移除 `O.filler` 列。

从外部输出返回行时，当优化器估计将返回几十行时，通常会应用预取。当前查询的计划不涉及预取，因为优化器估计从 `Customers` 只返回几行。如果你将 `Customers` 的查询过滤器从 `C.custname LIKE 'Cust_1000'` 更改为 `C.custname LIKE 'Cust_0%'`，它将使用预取。应用更改后，你会发现嵌套循环操作符有一个属性 `WithUnorderedPrefetch` 被设置为 `True`。它是无序预取的原因是不涉及按客户 ID 返回行。如果你在查询中添加 `ORDER BY`，优化器将更改为 `OrderedPrefetch`。完成后，在应用下一个更改之前确保还原原始查询。

我提到过当外部输入较小时，嵌套循环操作符很有用。将 `Customers` 的过滤器更改为 `C.custname LIKE 'Cust_10%'`。现在从 `Customers` 的估计匹配数从几个增加到数千，优化器将其连接算法的选择改为哈希。

当计划是并行的但输出只有几行时，优化器可以使用一种有趣的技巧。在这种情况下，如果没有优化器的干预，工作可能会不均匀地分配到不同的线程。因此，当优化器检测到只有几行时，它会在从外部输入获取行后添加 `Redistribute Streams` 操作符。该操作符会在线程之间更均匀地重新分配行。

## 合并

合并算法要求两个输入都按连接列排序。它像拉链一样合并两者。如果连接是一对多的（这在大多数查询中很可能），则每个输入只通过一次。如果连接类型是多对多的，一个输入被扫描，另一个输入则回溯。

通常情况下，优化器有两种方法获取排序输入。如果数据已经在索引中排序，优化器可以使用索引扫描。另一种方法是在计划中添加显式的排序操作，但这样会有与排序相关的成本。

考虑以下查询作为从索引获取排序数据的示例：

```sql
SELECT C.custid, C.custname, O.orderid, O.empid, O.shipper, O.orderdate
FROM dbo.Customers AS C
INNER JOIN dbo.Orders AS O
ON O.custid = C.custid;
```

`Customers` 表上的 `PK_Customers` 索引是定义在 `custid` 键上的聚集索引。因此，`Customers` 的数据被索引覆盖，并且类似于合并连接算法。

你为“嵌套循环”部分示例在 `Orders` 表创建的非聚集索引 `idx_nc_cid_oid_i_eid_sid` 对于合并连接来说非常高效。它根据 `custid` 引导键对数据进行了排序，并且涵盖了查询中来自 `Orders` 的元素。这些条件对于合并连接算法是最优的；优化器使用了这种策略，如图 3-21 所示的查询计划。

![](img/bdc38aa36f6e2987d913ee5381474711_266_0.png)

**图 3-21** 使用合并连接算法的计划。

作为一个涉及显式排序的合并连接示例，考虑以下查询：

```sql
SELECT C.custid, C.custname, O.orderdate, O.empid, O.shpperid, O.orderdate
FROM dbo.Customers AS C
INNER JOIN dbo.Orders AS O
ON O.custid = C.custid
WHERE O.orderdate > '20140101'
AND O.orderdate < '20140102';
```

数据可以从 `Customers` 表的聚集索引按 `custid` 排序获取。然而，由于在 `orderdate` 上有额外的范围过滤，无法创建一个主要按 `orderdate` 排序的索引来支持过滤，同时又用 `custid` 来支持合并连接。尽管如此，日期过滤具有高度选择性——只有几百行符合条件。此外，`Orders` 上的聚集索引是以 `orderdate` 定义为键的。因此，优化器使用它进行查找和范围扫描以获取符合订单，然后通过显式排序操作按 `custid` 对行进行排序。由于行数较少，排序的成本非常低。我们查询的计划实施了这一策略，如图 3-22 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_266_1.png)

**图 3-22** 使用排序算符和合并算法的计划。

观察与排序操作相关的较小成本。

注意，这种计划对导致 `Sort` 算符活动的基数估计不准确性非常敏感。当估计值是较少行但实际是大量行时，情况尤为如此，因为排序的扩展性并不好。首先，更准确的估计可能会导致优化器使用完全不同的连接算法。其次，低估值可能导致排序活动内存不足，从而导致使用 `tempdb`。你需要关注此类问题，如果你发现了此类问题，请尝试想办法帮助优化器得出更准确的估计。

## 哈希

哈希算法涉及基于输入之一（通常是较小的那一个）创建一个哈希表。优选较小的一侧作为输入的原因是它的内存占用通常较小。如果哈希表能够置于内存中，它就是理想的。如果不能，哈希表可以被分区，分区在内存和外部内存之间的交换会降低算法的效率。输入项根据哈希函数排列在哈希桶中。为了说明，假设连接列是一个整数，优化器选择 `modulo 50` 作为哈希函数。将创建多达 50 个哈希桶，所有哈希函数产生相同结果的项将组织在同一个桶的链表中。然后对另一个输入（称为探测输入）进行探测，将哈希函数应用于连接值，并根据结果，算法扫描哈希桶以寻找匹配项。

哈希算法在数据仓库查询中表现出色，这类查询往往涉及事实表中的大量数据和远小的维度表。它倾向于随着此类查询扩展，从并行处理中极大获益。注意，哈希表需要内存授予，且该算法对基数估计的不准确性敏感。如果内存授予不足，哈希表将溢出到 `tempdb`，导致处理效率降低。当使用列存储索引时，哈希算法可以使用第 2 章描述的批处理执行。在 SQL Server 2012 中，只有使用哈希算法的内连接可以使用批处理执行。此外，如果算符溢出到 `tempdb`，执行将切换到行模式。在 SQL Server 2014 中，使用哈希算法的外连接可以使用批处理执行，因此也会溢出到 `tempdb`。

除了经典的数据仓库查询外，还有另一种优化器选择哈希算法的有趣情况——当没有良好的索引来支持其他算法时。如果你仔细考虑，哈希表是 B-Tree 的替代结构。当没有良好的索引时，通常创建一个哈希表并在对 B-Tree 执行相同操作之前使用它会更有效。作为一个示例，运行以下代码以删除你之前创建的用于支持之前的两个索引：

```sql
DROP INDEX idx_nc_i_cid ON dbo.Customers;
DROP INDEX idx_nc_cid_oid_eid_sid ON dbo.Orders;
```

然后运行你之前在“嵌套循环”部分运行的相同查询：

```sql
SELECT C.custid, C.custname, O.orderid, O.empid, O.shipperid, O.orderdate
FROM dbo.Customers AS C
INNER JOIN dbo.Orders AS O
ON C.custid = C.custid
WHERE C.custname LIKE 'Cust%'
AND O.orderdate > '20140101'
AND O.orderdate < '20140102';
```

这一次，由于缺乏支持其他算法的高效索引，优化器选择了哈希算法。正如你在图 3-23 中所示，该查询的计划如下。

![](img/bdc38aa36f6e2987d913ee5381474711_266_0.png)

**图 3-23** 使用哈希连接的计划。

## 强制连接

如果你怀疑优化器选择了不优的连接算法，可以尝试以下几种方法来强制连接。一种方法是在 `JOIN` 关键字之前使用提示，例如 `LOOP`、`MERGE` 或 `HASH`。这里有一个强制使用嵌套循环的示例：

```sql
SELECT C.custid, C.custname, O.orderid, O.empid, O.shipperid, O.orderdate
FROM dbo.Customers AS C
INNER LOOP JOIN dbo.Orders AS O
ON O.custid = C.custid;
```

注意，使用这种方法，由于缺乏支持高效的索引，优化器选择了哈希表。另一种方法是使用 `OPTION` 子句中的提示。例如，假设你希望防止优化器选择算法，你可以这样做：

```sql
SELECT C.custid, C.custname, O.orderid, O.empid, O.shipperid, O.orderdate
FROM dbo.Customers AS C
INNER JOIN dbo.Orders AS O
ON O.custid = C.custid
OPTION(LOOP JOIN, HASH JOIN);
```

尽管如此，使用这种方法，查询中的所有连接都会受到影响。我不知道还有其他形式的提示可以指定算法。此外，与连接提示不同，查询提示不会影响连接顺序。如果你想强制连接顺序，你需要添加 `FORCE ORDER` 提示。记住关于性能提示的通常警告。此类提示作为性能故障排除工具非常方便；但在生产环境中使用它们消除了优化随环境变化变化的动态特性。如果你发现自己在生产代码中使用此类提示来解决问题，你应该将其视为临时解决方案。当你有时间时，可以深入研究问题并找到帮助优化器做出更优选择的方法。

## 分离元素

分离元素是一个经典的 T-SQL 挑战。它涉及一个名为 `Arrays` 的表，其中 `arr` 列包含分隔的值列表。运行以下代码创建 `Arrays` 表并填充示例数据：
