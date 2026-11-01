
```
var order = context.Orders
    .Include("Order_Details")
    .Include("Order_Details.Product")
    .First(o => o.OrderID == orderId);
order.Fulfill();
```

然而，你需要将这样的代码放在每个需要执行 Fulfill 业务规则的页面中，将数据访问逻辑泄漏到表示层，这在大多数情况下不是一个好主意。避免这样做的一个原因是，Entity Framework 4 迫使你将实体类及其属性的名称硬编码为字符串字面量，这些字符串脆弱且容易出现拼写错误。即使你用字符串常量解决这个问题，它仍然意味着在表示层硬编码特定业务规则所需的所有实体和关系的知识，可能在多个调用同一方法的地方重复。

## 将实体交互规则实现为上下文方法

当性能很重要且需要封装数据访问逻辑时，将业务规则实现为对象上下文类的方法而不是实体类的方法可能是有益的。以下是在 `NorthwindEntities` 类中重新实现订单履行业务规则的方法：

```
public partial class NorthwindEntities
{
    public void FulfillOrder(int orderId)
    {
        Order order = this.Orders
            .Include("Order_Details").Include("Order_Details.Product")
            .First(o => o.OrderID == orderId);
        order.OrderStatus = (byte)DataModel.OrderStatus.Fulfilled;
        order.ShippedDate = DateTime.Now;
        foreach (Order_Detail orderItem in order.Order_Details)
            orderItem.Product.UnitsInStock -= orderItem.Quantity;
    }
}
```

`FulfillOrder` 方法以 `OrderID` 作为参数，并在一次数据库往返中检索 `Order` 实体、其所有 `Order_Detail` 对象以及相关的 `Product` 实体。当所有实体都加载到上下文中后，代码执行与之前 `Fulfill` 方法中相同的步骤——更新 `OrderStatus` 和 `ShippedDate`，并递减 `UnitsInStock`。

这个版本的 `FulfillOrder` 方法假定调用者尚未从数据库加载 `Order` 实例，因此将其主键值作为参数是最佳选择。然而，如果 `Order` 实例已经加载，你可以更改或者创建一个重载版本的 `FulfillOrder` 方法，使其改为接受*实体实例*作为参数。下面的代码示例展示了一个可能的实现。正如你所看到的，你可以查询 `Order_Details` 实体集，并将 `Include` 调用的数量减少到一个，而不是查询 `Order` 实体集：

```
public partial class NorthwindEntities
{
    public void FulfillOrder(Order order)
    {
        order.OrderStatus = (byte)DataModel.OrderStatus.Fulfilled;
        order.ShippedDate = DateTime.Now;
        IQueryable<Order_Detail> orderItems = this.Order_Details
            .Include("Product")
            .Where(od => od.OrderID == order.OrderID);
        foreach (Order_Detail orderItem in orderItems)
            orderItem.Product.UnitsInStock -= orderItem.Quantity;
    }
}
```

尽管 `FulfillOrder` 的第二个版本感觉更“面向对象”，因为它接受一个 `Order` 对象作为参数而不是原始的主键值，但你的设计方法选择应该由需要实现的具体场景驱动。如果订单将从 ASP.NET 网页上一次一个地标记为已履行，并且调用代码只有存储在页面 `ViewState` 中的主键值，那么 `FulfillOrder` 方法的第一个版本将效果最好。更优雅的第二个版本的 `FulfillOrder` 方法可能只在以下场景中效果更好：*多个*订单已经从数据库加载，并且不会产生额外数据库调用来检索订单实例的开销。换句话说，第二种风格的方法更适合实现作为更大业务流程一部分的细粒度业务规则。

> **注意**
> 
> 在对象上下文方法中实现实体交互规则并消除对延迟加载的依赖，不仅有助于提高应用程序的*性能*，还有助于提高其*正确性*。除非依赖延迟加载的代码显式检查其已启用，否则延迟加载选项可能会被意外或故意关闭，从而让订单看起来为空，而实际上其订单项和产品只是尚未从数据库加载。
> 
> 不利的一面是，将业务规则实现为上下文方法可能会让人感到别扭，这取决于你认为该方法应该属于哪里。例如，如果你强烈认为履行是 `Order` 类的行为，那么将 `Fulfill` 方法移到 `NorthwindEntities` 类中就意味着破坏其封装。

将业务规则实现为上下文方法适用于业务逻辑量较小的简单实体模型。随着模型规模和复杂性的增长，业务规则方法的数量会达到一个临界点，在单个类中维护它们将变得困难。当这种情况发生时，你可以开始将方法提取到单独的类中，按它们所适用的实体类型（表模块）或所实现的业务流程（服务）进行分组。然而，最好避免在应用程序开发的早期就做出这种设计决策。如果没有对业务领域和所需功能的扎实理解，过早的架构决策往往是错误的，会导致不必要的复杂性和更高的成本。

## 验证规则

作为业务逻辑的一种形式，验证规则也容易受到许多相同潜在问题的影响。随着验证规则数量的增加，代码的复杂性迅速增长，如果你不小心，可能会对应用程序的性能以及维护能力产生重大影响。与一般的业务逻辑一样，保持验证规则简单且封装良好是有帮助的。

为了帮助理解验证规则，可以将它们分为两大类：

- 持久化验证
- 转换验证

持久化类别中的规则决定了实体成功保存到数据库所必须满足的条件。通常，此类验证规则适用于应用程序用户直接输入的属性。例如，订单要被 Northwind Traders 接受，需要提供收货地址（`ShipAddress`、`ShipCity`、`ShipRegion` 等属性）。

另一方面，转换规则决定了允许实体从一种状态更改为另一种状态的条件。例如，如果 Northwind Traders 公司要求客户预付订单，那么 `Order` 实体必须具有 `Paid` 的 `OrderStatus`，然后才能更改为 `Fulfilled`。`OrderStatus` 属性与 `Order` 实体的其他属性不同，因为它决定了其当前状态。

实体状态不仅可能有不同的转换规则；它们通常也有不同的持久化规则。例如，在保存处于 `Submitted` 状态的订单时，你可能希望验证库存中是否有足够的产品来满足订单中的所有项目；然而，这条规则不适用于 `Fulfilled` 状态的订单，因为箱子离开仓库后，你可能在系统中保留这些订单多年。

## 验证规则设计

为了在代码复用、复杂性和性能之间找到合理的折衷方案，同时避免以后进行大量重构，请在应用程序中设计验证逻辑时尝试以下经验法则：

- 使用数据注解实现持久化验证规则
- 使实体的状态属性为只读
- 在业务规则方法中实现状态转换和验证
- 在单独的验证方法中实现特定于状态的持久化验证

## 使用数据注解实现持久化验证规则

第 8 章讨论的验证框架提供了一种很好的方式来实现持久化验证规则，通过应用预构建的验证属性或为单个属性或整个实体编写自定义验证方法。你可以快速将 `RequiredAttribute` 应用于 `Order` 实体的收货地址属性，以确保订单在保存到数据库之前是有效的。

## 使实体的状态属性为只读

你不希望应用程序的用户（无论是客户还是员工）直接编辑 `OrderStatus` 属性，即使他们发起了状态转换。客户将通过点击结账页面上的“提交”按钮来提交订单，而处理信用卡付款的后台进程会将订单标记为已付款。确保实体的状态属性不能通过应用程序的用户界面更改的最佳方法是使其为只读。

使用 Entity Framework，你可以使用实体设计器将 `OrderStatus` 属性的 setter 设置为 `internal`，如图 9.7 所示。

