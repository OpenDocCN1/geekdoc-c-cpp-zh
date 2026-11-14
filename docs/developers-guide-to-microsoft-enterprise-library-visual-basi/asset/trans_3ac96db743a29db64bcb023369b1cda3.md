

在启动时加载所需类型可以提高运行时性能，代价是启动时间略微增加。当然，这还需要额外的内存和资源来保存所有已解析的实例，你需要将此与预期的运行时性能改进进行权衡。

你可以通过容器解析主窗体或启动类来填充所有依赖项。容器将自动创建每个类所需对象的适当实例，并将其注入到参数和属性中。但是，这依赖于容器能够创建并返回未在容器中注册的类型的实例。Unity 容器可以做到这一点。如果你使用备用容器，可能需要预先注册应用程序中的所有类型，包括主窗体或启动类。

通常，这种填充整个应用程序对象图的方法最适合使用基于窗体或基于窗口的技术构建的应用程序，例如 Microsoft® Presentation Foundation (WPF)、Windows 窗体、控制台应用程序和 Microsoft Silverlight®（使用专为 Silverlight 应用程序设计的 Unity 版本）。

有关如何解析应用程序的主窗体、窗口或启动类以及示例代码的信息，请参阅随 Enterprise Library 安装的文档或在线提供的文档 http://go.microsoft.com/fwlink/?LinkId=188874。

## 在基于请求的应用程序中维护容器引用

将 Enterprise Library 与默认 Unity DI 机制配合使用时，你只需在应用程序中初始化一次容器，然后使用它来解析（或获取）Enterprise Library 对象或你自己的类和对象的实例。初始化容器只需以下一行代码。

```
' Create and populate the default container with application configuration.
Dim container = New UnityContainer() _
.AddNewExtension(Of EnterpriseLibraryCoreExtension)()
```

但是，要在整个应用程序中使用容器来解析类型，你必须保留对它的引用。你可以将容器存储在 Windows 窗体或 WPF 应用程序的全局变量中，ASP.NET 应用程序的 **Application** 字典中，或 Windows Communication Foundation (WCF) 服务的 **InstanceContext** 的自定义扩展中。

表 1 将帮助你了解在使用 Windows 窗体、WPF 和 Silverlight 等技术构建的基于窗体和富客户端应用程序中，何时以及在哪里应保留对容器的引用。

### 表 1 在基于窗体和富客户端应用程序中保留对容器的引用

| 任务 | 何时 | 在哪里 |
| :--- | :--- | :--- |
| 创建和配置容器。 | 应用程序启动时。 | 主例程、启动事件、应用程序定义文件或技术适用的位置。 |
| 从容器获取对象。 | 应用程序启动时，以及以后如果需要。 | 代码中适当的位置。 |
| 存储对容器的引用。 | 应用程序启动时。 | 全局应用程序状态。 |
| 释放容器。 | 应用程序关闭时。 | 代码中适当的位置，或在应用程序结束时自动释放。 |

表 2 将帮助你了解在使用 ASP.NET Web 应用程序和 Web 服务等技术构建的基于请求的应用程序中，何时以及在哪里应保留对容器的引用。

### 表 2 在基于请求的应用程序中保留对容器的引用

| 任务 | 何时 | 在哪里 |
| :--- | :--- | :--- |
| 创建和配置容器。 | 应用程序启动时。 | HTTP 模块 (ASP.NET 和 ASMX)、InstanceContext 扩展 (WCF)。 |
| 从容器获取对象。 | 每个 HTTP 请求期间。 | 在请求启动事件或加载事件中。请求结束时会释放对象。 |
| 存储对容器的引用。 | 应用程序启动时。 | 全局应用程序状态或服务上下文。 |
| 释放容器。 | 应用程序关闭时。 | 代码中适当的位置。 |

有关如何在不同类型的应用程序中（特别是基于请求的应用程序）维护对容器的引用以及可用于实现此目的的代码的更多详细信息，请参阅随 Enterprise Library 安装的文档或在线提供的文档 http://go.microsoft.com/fwlink/?LinkId=188874。

## 使用备用服务定位器或容器

Enterprise Library 默认使用 Unity 依赖注入机制来创建 Enterprise Library 对象的实例。如果你已经在应用程序中使用或计划使用其他依赖注入容器，则可能可以使用它来创建 Enterprise Library 对象，而不使用 Unity。

要实现此目的，你可以获取或编写自己的配置器，该配置器可以使用你指定的 Enterprise Library 配置信息加载容器，或者创建实现 **IServiceLocator** 接口并能公开配置信息的类型。

Enterprise Library 的默认行为是创建一个新的 Unity 容器，为容器创建一个新的配置器，然后从应用程序的默认配置文件 (App.config 或 Web.config) 读取配置信息。以下代码段显示了发生的过程。

```vb
Dim container = New UnityContainer()
Dim configurator = New UnityContainerConfigurator(container)

' Read the configuration files and set up the container.
EnterpriseLibraryContainer.ConfigureContainer(container, _
    ConfigurationSourceFactory.Create())

' The container is now ready to resolve Enterprise Library objects
```

配置器的任务是将配置文件信息转换为容器中的一系列注册。Enterprise Library 仅包含 **UnityContainerConfigurator**，不过你可以编写自己的配置器以适合所选容器，或从第三方获取一个。

另一种方法是创建 **IServiceLocator** 接口的自定义实现，该实现可能不使用配置器，但可以读取应用程序配置并按需返回适当的完全填充的 Enterprise Library 对象。

有关 **IServiceLocator** 接口的更多信息，请参阅 http://commonservicelocator.codeplex.com。

要了解有关 Enterprise Library 备用配置选项的讨论，请参阅 CodePlex 上的论坛 http://www.codeplex.com/entlib/Thread/List.aspx。

策略注入描述了一种在客户端和客户端使用的对象之间插入代码的方法，以更改目标对象的行为，而无需更改该对象或客户端。这种技术的一般设计模式称为拦截，并通过面向切面编程 (AOP) 范式而变得流行。

自版本 3.0 起，拦截一直是 Enterprise Library 的一项功能。在 Enterprise Library 的早期版本中，启用拦截的方式是通过策略注入应用程序块，该块公开了静态门面，你可以使用它们来创建目标对象的包装实例以及客户端可用于访问该目标对象的适当代理。

该块还包含一系列插入到拦截管道（位于客户端和目标对象之间）的调用处理程序。版本 5.0 中包含与 Enterprise Library 早期版本中使用的相同的一组调用处理程序，但它们不再位于策略注入块中（该块主要用于与现有应用程序的向后兼容性）。

在 Enterprise Library 5.0 版本中，实现策略注入的推荐方法是通过 Unity 拦截机制。这支持多种不同的拦截实现技术，包括创建派生类而不是远程代理，并且对应用程序性能的影响要小得多。

你与 Unity 拦截机制一起使用的调用处理程序可以实例化应用程序块，使你能够应用块的功能来管理目标对象的横切关注点。通过 Unity 和 Enterprise Library 提供的拦截和策略注入功能，你可以：

- 通过使用验证处理程序添加验证功能。此调用处理程序使用验证块来验证传递给目标对象的参数中的值。这是一种绕过验证块局限性的有用方法，验证块除特定方案（例如 Windows® Communication Foundation (WCF) 应用程序）外，无法验证方法调用的参数。
- 通过使用日志处理程序为对象添加日志功能。此调用处理程序使用日志块生成日志条目并将其写入配置的目标源。

