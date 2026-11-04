

```
}
_region = value;
NotifyPropertyChanged(this, "SalesRegion");
}
}
```

## 清单 4-14：SalesRegion 模型类

```
public class SalesRegion:ModelBase
{
    private string _name;
    public int ID {get; set;}
    public string Name
    {
        get { return _name; }
        set
        {
            if (value == _name)
            {
                return;
            }
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
}
```

## 模型单元测试

模型中需要测试的内容不多。你通常不会针对 .NET Framework 本身编写测试——只能假定它能正常工作！本示例中唯一的真实逻辑是设置 IsDirty 标志，以及在发生变化时引发 PropertyChanged 事件。

第一个测试用于验证当属性变化时 IsDirty 标志是否会被设置，这非常直接。我们创建一个新的 Customer，断言 IsDirty 标志为 False，做一次更改，然后断言 IsDirty 标志为 True。该测试如清单 4-15 所示。

## 清单 4-15：测试 IsDirty 标志

```
[Test]
public void Should_Set_Is_Dirty_On_Property_Change()
{
    var sut = new Customer();
    Assert.IsFalse(sut.IsDirty);
    sut.Name="New Name";
    Assert.IsTrue(sut.IsDirty);
}
```

### 为什么是“SUT”？

这个变量名代表“被测系统”，是单元测试中的常见约定。它清晰地划定了被测对象与测试所需的其他对象之间的界限。为什么前面的示例没有使用这种命名？啊，新手——这是在循序渐进地引导，免得让你一下子接受不了太多东西！

第二个测试要复杂得多，因为它测试 PropertyChanged 事件的引发。我们必须创建一个订阅者来监听此事件。Windows（以及 WPF 渲染引擎）会自动挂接此事件，但我们不想为了测试一个方法而重新创建渲染引擎。要测试该事件，需要创建一个订阅者，引发事件，然后断言事件处理程序已被执行。

此类测试通常使用模拟框架来完成，例如 RhinoMocks（示例中使用的工具）。模拟框架不仅允许测试状态，还允许测试行为；由于测试需要验证事件是否被引发，RhinoMocks 非常合适。深入探讨模拟和行为测试超出了本书的范围。研究一下代码，消化它，并动手修改它。这是扩展你测试知识的好方法！

模拟框架基于接口创建代理对象。对于单个事件，创建一个接口（如清单 4-16 所示），该接口包含事件处理程序所需的签名——在本例中即 PropertyChanged 事件。

### 清单 4-16：事件订阅者

```csharp
public interface IPropertyChangedSubscriber
{
    void Handler(object sender, PropertyChangedEventArgs e);
}
```

测试首先创建一个订阅者的模拟对象，并将 PropertyChanged 事件与处理程序注册。测试通过更改名称来作用于 Customer 对象，然后断言处理程序被调用。`Arg<object>.Is.Anything` 语法告诉 RhinoMocks 不要测试参数是否相等。再次强调，该测试只是在验证当 Customer 对象上的属性更新时，事件是否被引发。参见清单 4-17 中的代码。

## 清单 4-17：测试事件是否被引发

```
[Test]
public void Should_Raise_Property_Changed_Event_On_Property_Change()
{
    var sut = new Customer();
    var eventArgs = new PropertyChangedEventArgs(string.Empty);
    var subscriber = MockRepository.GenerateMock<IPropertyChangedSubscriber>();
    sut.PropertyChanged += subscriber.Handler;
    sut.Name = "New";
    subscriber.AssertWasCalled(x => x.Handler(Arg<object>.Is.Anything, Arg<PropertyChangedEventArgs>.Is.Anything));
}
```

RhinoMocks 工具可在网上 http://ayende.com/projects/rhino-mocks/downloads.aspx 找到。关于 mock 与 stub 的详细说明，请参阅 Martin Fowler 的论文《Mocks Aren't Stubs》，网址为 http://martinfowler.com/articles/mocksArentStubs.html。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_644_0.png)

## 模型仓储

仓储模式通常用于业务应用程序，以在数据存储和模型类之间移动数据。对于示例 ViewModel，我提供了一个非常简单的接口（如清单 4-18 所示），其中包含一个 GetAll 方法和一个 Update 方法（这远不是一个完整的仓储，但已经足够用于示例）。注意，使用泛型来强制实现此接口的仓储具有强类型。

## 清单 4-18：仓储接口

```
public interface IRepository<T>
{
    IList<T> GetAll();
    bool Update(T model);
}
```

示例中的仓储返回硬编码值，而不是连接数据存储。常见的做法是创建仅用于测试或原型的类。我偏好的约定是在名称后面附加“Fake”来标识它们（如清单 4-19 所示），这样其他开发人员就不会对其预期用途产生疑问。此外，示例没有实现 Update 方法，因为它们不用于所展示的 ViewModel 示例。

## 状态测试与行为测试

基于状态的测试测试对象的值（例如，IsDirty 标志是否被设置）。行为测试用于测试对象的操作和交互。使用像 RhinoMocks 这样更高级的框架，测试某个特定方法是否被调用或某个事件是否被引发会变得简单得多。

## 清单 4-19：Fake SalesRegion 仓储

```
public class SalesRegionRepositoryFake : IRepository<SalesRegion>
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

要创建客户，必须有一个可用的销售区域列表，因此 Customer Repository Fake（如清单 4-20 所示）使用构造函数注入将允许的值插入仓储。它本来可以创建自己的列表，但这会破坏 XAML 中的绑定，因为对象将是不同的。

## 清单 4-20：Fake Customer 仓储

```
public class CustomerRepositoryFake : IRepository<Customer>
{
    readonly IList<SalesRegion> _salesRegions;
    public CustomerRepositoryFake(IList<SalesRegion> salesRegions)
    {
        _salesRegions = salesRegions;
    }
    public IList<Customer> GetAll()
    {
        var list = new ObservableCollection<Customer>();
        var customer = new Customer { Name = "Jane Doe", ID=1,
        SalesRegion = _salesRegions[0]};
        list.Add(customer);
        customer = new Customer { Name = "John Smith", ID=2,
        SalesRegion = _salesRegions[1]};
        list.Add(customer);
        customer = new Customer { Name = "John Doe", ID = 3,
        SalesRegion = _salesRegions[2] };
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

有趣的是，使用 ViewModel 模式，可以先于视图开发命令，从而实现对命令的测试驱动开发。采用本章前面“Commanding Attention”一节中讨论的相同方法，提取了一个 CommandBase 类（如清单 4-21 所示）来持有公共属性和 CanExecuteChanged 事件。

## 清单 4-21：CommandBase 类

```csharp
public abstract class CommandBase : ICommand
{
    public string Text { get; internal set; }
    public abstract void Execute(object parameter);
    public abstract bool CanExecute(object parameter);
    public event EventHandler CanExecuteChanged
    {
        add { CommandManager.RequerySuggested += value; }
        remove { CommandManager.RequerySuggested -= value; }
    }
}
```

AddCustomerCommand（如清单 4-22 所示）将以 Customer 列表作为参数，并向列表中添加另一个客户。在本示例中，它是一组硬编码的值，但实际上你可能会使用另一个窗口（或某种数据输入机制）来收集所需信息。

