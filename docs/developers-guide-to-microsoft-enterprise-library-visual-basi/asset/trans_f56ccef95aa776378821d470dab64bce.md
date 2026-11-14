

## 对象实例化的优缺点

如果您尚未决定为创建 Enterprise Library 对象采用哪种方法，下表将帮助您了解每种方法的优缺点。

| 对象实例化技术 | 优点 | 注意事项 |
| :--- | :--- | :--- |
| 使用 Enterprise Library 服务定位器 | 无需初始化代码。服务定位器会自动提供。您可以在应用程序代码的任何位置解析类型。您无需保留对容器的引用。 | 您只能解析 Enterprise Library 类型（作为接口、抽象类型或自动注册的具体类型）。您无法操作或向容器添加注册或映射。 |
| 将容器用作服务定位器 | 您可以直接访问 Unity 容器的所有功能。您可以遍历内容并读取或操作注册和映射（尽管您不应尝试更改 Enterprise Library 配置信息）。您可以添加和删除自己的注册和映射，从而充分利用 DI 技术。 | 需要初始化，但这只是在应用程序启动时执行的一行代码，或者在使用默认 Unity 容器时的简单配置设置。基于请求的应用程序（如 ASP.NET 和 Web 服务）需要额外代码来存储容器引用并解析请求类（如 Page）的依赖项。 |

直接访问容器这一更高级方法的主要优点之一是，您可以使用它来解析自定义类型的依赖项。例如，假设您有一个名为 **税务计算器** 的类，需要执行日志记录并实现整个应用程序中应用的一致异常处理策略。您的类将包含一个构造函数，接受 **异常管理器** 和 **日志写入器** 的实例作为依赖项。

```
Public Class TaxCalculator
    Private _exceptionManager As ExceptionManager
    Private _logWriter As LogWriter

    Public Sub New(em As ExceptionManager, lw As LogWriter)
        Me._exceptionManager = em
        Me._logWriter = lw
    End Sub
    ...
End Class
```

如果您使用 Enterprise Library 服务定位器方法，可以在需要时直接在类构造函数或方法中获取这些实例，而不是将其作为参数传递。然而，更常用的方法是在主应用程序代码中生成和重用实例，并在创建 TaxCalculator 实例时将其传递给它。

```
Dim exManager _
= EnterpriseLibraryContainer.Current.GetInstance(Of ExceptionManager)()
Dim writer _
= EnterpriseLibraryContainer.Current.GetInstance(Of LogWriter)()
Dim calc As New TaxCalculator(exManager, writer)
```

或者，如果您已创建并保留对容器的引用，只需通过容器解析 TaxCalculator 类型即可。Unity 将实例化该类型，检查构造函数参数，并自动将 ExceptionManager 和 LogWriter 的实例注入其中。它将返回所有依赖项均已填充的新 TaxCalculator 实例。

```
Dim calc As TaxCalculator = theContainer.Resolve(Of TaxCalculator)()
```

## 更高级方法的更多理由

从前面的示例可以清楚看出，在除最简单的应用程序或场景之外的所有情况下，自行管理容器都能带来显著优势。您所见的依赖注入示例仅触及了使用更高级方法所能实现的表面。例如，如果您持有对容器的引用，则可以：

- 管理自定义类型的生存期。容器可以将其解析为单例，其生存期基于创建它们的对象的生存期，或为每个执行线程创建新实例。
- 通过将接口和抽象类型映射到自定义类型的具体实现，实现插件和服务定位器等模式。
- 推迟创建解析的自定义类型，直到实际需要时才创建。
- 为解析的自定义类型实例的参数和属性指定依赖项和值。
- 将拦截应用于自定义类型，以修改其行为、实现横切关注点的管理或添加其他功能。
- 设置依赖项层次结构，这些层次结构会自动填充，以实现组件之间的最大解耦，协助调试，简化测试，并降低维护成本和工作量。

当您使用默认 Unity 容器时，您拥有一个强大的通用依赖注入机制。您可以在运行时以编程方式在容器中定义和修改注册和映射，也可以使用配置文件定义它们。附录 A，“使用 Unity 进行依赖注入”包含有关使用 Unity 的更多信息。

为了让您了解其使用有多简单，以下代码在名为 **IMyService** 的接口和名为 **客户服务** 的具体类型之间注册了一个映射，指定其应为单例。

```
theContainer.RegisterType(Of IMyService, CustomerService)(_
    New ContainerControlledLifetimeManager())
```

然后，您可以使用以下代码解析具体类型的单个实例。

```
Dim myServiceInstance As IMyService = theContainer.Resolve(Of IMyService)()
```

这将返回 **客户服务** 类型的实例，尽管您可以通过更改容器中的映射在运行时更改返回的实际类型。或者，您可以为接口或基类创建多个不同名称的注册或映射，并在解析类型时指定名称。

Unity 还可以从应用程序的 App.config 或 Web.config 文件（或任何其他配置文件）读取其配置。这意味着您可以使用创建 Enterprise Library 对象和自定义类型的高级方法，同时只需编辑配置文件即可更改应用程序的行为。

> 如果要从配置文件将类型注册和映射加载到 Unity 容器中，必须将程序集 Microsoft.Practices.Unity.Configuration.dll 添加到项目中，并可选择将命名空间 Microsoft.Practices.Unity.Configuration 导入到代码中。此程序集和命名空间包含用于加载配置信息的 Unity 容器扩展。

例如，配置文件中的以下摘录将初始化容器并向其中添加与上面所示 **RegisterType** 示例相同的自定义映射。

```
<unity>
  <alias alias="CoreExtension"
    type="Microsoft.Practices.EnterpriseLibrary.Common.Configuration
    .Unity.EnterpriseLibraryCoreExtension,
    Microsoft.Practices.EnterpriseLibrary.Common" />
  <namespace name="Your.Custom.Types.Namespace" />
  <assembly name="Your.Custom.Types.Assembly.Name" />
  <container>
    <extension type="CoreExtension" />
    <register type="IMyService" mapTo="CustomerService">
      <lifetime type="singleton" />
    </register>
  </container>
</unity>
```

然后，您只需将此配置加载到新的 Unity 容器中即可。这只需要一行代码，如下所示。

```
Dim theContainer = New UnityContainer().LoadConfiguration()
```

> 在附录 A，“使用 Unity 进行依赖注入”中，我们演示的其他技术包括使用特性来注册类型映射和依赖项、定义命名注册以及为参数和属性指定依赖项和值

使用创建对象的更高级技术时需要注意的一点是，您的应用程序负责管理容器、保留对其的引用，并使该引用可供必须访问容器的代码使用。在自动维护全局状态的基于窗体的应用程序中（例如，使用 Windows Forms、Windows Presentation Foundation (WPF) 和 Silverlight® 等技术构建的应用程序），您可以使用应用程序范围的变量来实现此目的。

但是，在使用 ASP.NET、ASMX 和 Windows Communication Foundation (WCF) 等技术构建的基于请求的应用程序中，您通常需要额外代码来维护容器并使其可用于每个请求。我们将在附录 B，“Enterprise Library 中的依赖注入”中讨论实现此目的的一些方法，您可以在随 Enterprise Library 安装的文档以及在线 http://go.microsoft.com/fwlink/?LinkId=188874 中找到完整详细信息。

## 从 Enterprise Library 的早期版本获取对象

如果您使用过 5.0 之前版本的 Enterprise Library，可能更熟悉在应用程序代码中创建对象的早期方法。早期版本通常支持或推荐使用一系列静态外观。虽然这些外观在版本 5.0 中仍受支持，以便与现有应用程序保持向后兼容，但它们不再是推荐的方法，并且未来版本中可能会被弃用。

图 5 总结了您可以用来访问 Enterprise Library 功能的所有方法。1 和 2 是 Enterprise Library 5.0 的推荐方法；3 和 4 仍受支持，以便更轻松地升级使用早期版本 Enterprise Library 的现有应用程序。

