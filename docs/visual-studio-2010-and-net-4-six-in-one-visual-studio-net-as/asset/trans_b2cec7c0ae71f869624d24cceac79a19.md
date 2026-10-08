

```cs
public string CustomerTable
{
    get { return "Customer_"; }
}
```

`DalParameters` 类有两个导入部分，分别由静态字段 `MaxRows` 和实例属性 `CustomerTable` 表示。由于它们对应的类型（`int` 和 `string`）是 CLR 原生类型，因此无法向这些类导入 `Export` 特性来表示它们。使用命名合约，你可以导入这些部分：

```
[Import("MaxRowsRetrieve")]
public int MaxRows { get; private set; }

[Import("CustomerTable")]
public string CustomerTableName { get; private set; }
```

如果将 `Export` 应用于字段或属性，MEF 将在组合时使用该属性或字段的值。这种方法还有一个额外的优点：

- 你可以在同一个类型中拥有一个或多个相关的导出项。
- 你可以导入密封类型、CLR 原生类型和第三方类型。
- 你可以将导出与它的创建方式解耦。

此外，MEF 的功能不仅限于属性和字段 —— 你可以导出方法！在这种情况下，方法被导出为由合约类型指示的委托。

假设你有一个具有 `Name` 和 `State` 字符串属性的 `Customer` 类。你可以定义一个可以过滤客户的部分：

```cs
public class CustomerFilter
{
    [Export("CustomerFilter", typeof(Func<Customer, bool>))]
    bool LivesInCA(Customer customer)
    {
        return customer.State == "CA";
    }
}
```

注意，`Export` 特性显式声明了代表合约的委托类型。如果没有它，MEF 将无法推断出委托类型作为默认合约类型。你可以将此部分绑定到想要轻松过滤客户的程序：

```cs
[Export]
class CustomerProcessor
{
    [Import("CustomerFilter")]
    Func<Customer, bool> Filter { get; set; }

    public void ProcessCustomers(IEnumerable<Customer> customers)
{
  foreach (var customer in customers.Where(Filter))
    Console.WriteLine(customer.Name);
}
}
```

这一次，合约是通过名称 `CustomerFilter` 和类型 `Func<Customer, bool>` 指定的。由于 `Func<Customer, bool>` 是一个可能频繁使用的类型，因此为合约使用一个区分性名称更为具体。MEF 能够从委托属性定义中推断类型，但你必须在 `Import` 特性中声明你的合约。

目前框架中有一个局限性 —— 方法导出不能有四个以上的参数。

方法导出为你提供了一个与其他导出项连接的机会 —— 轻量级代码生成。通过 .NET Framework，你可以动态生成类型和方法，并从导出的方法调用这些方法。

你可以用 `Import` 特性修饰字段和属性 —— 示例展示了这有多简单。在组合时，MEF 负责设置这些属性和字段的值。你没有义务使用 `public` 修饰符。你也可以使用其他修饰符标记成员，并可以使用私有字段和方法。然而，不要忘记归根结底，MEF 将能够设置成员的值。在设计组件时，你必须考虑以下几个后果：

- 在中等或受信任环境中，MEF 无法设置非公共成员。
- 如果你使用只读属性（只有 `get` 访问器的属性），MEF 将无法设置该属性的值，组合将失败。

# 组合容器与目录

导出的和导入的部分必须组合才能在应用程序中工作。这一角色由组合容器承担。它的名称准确地说明了它被假设的功能。它是一个容器，因为它包含了声明与其他组件共享服务（导出）的意图，以及愿意消费其他部分提供的服务（导入）的部分。组合容器是将销售服务的部分与购买服务的部分绑定在一起的匹配器。

组合容器是你必须与之交互的实体，以控制组合过程或查询信息（例如，代表特定合约的部分列表）。

你可以直接将部分添加到组合容器。例如，构建 `MefGreetings` 的部分可以通过以下代码进行组合：

```cs
var container = new CompositionContainer();
container.ComposeParts(this,
new SimpleGreeting(),
new UserGreeting(),
new AppInfo());
```

这个解决方案有一个重大问题 —— 它是静态的。这种方法明确列出了组成应用程序的部分。它使用了编译时已知的类型，并且缺乏部分的动态发现。

相反，`MefGreetings` 示例利用目录（catalog）构建组合容器：

```cs
var catalog = new AssemblyCatalog(Assembly.GetExecutingAssembly());
var container = new CompositionContainer(catalog);
container.Compose(this);
```

MEF 中的目录是包含部分的清单的抽象。目录的伟大之处在于它具有动态行为。它的内容是在运行时确定的，因此可以用于动态发现。例如，代码段中使用的 `AssemblyCatalog` 是包含特定物理程序集中所有可组合部分的清单。

MEF 默认带了多个目录。表 10-9

# 10-9: MEF 目录

| 类型名称 | 描述 |
|------|---|
| TypeCatalog | 此目录是类型的容器。在发现期间，将收集被目录中类型所利用的所有导出项。当你确切知道提供导出项的类型时，可以使用它 —— 例如，当你创建单元测试时。 |
| AssemblyCatalog | 此目录发现指定程序集中的所有导出项。当你知道哪些程序集包含部分时，可以使用它。通过 `AssemblyCatalog`，你为应用程序增加了灵活性。 |
| DirectoryCatalog | 此目录发现目录中的所有导出项。当你知道路径时，可以使用它。创建 `DirectoryCatalog` 为你的应用程序引入了动态性。 |
| AggregateCatalog | 如该类型名称所示，它将多个目录合并成单个目录。一种常见的模式是聚合多个 `DirectoryCatalog` 实例。 |

MEF 允许你创建自己的目录。例如，当将部分存储在数据库中时，你可以创建一个 `DatabaseCatalog`。

# 部分与元数据

在许多情况下，你可能会与导出项关联信息，以对组合提供更细粒度的控制。以下是控制可能重要的简单列表：

- 合约具有某些实现提供的功能，而其他实现没有。例如，某个部分只有在运行应用程序的计算机安装了软件（例如 Microsoft Word）时才能工作。
- 部分旨在提供有关其自身的某些信息，供其潜在消费者使用。例如，实现新用户控件的部分可能会告诉其主窗口它必须停留在底部。
- 部分可以提供关于自己的信息，这些信息决定了消费者如何处理它的服务。假设你的部分代表由处理器处理的管道中的一个步骤。处理器按特定顺序执行这些步骤，因此你必须为你的部分分配正确的顺序信息。

MEF 允许向导出项附加元数据。这些信息可以在组合引擎在匹配期间使用，并被部分的消费者访问以便它们利用这些数据。

`ExportMetadata` 特性提供了为部分添加此类信息的最简单方法。例如，你可以看到你的组件可能涉及数据库事务：

```cs
[Export(typeof(IDabaseTask))]
[ExportMetadata("SupportsTransaction", true)]
[ExportMetadata("PMC", "Remove_Customer")]
public class RemoveCustomerTask: IDabaseTask
{
    // ...
}
```

```cs
[Export(typeof(IDabaseTask))]
[ExportMetadata("SupportsTransaction", false)]
public class CalculateBonusTask: IDabaseTask
{
    // ...
}
```

`ExportMetadata` 的参数是键值对。你可以根据需要向导出项附加尽可能多个元数据属性。然而，如你所见，这种类型的元数据是弱类型的。MEF 允许向导出项附加强类型元数据 —— 此外，它鼓励你这样做。你可以创建自己的元数据属性。以下代码段是使用此功能的示例：

```cs
[MetadataAttribute]
[AttributeUsage(AttributeTargets.Class, AllowMultiple=false)]
public class LmMetadataAttribute: Attribute
```

