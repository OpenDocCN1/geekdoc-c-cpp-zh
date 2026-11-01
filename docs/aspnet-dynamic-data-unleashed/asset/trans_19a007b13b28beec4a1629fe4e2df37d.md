

### 注意

你也可以将 CustomValidationAttribute 直接放在 Order 类上以达到同样的效果。这主要是个人喜好问题。将数据注解特性放在私有 Metadata 类上有助于保持实体类的整洁，并避免不必要的细节泄露到你可能使用 Sandcastle 之类的工具从文档注释生成的帮助文件中。

下面是验证方法本身的更新版本：

```csharp
public static ValidationResult ValidateOrderDate(
    Order order, ValidationContext context)
{
    if (order.OrderStatus == null)
    {
        if (order.OrderDate != null &&
            order.OrderDate.Value < DateTime.Today)
        {
            return new ValidationResult(
                "Order Date cannot be in the past",
                new string[] { "OrderDate" });
        }
    }

    return ValidationResult.Success;
}
```

验证方法的新版本将 Order 作为第一个参数，并使用该实例访问 OrderStatus 和 OrderDate 属性的值。不幸的是，由于该方法现在验证的是 Order 实体，你不能再使用 ValidationContext 对象的 DisplayName 和 MemberName 属性来生成 ValidationResult。为简单起见，本示例中对它们进行了硬编码，尽管更好的做法是使用字符串常量或资源。

### 注意

自定义验证方法作为第二参数接收的 ValidationContext 对象有一个名为 ObjectInstance 的属性，它允许你在属性验证方法中访问实体实例。尽管这在编程测试中工作正常，但当 DynamicValidator 控件在网页回发期间调用属性验证方法时，原始实体实例并不存在，你唯一拥有的只是一个属性值。换句话说，如果你需要访问多个实体属性来执行验证，就必须使用类级验证方法。

## 验证多个规则

你可以使用多个验证方法和多个 CustomValidationAttribute 实例来实现不同的验证规则。然而，如果某些验证规则彼此相关，将它们合并到一个方法中实现可能会更简单。继续这个验证订单的示例，假设 Northwind Traders 公司允许客户指定他们希望订单送达的日期；但是，订单不能少于三天内送达。Order 实体的 RequiredDate 属性的验证与 OrderDate 属性的验证密切相关，因为这两个属性在订单提交时都必须进行验证。

System.ComponentModel.DataAnnotations 命名空间定义了一个特殊接口 IValidatableObject，你可以在实体类中实现该接口以同时验证多个规则。该接口定义了一个名为 Validate 的方法，它接受一个 ValidationContext 对象作为参数，并返回一个 ValidationResult 对象的集合：

```csharp
public interface IValidatableObject
{
    IEnumerable<ValidationResult> Validate(
        ValidationContext validationContext);
}
```

注意此方法与之前创建的自定义验证方法有多么相似。由于 Validate 是一个实例方法，它不需要单独的参数来接收要验证的对象，而且由于它可以验证多个规则，它返回的是 IEnumerable 而不是单个 ValidationResult。清单 8.4 展示了如何在 Order 实体类中实现它，以验证与 OrderDate 和 RequiredDate 属性相关的规则。

### 清单 8.4 实现 IValidatableObject 接口

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.ComponentModel.DataAnnotations;

partial class Order : IValidatableObject
{
    public IEnumerable<ValidationResult> Validate(
        ValidationContext validationContext)
    {
        var results = new List<ValidationResult>();
        if (this.OrderStatus != null)
        {
            if (this.OrderDate == null)
            {
                results.Add(
                    new ValidationResult("Order Date is required", new[] { "OrderDate" }));
            }
            else
            {
                if (this.OrderDate.Value < DateTime.Today)
                {
                    results.Add(
                        new ValidationResult("Order Date cannot be in the past",
                            new[] { "OrderDate" }));
                }

                if (this.RequiredDate != null &&
                    this.RequiredDate <= this.OrderDate.Value.AddDays(3))
                {
                    results.Add(
                        new ValidationResult(
                            "Required Date must be greater than Order Date + 3 days",
                            new[] { "RequiredDate" }));
                }
            }
        }

        return results;
    }
}
```

如你所见，该方法执行了多项检查，并在 List 中返回零个或多个 ValidationResult 对象。

> **注意**
> 
> 你还可以利用 C# 迭代器，它允许使用 yield return 语句，从而无需维护 ValidationResult 对象的列表。你可以从 http://msdn.microsoft.com/en-us/library/dscyy5s0.aspx 找到有关迭代器的更多详细信息。

在验证实现了 IValidatableObject 接口的对象时，Validator 类会在调用可能应用于该类或其属性的任何验证特性之后，调用其 Validate 方法。

## 报告多个错误

正如你从清单 8.1 中回忆的那样，UnleashedObjectContext 类的 Validate 方法调用 Validator 类的静态 ValidateObject 方法来验证所有新增和修改的实体对象。该方法会在遇到第一个验证错误时抛出 ValidationException。即使 Order 类的 Validate 方法可能同时报告两个错误（一个针对 OrderDate 属性，一个针对 RequiredDate 属性），但通过异常只会报告第一个错误。

虽然一次只报告一个错误在简单页面中可能不是问题，比如示例应用程序中的订单录入表单，但随着表单中字段数量的增加，修复一个错误后又出现另一个错误对用户非常不友好。图 8.9 说明了这个问题。

![](img/11b373b78859e17d318fd76939a0df9d_270_0.png)

图 8.9 在 Dynamic Data 网页中报告多个错误中的第一个。

这不是应用于单个属性的内置验证特性（如 RequiredAttribute 或 CustomValidationAttribute）的问题，因为它们由网页字段模板中独立的 DynamicValidator 控件直接调用。换句话说，所有属性级验证特性都被独立评估，所有错误都会同时报告给用户。然而，类级 CustomValidationAttribute 实例和 IValidatableObject 接口的 Validate 方法仅由 UnleashedObjectContext 类的 SaveChanges 方法中调用的 ValidateObject 方法调用，并且只报告第一个错误。

### IDynamicValidatorException 接口

Dynamic Data 定义了一个特殊接口 IDynamicValidatorException，它允许异常类提供有关单个操作期间可能发生的多个错误的信息。该接口定义了一个属性 InnerExceptions，它返回一个字典，包含实体属性名以及针对这些属性遇到的异常。

```csharp
public interface IDynamicValidatorException
{
    IDictionary<string, Exception> InnerExceptions { get; }
}
```

内置的 EntityDataSource 控件在报告将表单控件接收到的字段值赋给实体对象属性时发生的错误时，会利用此接口。Entity Framework 基于实体数据模型（EDMX）中直接嵌入的规则（例如阻止向不允许 null 值的实体属性分配 null 值）实现其自身有限的验证。当检测到这些错误时，EntityDataSource 控件会收集给定实体对象的所有错误，并抛出实现了 IDynamicValidatorException 接口的 EntityDataSourceValidationException。在表示层中，DynamicValidator 控件会检查数据源控件抛出的所有异常，如果某个特定异常实现了 IDynamicValidatorException 接口，验证控件就会使用其 InnerExceptions 字典来查找适用于它们所验证的实体属性的异常。

不幸的是，IDynamicValidatorException 定义在 System.Web.Extensions 程序集中，而 EntityDataSourceValidationException 定义在 System.Web.Entity 中。对于 Web 应用程序来说这不是问题；然而，对于其他类型的应用程序，使用这些类型意味着依赖 ASP.NET，而 ASP.NET 仅包含在 .NET Framework 的完整版本中，不包含在客户端配置文件（Client Profile）中。

### 修改 ObjectContext 以报告多个错误

为了避免在应用程序的业务层中增加对表示框架的依赖，你可以使用另一种内置异常类型——AggregateException。.NET Framework 4 在 System 命名空间中引入了这个类，以支持在并行任务库（TPL）中报告多个错误。AggregateException 也定义了一个名为 InnerExceptions 的属性，不过它存储的是 Exception 对象的 ReadOnlyCollection，而不是 Dictionary。以下是该类的简化形式声明：

```csharp
public class AggregateException : Exception
{
    public ReadOnlyCollection<Exception> InnerExceptions { get; }
}
```

下面是 UnleashedObjectContext 类的 Validate 方法的新版本，它在单个 AggregateException 中报告多个验证错误：

```csharp
private void Validate(ObjectStateEntry stateEntry)
{
    object entity = stateEntry.Entity;
    var context = new ValidationContext(entity, null, null);
    var results = new List<ValidationResult>();
```

