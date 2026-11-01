
Details 页面模板常用的编辑、删除和显示所有项目链接。清单 9.4 展示了其代码后置。

## 清单 9.4 带有 Fulfill 按钮的自定义订单页面（代码后置）

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web.DynamicData;
using DataModel;

namespace WebApplication.Samples.Ch9.ContextMethod
{
    public partial class SamplePage : System.Web.UI.Page
    {
        protected MetaTable ordersTable;

        protected void Page_Init(object sender, EventArgs e)
        {
            this.ordersTable = MetaModel.Default.GetTable(typeof(Order));
            this.formView.SetMetaTable(this.ordersTable);
            this.dataSource.Include = this.ordersTable.ForeignKeyColumnsNames;
        }

        protected void FulfillButton_Click(object sender, EventArgs args)
        {
            using (var context = new NorthwindEntities())
            {
                int orderId = (int)this.formView.DataKey.Value;
                context.FulfillOrder(orderId);
                context.SaveChanges();
                this.Response.Redirect(
                    this.ordersTable.GetActionPath(PageAction.Details,
                    new List<object>(new object[] { orderId })));
            }
        }
    }
}
```

FulfillButton_Click 方法处理 Fulfill 按钮的 Click 事件。因为事件处理器是在回发期间调用的，页面上显示的原始 Order 实体实例不再可用。在此示例中，OrderID 是从 FormView 控件的 DataKey 属性中提取的。或者，如果这是一个自定义页面模板，且 OrderID 在 URL 中可用，则可以通过调用第 7 章讨论的 MetaTable 对象的 GetColumnValuesFromRoute 方法来获取它。

FulfillButton_Click 事件处理器的新版本在 FulfillOrder 和 SaveChanges 方法调用周围包裹了一个 try/catch 块，这些调用可能抛出验证异常。catch 块捕获所有异常，并将它们传递给 UnleashedValidator 的 HandleException 方法（该方法定义在清单 9.3 的页面顶部）。如果 HandleException 方法返回 false，代码将重新抛出该异常。

如第 8 章所述，UnleashedValidator 类继承自内置的 DynamicValidator，并扩展了错误处理以支持 AggregateException。HandleException 方法接收一个 Exception 对象作为参数，遍历页面上的所有 UnleashedValidator 控件，包括字段模板中的控件，并尝试通过将异常传递给每个验证器的 ValidateException 方法来处理该异常。如果页面上一个或多个验证器能够通过设置其 ValidationException 属性来处理该异常，则 HandleException 返回 true。有关完整细节，请参阅本书附带的 Unleashed.DynamicData 项目中的 UnleashedValidator 源代码。

图 9.8 显示了一个由于 FulfillOrder 业务规则方法中抛出的 ValidationException 而显示的错误消息示例。

![](img/11b373b78859e17d318fd76939a0df9d_315_0.png)

图 9.8 调用业务规则方法时的验证错误。

**注意**

默认情况下，只读字段模板不包含验证器。Dynamic Data 项目默认自带的只读字段模板不足十个，你可以将 UnleashedValidator 控件添加到这些字段模板中，以改进属性特定错误的显示。但是，如果你选择这样做，请确保在没有错误时隐藏验证器；否则，生成的 HTML 和 JavaScript 体积增加可能会对应用程序中所有只读页面的性能产生显著影响。

## 数据库中的业务规则

本章讨论的部分业务逻辑与数据库存储过程、触发器和检查约束可以完成的工作类似。确实可以在数据库级别直接实现健壮的业务规则；然而，这样做会直接影响整个系统的性能和可伸缩性，而这些对于高流量的 Web 应用程序尤其重要。

当可以通过在单个物理计算机上安装更快或更多的 CPU 和 RAM 来提高系统性能时，系统进行垂直扩展。另一方面，当可以通过添加更多计算机来提高系统性能时，系统进行水平扩展。垂直扩展成本高昂；当 CPU 数量和 RAM 容量超过典型的商品化水平时，硬件和软件的成本都会呈指数级增长。在实践中，这意味着数据库服务器能提供的性能存在一个实际限制，有时称为“玻璃天花板”，要突破它需要不合理的高昂成本。水平扩展则便宜得多，因为向系统添加商品化服务器的成本仅线性增长。不幸的是，当今存在的大多数关系数据库管理系统在垂直扩展方面远优于水平扩展；事实上，不重新设计系统本身，几乎不可能对数据库服务器进行水平扩展。

通常，信息系统可以通过在应用服务器（例如我们示例中的 Web 服务器）上执行 CPU 密集型任务、在数据库服务器上执行 I/O 密集型任务来提高可伸缩性。到目前为止讨论的大多数业务规则都是 CPU 密集型的，换句话说，它们只需要 CPU 周期即可执行，不需要访问数据库。因此，在应用程序的实体类中实现这些规则，可以通过添加应用服务器来水平扩展系统，同时将数据库服务器的宝贵资源保留用于编译查询和计算执行计划。

然而，某些类型的业务逻辑（例如唯一性或引用完整性验证）是 I/O 密集型的。它们需要访问数据，并且可以在数据库服务器上更高效地实现。假设 Northwind 数据库中的所有产品都必须具有唯一的产品名称。如果在 Product 实体类中实现此验证逻辑，应用程序需要向服务器发送一个请求来查询 Products 表中具有给定名称的产品，然后再发送另一个请求来插入新记录。但是，如果在数据库中为 Products 表创建 UNIQUE KEY 约束，则应用程序只需发送一个请求来插入新记录，即可依赖数据库服务器验证新记录的 ProductName 是否唯一。两种实现需要相同数量的逻辑操作；然而，数据库实现需要更少的服务器请求，减少来回发送的数据量，并允许数据库服务器选择最佳方式执行唯一性规则。

## 在 Dynamic Data 应用程序中集成数据库验证

以下是一个 T-SQL 脚本，可用于在数据库级别实现 ProductName 唯一性验证：

```
ALTER TABLE [dbo].[Products]
    ADD CONSTRAINT [UK_Products]
    UNIQUE (ProductName)
```

如果不做额外修改，通过 Dynamic Data Web 应用程序创建具有重复名称的新 Product 的尝试将导致“死亡黄屏”，如图 9.9 所示。

![](img/11b373b78859e17d318fd76939a0df9d_317_0.png)

图 9.9 针对数据库异常生成的默认错误页面。

显然，在生产就绪的 Web 应用程序中，“死亡黄屏”是不可接受的，你需要更改它，使其与应用程序代码中实现的其他验证结果一致地报告错误。具体来说，你需要捕获适当的异常，并重新抛出包装在 ValidationException 实例中的异常。以下是如何重写 NorthwindEntities 类的 SaveChanges 方法来实现这一点：

```
public override int SaveChanges(SaveOptions options)
{
    try
    {
        return base.SaveChanges(options);
    }
    catch (UpdateException e)
    {
        HandleSqlException(e);
        throw;
    }
}
```

SaveChanges 方法的新版本将对基类方法的调用放在 try/catch 块中，以拦截 Entity Framework 报告为 UpdateException 类实例的数据库错误。UpdateException 本身提供的错误消息非常通用，只说在尝试保存更改时发生了错误；但是，底层数据库错误仍然可以通过其 InnerException 属性获得，该属性被用于下面显示的 HandleSqlException 方法：

```
private static void HandleSqlException(Exception e)
{
    SqlException error = e.InnerException as SqlException;
    if (error != null)
    {
        if (error.Number == 547)
            HandleReferenceConstraintViolation(error);
        else if (error.Number == 2627)
            HandleUniqueKeyConstraintViolation(error);
    }
}
```

在此示例中，使用的是 Microsoft SQL Server，因此内部异常将是 System.Data.SqlClient 命名空间中定义的 SqlException 类型。你可以通过查看 SQL 错误号来确定发生了哪种错误：违反 UNIQUE KEY 约束时错误号为 2627，违反 FOREIGN KEY 约束时错误号为 547。

