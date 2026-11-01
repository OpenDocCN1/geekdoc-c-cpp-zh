
相反，应修改项目中的 ObjectContext 类，使其在实体对象保存前通知它们，并允许实体对象在执行验证前执行属性交互规则。例如，本书附带的示例解决方案中的 Unleashed.EntityFramework 程序集定义了一个名为 ISavableObject 的接口（以便与内置的 IValidatableObject 接口保持一致），实体类在需要属性交互逻辑时可以实现该接口。

```csharp
interface ISavableObject
{
    void BeforeSave(ObjectStateEntry stateEntry);
}
```

现在，您可以在 Order 实体类中实现此接口，并让 BeforeSave 方法从 ObjectStateEntry 获取 OrderStatus 属性的原始值，将其与 OrderStatus 属性本身的当前值进行比较，然后使用系统日期和时间设置 SubmittedDate 属性。

```csharp
partial class Order : ISavableObject
{
    public void BeforeSave(ObjectStateEntry stateEntry)
    {
        byte? oldStatus = (byte)DataModel.OrderStatus.Draft;
        if (stateEntry.State == EntityState.Modified)
            oldStatus = stateEntry.OriginalValues.Get(() => this.OrderStatus);

        if (this.OrderStatus == (byte)DataModel.OrderStatus.Submitted &&
            oldStatus == (byte)DataModel.OrderStatus.Draft)
        {
            this.SubmittedDate = DateTime.Now;
        }
    }
}
```

UnleashedObjectContext 类会调用每个实现了 ISavableObject 接口的实体对象的 BeforeSave 方法。

```csharp
partial class UnleashedObjectContext
{
    private void BeforeSaveChanges(ObjectStateEntry stateEntry)
    {
        var savable = stateEntry.Entity as ISavableObject;
        if (savable != null)
            savable.BeforeSave(stateEntry);

        if (stateEntry.State != EntityState.Deleted)
            this.Validate(stateEntry);
    }
}
```

如第 8 章所述，`UnleashedObjectContext` 类重写的 `SaveChanges` 方法会在将更改提交到数据库之前，为每个已添加、已修改或已删除的实体调用 `BeforeSaveChanges` 方法。该方法接收一个 `ObjectStateEntry`，其中存储了实体的当前值和原始属性值。它会检查该实体是否实现了 `ISavableObject` 接口，并调用其 `BeforeSave` 方法。

当您的对象上下文类继承自 `UnleashedObjectContext` 或具有类似功能时，属性交互规则会在实体对象保存到数据库时自动调用。换句话说，只要网页通过 `NorthwindEntities` 上下文更改 `Order` 实体，`SubmittedDate` 就会根据 `OrderStatus` 属性的值自动更新。网页本身无需进行任何更改，无论是为编辑 Order 实体创建的自定义页面，还是动态 Edit 页面模板。

> **注意**
>
> `ISavableObject` 接口及其 `BeforeSave` 方法的工作方式与 Microsoft SQL Server 和其他关系数据库管理系统中的 UPDATE 触发器非常相似。虽然您确实可以在数据库触发器中实现此逻辑，但在实体级别工作可以为您提供更大的灵活性和更好的工具来实现业务规则。您仍然可以选择将触发器作为优化步骤（请参阅本章后面的*数据库中的业务规则*）。

## 实体交互规则

复杂的交互规则可能不限于单个实体对象，甚至不限于单个实体类型。例如，当订单完成时，系统需要更新产品库存，将库存数量减去已发货给客户的数量。在 Northwind 示例中，这意味着当 Order 实体的 `OrderStatus` 属性变为 `Fulfilled` 时，需要将 `Order_Detail` 实体的 `Quantity` 属性值从相应 Product 实体的 `UnitsInStock` 属性中减去。换句话说，订单履行业务规则跨越 `Order`、`Order_Detail` 和 `Product` 三个类，属于*实体交互规则*的范畴。

使用 Entity Framework 实现实体交互规则时，有几种不同的方法可以采用，包括（但不限于）：

- 将实体交互规则实现为 BeforeSave 方法
- 将实体交互规则实现为实体方法
- 将实体交互规则实现为上下文方法

本节将讨论这些方法，以及在选择如何在应用程序中实现实体交互规则时您必须考虑的一些权衡因素。

### 在 BeforeSave 方法中实现实体交互规则

您可以使用 BeforeSave“触发器”方法不仅实现属性交互规则，还可以实现实体交互规则。例如，您可以修改 Order 实体类的 BeforeSave 方法，以检测 OrderStatus 属性是否从 Paid 变为 Fulfilled，并更新此订单中购买的所有 Product 实体的 UnitsInStock 属性。下面的代码示例说明了实现的可能方式：

```csharp
partial class Order : ISavableObject
{
    public void BeforeSave(ObjectStateEntry stateEntry)
    {
        byte? oldStatus = (byte)DataModel.OrderStatus.Draft;
        if (stateEntry.State == EntityState.Modified)
            oldStatus = stateEntry.OriginalValues.Get(() => this.OrderStatus);

        if (this.OrderStatus == (byte)DataModel.OrderStatus.Fulfilled &&
            oldStatus == (byte)DataModel.OrderStatus.Paid)
        {
            this.ShippedDate = DateTime.Now;
            foreach (Order_Detail orderItem in this.Order_Details)
                orderItem.Product.UnitsInStock -= orderItem.Quantity;
        }
    }
}
```

尽管这种方法对于诸如本例中的简单场景是可行的，但随着规则数量及其复杂性的增加，维护起来会迅速变得异常困难。发生这种情况的原因之一是代码在猜测表示层想要完成什么。当只有 OrderStatus 属性从 Paid 变为 Fulfilled 时，很容易看出发生了什么，但如果 Order 实体的另一个属性也发生了变化呢？例如，您可能有另一个与 Order 实体的 ShipVia 属性相关的业务规则，用于根据客户选择的运输选项计算运费（Freight 属性）。如果 OrderStatus 与 ShipVia 属性同时变为 Fulfilled，这是否意味着员工选择了不同的承运商以不增加额外成本的方式加快客户的订单，还是客户顺路到实体店取走订单而您需要退还运费？这个问题在应用程序的业务层中无法回答，因为它取决于表示层的实现方式。

在 BeforeSave 方法（甚至数据库触发器）中实现复杂的业务规则（例如订单履行），会让您逐渐意识到，用户所能看到的内容比操作的总时长更为重要。ObjectContext 在桌面应用程序中也可以是长生命周期对象，自动将先前已加载的实体缓存在内存中，并提高后续操作的性能。然而，在 Web 应用程序中，每个页面请求都会创建一个新的 ObjectContext，并且在所有数据访问完成且整个页面生成之前用户什么也看不到，延迟加载可能会显著影响系统所有用户的性能。为了避免单独加载各个 Product 实体所带来的性能影响，请利用 ObjectQuery 类的 Include 方法，在单个数据库查询中将所有 Order_Detail 和 Product 实体连同订单一起加载。
