
| tempdb | sequence - 50 | 6562 | 0.43933868 | 34 | 6177 | 1709 |
| testdb | sequence | 10 | 6562 | 0.43933868 | 48 | 11625 | 7157 |
| testdb | NO CACHE | 6562 | 0.43933868 | 34 | 7036 | 65899 |
| testdb | none | 29688 | 2.75302168 | 32 | 4743 | 511 |
| testdb | identity DFT | 32751 | 1.75932012 | 38 | 6013 | 1270 |
| testdb | identity TF272 | 1002862 | 1.25627928 | 13444 | 103541 | 100598 |
| testdb | sequence | 23801 | 1.41382026 | 1000 | 5254 | 511 |
| testdb | sequence | 32759 | 2.00628615 | 10040 | 10489 | 6746 |
| testdb | sequence - 50 | 222863 | 15.85624122 | 290002 | 68390 | 63647 |
| testdb | sequence | 1022872 | 73.8738406 | 100004 | 292110 | 287367 |
| testdb | sequence NO CACHE | 1003130 | 27.8267402 | 1000050 | 2812090 | 280734 |

结果中有一些有趣的现象可以观察并推导出最佳实践。观察发现，对于标识和序列，目标对象与缓存大小和日志记录之间没有关系。因为 `tempdb` 中的缓存相关写入不会持久化。所需的日志记录数、总大小和日志刷数的最小数值是因为，如果需要执行回滚，恢复过程也会撤销插入操作。持续时间随缓存大小的减小而增加，并不是由于日志记录的原因。你可以看到，特别是在缓存较小的情况下，`tempdb` 的性能明显优于 `testdb`。

另一个有趣的观察是，在用户数据库 (`testdb`) 中，具有相同的缓存值，标识和序列的日志记录数和总大小是相同的，但刷新次数和实际性能却大不同。以下是性能结果的一个子集，方便你观察：

| 数据库对象 | 缓存 | 记录数 | 大小(MB) | 刷新次数 | 持续时间 | 标准时长 |
|---|---|---|---|---|---|---|
| tempdb | identity DFT | 6563 | 0.4395593 | 13 | 5996 | 1501 |
| tempdb | sequence | 1000 | 6562 | 0.43933868 | 34 | 4889 | 421 |
| testdb | identity DFT | 32751 | 2.06031689 | 38 | 6013 | 1270 |
| testdb | sequence | 1000 | 32759 | 2.06822615 | 10000 | 10489 | 5746 |
| tempdb | identity TF272 | 6563 | 0.43945693 | 9 | 93933 | 89465 |
| testdb | sequence NO CACHE | 6562 | 0.43933868 | 34 | 70367 | 65899 |

你还可以在图 6-2 中看到某些缓存大小下标识和序列的运行时间对比。

![](img/bdc38aa3fe2987d913ee5381474711_417_0.png)

**图 6-2** 序列和标识性能测试。

很清楚为什么在相同缓存大小下，标识和序列的日志记录数及其总大小应该是相似的——毕竟，它们在内部都是在同一个对象上实现的。那么，为什么刷新次数会有差异呢？

这与标识是特定于表的而序列不是有关。所以你向带有标识列的表中插入了一个新行。恰好这次插入触发了缓存相关的磁盘写入。日志记录被写入日志缓冲区，但假设缓冲区尚未填满。然后在日志缓冲区刷新之前发生了断电。如果恢复的标识值是较早的值也没关系，因为恢复过程也会撤销插入操作。所以重用由未提交的插入所生成的旧标识值并不是问题。因此，SQL Server 不需要为每次标识缓存相关的写入刷新日志缓冲区。

对于序列对象，情况则不同。应用程序可以请求一个序列值并将其用于任何目的——不一定将其存储在数据库的行中。如果 SQL Server 崩溃，然后应用程序请求新值，什么能保证它不会产生旧值？为了保证这一点，SQL Server 会为每次序列缓存相关的写入刷新日志缓冲区。

## 总结标识与序列的比较

本章关于序列的部分将序列对象与标识列属性进行了对比分析。文中讨论了许多方面。为了方便参考，这些信息以摘要的形式在表 6-2 中提供。

### 表 6-2 标识与序列对比

| 特性 | 标识 | 序列 |
|---|---|---|
| 表无关 | 否 | 是 |
| 可以与现有列关联/取消关联 | 否 | 是 |
| 可用于允许空列 | 否 | 是 |
| 使用前获取值 | 否 | 是 |
| 用于 SELECT | 否 * `IDENTITY()` 函数可以用于 INTO | 是 |
| 控制顺序 | 不用于 SELECT INTO 是在 INSERT SELECT 中 | 是 |
| 用于 UPDATE | 否 | 是 |
| 定义最小值和最大值 | 否 | 是 |
| 可以循环 | 否 | 是 |
| 可以更改当前值 | 是 | 是 |
| 可以更改增量 | 否 | 是 |
| 支持用户定义的缓存值 | 否，可以通过 `TF272` 禁用缓存 | 是 |
| 默认缓存值（as于 SQL Server 2014 RTM 和 SQL Server 2012 SP2） | 取决于类型（TINYINT - 10, SMALLINT - 100, INT - 1000, BIGINT 和 NUMERIC - 10000） | 50 |
| 受回滚影响 | 否 | 是 |
| 写入磁盘时需要刷新日志 | 否 | 是 |
| 获取值的范围 | 否 | 是 |

## 删除数据

本节涵盖了数据删除的两个方面：`TRUNCATE TABLE` 语句和删除重复项。你可以在第 5 章中找到更多关于数据删除的内容。

## TRUNCATE TABLE

`TRUNCATE TABLE` 语句是一种高效的语句，它会删除表中的所有行，并在存在标识（identity）属性时重置它，但保留表定义。

该语句具有基本语法。例如，如果你有一个名为 `T1` 的表，你可以通过以下方式对其进行截断：

```sql
TRUNCATE TABLE dbo.T1;
```

无论数据库恢复模型如何，`TRUNCATE TABLE` 语句涉及的日志都远少于 `DELETE` 语句；因此，它的速度要快得多。前者只需要记录哪些区（extents）或页被释放，以支持回滚和向前恢复能力。后者则需要记录每一个被删除的行。

由于性能上的巨大差异，通常建议你使用 `TRUNCATE TABLE` 语句而不是 `DELETE` 语句。但你应该注意性能之外的几点区别。

`TRUNCATE TABLE` 语句需要更高级别的权限。你至少需要目标表的 `ALTER` 权限。如果你不想向执行用户授予权限，可以将该语句包含在用 `EXECUTE AS` 子句定义的存储过程中，并确保被模拟的用户具有相应的权限。

如前所述，与 `DELETE` 语句不同，`TRUNCATE TABLE` 语句在存在标识属性时会重置它。如果你想清空表但保持当前标识值不变，你需要自己处理。你可以通过以下步骤实现：

1. 开启事务。
2. 锁定表。
3. 在变量中捕获当前标识值加 1。
4. 执行 `TRUNCATE TABLE` 语句。
5. 使用存储在变量中的值重新设置种子标识属性。
6. 提交事务。

我将使用以下示例数据来演示此解决方案：

```sql
IF OBJECT_ID(N'dbo.T1', N'U') IS NOT NULL DROP TABLE dbo.T1;
GO
```

```sql
CREATE TABLE dbo.T1
(
  keycol INT NOT NULL IDENTITY,
  datacol VARCHAR(10) NOT NULL
);
```

```sql
INSERT INTO dbo.T1 (keycol, datacol) VALUES ('A'),('B'),('C');
```

```sql
SELECT keycol, datacol FROM dbo.T1;
```

这里是最后一次查询的输出，显示了表 `T1` 的内容：

| keycol | datacol |
|---|---|
| 1 | A |
| 2 | B |
| 3 | C |

当前标识值为 3。

以下代码截断表并手动将标识属性重新置为当前值加 1：

```sql
IF EXISTS(SELECT * FROM dbo.T1)
BEGIN
BEGIN TRAN
DECLARE @tmp INT = (SELECT TOP (1) keycol FROM dbo.T1 WITH (LOCKX)) -- lock
DECLARE @reseedval AS INT = IDENTITY_CURRENT(N'dbo.T1') + 1; -- reseed
TRUNCATE TABLE dbo.T1; -- truncate
DBCC CHECK_IDENT(N'dbo.T1', RESEED, @reseedval); -- reseed
PRINT 'Identity reseeded to ' + CAST(@reseedval AS VARCHAR(10)) + '.';
COMMIT TRAN
END
ELSE
PRINT 'Table is empty, no need to truncate.';
```

此代码生成了以下输出：

Identity reseeded to 4.

现在向表中添加新行并进行查询：

```sql
INSERT INTO dbo.T1(datacol) VALUES('X'),('Y'),('Z');
SELECT keycol, datacol FROM dbo.T1;
```

你将得到以下输出，显示生成的第一个标识值为 4：

```
keycol      datacol
4           X
5           Y
6           Z
```

如果存在指向该表的外键，则无法截断表，即使引用表是空的。你必须在截断表之前删除外键，并在完成后重新创建它们。

同样，如果存在基于该表的索引视图（indexed views），也无法截断表。与外键类似，一种方案是在截断表之前删除索引视图，并在完成后重新创建它们。

另一个方案是依靠分区切换（partitioning switching）。通过分区切换，你不需要删除并重新创建索引视图。当存在基于表的索引视图时，SQL Server 支持分区切换，只要索引视图的分区与表分区对齐。如果你没有显式对表和索引视图进行分区，根据定义你就满足了这一要求。解决方案涉及以下步骤：

1. 创建一个与源结构相同的临时表（staging table）。
2. 将源表切换到临时表。
3. 删除临时表。

例如，10,000 行——使用一个完全记录日志的单个 `DELETE` 语句是完全可以的。在这种情况下，你可以使用以下解决方案来实现该任务：

```sql
WITH C AS
SELECT *,
ROW_NUMBER() OVER(PARTITION BY orderid ORDER BY (SELECT NULL)) AS n
FROM dbo.Orders
DELETE FROM C
WHERE n > 1;
```

内部查询查询了行数（称之为 `n`），在我们的案例中，它是按逻辑键 `orderid` 进行分区的。只要每个唯一的订单 ID 只保留一个出现次数，那么保留哪一行其实并不重要，此时可以像我们的查询那样，在窗口 order 子句中使用任意排序——即 `ORDER BY (SELECT NULL)`。如果具有相同 order ID 值的不同行彼此是不同的，并且你有决定优先选择哪一行的属性，请务必在窗口 order 子句中指定这些属性。列 `n` 代表重复的序号。假设你有三行 order ID 为 10248 的数据；你将获得不同的值 1、2 和 3。该代码基于计算 `n` 的查询定义了一个 CTE。外部查询通过 CTE 删除了 `n` 大于 1 的行。底层表 `Orders` 受 `DELETE` 语句影响的表。

如果需要删除的行百分比很小，但行数仍然很大——例如 5,000,000 行——之前的解决方案可能并不理想。它可能会导致日志显著膨胀，并可能导致锁升级。为了避免这种情况，你可以像第 5 章“分块修改”节描述的那样，将大删除拆分为分块。以下是该方法的实现：

```sql
WHILE 1 = 1
BEGIN
WITH C AS
SELECT *,
ROW_NUMBER() OVER(PARTITION BY orderid ORDER BY (SELECT NULL)) AS n
FROM dbo.Orders
DELETE TOP (3000) FROM C
WHERE n > 1;
IF @@ROWCOUNT < 3000 BREAK;
END
```

如果需要删除的行百分比和行数都很大——例如 25,000,000 行，第三种解决方案可能是最优的。可以使用如 `SELECT INTO` 这样的最小日志操作将 `n` 等于 1 的行复制到临时表中。复制完成后，删除原始表，将临时表重命名为原始表名，然后在其上创建所需的任何内容（约束、索引、触发器、权限）。以下是该方法的代码：

## 第 6 章 数据修改

```sql
-- 将唯一行复制到临时表
WITH C AS
(
SELECT *,
ROW_NUMBER() OVER(PARTITION BY orderid ORDER BY (SELECT NULL)) AS n
FROM dbo.Orders
)
SELECT orderid, custid, empid, orderdate, requireddate, shippedate, shipper,
freight, shipname, shipaddress, shipcity, shipregion, shippostcode, shipcountry
INTO dbo.Orders_Stage
FROM C
WHERE n = 1;
```

```sql
-- 删除原始表
DROP TABLE dbo.Orders;
```

```sql
-- 在 Orders 上创建约束、索引、触发器和权限
ALTER TABLE dbo.Orders ADD CONSTRAINT PK_Orders PRIMARY KEY(orderid);
```

## 更新数据

本节介绍了 T-SQL 中的两种特殊的更新能力：通过表表达式更新数据以及使用变量更新数据。

作为更新数据章节以及后续合并数据章节的示例数据，我将使用 `Customers` 和 `CustomersStage` 表，你可以使用以下代码在 `tempdb` 中创建并填充它们：

```sql
USE tempdb;

IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL DROP TABLE dbo.Customers;
```

```sql
CREATE TABLE dbo.Customers
(
custid INT NOT NULL,
companyname VARCHAR(25) NOT NULL,
phone VARCHAR(20) NOT NULL,
address VARCHAR(50) NOT NULL,
CONSTRAINT PK_Customers PRIMARY KEY(custid)
);
GO
```

```sql
INSERT INTO dbo.Customers(custid, companyname, phone, address)
VALUES(1, 'cust 1', '(111) 111-1111', 'address 1'),
(2, 'cust 2', '(222) 222-2222', 'address 2'),
(3, 'cust 3', '(333) 333-3333', 'address 3'),
(4, 'cust 4', '(444) 444-4444', 'address 4'),
(5, 'cust 5', '(555) 555-5555', 'address 5');
GO
```

```sql
IF OBJECT_ID('dbo.CustomersStage', 'U') IS NOT NULL DROP TABLE dbo.CustomersStage;
```

```sql
CREATE TABLE dbo.CustomersStage
(
  custid INT NOT NULL,
  companyname VARCHAR(25) NOT NULL,
  phone VARCHAR(20) NULL,
  address VARCHAR(50) NOT NULL,
  CONSTRAINT PK_CustomersStage PRIMARY KEY(custid)
)
GO
```

```sql
INSERT INTO dbo.CustomersStage(custid, companyname, address)
VALUES(2, 'AAAAA', '(222) 222-2222'),
(3, 'cust 3', '(333) 333-3333'),
(4, 'cust 4', '(444) 444-4444'),
(5, 'cust 5', '(555) 555-5555');
```

### 使用表表达式更新

假设你需要根据另一个表中的值更新一个表中的列。这通常通过 `UPDATE` 语句中的连接来实现。
