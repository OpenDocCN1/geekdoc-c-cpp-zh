
```csharp
[Test]
public void Should_Not_Execute_If_Parameter_Is_Empty_String()
{
    ICCommand command = new CustomSaveCommand("Save");
    bool canExecute = command.CanExecute(string.Empty);
    Assert.IsFalse(canExecute);
}
```

```csharp
[Test]
public void Should_Execute_If_Parameter_Is_Not_Empty_String()
{
    ICCommand command = new CustomSaveCommand("Save");
    bool canExecute = command.CanExecute("Test");
    Assert.IsTrue(canExecute);
}
```

## 获取你的 ViewModel

设计模式已经存在相当长时间了。随着时间的推移，一些旧模式失效，新的模式被创建以满足需求。一种在 WPF 和 Silverlight 中获得广泛关注的模式是模型-视图-模型。通常被称为“ViewModel”（尽管这在微软内部变动很大），这种模式与 Martin Fowler 的 Presentation Model 非常相似。

![](img/3659fb11aa4233d5cab0dddd1d82_637_0.png)

你可以在此处阅读 Martin Fowler 关于 Presentation Model 的文章：http://martinfowler.com/eaaDev/PresentationModel.html

## 关心

我知道你在想。“为什么我不能直接坐下来用我学到的所有东西来编写 WPF 应用呢？”短答案是，你可以。但你应该这样做吗？在喜欢讨论这些事情的人中仍在争论。使用一种促进关注点分离、减少重复代码、提高可测试性并降低复杂性的用户界面模式（例如 ViewModel）将有所帮助。

> “使用这些模式之一会使开发花费更长时间吗？”这是一个常见问题，答案是肯定的，“取决于”。一旦开发者完全理解了目标和技术，速度（团队在给定时间内完成的工作量）就会跟上。要达到这种理解水平，需要时间，并且通常伴随着反复尝试。

## MVVM? ViewModel? 谁在第一？

该模式的多个版本正在流传，还有同样数量的“框架”。它们似乎都有不同的名称和实现方式。MVVM 是一个新创建的模式（模式会更替），目前很少人试图让“自己的”名称固定下来。最终，名称并不如获得的益处重要。

当出现更改请求时（用户称之为“bug”，但我更倾向于使用不同的命名法），如果你使用的是确保关注点分离的演示模式，那么很清楚应该去代码库的哪个位置解决该问题。传统的开发风格（如在 Windows Forms 中常用的样式）非常很容易将业务代码置于事件处理器和代码后文件（code-behind files）中，从而导致关注点和依赖混合。

第五卷

第四章

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_638_0.png)

# 传统！

为了充分理解 ViewModel 模式如何提供帮助，你需要了解“传统”应用程序架构的部分。

## 数据访问层 (DAL)

`DAL` 是一组从数据存储（如 SQL Server）获取数据并填充 Model（见下一项）的类和方法。它还负责将数据的更改持久化回数据存储。

## Model

`Model` 是组成你的应用程序的数据——不是存储器（例如数据库），而是表示应用程序数据的对象图。在销售应用程序中，示例对象可以是像 `Customer`（客户）、`SalesRegion`（销售区域）和 `SalesPerson`（销售人员）这样的类。

## 业务层 (BL)

`BL` 是应用程序业务规则的实现。该层确保 `Model` 中的数据符合业务规则。

## View

`View` 代表与用户交互的应用程序部分。对于 WPF 来说，这就是组成应用程序的 Window 集合。

在 View 中显示对象图（Model）时，最大的差距是应用程序很少一次只显示一种类型的对象。窗口允许编辑一个客户，然后它可能需要显示销售区域，依此类推。

将多个对象组合成一个数据对象会模糊 Model，而将所有代码放在视图中会使 View 负载过多的知识——更不用说测试性的失败了。对象图所需部分的编译不应该影响应用程序的任何其他部分。

命令对象（Command Objects）是另一个考虑因素。在传统的应用程序层中，没有整洁的地方放置自定义命令。命令中包含的代码（通常）是业务逻辑，但 View 需要绑定到这些命令，因此它是特定于 View 的。

# ViewModel

`ViewModel` 填补了这个空白。它被设计成一个类，将所有必要的数据点和命令汇集到特定视图的一站式服务中。每个视图通常有自己的 ViewModel，但这完全取决于你的特定应用程序。

正如第 3 章所讨论的，WPF 会自动监控实现了 `INotifyPropertyChanged`（针对绑定到类属性的项）和/或 `INotifyCollectionChanged`（针对绑定到项集合的项）的任何类。这些接口应该在两个阵营之一实现——ViewModel 或 Model。

在 ViewModel 中实现这两个接口是更学术化、教科书式的实现。这是因为将用户界面与 Model 分离开。这还需要大量的额外工作，因为它意味着重新编写 Model 的所有属性和集合以包含引发适当的事件。

在 Model 中实现可以减少工作量，因为只需要在类中已实现的属性中添加几行代码。反对 Model 实现的一个主要论点围绕代码复用。例如，如果 Model 被用作 ASP.NET 应用程序，这些事件仍然会被触发，但没有人在监听。这可能防止出现性能问题。当然，如果你为 WPF 和非 WPF View 使用相同的模型，那么通过向 Model 类的构造函数传递一个简单的标记来指示是否应该触发事件，就可以解决该问题。

两种方式都是有效的实现。特定的具体情况可能会决定这些接口在何处实现。

在第 3 章中，你会发现如果一个控件没有显式的 `DataContext`，它将继承自控件树中显式分配了 `DataContext` 的最近父节点。

在使用 ViewModel 模式开发 WPF 应用程序时，实例化的 ViewModel 成为 Window（或用户控件）的 `DataContext`。

# 查看代码！

ViewModel 示例的完整代码位于 Chapter4 解决方案中的 Chapter4ViewModels 和 Chapter4ViewModelTests 项目中。

# 我们在构建什么？

Window（或者用“架构术语”来说）是一个简单的客户维护表单。用户可以选择一个客户并编辑他的名字和

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_639_0.png)

销售区域。点击“添加客户”（Add Customer）按钮会将客户添加到列表中。你是对的——这并不现实，但它展示了 ViewModel 的原则。图 4-6 显示了完整的示例用户界面。

# 图 4-6：客户维护

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_640_0.png)

# Model

好了，话得多了了。对于示例 ViewModel，我们需要定义一个 Model。

列表 4-12 显示了所有 Model 类将派生的基类。该基类实现了 `INotifyPropertyChanged` 接口以及 `IsDirty` 属性。

# 列表 4-12：ModelBase

```
public class ModelBase : INotifyPropertyChanged
{
    public bool IsDirty { get; private set; }
    public event PropertyChangedEventHandler PropertyChanged;
    internal void NotifyPropertyChanged(object sender, string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(sender, new PropertyChangedEventArgs(propertyName));
        }
        IsDirty = true;
    }
}
```

列表 4-13 和 4-14 显示了填充 View 的 Customer 和 Sales 类。对于类中的每个属性（除主键和集合属性外），都有检查检查查看设置的属性值是否为新值。如果是新值，则会触发 `PropertyChanged` 事件。`NotifyPropertyChanged` 方法还会将 `IsDirty` 标记置为 True，以指示模型有需要持久化的更改。

# 为什么用“internal”？

`NotifyPropertyChanged` 方法标记为 `internal` 访问修饰符而不是 `protected` 是出于一个原因——测试。`protected` 方法只能从派类访问，而 `internal` 方法可以被同一程序集中的任何子类访问。程序集级别的属性 `InternalsVisibleTo` 指定了哪些程序集可以访问被装饰的程序集的内部方法和类。将此属性添加到 Chapter4ViewModels 项目（通常放置在 assemblyinfo.cs 类中）并指定测试项目（Chapter4ViewModelsTests），将允许你的测试访问这些内部成员。

主键（在本例中）是由数据存储设置的，因此它在视图中永远不会改变。因为永远不需要触发属性更改事件，该属性可以被编码为自动属性。

### 列表 4-13：Customer Model

```
public class Customer : ModelBase {
    private string _name;
    private SalesRegion _region;
    public int ID { get; set; }
    public string Name {
        get { return _name; }
        set {
            if (value == _name)
                return;
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
    public SalesRegion Region {
        get { return _region; }
        set {
            if (value == _region)
                return;
        }
    }
}
```

### 列表 4-14：SalesRegion:Model 类

```
public class SalesRegion:ModelBase{
    private string _name;
    public int ID { get; set; }
    public string Name
    {
        get { return _name; }
        set{
            if (value == _name)
                return;
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
}
```

# Model 单元测试

 Model 中没有可测试的内容。通常不会针对 .NET Framework 本身编写测试——必须假设它可以工作！此示例中真正的逻辑是设置 `IsDirty` 以及在发生更改时引发 `PropertyChanged` 事件。

第一个测试是验证在属性更改时是否设置了 `IsDirty`，这非常直观。我们创建一个 `Customer`，断言 `IsDirty` 标记为 False，进行更改，然后断言 `IsDirty` 标记为 True。该测试显示在列表 4-15 中。

# 列表 4-15：测试 IsDirty 标记

```
[Test]
public void Should_Set_Is_Dirty_On_Property_Change(){
    var sut = new Customer();
    Assert.IsFalse(sut.IsDirty);
    sut.Name="New Name";
    Assert.IsTrue(sut.IsDirty);
}
```

## 为什么用 "SUT"？

变量名代表“被测试系统”（System Under Test），是单元测试中的常用惯例。它清晰地将被测试的对象与测试所需的其他对象区分开来。为什么之前的示例没有使用它呢？啊，小菜鼠——这是为了循序渐进地引入，让你不至于被信息像洪水一样冲没。

第二个测试要复杂得多，因为它测试了 `PropertyChanged` 事件的触发。我们需要创建一个订阅者来监听此事件。Windows（以及 WPF 渲染引擎）会自动附加到此事件，而我们不想为了测试一个方法就重新创建渲染引擎。要测试该事件，需要创建一个订阅者、触发事件，然后断言事件处理程序已执行。

此类类型的测试通常使用模拟框架（mocking framework）完成，例如 Mocks（示例中使用的工具）。模拟框架允许除状态测试之外的行为测试，由于测试需要验证事件是否已触发，RhinoMocks 是完美的选择。深入研究模拟和行为测试超出了本书的范围。请观察代码、理解并尝试修改。这是扩展你测试知识的绝佳方法！

模拟框架基于接口创建代理对象。对于单个事件，创建一个接口（如列表 4-16 所示），它具有处理程序所需的签名——在这种情况下，即 `PropertyChanged` 事件。

### 列表 4-16：事件订阅者

```csharp
public interface IPropertyChangedSubscriber
{
    void Handler(object sender, PropertyChangedEventArgs e);
}
```

测试开始时会创建一个订阅者的 mock，并将处理程序注册到 `PropertyChanged` 事件。测试通过更改名称对 `Customer` 对象进行操作，并断言处理程序已被调用。`Arg<object>.Is.Any` 语法告诉 Mocks 不要测试参数的等价性。再次，该测试仅仅是验证当 `Customer` 对象上的属性更新时是否触发了事件。请看列表 4-17 中的代码。

## 开始你的 ViewModel之旅

### 列表 4-17：测试事件是否触发

```csharp
[Test]
public void ShouldRaise_Property_Changed_Event_On_Property_Change()
{
    var sut = new Customer();
    var eventArgs = new PropertyChangedEventArgs(string.Empty);
    var subscriber = MockRepository.GenerateMock<IPropertyChangedSubscriber>();
    sut.PropertyChanged += subscriber.Handler;
    sut.Name = "New Name";
    subscriber.AssertWasCalled(x => x.Handler(Arg<PropertyChangedEventArgs>.Is.Anything()));
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_644_0.png)

可以在网上找到 MockTools：http://ayende.com/projects/rhino-mocks/downloads.aspx。关于 mock 和存根（stubs）的良好描述，请参考 Martin Fowler 的论文《Mocks Aren't Stubs》，地址为：http://martinfowler.com/articles/mocksArenStubs.html。

## 模型仓库 (Model repositories)

仓库模式通常用于业务逻辑驱动的应用程序，以便在数据存储和模型类之间移动数据。对于示例中的 ViewModel，我包含了一个非常简单的接口（如列表 4-18 所示），它包含 `GetAll` 和 `Update` 方法（远不是完整的仓库，但已满足示例所需）。请注意泛型使用，以便在实现此接口的仓库中强制执行严格类型。

### 列表 4-18：仓库接口

```csharp
public interface IRepository<T>
{
    IList<T> GetAll();
    bool Update(T model);
}
```

示例中的仓库返回硬编码的值，而不是连接到数据存储。创建仅用于测试或原型设计的类是一种常见做法。我倾向的惯例是在名称后添加 `Fake`（如列表 4-19 所示），这样其他开发者就不会对其预期用途产生疑问。此外，示例没有实现 `Update` 方法，因为它们在所示的 ViewModel 示例未使用。

## 状态与行为测试

状态测试测试对象的值（例如 `IsDirty` 标志是否被设置）。行为测试用于测试对象的动作和交互。使用像 RhinoMocks 这样高级的框架，测试特定方法是否被调用或事件是否触发变得非常简单。

### 列表 4-19：Fake SalesRegion 仓库
