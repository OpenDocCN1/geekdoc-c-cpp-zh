
| 步骤 | 事务 1 | 事务 2 |
| --- | --- | --- |
| 1 | BEGIN TRANSACTION; | |
| 2 | | BEGIN TRANSACTION; |
| 3 | UPDATE dbo.T1<br>SET C2 = 2<br>WHERE C1 = 1; | UPDATE dbo.T1<br>SET C2 = 3<br>WHERE C1 = 1; |
| 4 | | |
| 5 | COMMIT; | |
| 6 | | COMMIT; |

相比之下，如果对一个非内存优化表尝试执行相同的系列更新，则会发生以下情况：

- 在步骤 1 和 2 中，事务 1 和事务 2 发出 `BEGIN TRANSACTION` 语句并启动上下文。
- 在步骤 3 中，事务 1 更新了数据库中的某行。它在这些行上获取了排他锁。
- 在步骤 4 中，事务 2 尝试修改同一行，但它被事务 1 的排他锁阻塞。它将一直等待，直到事务 1 完成。
- 在步骤 5 中，事务 1 通过提交完成。这释放了该行上的锁，事务 2 继续执行其更新。
- 在步骤 6 中，事务 2 通过提交完成。

注意，在内存优化表的情况下，由于事务 2 的更新不会完成，C2 的值将是事务 1 更新后的值 2。在传统表中，事务 2 最终会成功，因此 C2 的最终值将为 3。

为了处理提交验证错误，编写事务时应采用相同的死锁重试逻辑，如列表 10-6 所示。

### 列表 10-6 验证失败的重试逻辑

```
-- 重试次数 - 根据工作负载进行调整
DECLARE @retry INT = 10;

WHILE (@retry > 0)
BEGIN
    BEGIN TRY
        exec usp_my_native_proc @param1, @param2, ...
        -- BEGIN TRANSACTION
        ..
        -- COMMIT TRANSACTION

        SET @retry = 0;
    END TRY
    BEGIN CATCH
        SET @retry -= 1;

        IF (@retry > 0 AND error_number() IN (41302, 41305, 41325, 41301, 12055))
        BEGIN
            -- 这些错误无法恢复并继续。事务必须
            -- 回滚并完全重试。
            -- 原生过程在抛出错误时将简单回滚，因此在这种情况下跳过
            -- 回滚。
            IF XACT_STATE() = -1
                ROLLBACK TRANSACTION;
            -- 如果存在高频率写入冲突 (41302)，则使用延迟
            -- 延迟长度取决于冲突事务的典型
            -- 持续时间
            WAITFOR DELAY '00:00:00.001';
        END
        ELSE
        BEGIN
            -- 在此处为其他错误条件插入自定义错误处理
            -- 如果这不是符合条件的错误条件，则抛出异常
            THROW;
        END
    END CATCH;
END
```

## 跨数据库查询

在 SQL Server 2014 中，你无法执行同时访问内存优化表和另一个数据库中任何表的查询，无论该数据库是在同一实例中还是在另一个实例中。但是，你可以在跨数据库事务中使用内存优化变量。

## 并行

以任何方式访问内存优化表的事务都不会使用并行计划。这是 SQL Server 2014 的一个限制，可能会在未来的版本中移除。这些事务的有效并行度 (`MAXDOP`) 将为 1。这可能对查询性能产生严重影响，在某些情况下，可能会抵消内存优化表的性能优势。例如，如果你正在将一个内存优化表与一个基于聚集列存储索引（Clustered Column Store index）的表进行连接，你可能会认为这两个在各自领域都极快的技术可以配合得非常好。遗憾的是，列存储的性能设计是基于高度并行的。列存储能够利用系统的所有核心在极短的时间内对海量数据集进行扫描。当引入内存优化表进行查询时，查询的整体并行度下降到 1，列存储索引的性能会受到严重影响。

这是内存 OLTP 查询中当前并行性限制对性能影响的一个极端示例，但在许多其他情况下，可能仍然能感觉到这种影响，尽管它可能并不明显。幸运的是，通过查看基于磁盘的查询的计划并将其与内存优化查询的计划进行比较，很容易检测出何时存在性能问题。

你可以从第一个计划看到，并行操作符在整个计划中一致使用，而在内存优化查询的第二个计划中，计划完全基于串行操作符。

你也可以查看或搜索查询计划的 XML 表示中的 `<RelOp>` 标签，并查找 `Parallel` 属性：

在带有内存优化表的查询中，显示如下：

```
<RelOp AvgRowSize="90" EstimateCPU="2.51839" EstimateIO="0" EstimateRewinds="0" EstimatedExecutionMode="Row" EstimateRows="99900" LogicalI0="Inner Join" NodeId="7" Parallel="false" PhysicalIO="Hash Match" EstimatedTotalSubtreeCost="20.3456">
```

为了验证这确实是问题，你可以在预期性能良好的磁盘表上执行查询，并将 `MAXDOP` 设置为 1，然后查看结果是否一致。

## 基数与统计

为了查询优化器正确确定查询计划，它需要每个表的基数信息。SQL Server 会自动创建并更新统计信息，以确保拥有准确的数据。在触发更新时，会涉及某些成本开销。

内存 OLTP 具有某些在经典 SQL 中可能使用的行为。其中某些是 SQL Server 2014 的限制，并且在未来版本中可能会发生变化。

### 统计信息与原生过程

由于原生编译过程在编译为 DLL 之前已通过 SQL Server 优化器进行了优化，它们不会更改。在内存优化环境之外，更改统计信息会触发查询的重新编译，但对于原生编译过程，不会发生。

> **注意** 在设置内存优化表时，最好先向表中加载数据。这样优化器将拥有更多数据，过程将拥有更优的计划。

如果访问原生编译过程的表的内容足以导致性能下降，你可能需要删除并重建过程，以强制其根据当前统计信息重新编译。

### 更新统计信息

在 SQL Server 2014 中，当更新内存优化表的统计信息时引擎不会像传统表那样使用采样。相反，它将对表执行全扫描。虽然这通常会提供更多结果，但耗时会更长，可能会对性能产生某些干扰。

## 原子块

原生编译过程要求由恰一个原子块组成。它必须封装过程中所有的 T-SQL 逻辑。

原子块是 SQL Server 2014 引入的一个新概念。它代表一组保证作为一个单元原子地成功或失败的语句。原子块与 SQL 事务的交互方式如下：

- 如果存在当前的 SQL 事务，原子块将创建一个保存点并加入现有事务。
- 如果没有当前事务，原子块将创建一个作用域，即该块本身。
- 如果块抛出异常，则该块将作为整体进行回滚。
- 如果块成功，它创建的保存点将提交提交，如果它创建了自己的事务，则该事务将被提交。

## 原生编译存储过程

如所述，原生编译的存储过程效率极高，因为它们被预编译为 DLL 并加载到引擎上下文中。请注意，在您用于解释器查询的解释器环境（或不访问内存优化表的存储过程环境）与原生编译环境之间进行转换会存在一些开销。对于非常少量的逻辑（例如单语句事务），您可能会发现直接在解释器中执行查询的性能更好。然而，在原生存储过程的上下文中执行的逻辑越多，您获得的益处就越多。

为了充分利用原生编译存储过程的优势，您应该尝试在每次调用原生存储过程中，尽可能地处理多的业务逻辑。一种方法是以表值参数（TVP）的形式将一组工作单元传递给原生存储过程，以便在存储过程内部进行完全处理。

### TVPs

为了在原生编译存储过程内部进行访问，TVP 必须是经过内存优化的。它们提供了超越原生编译存储过程的巨大优势。内存优化的 TVP 可以像临时表一样被传统的 T-SQL 存储过程使用，在许多情况下，它们的效率高得多，因为不需要在 tempdb 中实例化。创建内存优化表类型的语法可以参见前面提到的 AdventureWorks 示例，如列表 10-7 所示。

#### 列表 10-7 内存优化表类型

```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem AS TABLE(
    OrderQty SMALLINT NOT NULL,
    ProductID INT NULL,
    SpecialOfferID INT NULL,
    LocalID INT NULL,
    INDEX IX_ProductID NONCLUSTERED HASH
    (
        ProductID
    ) WITH ( BUCKET_COUNT = 8),
    INDEX [IX_SpecialOfferID] NONCLUSTERED HASH
    (
        SpecialOfferID
    ) WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```

随后，在调用原生存储过程时使用该类型，如列表 10-8 所示。

#### 列表 10-8 在原生存储过程使用表值参数

```sql
-- 表值参数
-- 如果对象存在，则删除旧对象

IF (OBJECT_ID('Sales.usp_InsertSalesOrder_inmem') IS NOT NULL)
    DROP PROCEDURE Sales.usp_InsertSalesOrder_inmem;

IF (TYPE_ID('Sales.SalesOrderDetailType_inmem') IS NOT NULL)
    DROP TYPE Sales.SalesOrderDetailType_inmem;

-- 内存优化表类型
CREATE TYPE Sales.SalesOrderDetailType_inmem AS TABLE(
    OrderQty SMALLINT NOT NULL,
    ProductID INT NOT NULL,
    SpecialOfferID INT NOT NULL,
    LocalID INT NOT NULL,
    INDEX IX_ProductID NONCLUSTERED HASH
    (
        ProductID
    ) WITH (BUCKET_COUNT = 8),
    INDEX [IX_SpecialOfferID] NONCLUSTERED
    (
        SpecialOfferID
    ) WITH (BUCKET_COUNT = 8)
)
WITH (MEMORY_OPTIMIZED = ON);
GO

-- 在原生存储过程中使用表值参数

CREATE PROCEDURE Sales.usp_InsertSalesOrder_inmem
    @OrderID INT OUTPUT,
    @DueDate DATETIME2(7) NOT NULL,
    @CustomerID INT NOT NULL,
    @BillToAddressID INT NOT NULL,
    @ShipToAddressID INT NOT NULL,
    @ShipMethod INT NOT NULL,
    @SalesOrderDetails Sales.SalesOrderDetailType_inmem READONLY,
    @Status TINYINT NOT NULL = 1,
    @onlineOrderFlag BIT NULL = 1,
    @PurchaseOrderNumber NVARCHAR(25) = NULL,
    @AccountNumber NVARCHAR = NULL,
    @SalesPersonID INT NOT NULL = -1,
    @TerritoryID INT = NULL,
    @CreditID INT = NULL,
    @CreditCardApprovalCode VARCHAR(15) = NULL,
    @CurrencyRate INT = NULL,
    @Comment NVARCHAR(128) = NULL

WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE OWNER
AS
BEGIN ATOMIC WITH
(TRANSACTION ISOLATION LEVEL = SNAPSHOT,
LANGUAGE = 'us_english')
DECLARE @StartDate DATETIME2 NULL = sysdatetime();
DECLARE @SubTotal MONEY NULL = 0;
SELECT @SubTotal = ISNULL(SUM(p.ListPrice * (1 - so.DiscountPct)),0)
FROM Sales.SalesOrderDetails od
JOIN Sales.SpecialOffer_inmem so ON od.SpecialOfferID=so.SpecialOfferID
JOIN Sales.Product_inmem p ON od.ProductID=p.ProductID;

INSERT INTO Sales.SalesOrderHeader_inmem
(@DueDate,
@Status,
@OnlineOrderFlag,
@PurchaseOrderNumber,
@CustomerID,
@SalesPersonID,
@TerritoryID,
@BillToAddress,
@ShipToAddress,
@ShipMethodID,
@CreditCardID,
@CreditCardApprovalCode,
@CurrencyRateID,
@Comment,
@Order,
@SubTotal,
@ModifiedDate)
VALUES
(@DueDate,
@Status,
@OnlineOrderFlag,
@PurchaseOrderNumber,
@AccountNumber,
@CustomerID,
@SalesPersonID,
@TerritoryID,
@BillToAddress,
@ShipToAddress,
@ShipMethodID,
@CreditCardID,
@CreditCardApprovalCode,
@CurrencyRateID,
@Comment,
@Order,
@SubTotal,
@OrderDate);

SET @OrderID = SCOPE_IDENTITY();
END
```

## 限制与变通方法

- **外键约束**：由于不支持外键约束，我建议在应用程序逻辑中对与其他表具有关键关系的表执行任何更新操作（插入、更新或删除），并在应用逻辑中进行验证，以避免数据不一致。这种验证可以在 DML 语句的封装函数中完成以验证一致性，也可以直接内联在应用程序代码中。
- **检查约束**：与外键约束一样，检查约束必须在应用程序代码中模拟，并封装可能违反条件的更新语句。
- **唯一性约束**：这些约束不支持直接支持；然而，所有具有 `SCHEMA AND DATA` 持久性的内存优化表都必须有一个唯一主键索引。在许多情况下，该唯一索引将充当约束的作用。
- **ALTER TABLE**：SQL Server 2014 不支持任何方式的修改表。如果你想更改表或索引的定义，需要卸载、删除并重新加载表。这包括对索引的任何更改或添加。
- **大对象 (LOB) 数据类型**（例如 `varchar(max)`、`image`、`xml`、`text` 和 `ntext`）：内存优化表的所有列组合最大行大小为 8,060 字节。虽然你可以使用 `varchar(8000)` 等列，但你不能使用 `(max)`，这将超过 8,060 字节的限制。当需要更大的 LOB 时，通常将列拆分为 8,000 字节的记录并在检索时重新组装，并将数据留在传统表中会速度更快。关于如何实现此点的示例，你可以查看使用内存优化表的 ASP.NET Session Cache 的实现，该实现已发布在 CodePlex 上：https://msftdbpsamples.codeplex.com/releases/view/125282。
- **聚集索引**：与其说这是一个限制，不如说需要理解这些索引是如何工作的。内存优化表上的索引实际上都是指向实际数据的指针，聚集索引和非聚集索引之间没有区别。由于行数据并不物理存在于索引结构中，因此内存优化表上的所有索引都是 `NONCLUSTERED`（非聚集）。它们可以被认为是覆盖索引，因为索引直接引用了表中的所有列。

## DML

SQL Server 2014 的原生编译存储过程在可用范围方面存在一些限制，这可能需要一些变通。在某些情况下，这些限制可能意味着存储过程留存在交互模式（interop mode）中更好。在许多情况下，可以将过程拆分为位于交互模式的封装存储过程和一个原生编译的内部存储过程。外部封装器包含原生编译存储过程中不支持的构造结构，而内部存储过程是原生编译的，用于执行对性能最敏感的逻辑。以下是需要考虑的关键点：

- **游标**：原生编译存储过程中不支持游标。相反，作为通用最佳实践，请使用基于集合的逻辑或 `WHILE` 循环。
- **子查询**：不支持嵌套在另一个查询中的子查询。请重写查询或在交互模式下执行它。
- **SELECT INTO**：不支持 `SELECT INTO` 语法；然而，可以将其重写为 `INSERT INTO Table`。
- **跨数据库事务**：在 SQL Server 2014 中，涉及内存优化表的事务无法访问另一个数据库中的数据，无论它是本地还是远程。
- **EXECUTE, INSERT EXEC**：你不能从原生编译存储过程内部调用存储过程。在某些情况下，为了遵守此限制，你必须内联已提取提取的代码。
- **外部连接，Union**：外部连接或联合必须通过聚合较小的查询来实现，通常使用本地的内存优化表变量。
- **逻辑取或 (OR, IN)**：原生编译存储过程中不支持这些逻辑操作。你必须为每种情况创建查询，然后聚合结果。

## 结论

你已经看到 SQL Server 2014 中的内存 OLTP 系统具有极大提高数据库操作速度的潜力——在某些情况下，它代表了业务的“游戏规则改变者”。然而，这并不能消除理解你正试图解决的性能问题并找出导致这些问题的瓶颈的需求。通过理解这种新环境与传统数据库表在行为上的不同方式，你可以获得巨大的收益。
