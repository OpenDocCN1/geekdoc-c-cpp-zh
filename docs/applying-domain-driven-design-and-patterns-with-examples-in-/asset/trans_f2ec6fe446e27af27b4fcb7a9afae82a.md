

这种处理方式意味着假日日历是一个可选依赖。通过构造函数依赖注入，我们提供两个构造函数来表达这一点，每个构造函数对应一组有效的依赖。

```csharp
public class BondPricer {
    private readonly IDiscountCurve curve;
    private readonly IHolidayCalendar calendar;

    public BondPricer(IDiscountCurve aCurve) {
        curve = aCurve;
    }
    public BondPricer(IDiscountCurve aCurve
        , IHolidayCalendar aCalendar) : this(aCurve) {
        calendar = aCalendar;
    }
}
```

也可以使用一个包含所有参数的构造函数，并为可选参数传入 `null`，但这会降低契约的明确性，尤其是当依赖数量增加时。因此，建议始终为每一组有效的依赖提供一个构造函数，并且尽可能地在构造函数之间进行链式调用。如果这看起来不可行，那么所涉及的类很可能拥有过多的依赖，应该进行拆分。

## Setter 依赖注入

正如这个恰当名字所暗示的那样，Setter 依赖注入使用 setter 而不是构造函数来注入依赖。因此，定价器有一个默认构造函数，但需要提供一个带 setter 的额外属性。

```csharp
public class BondPricer {
    private IDiscountCurve curve;

    public BondPricer() {
    }
    public IDiscountCurve DiscountCurve {
        set { curve = value; }
    }
}
```

Setter 注入提供了与构造函数注入相同程度的解耦，并且不难看出，在单元测试中创建定价器对象与构造函数注入一样简单。一个重要的区别是，在调用 setter 方法之前，定价器处于无效状态，而这在构造函数注入中是不会发生的。此外，我们不能将 `curve` 变量声明为 `readonly`，因为它没有在构造函数中初始化；最后，使用 setter 注入实现需要在所有依赖注入之后运行的最终初始化功能会更加棘手且容易出错。

尽管存在这些缺点，Setter 注入仍有其用武之地，因为它在依赖较多的组件上具有更好的扩展性。对于一个有三个可选依赖且严格使用构造函数注入的组件，我们将需要八个构造函数。有人可能会说该组件需要重构，但这并不总是可行的；在这种情况下，手头有一个模式是很好的。类似地，许多现有对象都有默认构造函数和属性，因此我们只能将它们与支持 Setter 依赖注入的 IoC 容器一起使用。

还有更多 Setter 依赖注入的变体，例如接口驱动的 Setter 依赖注入（Interface Driven Setter Dependency Injection），它使用标记接口来区分描述依赖的 setter 方法和其他公共 setter 方法。这些变体要么未被广泛使用，要么没有显著改变 setter 注入的关键特性，因此我在此不做讨论。

## 控制反转

在讨论了依赖注入模式及其具体实现之后，现在让我们转向控制反转（Inversion of Control），它也被称为好莱坞原则（Hollywood Principle）：“别给我们打电话，我们会打给你！”严格来说，IoC 不是一种模式，而是一个通用原则，它简单地表明对象应该依赖于其环境来提供其他对象，而不是主动获取这些对象。

从历史上看，IoC 一词经常被用来描述某些容器在运行时创建组件所采用的方法。Martin Fowler 在审视这些容器时提出了一个重要问题，即“它们反转了控制的哪个方面？”他建议我们将这些容器所实现的基于 setter 和构造函数的方法视为一种具体模式，并为它使用更具体的名称——依赖注入 [Fowler Inversion-OfControl]。这也使人们能够区分依赖注入模式和其他类型的 IoC。

一种遵循 IoC 原则但不是依赖注入变体的广泛使用的模式是上下文相关依赖查找（Contextualized Dependency Lookup）。对于我们的债券定价器而言，使用这种模式意味着我们继续使用一个类似注册表的类（在此模式中通常称为 context），但让容器将该 context 提供给我们的对象，这就是控制反转的方面。在代码中，可以如下所示：

```csharp
public interface IServiceContext {
    public Object GetInstance(String name);
}

public interface IComponent {
    public void Initialize(IServiceContext context);
}

public class BondPricer : IComponent {
    private IDiscountCurve curve;

    public void Initialize(IServiceContext context) {
        curve = (IDiscountCurve)context
            .GetInstance("MyBank.IDiscountCurve");
    }
}
```

仔细审视后，这种模式看起来像是服务定位器（Service Locator）和 Setter 依赖注入模式之间的混合体。这并非偶然，因为从历史上看，这种模式是最早的 IoC 模式之一，并且被证明是通往更优雅的依赖注入模式的重要垫脚石。

## 使用 Spring.NET 框架的依赖注入

Spring.NET 应用程序框架 [Spring.NET] 是广泛使用的 Java Spring 框架 [Spring] 的一个移植版本，它提供了一个非常灵活的 IoC 容器，支持各种形式的依赖注入。这个容器只是一个组件，实际上是一个带有多个实现的接口，负责加载配置并相应地设置对象。从历史上看，容器一词被用来说明 IoC 容器可以替代 Java 平台上的标准 J2EE 容器。

回到前面描述的构造函数注入示例，让我们研究如何使用 Spring.NET 提供的容器来获取已配置的定价器实例。

使用 Spring.NET 描述组件及其依赖的首选方式是使用 XML 配置文件。我们按类型声明对象，包括它们所加载的程序集，然后通过定价器声明中的嵌套 `constructor-arg` 元素来解析定价器对折扣曲线的依赖。

```xml
<objects>
<object name="DbCurve" type="MyBank.DatabaseDiscountCurve, MyBank"/>
<object name="DbPricer" type="MyBank.BondPricer, MyBank">
<constructor-arg><ref local="DbCurve"/></constructor-arg>
</object>
</objects>
```

为了在代码中访问对象，我们可以创建 `IApplicationContext` 的实例，让它从配置文件中加载配置，然后按名称请求对象。上下文确保所有依赖对象都会被创建并注入到需要的地方。

```csharp
IApplicationContext context = new XmlApplicationContext("spring.xml");
BondPricer pricer = (BondPricer)context.GetObject("DbPricer");
```

在实际应用中，直接使用应用程序上下文并不常见，因为这使得创建定价器的代码依赖于上下文。这非常类似于我们想要避免的类与注册表（Registry）模式中注册表之间的依赖。如果我们假设需要定价器的类是一个 Windows 窗体，我们可以为窗体本身使用依赖注入，并将窗体添加到 XML 配置中。现在，当窗体被创建时，定价器由容器注入，窗体无需处理应用程序上下文。

然而，在这种情况下，必须有其他代码来创建窗体，而这段代码会从上下文中查找窗体，因此会与上下文耦合。显然，不能一直嵌套依赖下去。为了解决这个问题，大多数容器都提供了与应用程序框架的集成，例如 Spring.Web，这样最初的应用程序特定组件（Windows 窗体和 Web 页面）就可以直接使用依赖注入，而由应用程序框架负责使用上下文来创建它们。如果某个特定的容器/框架组合没有集成，最好尽可能多地使用依赖注入，并将对上下文的依赖限制在一个类中。

