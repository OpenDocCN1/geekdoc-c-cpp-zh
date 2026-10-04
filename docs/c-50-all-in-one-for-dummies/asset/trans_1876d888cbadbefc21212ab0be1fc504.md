

## 642 开启你的 ViewModel 之旅

你可以在网上 http://ayende.com/projects/rhino-mocks/downloads.aspx 找到 RhinoMocks 工具。关于模拟对象（mocks）与存根（stubs）的良好描述，请参考 Martin Fowler 的论文《Mocks Aren't Stubs》，地址为：http://martinfowler.com/articles/mocksrentStubs.html。

![](img/6df7bb88e9302e98442acc219cfbd7fc_667_0.png)

## 模型仓库
该模式通常用于业务系统（Line of Business applications），以便在数据存储和模型类之间移动数据。对于示例 ViewModel，我包含了一个非常简单的接口（如列表 4-18 所示），它包含一个 `GetAll` 方法和一个 `Update` 方法（这完全不是一个仓库，但已涵盖示例所需的所有内容）。请注意使用泛型来对实现此接口的仓库强制执行强类型。

# 列表 4-18：仓库接口

```csharp
public interface IRepository<T>
{
    IList<T> GetAll();
    bool Update(T model);
}
```

示例中的仓库返回硬编码的值，而不是连接到数据存储。创建仅用于测试或原型制作的类是常见做法。我偏好的习惯是在名称末尾添加 `Fake` 来命名它们（如列表 4-19 所示），这样其他开发者对它们的意图就不会产生疑问。此外，示例没有实现 `Update` 方法，因为它们在 ViewModel 示例中没有被用到。

# 列表 4-19：Fake销售区域仓库

```csharp
public class SalesRegionRepository : IRepository<SalesRegion>
{
    public IList<SalesRegion> GetAll()
    {
        var list = new ObservableCollection<SalesRegion>
        {
            new SalesRegion (ID = 1, Name = "East"),
            new SalesRegion (ID = 2, Name = "Central"),
            new SalesRegion (ID = 3, Name = "West")
        };
        return list;
    }
    public bool Update(SalesRegion region)
    {
        throw new NotImplementedException();
    }
}
```

## 开启你的 ViewModel 之旅 643

为了创建一个客户，必须有一个销售区域列表可用，因此 `CustomerRepositoryFake`（如列表 4-20 所示）使用构造函数注入将允许的值插入仓库中。它本可以创建自己的列表，但由于对象不同，会导致 XAML 中的绑定失效。

什么是 Fake？单元测试人员需要编写“双重测试”：一个伪造或模拟真实对象的对象。通常，测试替体（test doubles）是查看原本不可渗透内部对象的唯一方法，或者该对象执行了你在测试期间不希望执行的操作。列表 4-20 中的伪 `SalesRegion` 仓库就是测试替体的一个示例。关于测试替体及其用途的更多信息，请访问网站 http://csharp12.info。为了测试目的而伪造某些事物是合理的做法。只需不要伪造你正在测试的对象以及它所使用的对象。

Practical WPF - 第4章

# 列表 4-20：Fake客户仓库

```csharp
public class CustomerRepositoryFake : IRepository<Customer>
{
    private readonly IList<SalesRegion> _salesRegions;

    public CustomerRepositoryFake(IList<SalesRegion> salesRegions)
    {
        _salesRegions = salesRegions;
    }

    public List<Customer> GetAll()
    {
        var list = new ObservableCollection<Customer>();
        var customer = new Customer(Name = "Jane Doe", ID=1, SalesRegion = salesRegions[0]);
        list.Add(customer);
        var customer = new Customer(Name = "John smith", ID=2, SalesRegion = salesRegions[1]);
        list.Add(customer);
        var customer = new Customer(Name = "John Doe", ID = 3, SalesRegion = salesRegions[2]);
        list.Add(customer);
        return list;
    }

    public bool Update(Customer customer)
    {
        throw new NotImplementedException();
    }
}
```

## 添加客户命令

有趣的是，使用 ViewModel 模式，命令可以在 ViewModel 出现之前开发，从而实现命令的测试驱动开发（TDD）。使用本章讨论的相同方法在本章早前的“命令基类”部分，提取了一个 `CommandBase` 类（如列表 4-21 所示），用于持有公共属性和 `CanExecute` 事件。

## 644 开启你的 ViewModel

# 列表 4-21：CommandBase : ICommand

```csharp
public abstract class CommandBase : ICommand
{
    public string Text { get; set; }
    public abstract void Execute(object parameter);
    public abstract bool CanExecute(object parameter);
    public event EventHandler CanExecuteChanged
    {
        add { CommandManager.QuerySuggested += value; }
        remove { CommandManager.QuerySuggested -= value; }
    }
}
```

`AddCustomer`（如列表 4-22 所示）接收列表作为参数并添加客户。在这个示例中，它是硬编码的值集，可能还没有窗口（或数据输入机制）来收集信息。

`Execute` 事件处理程序检查参数是否为 `List<Customer>`。在 `Execute` 方法中额外的检查是多余的——如果参数不是 `IList<Customer>`，命令不应执行。然而防御性编程介入了作用，始终检查以抛出错误。

# 列表 4-22：AddCustomer : CommandBase

```csharp
public class AddCustomerCommand : CommandBase
{
    public AddCustomerCommand()
    {
        Text = "Add Customer";
    }
    public override void Execute(object parameter)
    {
        var list = parameter as IList<Customer>;
        if (list == null)
        {
            return;
        }
        list.Add(new Customer (ID = 4, Name = 'New Customer'));
    }
    public override bool CanExecute(object parameter)
    {
        return parameter is IList<Customer>;
    }
}
```

## 添加客户单元测试

`AddCustomerCommand` 的测试与本章早前的“命令”部分相似。在列表 4-23 代码中，前三个测试验证了 `CanExecute` 事件；最后一个测试验证了 `Execute` 处理器。

## 防御性编程还是 try-catch？

编写额外的代码来防止异常还是放在 `try-catch` 块中更好？异常是昂贵的，通常不应被视为控制流设备。异常应该是“异常的”。

为什么这些示例没有 `try-catch`？仅仅是为了简洁。在任何实际代码中，日志和错误处理都是必要的，但可能会让读者带入远离本节概念的兔子洞。

# 列表 4-23：AddCustomerUnitTests

```csharp
[Test]
public void Should_Execute_If_Parameter_Is_Null()
{
    var cmd = new AddCustomerCommand();
    var canExecute = cmd.Execute(null);
    Assert.IsFalse(canExecute);
}

[Test]
public void Should_Execute_If_Parameter_Is_List_Customer()
{
    var cmd = new AddCustomerCommand();
    var canExecute = cmd.Execute("");
    Assert.IsFalse(canExecute);
}

[Test]
public void Should_Execute_If_Parameter_Is_List_Customer()
{
    var cmd = new AddCustomerCommand();
    var canExecute = cmd.Execute(new List<Customer>());
    Assert.IsTrue(canExecute);
}

[Test]
public void Should_Add_Customer_To_List_On_Execute()
{
    var cmd = new AddCustomerCommand();
    var customers = new List<Customer>();
    var count = customers.Count;
    cmd.Execute(customers);
    Assert.AreEqual(count+1, customers.Count);
}
```

## ViewModel
所以，你现在心里在想：“到目前代码有点枯燥。而且我们甚至还没有碰到 ViewModel 呢？”你是对的。然而，正如你所看到的，由于你已经做了准备，ViewModel 变成了一个相当微不足道的练习。ViewModel 中只有三个属性，以及需要在构造函数中运行的两行代码（其中一个是 XAML 渲染引擎要求的）。是的，就是这样。

图4-6 中的图像包含两个需要填充的组合框（combo boxes）。ViewModel 模式的原则之一是为视图提供一站服务。除了主数据（客户），还包括引用数据（销售区域）。ViewModel（如列表 4-24 所示）包含这些 `IList<T>` 属性，它们可以绑定到视图并在在本示例中于构造函数中进行填充。

窗口还包含一个需要绑定到 `AddCustomerCommand` 的单个按钮。命令需要更多的管道工作，因为它们在使用之前必须实例化。此示例中显示的技术是即时实例化，旨在减少资源消耗。如果按钮从未被点击，为什么要在内存中保留命令？

# 列表 4-24：ViewModel

```csharp
public class CustomerMaintenanceViewModel
{
    private ICommand _addCustomerCmd;

    public CustomerMaintenanceViewModel()
    {
        Regions = new SalesRegionRepositoryFake().GetAll();
        Customers = new CustomerRepositoryFake(Regions).GetAll();
    }
    public IList<Customer> Customers { get; set; }
    public IList<SalesRegion> Regions { get; set; }

    public ICommand AddCustomerCmd()
    {
        get { return _addCustomerCmd ?? (_addCustomerCmd = new AddCustomerCommand(this)); }
        set { _addCustomerCmd = value; }
    }
}
```

## 视图
在这个 ViewModel 中实际上没有可以测试的内容，因为它们已经在其他地方测试过了。但如果 ViewModel 确实包含需要测试的代码，你可以像测试任何其他类库一样测试它。

关于视图，有几个值得注意的。。首先，视图的构造函数需要将 `DataContext` 赋值给 ViewModel 的实例（参见列表 4-25 中的加粗行）。

