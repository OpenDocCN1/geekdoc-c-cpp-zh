
![](img/11b373b78859e17d318fd76939a0df9d_95_0.png)

## 图 2.16 添加函数导入。

当你在“添加函数导入”对话框中单击“确定”按钮时，函数导入将被添加到模型的概念部分。你可以在模型浏览器中的“实体容器/函数导入”下找到它；图 2.17 显示了一个示例。

![](img/11b373b78859e17d318fd76939a0df9d_95_1.png)

## 图 2.17 模型浏览器概念部分中的函数导入。

为每个函数导入，实体设计器会在 ObjectContext 类中生成一个强类型方法。以下是使用新添加的 GetProductsToReorder 方法列出存储过程返回的所有产品的示例：

```
using (NorthwindEntities context = new NorthwindEntities())
{
    IEnumerable<Product> products = context.GetProductsToReorder();
    foreach (Product p in products)
        Console.WriteLine(p.ProductName);
}
```

生成的 方法 返回 IEnumerable 而不是 IQueryable。虽然你可以使用熟悉的 LINQ 运算符进一步操作它，但请记住这些操作是在应用程序内存中执行，而不是由数据库服务器执行。相反，通常最好修改存储过程本身的定义，使其返回更集中的结果集。

## 插入、更新和删除存储过程

实体框架还允许你使用存储过程执行插入、更新和删除操作，而不是动态生成 SQL 语句。当与将应用程序权限限制为仅读取数据结合使用时，此技术可以帮助减少因随意浏览而导致的数据损坏和锁定，例如当开发人员或管理员使用 SQL Server Management Studio 等工具交互式地探索生产系统中的实时数据时。

以下是将新的 Product 实体插入 Products 表的存储过程示例：

```
CREATE PROCEDURE [dbo].[Products_Insert]
@ProductName nvarchar(40), @SupplierID int,
@QuantityPerUnit nvarchar(20), @UnitPrice money, @UnitsInStock smallint,
@UnitsOnOrder smallint, @ReorderLevel smallint, @Discontinued bit
AS
BEGIN
    INSERT INTO Products
    (ProductName, SupplierID, CategoryID,
    QuantityPerUnit, UnitPrice, UnitsInStock,
    UnitsOnOrder, ReorderLevel, Discontinued)
    VALUES
    (@ProductName, @SupplierID, @CategoryID,
    @QuantityPerUnit, @UnitPrice, @UnitsInStock,
    @UnitsOnOrder, @ReorderLevel, @Discontinued);
    
    SELECT SCOPE_IDENTITY() as ProductID;
END
```

请注意，此存储过程接受一组参数，每个参数代表特定的表列，例如 ProductName 和 SupplierID。存储过程执行 INSERT 语句和 SELECT 语句，以返回新插入行的 ProductID 值。

为了让实体框架利用此存储过程，它需要像前面讨论的 GetProductsToReorder 存储过程一样添加到实体模型存储部分。然而，与将其作为函数导入添加到概念模型不同，请在实体设计器中右键单击 Product 实体并从上下文菜单中选择“存储过程映射”。你将看到与图 2.18 所示类似的映射详细信息窗口。

![](img/11b373b78859e17d318fd76939a0df9d_97_0.png)

图 2.18 插入函数映射。

映射窗口的“函数”选项卡允许你将存储过程参数（显示在左侧）映射到实体属性（显示在右侧）。在此示例中，生成的 ProductID 值在“结果列绑定”部分中映射。

更新存储过程稍微复杂一些，因为它们需要实现实体框架通常执行的乐观并发控制。除了用于唯一标识目标行的主键值和所有字段的当前值之外，更新过程还需要为实体模型中并发模式设置为 Fixed 的每个实体属性提供单独的参数。在以下示例中，Products_Update 过程为所有属性提供单独的参数集，一组用于更新行的新值，另一组用于旧值，以确保实体自上次从数据库检索以来未被修改。

更新存储过程也需要添加到模型中并用于映射 Product 实体，如图 2.19 所示。Product 实体的每个属性都映射两次——首先映射到接收实体属性“旧”值的参数，即其从数据库中最初检索时的值，然后映射到接收需要持久化的“新”值的参数。请注意，存储过程的 @RowsAffected 输出参数返回存储过程实际修改的行数，在“受影响行参数”列中有复选框。实体框架使用此参数来确定乐观并发控制是否成功执行，如果返回零则抛出 OptimisticConcurrencyException。

![](img/11b373b78859e17d318fd76939a0df9d_99_0.png)

图 2.19 更新函数映射。

删除存储过程与更新存储过程类似，它们也需要实现乐观并发控制，并确保被删除的实体自上次从数据库检索以来未被修改。然而，由于没有需要持久化的新值，它们的参数列表通常要短得多。以下是 Product 实体的删除过程示例：

```sql
CREATE PROCEDURE [dbo].[Products_Delete]
    @ProductID int, @ProductName nvarchar(40), @SupplierID int, @CategoryID int,
    @QuantityPerUnit nvarchar(20), @UnitPrice money, @UnitsInStock smallint,
    @UnitsOnOrder smallint, @ReorderLevel smallint, @Discontinued bit,
    @RowsAffected int out
AS
BEGIN
    DELETE FROM Products
    WHERE
        ProductID = @ProductID AND
        SupplierID = @SupplierID AND
        CategoryID = @CategoryID AND
        QuantityPerUnit = @QuantityPerUnit AND
        UnitPrice = @UnitPrice AND
        UnitsInStock = @UnitsInStock AND
        UnitsOnOrder = @UnitsOnOrder AND
        ReorderLevel = @ReorderLevel AND
        Discontinued = @Discontinued;

    SET @RowsAffected = @@ROWCOUNT
END
```

实体框架针对每次检索和操作相对少量记录的富客户端应用程序进行了优化。然而，通过关闭对象跟踪选项，其性能可以改进，以用于多线程 Web 应用程序以及以批处理模式处理大量记录的应用程序。虽然实体框架为大多数常见数据访问场景生成高质量的参数化 SQL 代码，但它也允许使用存储过程来创建、读取、更新和删除实体/数据库记录。

实体框架支持来自 System.Transactions 命名空间的 TransactionScope 类，并在多用户场景中支持乐观并发以进行冲突检测。它开箱即用不支持悲观锁定；然而，在自定义存储过程的帮助下实现它是可能的。

实体框架代表了微软的一项长期战略投资。截至 .NET 版本 4，它是一个功能强大的框架，适用于大多数企业应用程序项目。与经典 ADO.NET 相比，它提供了显著的生产力提升，并已成为微软开发的一些新技术（包括 ASP.NET Dynamic Data）的推荐选择。实体框架正在积极开发中。版本 4.1 添加了对 Code-First 方法的支持，使得可以直接在应用程序代码中以类的形式定义实体模型。即将推出的版本 4.5 将为实体设计器带来重大增强，包括对枚举类型和多图的支持，使本章讨论的数据库优先方法以及模型优先方法的开发人员更具生产力。
