
多样性，并且对于此容器，自动装配是首选方案。

使用 PicoContainer.NET，使容器能够解析依赖并创建对象所需的唯一步骤就是将具体的实现类注册到容器中。

```
IMutablePicoContainer pc = new DefaultPicoContainer();
pc.RegisterComponentImplementation (typeof(DatabaseDiscountCurve));
pc.RegisterComponentImplementation ("pricer", typeof(BondPricer));
```

通过将声明放入代码中，我们消除了冗余，并且获得了 IDE 的更好支持，因为它现在能够检测拼写错误的类名，并且可以在自动重构中安全地重命名类型。

对象是从容器中获取的，方式几乎与从 Spring.NET 中的 application context 获取的方式相同，因此关于对容器的依赖的相同考虑也适用：几乎所有类都应使用依赖注入，只留下一个中心类与容器交互以获取初始组件。

```
BondPricer pricer = (BondPricer)container.GetComponentInstance("pricer");
```

前面的示例还表明，除了使用类型系统之外，PicoContainer.NET 还支持命名组件：本例中的 pricer。这使得可以在不指定其类型的情况下查找对象，从而引入了另一个解耦程度。

可选依赖会自动处理，因为 PicoContainer.NET 使用它能够满足依赖的最复杂的构造函数。在前面的示例中，PicoContainer.NET 使用 BondPricer 的一个参数构造函数，它只接受一个曲线，但如果我们添加假日日历的注册，PicoContainer 在获取 pricer 对象时将使用两个参数的构造函数。

```
IMutablePicoContainer pc = new DefaultPicoContainer();
pc.RegisterComponentImplementation (typeof(DatabaseDiscountCurve));
pc.RegisterComponentImplementation(typeof(HolidayCalendar));
pc.RegisterComponentImplementation ("pricer", typeof(BondPricer));
```

就对象依赖而言，使用基于类型的自动装配而不是基于配置文件的方案并不会失去任何灵活性，同时我们还能受益于改进的开发体验。自动装配如果一个类在其构造函数中期望参数，例如主机名、端口号和超时时间，则效果不佳，因为原始类型并不能传达太多关于其预期用途的信息。如果我们向容器注册两个整数，一个指定端口号，另一个指定超时时间，容器将两者都视为整数，无法确定在接受一个整数的构造函数中使用哪一个。

根本问题在于容器是否应以与处理配置参数设置相同的方式支持必需组件的注入，或者是否将这两个需求视为不同的关注点，应针对每个关注点采用最合适的方案来处理。基于类型的自动装配在管理依赖关系时 arguably 比配置文件更有优势，因此可以为此目的使用自动装配。在同一场景中，配置参数可以用命名属性的 setter 设置，这对于该目的 arguably 更直观。

可用于 .NET 平台的第三个 IoC 容器是 Windsor，它是 Castle 项目 [Castle] 的一部分。Castle 项目的核心容器实现，开发者称之为 micro-kernel，使用基于类型的自动装配，但它也允许插件添加额外的依赖解析策略。基于 micro-kernel 的 Windsor 容器 [Windsor] 添加了对配置文件的支持，从而允许开发者选择最合适的机制。这是 NanoContainer [NanoContainer] 成功开创的一种方法，NanoContainer 是一个 Java 容器，构建在 PicoContainer 的 Java 版本之上。

## 嵌套容器

Spring.NET 中的容器被命名为 ApplicationContext 这一事实暗示了容器为从容器中检索组件的对象定义了一个上下文。这些对象与返回的对象交互，其行为取决于容器提供的具体实现；因此，容器可以被视为提供对象所作用的上下文的提供者。该名称进一步暗示，从配置文件创建的上下文是应用范围的，并且应用程序中的所有查找共享相同的上下文。

Web 应用程序使用多个上下文，大多数 Web 框架以 application、session 和 request 对象的形式明确表示它们。请求处理代码，例如 Web 页面背后的代码，通常依赖于多个组件。某些组件是应用程序上下文的一部分，因为它们可以被所有请求处理器共享，而其他组件是单个请求上下文的一部分，因为它们只能被单个请求使用。

一些 IoC 容器实现支持此模型并允许容器嵌套，这意味着一个容器可以有一个父容器，并且作为直接结果，有子容器。当容器无法满足创建组件所需的所有依赖项时，它会尝试从其父容器获取缺失的组件，而父容器反过来可以从其自己的父容器请求组件。这种设置大致类似于职责链设计模式 [GoF Design Patterns]。

例如，考虑创建具有数据库连接和记录器依赖的请求处理器或页面。数据库连接一次只能被一个请求使用，而记录器可以被所有请求共享。然而，这与请求处理器无关。

```
public ResultPage : Page {
    private Logger logger;
    private IDbConnection connection;

    public ResultPage(Logger aLogger, IDbConnection aConnection) : base() {
        logger = aLogger;
        connection = aConnection;
    }
}
```

在我们的应用程序中，一个容器与应用程序相关联。此外，每个会话都有一个子容器，并且对于会话中的每个请求，都会创建相应会话容器的子容器。我们的应用程序将请求 URL 映射到页面类型，并且包含以下通用代码，用于为给定页面类型创建新的请求处理器：

```
public RequestHandlerFactory {
    IPicoContainer sessionContainer;

    public Page CreatePage(Type pageType) {
        IImmutablePicoContainer reqContainer = CreateRequestContainer();
        reqContainer.RegisterComponentImplementation(pageType);
        return (Page)reqContainer.GetComponentInstance(pageType);
    }
    private IImmutablePicoContainer CreateRequestContainer() {
        IImmutablePicoContainer pc = new DefaultPicoContainer(sessionContainer);
        pc.RegisterComponentImplementation (typeof(SqlDbConnection));
        /* register all other components here that should be available
           to requests on a per request basis. */
        return pc;
    }
}
```

在 CreatePage() 方法中创建请求容器后，代码将页面类型注册到请求容器中，以便页面本身可以使用依赖注入。当它在第三行检索实际的页面实例时，请求容器尝试创建页面，但假设需要 ResultPage，它无法解析对 Logger 类的依赖，因为这未在请求容器中注册。在这种情况下，它将尝试从其父容器会话容器获取缺失的组件，会话容器中也没有记录器，因此会从其父容器应用程序容器请求记录器。只要在该容器中注册了记录器，页面的所有依赖项就可以得到满足，并且由请求容器创建。

这种方法的优点在于，一方面组件可以在适当的级别注册和共享，而另一方面从容器检索组件的对象只需处理一个容器，并且可以依赖它在容器链中找到所需的组件。

## 服务定位器与依赖注入

到目前为止，我们讨论了两种不同的模式，它们解决了本章开头描述的耦合和实例管理问题。剩下的问题是何时使用哪种模式。

可以肯定地说，服务定位器模式今天更常用，但这不一定是因为它更适合大多数应用程序。更可能的原因是服务定位器模式已经存在很长时间，而依赖注入是相对较新的模式，尚未广为人知。事实上，开发者在尝试改进服务定位器模式时得出了依赖注入模式。

依赖注入模式实现的组件与依赖解析机制的完全解耦提高了可测试性，因为测试不必设置定位器的专用版本来提供存根或模拟对象。它还有助于重用
