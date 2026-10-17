
在引用修改行中的列时，需要使用 `inserted` 或 `deleted` 关键字作为前缀。在 `INSERT` 语句中，你通常引用 `inserted`，在 `DELETE` 语句中你引用 `deleted`。在 `UPDATE` 和 `MERGE` 语句中，你可能想引用两者以获取更新行的新旧状态。

`OUTPUT` 子句的妙之处在于它是为 `SELECT` 子句设计的。你不局限于直接引用列；相反，你可以对结果列进行计算、函数操作和别名。

在接下来的章节中，我将提供在不同修改语句中使用 `OUTPUT` 子句的实际示例。

## 插入标识列的示例

假设你正在对一个标识列（identity column）进行多行插入，并需要获取新生成的标识值以供后续使用。SQL Server `SCOPE_IDENTITY` 函数来获取当前会话中生成的最后一个标识值，但它没有提供捕获多个生成的标识值的工具。解决方案是使用 `OUTPUT` 子句。

为了演示这一点，首先运行以下代码，创建一个带有标识列的表 `T1`：

```sql
USE tempdb;
IF OBJECT_ID(N'dbo.T1', N'U') IS NOT NULL DROP TABLE dbo.T1;
```

```sql
CREATE TABLE dbo.T1
(
  keycol INT NOT NULL IDENTITY(1, 1) CONSTRAINT PK_T1 PRIMARY KEY,
  datacol VARCHAR(40) NOT NULL
);
```

以下 `INSERT` 语句从 `TSQLV3.HR.Employees` 表复制五行到 `T1` 表，从而导致标识值的生成：

```sql
INSERT INTO dbo.T1(datacol)
OUTPUT inserted.$identity, inserted.datacol
SELECT lastname
FROM TSQLV3.HR.Employees
WHERE country = N'USA';
```

使用 `OUTPUT` 子句，该语句返回了新生成的标识值以及来自插入行的其他信息。注意这里使用了通用格式 `$identity` 对标识列的引用。SQL Server 支持这种通用形式，是因为每个表只允许一个标识列。当然，如果你愿意，可以直接引用插入的原始列名 `inserted.keycol`。

此代码生成了以下输出：

```
keycol datacol
----------
1 Davis
2 Funk
3 Lew
4 Peled
5 Cameron
```

要将输出行重定向到表变量以便后续使用，请添加 `INTO` 子句。为了演示这一点，首先清空 `T1` 表：

```sql
TRUNCATE TABLE dbo.T1;
```

然后，在之前的示例中添加表变量的声明和 `INTO` 子句，如下所示：

```sql
DECLARE @NewRows TABLE(keycol INT, datacol VARCHAR(40));
```

```sql
INSERT INTO dbo.T1(datacol)
OUTPUT inserted.identity, inserted.$datacol
INTO @NewRows(keycol, datacol)
SELECT keycol, lastname
FROM TSQLV3.HR.Employees
WHERE country = 'USA';
```

```sql
SELECT keycol, datacol FROM @NewRows;
```

你将得到以下显示表变量内容的输出：

| keycol | datacol |
| ------ | ------ |
| 1 | Davis |
| 2 | Funk |
| 3 | Lew |
| 4 | Peled |
| 5 | Cameron |

## 归档删除数据的示例

为了更好地理解 `DELETE` 语句中的 `OUTPUT` 子句，请考虑一个涉及删除的任务，并要求归档所删除的行。可以使用 `DELETE` 语句中的 `OUTPUT` 子句来实现删除。

为了演示这一点，首先运行以下代码，在 `tempdb` 中创建一个带有示例数据的 `Orders` 表，并在名为 `Archive` 的数据库中创建一个 `Orders` 表以吸收归档的订单：

```sql
IF DB_ID('Archive') IS NULL CREATE DATABASE Archive;
GO
```

```sql
USE Archive;
IF OBJECT_ID(N'dbo.Orders', N'U') IS NOT NULL DROP TABLE dbo.Orders;
```

```sql
SELECT ISNULL(orderid,0) AS orderid, orderdate, empid, custid
INTO dbo.Orders
FROM TSQLV3.Sales.Orders WHERE 1 = 2;
```

```sql
ALTER TABLE dbo.Orders ADD CONSTRAINT PK_Orders PRIMARY KEY(orderid);
```

```sql
USE tempdb;
IF OBJECT_ID(N'dbo.Orders', N'U') IS NOT NULL DROP TABLE dbo.Orders;
```

```sql
ALTER TABLE dbo.Orders ADD CONSTRAINT PK_Orders PRIMARY KEY(orderid);
```

```sql
-- 删除前
SELECT orderid, orderdate, empid, custid FROM dbo.Orders;
SELECT orderid, orderdate, empid, custid FROM Archive.dbo.Orders;
```

最后两个查询显示了删除之前活动和归档的 `Orders` 表的内容。

假设你需要删除 `tempdb` 中活动 `Orders` 表中 2014 年之前的订单，并将删除的订单归档到 `Archive` 数据库的 `Orders` 表中。你可以如下使用 `OUTPUT` 子句完成操作：

```sql
DELETE FROM dbo.Orders
OUTPUT
deleted.orderid,
deleted.orderdate,
deleted.empid,
deleted.custid
INTO Archive.dbo.Orders
WHERE orderdate < '20141001';
```

如果需要删除的行数很多，你可以应用早期演示的分批修改技术，这次添加了 `OUTPUT INTO` 子句，如下所示：

```sql
WHILE 1 = 1
BEGIN
DELETE TOP (3000) FROM dbo.Orders
OUTPUT
deleted.orderid,
deleted.orderdate,
deleted.empid,
deleted.custid
INTO Archive.dbo.Orders
WHERE orderdate < '20141001';

IF @@ROWCOUNT < 3000 BREAK;
END;
```

运行以下查询以显示删除后活动和归档的 `Orders` 表的内容：

```sql
SELECT orderid, orderdate, empid, custid FROM dbo.Orders;
SELECT orderid, orderdate, empid, custid FROM Archive.dbo.Orders;
```

## 使用 MERGE 语句的示例

使用 `MERGE` 语句，你面临着其他语句不具备的复杂性。如何知道哪个操作影响了哪些行？对于此，SQL Server 为你提供了 `$action`，它返回字符串 'INSERT'、'UPDATE' 或 'DELETE'。为了演示这一点，首先通过运行以下代码重新填充 `CustomersStage` 表：

```sql
TRUNCATE TABLE Customers;
```

```sql
INSERT INTO Customers (custid, name, phone, address)
VALUES (1, 'Alice', '555-0101', 'USA'),
(2, 'Bob', '555-0102', 'USA'),
(3, 'Charlie', '555-0103', 'UK'),
(4, 'David', '555-0104', 'USA'),
(5, 'Eve', '555-0105', 'Canada');
```

现在带有操作的 `OUTPUT` 子句使用 `MERGE` 语句：

```sql
MERGE INTO Customers AS TGT
USING CustomersStage AS SRC
ON TGT.custid = SRC.custid
WHEN MATCHED
UPDATE SET
  TGT.name = SRC.name,
  TGT.phone = SRC.phone,
  TGT.address = SRC.address
WHEN NOT MATCHED
INSERT (custid, name, phone, address)
VALUES (SRC.custid, SRC.name, SRC.phone, SRC.address)
OUTPUT $action AS action, deleted.custid AS del_custid, inserted.custid AS ins_custid;
```

此语句生成以下内容：

| action | del_custid | ins_custid |
|--------|------------|------------|
| UPDATE | 1          |            |
| UPDATE | 2          |            |
| INSERT |            | 3          |
| UPDATE | 4          |            |
| INSERT |            | 5          |

## 可组合 DML (Composable DML)

假设你需要修改某些表中的行，并将修改后的输出信息写入某些目标表。通常情况下，你只需使用 `OUTPUT INTO` 子句。但你只需要捕捉输出行的子集——而不是所有行。在一个示例中，假设你想从 `tempdb` 数据库的 `Orders` 表中删除所有 2014 年之前创建的订单行。你需要将删除的行归档到 `Archive` 数据库的 `Orders` 表，但仅针对客户 11 和 42。你不需要将整组输出行写入临时表，然后仅从临时表中复制感兴趣的子集行，这可能会导致大量不必要的工作。

T-SQL 支持在 `INSERT` 语句中嵌套带有 `OUTPUT` 子句的 DML 语句——这一特性在某些平台上被称为可组合 DML。通过此功能，你可以在无需中间阶段的情况下完成上述删除任务，如下所示：

```sql
INSERT INTO Archive.dbo.Orders (orderid, orderdate, empid, custid)
SELECT orderid, orderdate, empid, custid
FROM ( DELETE FROM dbo.Orders
    OUTPUT
    deleted.orderid,
    deleted.orderdate,
    deleted.custid
WHERE orderdate < '20140101' ) AS D
WHERE custid IN (11, 42);
```

可组合 DML 也适用于处理数据仓库中的缓慢变化维度（SCD）类型 2。你可以定义基于 `MERGE` 语句的派生表，该语句包含一个调用 `$action` 函数的 `OUTPUT` 子句。然后，在查询中，你可以过滤出已更新的输出行（操作为 'UPDATE'），并将它们插入表中，作为行的新版本。

目前 T-SQL 仅以有限的形式实现了可组合 DML。你只能在 `INSERT SELECT` 语句中使用此功能。你可以指定 `WHERE` 过滤器，但不能应用任何进一步的操作，如连接或其他操作符、分组等。

最后，该功能具有与 `OUTPUT` 子句相似的限制。表可以是永久表、临时表或表变量。目标不能是具有触发器的表表达式（如视图），也不能参与了主键-外键关系的表。

## 结论

本章涵盖了许多与数据修改相关的主题。它描述了 SQL Server 支持的一些批量导入工具，以及它们为了以最少日志进行处理而需要满足的要求。它涵盖了 `sequence` 对象，将其与 `identity` 列属性进行了对比分析，并提供了重要的性能考虑。本章还涵盖了删除和更新主题，并提供了一些正确使用 `MERGE` 语句并避免可能陷阱的提示。最后，本章涵盖了 `OUTPUT` 子句，描述了该功能的实际用例。

# 第 7 章

# 处理日期和时间

处理日期和时间是任何层级处理 T-SQL 的人员都需要熟练掌握的关键主题之一。这是因为你存储在数据库中的几乎每条数据都与某种日期时间元素相关。有许多需要注意的陷阱，这些陷阱会导致产生 Bug 和性能低的代码。

本章首先介绍了 Microsoft SQL Server 支持的日期和时间类型，随后涵盖了操作这些类型输入的内置函数。然后，它涵盖了你在处理日期时间数据时面临的复杂性，并提供了处理这些数据的最佳实践。最后，本章涵盖了日期时间查询任务、某些解决这些任务的常见方案的效率问题，以及创意且高效的解决方案。

## 日期和时间类型

在本文写作时，最新版本的 SQL Server（SQL Server 2014）支持六种日期时间类型。`DATETIME` 和 `SMALLDATETIME` 是该产品长期以来特性。其他类型——`DATE`、`TIME`、`DATETIME2` 和 `DATETIMEOFFSET`——是在 SQL Server 2008 中引入的后续新增。表 7-1 提供了支持的日期时间类型的规范。

选择类型的法则是使用涵盖日期范围、精度、功能和 API 支持所需的最小类型。类型越小，占用的存储越少。对于大表来说，这种节省会累积，导致处理查询时的读取减少，从而转化为更快的查询。

老旧类型 `DATETIME` 和 `SMALLDATETIME` 仍然被广泛使用，特别是前者。这主要是由于遗留数据、代码和习惯。除非有迫切的原因，否则人们通常不会因为涉及的复杂性而更改列类型和相关代码。此外，当你同时存储日期和时间且不需要比分钟更高的精度时，`SMALLDATETIME` 仍然是最经济的选择。

在支持的日期范围方面，对于 `DATE`、`DATETIME2` 和 `DATETIMEOFFSET` 类型，SQL Server 使用的是推测格高利历（proleptic Gregorian calendar）。这种历法扩展了对 1582 年引入的格高利历之前的日期的支持。详情请参见 http://en.wikipedia.org/wiki/Proleptic_Gregorian_calendar。

### 表 7-1 日期时间数据类型

| 数据类型 | 存储（字节） | 日期范围 | 精度 | 推荐的输入格式和示例 |
|---|---|---|---|---|
| DATETIME | 8 | 1753年1月1日日至9999年12月31日 | 3 1/3 毫秒 | YYYYMMDD hh:mm:ss.nnn '20090101 120000' |
| SMALLDATETIME | 4 | 1900年1月1日至2079年6月6日 | 1 分钟 | YYYYMMDD hh:mm '20090101 1200' |
| DATE | 3 | 0001年1月1日至9999年12月31日 | 1 天 | YYYYMMDD '20090101' |
| TIME(p) | 3 to 5 | | 100 纳秒 | hh:mm:ss.nnnnnn '12:30:00.000000' |
| DATETIME2(p) | 6 to 8 | 0001年1月1日至9999年12月31日 | 100 纳秒 | YYYY-MM-DD hh:mm:ss.nnnn '2009-01-01 12:30:00.000' |
| DATETIMEOFFSET(p) | 8 to 10 | 0001年1月1日至9999年12月31日 | 100 纳秒 | YYYY-MM-DD hh:mm:ss.nnnnnn[+-]hh:mm '2009-01-01 12:30:00.000000+02:00' |

如果你需要分离日期和时间，应该分别使用 `DATE` 和 `TIME`。存储仅日期的信息更为常见，例如订单日期、发货日期、发票日期等。`DATE` 类型是此类信息最经济的选择。如果你需要存储仅时间的信息，例如营业开始和结束时间，`TIME` 类型是最经济的选项。

2015 年 11 月 1 日凌晨 2:00 的标准时间 (PST)，时钟拨回到 1 点。因此，2015 年 11 月 1 日凌晨 1:30 PDT 对 UTC 的偏移量为 -7 小时，此时为 2015 年 11 月 1 日上午 8:30。一小时后，2015 年 11 月 1 日凌晨 1:30 PST 对 UTC 的偏移量为 -8 小时，此时为 2015 年 11 月 1 日上午 9:30。通过 `DATETIMEOFFSET` 类型，你可以正确地捕获时区中的日期和时间值为 `'2015-11-01 01:30:00.0000000-07:00'` 和 `'2015-11-01 01:30:00.0000000-08:00'`。你还可以使用 `SYSDATETIMEOFFSET` 函数作为 `DATETIMEOFFSET` 值捕获日期和时间。（稍后你将阅读更多关于日期和时间函数的内容）假设你在 2015 年从 PDT 切换到 PST 前几秒和几秒后运行了代码：

```sql
SELECT SYSDATETIMEOFFSET();
```

我实际上将电脑时钟设置到了切换前的几秒，然后在切换前后各运行了代码。我得到了以下输出：
