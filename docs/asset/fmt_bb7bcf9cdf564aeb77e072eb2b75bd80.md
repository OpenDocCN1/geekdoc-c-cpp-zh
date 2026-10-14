
```
allTasks.Add(
    new TaskDto
    {
        ID = reader.GetInt32(IDIndex),
        Description = reader.GetString(DescriptionIndex),
        Priority = reader.GetString(PriorityIndex),
        DueDate = reader.GetDateTime(DueDateIndex),
        Completed = reader.GetBoolean(CompletedIndex)
    }
);
}
}
}
}
}
finally
{
    if(connection is IDisposable)
    {
        var disposableConnection = connection as IDisposable;
        disposableConnection.Dispose();
    }
}

    return allTasks;
}
```

只有当连接是 `IDisposable` 类型时，你才会尝试在其上调用 `Dispose` 方法。这无论工厂返回的产品是否实现 `IDisposable` 都能工作，但如果实现了，它将正确地释放它，从而正确清理其资源。

负责所有者模式会确定性地释放实现 `IDisposable` 的对象。该模式有效地忽略了未实现 `IDisposable` 的对象。然而，SOLID 代码通常会产生多个装饰器相互包裹以添加额外功能。在这种情况下，只有当最外层的对象实现了 `IDisposable` 时，负责所有者模式才会正确运行。当外部装饰器未实现 `IDisposable`，但后续层实现了时，负责所有者模式将无法正确释放这些实例。相反，你必须使用工厂隔离模式。

### 工厂隔离模式

该模式能够确定性地释放由于 SOLID 代码而经常形成的复杂对象图。它以实验室中常见的手套箱隔离器命名。这些是带集成手套的玻璃或金属箱，可安全受控地访问内容物。类似地，工厂隔离模式允许安全受控地访问一个对象实例，并在使用后正确释放它。

工厂隔离模式仅在目标接口未实现 `IDisposable` 时才需要。扩展 `IDisposable` 接口会给所有实现带来必须实现 `Dispose` 方法的要求，即使在不必要的情况下也是如此。相反，`IDisposable` 应被视为实现细节，并根据具体情况分配给类。这自然地导向了负责所有者模式和工厂隔离模式的应用。

迄今为止的示例都针对 `IDbConnection` 接口的生命周期。不幸的是，该接口扩展了 `IDisposable` 接口。如果相反假设目标接口不扩展 `IDisposable`，客户端对工厂隔离模式的视图将看起来像清单 9-18 中的代码。

#### LISTING 9-18 使用工厂隔离模式的客户端示例。

Click here to view code image

```
public IEnumerable<TaskDto> GetAllTasks()
{
    var allTasks = new List<TaskDto>();
    connectionFactory.With(connection =>
    {
        connection.Open();
        using (var transaction = connection.BeginTransaction())
        {
            var command = connection.CreateCommand();
            command.Transaction = transaction;
            command.CommandType = CommandType.StoredProcedure;
            command.CommandText = "[dbo].[get_all_tasks]";
            using (var reader = command.ExecuteReader(CommandBehavior.CloseConnection))
            {
                while (reader.Read())
                {
                    allTasks.Add(
                        new TaskDto
                        {
                            ID = reader.GetInt32(IDIndex),
                            Description = reader.GetString(DescriptionIndex),
                            Priority = reader.GetString(PriorityIndex),
                            DueDate = reader.GetDateTime(DueDateIndex),
                            Completed = reader.GetBoolean(CompletedIndex)
                        }
                    );
                }
            }
        }
    });
```

```
return allTasks;
}
```

`Factory Isolation` 模式取代了常见的 `Create` 方法，该方法返回工厂产品的实例，而是提供一个 `With` 方法，该方法接受一个以工厂产品作为参数的 lambda 方法。

这里的优势在于，工厂产品的生命周期与 lambda 方法的作用域显式关联。这简洁地传达给客户端，它并不控制产品的生命周期。工厂实现本身非常简单，如清单 9-19 所示。

**LISTING 9-19** 创建隔离工厂很简单。

```
public class IsolationConnectionFactory : IConnectionIsolationFactory
{
    public void With(Action<IDbConnection> action)
    {
        using(var connection = CreateConnection())
        {
            action(connection);
        }
    }
}
```

`With` 方法能够构建装饰器、适配器和组合体的流畅对象图——正如 SOLID 所建议的那样——并管理它们的生命周期，而调用客户端无需关心任何事情，只需使用最终产品即可。

请注意，可以通过将 lambda 作用域的产品实例分配给作用域更广的变量来规避 Factory Isolation 模式，因此不建议客户端代码这样做。

### 超越简单的注入

依赖注入可以通过使用各种不同的框架以多种不同的方式实现。有些模式是良性的，支持并增强 DI，同时强化其所要实现的目标。其他模式则恰恰相反：它们削弱了 DI 的根本目的，积极地破坏它并偏离了重点。

当你使用 DI 时，每种类型的应用程序都需要不同种类的设置。在每种情况下，你都需要识别组合根，以便正确集成你的注册代码。WPF 应用程序中组合根的位置与 Windows Forms 应用程序不同。两者都与 ASP.NET MVC 应用程序不同。

在高级场景中，通过 Poor Man’s DI 手动组合类以及通过控制反转容器单独注册类都过于繁琐和冗长。通过将注册推迟到一个或多个约定，你可以消除大量样板代码，同时也提供一些手动注册，以处理约定不足的边缘情况。

### Service Locator 反模式

服务定位器看起来与控制反转容器非常相似，这正是它们不总是被认为对代码有害的原因。清单 9-20 显示了 Microsoft Patterns and Practices 团队提供的服务定位器示例。

**LISTING 9-20** `IServiceLocator` 接口看起来只是另一个 IoC 容器。

```
public interface IServiceLocator : IServiceProvider
{
    object GetInstance(Type serviceType);

    object GetInstance(Type serviceType, string key);

    IEnumerable<object> GetAllInstances(Type serviceType);

    TService GetInstance<TService>();

    TService GetInstance<TService>(string key);

    IEnumerable<TService> GetAllInstances<TService>();
}
```

请注意，像 `TService GetInstance<TService>()` 这样的方法本可以直接取自 `IUnityContainer` 接口——只需将名称替换为 `Resolve` 即可。问题在于服务定位器的使用方式，由于静态 `ServiceLocator` 类，如清单 9-21 所示。

**LISTING 9-21** 这个静态类是反模式的根源。

```
/// <summary>
/// This class provides the ambient container for this application. If your
/// framework defines such an ambient container, use ServiceLocator.Current
/// to get it.
/// </summary>
public static class ServiceLocator
{
    private static ServiceLocatorProvider currentProvider;

    public static IServiceLocator Current
    {
        get { return currentProvider(); }
    }

    public static void SetLocatorProvider(ServiceLocatorProvider newProvider)
    {
        currentProvider = newProvider;
    }
}
```

我保留的类摘要注释暗示了问题。*ambient container* 的概念意味着容器存在的知识泄漏。虽然通过接口对服务定位器的具体实现进行了值得称赞的解耦，但问题在于——在组合根之外的任何类中——对服务定位器或容器的承认。清单 9-22 显示了如果 `TaskListController` 被重写为使用 ServiceLocator 会是什么样子。

**LISTING 9-22** 服务定位器允许类检索任何东西，无论是否合适。

```
public class TaskListController : INotifyPropertyChanged
{
    public void OnLoad()
    {
        var taskService = ServiceLocator.Current.GetInstance<ITaskService>();
        var taskDtos = taskService.GetAllTasks();
        var mapper = ServiceLocator.Current.GetInstance<IObjectMapper>();
        AllTasks = new ObservableCollection<TaskViewModel>(mapper.Map<IEnumerable<TaskViewModel>>(taskDtos));
    }

    public ObservableCollection<TaskViewModel> AllTasks
    {
        get
        {
            return allTasks;
        }
        set
        {
            allTasks = value;
            PropertyChanged(this, new PropertyChangedEventArgs("AllTasks"));
        }
    }

    public event PropertyChangedEventHandler PropertyChanged = delegate { };

    private ObservableCollection<TaskViewModel> allTasks;
}
```

现在没有构造函数，也没有构造函数注入。相反，当需要时，类会调用静态 `ServiceLocator` 类并返回请求的服务。回想一下，像这样的静态类是 skyhooks——一种代码异味。

更糟糕的是，类能够从服务定位器检索任何东西。你不再遵循依赖注入的“好莱坞原则”：不要调用我们，我们会调用你。相反，你直接索要所需的东西，而不是让它们交给你。你如何知道这个类需要什么依赖？使用服务定位器，你必须检查代码，搜索检索所需服务的随意调用。构造函数注入允许你通过看一眼构造函数，或通过 IntelliSense 在远处查看所有依赖项。

问题不一定是单元测试。服务定位器允许你在使用前设置一个 `IServiceLocator` 实现，这意味着它可以被模拟，类可以进行单元测试。至少它不会阻止这一点。只是将类注册并映射到它们的接口——一项不小的任务——然后只为污染控制器、服务和其他类添加此类基础设施代码似乎很荒谬。当没有问题需要解决时就更荒谬了——构造函数注入不需要以这种方式被规避。

为 Unity 提供了服务定位器的适配器。清单 9-23 显示了在设置映射后如何注册它。

**LISTING 9-23** 服务定位器将直接委托给 `UnityContainer` 实例以解析实例。

```
private void OnApplicationStartup(object sender, StartupEventArgs e)
{
    CreateMappings();

    container = new UnityContainer();
    container.RegisterType<ISettings, ApplicationSettings>();
    container.RegisterType<IObjectMapper, MapperAutoMapper>();
    container.RegisterType<ITaskService, TaskServiceAdo>();
    container.RegisterType<TaskListController>();
    container.RegisterType<TaskListView>();

    ServiceLocator.SetLocatorProvider(() => new UnityServiceLocator(container));

    MainWindow = container.Resolve<TaskListView>();
    MainWindow.Show();

    ((TaskListController)MainWindow.DataContext).OnLoad();
}
```

这看起来与之前的版本非常相似，除了设置定位器提供程序。`Resolve` 的调用，不过，并没有真正“解析”对象图；`TaskListView` 中已不再有任何依赖需要注入。它们都是在类的各个方法中按需单独获取的。

Service Locator 反模式是编程上下文中文字讽刺的一个很好的例子，因为所声称的内容与现实相反。声称类没有依赖项，因为它们有默认构造函数，但事实并非如此：它们确实有依赖项，否则你就不会试图从服务定位器中获取它们！

不幸的是，服务定位器有时是不可避免的反模式。在某些类型的应用程序中——特别是 Windows Workflow Foundation——基础设施不利于构造函数注入。在这些情况下，唯一的选择是使用服务定位器。这比根本不注入依赖项要好。对于我对该（反）模式的激烈批评，它仍然比手动构造依赖项好得多。毕竟，它仍然提供了接口提供的那些至关重要的扩展点，允许装饰器、适配器和类似的好处。

### 注入容器

与服务定位器密切相关的是将容器直接注入到类中的概念。这同样把保险箱的钥匙交给了类，因为它可以自由地从容器中检索任何想要的东西。想象一个这样的类，在其众多方法中散布着检索十几个服务的代码。现在将其与一个构造函数需要这十几个服务并通过提前前提条件强制其存在——如果传入空引用则抛出异常——的类进行比较。这两个类显然都做了太多——正如它们所需的依赖项所表明的那样——应该被重构为更小的类或将依赖项分组为有意义的装饰器。然而，只有后者才会在一眼就能显式地表明这种异味的存在。

此外，要求容器作为构造函数参数的类还必须引用容器的程序集。这将使基础设施代码在整个代码库中泛滥，因为每个类都接受容器以访问它真正需要的服务。

### 非法注入

非法注入看起来与正常、正确实现的依赖注入非常相似。它有一个接受依赖项的构造函数，并且这些依赖项要么通过“穷人版 DI”提供，要么通过控制反转容器提供。

然而，这种模式被污染了——实际上是被致命地毒害了——因为存在第二个默认构造函数。如清单 9-24 所示，这第二个构造函数直接为依赖项构造了一些实现，从而绕过了 DI。

**清单 9-24** 拥有一个直接引用实现的构造函数会抵消依赖注入的部分好处。
