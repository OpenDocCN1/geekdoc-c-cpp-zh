

```csharp
[Authorization(
    new Allow(Roles = "Manager, Employee"),
    new Deny(Users = "*"))]
```

如果无法使用多个特性和自定义类型，你只能使用原始类型，比如字符串和枚举，它们可以用于常量表达式。

AuthorizationAttribute 还允许你通过在规则中包含一个或多个 Actions 来定义操作级权限。例如，下面展示了如何允许员工以只读模式访问供应商，同时仍允许经理完全访问：

```csharp
[Authorization(
    Allow.Roles, "Manager",
    Allow.Roles, "Employee", Actions.Read,
    Deny.Users, "*")]
partial class Supplier { ... }
```

Actions 是下面展示的一个枚举类型。注意它表示一个位字段，使你能在同一规则中使用按位或运算符（C# 中的 `|`）指定多个操作。例如，你可以通过将操作指定为 `Actions.Read | Actions.Update` 来允许员工读取和更新供应商。除非在规则中显式指定了 Actions 值，否则 AuthorizationAttribute 会假定其为 All，这就是为什么刚描述的规则允许经理执行所有操作，而将客户限制为只读访问：

```csharp
[Flags]
public enum Actions
{
    None   = 0x00,
    Read   = 0x01,
    Insert = 0x02,
    Update = 0x04,
    Delete = 0x08,
    All = Read | Insert | Update | Delete
}
```

如你所见，AuthorizationAttribute 允许你基于每个用户或每个角色表示实体级和操作级权限。生成的注解非常类似于 `<authorization>` 配置节的结构，除了 Actions 参数，该参数在 `<allow/>` 和 `<deny/>` 元素中不可用。虽然这种差异一开始可能令人困惑，但生成的授权规则定义比典型的操作级规则所需的 Web 配置要紧凑得多，因为后者需要为每个操作创建单独的 `<location/>` 节。基于特性的授权规则还允许你更改路由配置，而无需更新 web.config 中的规则。

现在让我们仔细看看这个特性是如何实现的，以及如何使用它来扩展 Dynamic Data 元模型：

```csharp
[AttributeUsage(AttributeTargets.Class)]
public class AuthorizationAttribute : Attribute
{
    public AuthorizationAttribute(params object[] rules);
    public ReadOnlyCollection<AuthorizationRule> Rules { get; }
    public bool IsAuthorized(IPrincipal principal, Actions actions);
}
```

AuthorizationAttribute 的主要访问点是 IsAuthorized 方法。它接收一个 IPrincipal 对象（表示应用程序的用户）、用户需要执行的一个或多个 Actions，并返回一个布尔值，指示用户是否被允许执行。在首次评估给定特性中的规则之前，IsAuthorized 方法会将在构造函数中指定的对象数组解析为 AuthorizationRule 对象的集合，该集合由 Rules 属性公开。

```csharp
public class AuthorizationRule
{
    public bool Authorize { get; }
    public Actions Actions { get; }
    public ReadOnlyCollection<string> Roles { get; }
    public ReadOnlyCollection<string> Users { get; }
}
```

尽管 AuthorizationRule 类的主要目的是辅助规则评估，但在应用程序中实现管理功能时，你可能会发现它很有用。例如，示例应用程序内置的元数据资源管理器使用它来显示关于实体类型的安全信息。

> **注意**
>
> 为了模拟基于配置的授权规则的默认行为，除非一个或多个请求的操作被匹配的规则显式拒绝，否则 IsAuthorized 方法返回 true。正如本章前面所讨论的，在指定所有适当的允许规则后，包含一个通配符拒绝规则以防止未经授权的访问非常重要。

## 使用 AuthorizationAttribute 实现 MetaTable 权限方法

在自定义 MetaTable 类中重写 CanRead、CanInsert、CanUpdate 和 CanDelete 方法时，你可以利用 AuthorizationAttribute。下面展示了 UnleashedMetaTable 中如何实现 CanDelete 方法（你可以在本书配套示例解决方案的 Unleashed.DynamicData 项目中找到它）：

```csharp
public partial class UnleashedMetaTable : MetaTable
{
    private readonly AuthorizationAttribute authorizationAttribute;

    public UnleashedMetaTable(
        UnleashedMetaModel model, TableProvider provider)
        : base(model, provider)
    {
        this.authorizationAttribute = this.Attributes
            .OfType<AuthorizationAttribute>().FirstOrDefault();
    }

    private bool IsAuthorized(IPrincipal user, Actions actions)
    {
        if (this.authorizationAttribute == null) return true;
        return this.authorizationAttribute.IsAuthorized(user, actions);
    }

    public override bool CanDelete(IPrincipal user)
    {
        return base.CanDelete(user) && this.IsAuthorized(user, Actions.Delete);
    }
}
```

注意 UnleashedMetaTable 构造函数如何尝试查找可能应用于此元表对象所表示的实体类的 AuthorizationAttribute，并将其存储在 authorizationAttribute 字段中。在创建元表对象时仅执行此步骤一次对于提高应用程序性能很重要，因为权限方法在每次页面请求中都会被多次调用。

IsAuthorized 方法负责确定给定用户是否被允许执行一个或多个 Actions。该方法负责检查实体类是否应用了 AuthorizationAttribute，如果应用了，则将授权委托给该特性。如果实体类没有 AuthorizationAttribute，该方法假定所有用户都被允许对该实体执行所有操作，并返回 true。虽然这可能不是很安全，但它与 Web 配置文件中授权规则的行为一致。

重写的 CanDelete 方法只调用继承的实现和 IsAuthorized 方法，如果两者都返回 true，则返回 true。CanInsert、CanUpdate 和 CanRead 方法的实现非常相似。它们仅在传递给 IsAuthorized 方法的 Actions 值上有所不同，例如，CanRead 方法使用 Actions.Read 而不是 Actions.Delete。

```csharp
public override bool CanRead(IPrincipal user)
{
    return base.CanRead(user) && this.IsAuthorized(user, Actions.Read);
}
```

使用 AuthorizationAttribute 实现 MetaTable 权限方法，比最初在单个方法中为多个实体硬编码规则的实现要简短得多。将最后一段代码片段与你在本章前面看到的下面的代码进行比较：

```csharp
public override bool CanRead(IPrincipal principal)
{
    if (this.Name == "Products") return true;
    if (this.Name == "Categories") return true;
    return principal.IsInRole("Employee");
}
```

当然，代码并没有消失；它只是从元模型移动到了各个实体类：

```csharp
[Authorization(
    Allow.Roles, "Manager",
    Allow.Users, "*", Actions.Read,
    Deny.Users, "*")]
partial class Product { ... }
```

尽管将规则应用于实体的安全系统更加冗长，封装性也不那么强，但实际上更容易维护。对于集中式硬编码实现，你所做的任何更改总是有可能影响无关实体的规则，而且对于一个规模适中的实体模型，真实的安全实现将比我们示例中的大很多倍，也复杂得多。然而，更重要的好处是能够在动态网页、普通网页以及其他应用程序中一致地强制执行它。

## 扩展 ObjectContext 以授权 Insert、Update 和 Delete 操作

你可以扩展 Entity Framework 的 ObjectContext 类，以利用 AuthorizationAttribute 并防止未经授权的 Insert、Update 和 Delete 操作。这样做使你能够在 Web 应用程序的自定义页面中强制实施动态页面已经强制实施的相同安全规则。

在第 8 章中，我们引入了 UnleashedObjectContext 基类，用于在 ObjectContext 级别执行验证。由于授权逻辑与验证非常相似，你可以使用相同的方法来实现它。具体来说，授权需要在 ObjectContext 类的重写 SaveChanges 方法中，在调用继承实现以持久化更改之前进行。下面是示例项目中 UnleashedObjectContext 类的实现方式：

