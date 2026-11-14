

```
Dim theInstance As MyType = container.Resolve(Of MyType)()
```

编写指定接口而非特定具体类型的代码意味着，您可以更改配置以指定不同的具体类型，而无需更改代码。Unity 始终会返回一个具体类型（除非它无法解析您指定的接口或抽象类型；在这种情况下，将引发异常）。

您还可以通过调用 **解析所有** 方法来解析使用命名映射（而非默认无名称映射）注册的类型集合。如果您想要检查运行时代码中注册了哪些类型，或显示可用类型列表，这可能很有用。不过，Unity 也公开了允许您遍历容器并获取所有注册信息的方法。

此处无法提供关于使用 Unity 的完整指南。不过，本讨论应该已让您了解使用依赖注入可以实现什么。有关使用 Unity 的更详细信息，请参阅随企业库安装的文档，并在线访问 http://go.microsoft.com/fwlink/?LinkId=188874。

本附录讨论了一些更高级的主题，这些主题将帮助您在创建对象和管理依赖注入容器方面从企业库中获得最大收益。它包括以下内容：

- 将配置信息加载到 Unity 容器中
- 查看容器中的注册
- 在应用程序启动时填充整个对象图
- 在基于请求的应用程序中保持对容器的引用
- 使用备用服务定位器或依赖注入容器

这些主题提供了有关如何使用更复杂的依赖注入方法来创建企业库对象实例的信息（如第 1 章“简介”中所述）。如果您决定不使用此方法，并且正在使用企业库服务定位器及其 **获取实例** 方法来实例化企业库类型，则它们不适用于您的场景。

## 将配置信息加载到 Unity 容器中

与许多应用程序以及企业库中的应用程序块不同，Unity 在启动时不会自动加载配置信息。这是故意为之；这意味着您可以将配置信息加载到一个或多个新容器或现有容器中，包括您作为父子容器层次结构创建的容器。

这也意味着您可以对类型请求的处理方式进行相当大的控制。例如，您可以使用多个容器为应用程序的不同部分指定依赖项，同时允许无法在子容器中满足的请求通过父容器层次结构向上传递，直到找到合适的注册。

这也意味着您可以从不同来源加载配置信息。典型示例是从 App.config 或 Web.config 以外的文件加载配置，或通过以编程方式添加注册（例如，从数据库读取它们并将其应用到容器）。

Unity 容器类公开了 **加载配置** 方法，您可以使用该方法填充容器。您可以不带参数调用此方法，以从当前应用程序配置文件（App.config 或 Web.config）中读取 <unity> 节，如本指南第 1 章中所示。或者，您可以向该方法提供包含配置信息的 UnityConfigurationSection 实例。以下代码使用 Microsoft® .NET Framework 配置系统的方法打开配置文件，将其转换为 UnityConfigurationSection 类型，并将名为 MyContainerName 的 <container> 节中的注册加载到新的 Unity 容器中。

```
' Read a specified config file using the .NET configuration system.
Dim map As New ExeConfigurationFileMap()
map.ExeConfigurationFilename = "c:\\configfiles\\myunityconfig.config"
Dim config As System.Configuration.Configuration = _
    ConfigurationManager.OpenMappedExeConfiguration(map, _
    ConfigurationUserLevel.None)

' Get the unity configuration section.
Dim section As UnityConfigurationSection = _
    DirectCast(config.GetSection("unity"), UnityConfigurationSection)

' Create and populate a new UnityContainer with the configuration information.
Dim theContainer As IUnityContainer = New UnityContainer()
theContainer.LoadConfiguration(section, "MyContainerName")
```

您可以在配置文件的 <unity> 节中定义多个容器，前提是每个容器都有唯一名称，并在运行时将每个容器加载到单独的容器中。如果您未在配置文件中为容器分配名称，则它将成为默认容器，您可以通过在 **加载配置** 方法中省略名称参数来加载它。

若要以这种方式以编程方式加载容器，必须将 System.Configuration.dll 程序集和 Microsoft.Practices.Unity.Configuration.dll 程序集添加到项目中。还应导入以下命名空间：

- Microsoft.Practices.EnterpriseLibrary.Common.Configuration.Unity
- Microsoft.Practices.Unity

## 查看容器中的注册

有时您可能会发现应用程序引发错误，指示它无法解析特定类型。Unity 返回的错误消息很详细，应该能帮助您快速找到问题。不过，您可能会发现能够浏览容器内容以查看其包含的注册和映射很有用。

Unity 容器公开了 Registrations 属性，该属性返回一组 ContainerRegistration 实例，容器中的每个注册或类型映射对应一个实例。以下示例代码展示了如何提取每个注册的详细信息：已注册的类型、它映射到的类型（如果有）、注册的名称（如果不是默认注册）以及生存期管理器类型。

```vb.net
For Each item As ContainerRegistration In theContainer.Registrations
    regType = item.RegisteredType.Name
    mapType = item.MappedToType.Name
    regName = If(item.Name, "[default]")
    lifetime = item.LifetimeManagerType.Name
    If mapType <> regType Then
        mapTo = " -> " & mapTo
    Else
        mapTo = String.Empty
    End If
    lifetime = lifetime.Substring(0, lifetime.Length - "LifetimeManager".Length)
    ' Display details of the registration as appropriate.
Next
```

## 在应用程序启动时填充整个对象图

在使用配置信息（包括企业库信息以及您自己的自定义类型的注册和映射）填充容器后，您可以通过依赖注入解析这些自定义类型，并填充其所有依赖项。您可以通过三种方式定义依赖项：

- 作为目标类中构造函数的一个或多个参数。Unity 将创建适当类型的实例，并在实例化目标对象时填充构造函数参数。这是您通常会使用的方法。例如，您可以让 Unity 自动创建并向构造函数传递 LogWriter 或 ExceptionManager 的实例，将引用存储在类变量或字段中，并在该类中使用它。
- 作为目标类的一个或多个属性。Unity 将创建属性或配置中定义的类型的实例，并在通过容器解析类时将该实例设置为属性的值。
- 作为目标类中方法的一个或多个参数。Unity 将创建适当类型的实例，并在实例化目标对象时填充方法参数，然后调用该方法。您可以将参数中传递的引用存储在类变量或字段中，以便在该类中使用。当您有一个应在实例化类时执行的 Initialize 或类似方法时，通常会使用此方法。

通过利用填充整个对象图的功能，您可以决定让容器在应用程序启动时（或至少在其很大一部分时）创建并注入整个应用程序中定义的所有依赖项的适当类型的实例。

虽然这可能是一个奇怪的概念，但这意味着在执行此初始依赖项填充后，您不需要保留对容器的引用。这并不意味着您不能同时保留对容器的引用，但解析所有的

