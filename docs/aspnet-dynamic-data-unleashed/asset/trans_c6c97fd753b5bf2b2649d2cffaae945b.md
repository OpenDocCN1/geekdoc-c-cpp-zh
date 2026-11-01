

```
var context = new ValidationContext(entity, null, items);

var results = new List<ValidationResult>();
if (!Validator.TryValidateObject(entity, context, results, true))
{
    ThrowValidationException(entity, results);
}
```

注意，ObjectStateEntry 实例以自身类型作为键存储在字典中。这并非硬性要求；你只需要一个已知的值作为键，以便验证方法能在字典中找到它。使用类型本身只是为了省去为此专门定义额外常量的麻烦。该字典作为第三个参数传递给 ValidationContext 构造函数。

在将验证基础结构改为在 ValidationContext 中存储 ObjectStateEntry 实例之后，现在可以在 Order 类中实现一个利用这一点的验证方法：

```
[MetadataType(typeof(Order.Metadata))]
partial class Order
{
    private abstract class Metadata
    {
        [CustomValidation(typeof(Order), "ValidateOrderStatus*")]
        public object OrderStatus { get; set; }
    }

    public static ValidationResult ValidateOrderStatus(
        byte? newStatus, ValidationContext context)
    {
        var stateEntry = (ObjectStateEntry)
            context.Items[typeof(ObjectStateEntry)];
        if (stateEntry.State == EntityState.Modified)
        {
            byte? oldStatus = (byte?)stateEntry.OriginalValues["OrderStatus"];
            if (oldStatus == (byte?)DataModel.OrderStatus.Fulfilled &&
                newStatus != (byte?)DataModel.OrderStatus.Fulfilled)
            {
                return new ValidationResult(
                    "Status of fulfilled orders should not be modified",
                    new string[] { "OrderStatus" });
            }
        }
        return ValidationResult.Success;
    }
}
```

```
}
```

在本例中，一个名为 `ValidateOrderStatus` 的自定义验证方法与元数据类中的 `OrderStatus` 属性相关联。验证方法首先从 `ValidationContext` 对象的 `Items` 字典中检索包含正在验证的订单实体的 `ObjectStateEntry` 实例。然后检查实体的当前 `State`，仅在实体被修改时才执行验证。由于实体状态也可能是 Added、Deleted、Detached 或 Unchanged，因此你只希望在根据业务规则判断合适时检查 `OrderStatus` 属性。此外，应该只在原始值确实可用时才访问 `OriginalValues` 属性；当实体状态为 Added 时，该属性会抛出 `InvalidOperationException`。

## 处理 DBNull 值

`ObjectStateEntry` 类的 `OriginalValues` 属性返回一个类型为 `DbDataRecord` 的对象，该类型由 Entity Framework 与经典 ADO.NET 共享。不幸的是，这意味着原始的 null 值会作为 `DBNull` 类型的对象返回，因此代码必须做好相应处理的准备。特别是，你不能简单地将原始的 `OrderStatus` 值强制转换为 `Nullable<Byte>` 类型，因为 `DBNull` 值无法转换为该类型，并会抛出 `InvalidCastException`。

解决此问题的一种变通方法是将 `OrderStatus` 值存储在 `Object` 类型的变量中，并使用静态的 `Object.Equals` 方法进行比较。由于该方法会考虑对象类型，因此可以安全地比较 `DBNull` 和 `Nullable<Byte>` 类型的值是否相等。以下是 `ValidateOrderStatus` 方法的新版本，它现在可以正确处理 `OrderStatus` 原始值为 `DBNull` 的情况：

```
public static ValidationResult ValidateOrderStatus(
    byte? newStatus, ValidationContext context)
{
    var stateEntry = (ObjectStateEntry)
        context.Items[typeof(ObjectStateEntry)];
    if (stateEntry.State == EntityState.Modified)
    {
        object oldStatus = stateEntry.OriginalValues["OrderStatus"];
        if (object.Equals(oldStatus, (byte)DataModel.OrderStatus.Fulfilled)
            && !object.Equals(newStatus, (byte)DataModel.OrderStatus.Fulfilled))
        {
            return new ValidationResult(
                "Status of fulfilled orders should not be modified",
                new string[] { "OrderStatus" });
        }
    }
    return ValidationResult.Success;
}
```

```
var order = (Order)stateEntry.Entity;
byte? oldStatus = stateEntry.OriginalValues
.Get(() => order.OrderStatus);
if ((oldStatus == (byte)DataModel.OrderStatus.Fulfilled)
&& newStatus != (byte)DataModel.OrderStatus.Fulfilled)
{
    return new ValidationResult(
        "Status of fulfilled orders should not be modified",
        new string[] { "OrderStatus" });
}
return ValidationResult.Success;
}
```

在这里，Get 扩展方法使用 () => order.OrderStatus lambda 表达式来确定属性名称 OrderStatus，并将该名称传递给 DbDataRecord 对象的索引器以检索原始属性值。如果原始值为 DBNull，Get 方法会返回属性类型的默认值——即该类型的未初始化变量所具有的值。对于 OrderStatus 属性，其类型为 Nullable<Byte>，默认值为 null；对于非可空类型（如 Byte），默认值将是 0。然而，如果从 DbDataRecord 对象检索到的原始值不是 DBNull，Get 方法会在将其强制转换为属性本身的类型后返回实际值。

Get 扩展方法有几个优点。一方面，它可以让你避免编写处理 DBNull 值的特殊逻辑。另一方面，它允许你用强类型的 lambda 表达式来指定属性，而不是使用硬编码的字符串字面量或常量。它们不仅更容易编写（借助 Visual Studio 编辑器中的 IntelliSense），而且如果你需要重命名属性，编译器会确保所有引用都被正确更新。

## 摘要

System.ComponentModel.DataAnnotations 命名空间提供了一个健壮的验证框架，允许通过放置数据注解属性以声明方式实现验证规则，或通过编写代码以命令方式实现。

验证框架已完全集成到 Dynamic Data Web 应用程序中；辅助类 Validator 也可用于将验证集成到其他框架。Entity Framework 4.0 版本没有开箱即用地支持验证框架，需要额外步骤来扩展对象上下文类，以便在实体对象提交到数据库之前自动对其进行验证。

自动化测试让你无需大量额外工作即可提高应用程序的质量。通过集成测试，你几乎可以立即开始收获自动化测试的好处。然而，应注意隔离测试，并确保它们可以重复运行且彼此独立。`TransactionScope` 是隔离访问数据库的集成测试的最简单方法。

框架开箱即用地包含许多内置验证属性，包括用于执行必填、字符串长度、范围、枚举和正则表达式检查的属性。可以通过继承 `ValidationAttribute` 类来实现其他验证属性。

命令式验证逻辑可以通过在单个属性或整个类上放置 `CustomValidationAttribute`，并实现返回 `ValidationResult` 对象的特殊验证方法来实现。类还可以实现 `IValidatableObject` 接口，以验证多条规则并返回多个验证结果。

## 第 9 章

### 实现业务逻辑

### 本章内容

- 实体设计
- 默认属性值
- 属性交互规则
- 实体交互规则
- 验证规则
- 保存更改
- 在 Web 应用程序中调用业务规则
- 数据库中的业务规则

业务逻辑，也称为*领域逻辑*，是代码实现开发者对业务领域的理解，其中应用程序旨在解决一个或多个问题并抓住机会。由于特定的业务领域可以从不同角度描述，因此对于什么构成业务逻辑有不同的定义。本章讨论与真实*实体*（如客户、产品和订单）相关的逻辑实现，以及决定这些实体如何相互交互的*规则*。

实体和规则并不直接与任何特定软件应用程序相关；相反，它们描述的是业务本身。就像零售商可以通过实体店直接向客户销售产品、通过电话接受订单、允许客户自行取货，或提供网站让客户提交订单并通过邮寄发货一样，不同的软件应用程序也可以实现相同的业务逻辑。实体店的销售职员可以使用基于 Windows 的销售点应用程序来销售产品，而客户可以使用基于 Web 的应用程序在线下单。在这两种情况下，都需要检查订单以确保产品有货，计算订单总额，更新产品库存，对缺货产品进行补货，等等。

部分原因是需要通过不同应用程序支持相同业务服务的共同需求，部分原因是业务逻辑相对稳定，软件开发行业已广泛认同将业务逻辑与其表示层分离是有益的，因为它允许复用

