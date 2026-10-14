

## 非法注入

非法注入看起来与正常、正确实现的依赖注入非常相似。它有一个接受依赖项的构造函数，并且这些依赖项要么通过“穷人版 DI”提供，要么通过控制反转容器提供。

然而，这种模式被污染了——实际上是被致命地毒害了——因为存在第二个默认构造函数。如清单 9-24 所示，这第二个构造函数直接为依赖项构造了一些实现，从而绕过了 DI。

**清单 9-24** 拥有一个直接引用实现的构造函数会抵消依赖注入的部分好处。

```
public class TaskListController : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged = delegate { };

    private readonly ITaskService taskService;
    private readonly IObjectMapper mapper;
    private ObservableCollection<TaskViewModel> allTasks;

    public TaskListController(ITaskService taskService, IObjectMapper mapper)
    {
        this.taskService = taskService;
        this.mapper = mapper;
    }

    public TaskListController()
    {
        this.taskService = new TaskServiceAdo(new ApplicationSettings());
        this.mapper = new MapperAutoMapper();
    }

    public void OnLoad()
    {
        var taskDtos = taskService.GetAllTasks();
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
}
```

这意味着该类必须引用实现所在的程序集，以及随之而来的所有后续依赖项。这又是“随从”反模式。虽然第一个构造函数（只接受接口）为“阶梯”模式和规范的 DI 做好了铺垫，但第二个默认构造函数却破坏了这一切。

当这个“默认”实现不再是你想要的时候会发生什么？这个类将被修改，转而构造首选的类。当只有一个默认构造函数不够用，在某些场景下你想要实现 A，而在另一些场景下你想要实现 B 时，又该怎么办？这足以让人感到恶心。

有时这种反模式被用来支持单元测试，其默认实现是不依赖其他东西的模拟实现，并且可能位于该类的本地。类中绝不应包含任何仅为支持单元测试而存在的东西。这类做法的常见例子是将私有方法转换为 internal，并使用 InternalsVisibleToAttribute 允许测试程序集访问这些方法——而不是仅通过类的公共接口来测试类。诚然，这看起来可能是一条任意划分的界线——毕竟，DI 因其对单元测试的支持而备受推崇。但这恰恰是关键点：你已经通过使用接口及其构造函数注入来支持单元测试了。模拟对象可以而且应该通过那个构造函数来提供。

值得注意的是，将“非法注入”归类为反模式并不取决于构造函数的可见性。无论构造函数是 public、protected、private 还是 internal，结果都一样：你在本不该引用实现的地方引用了实现。

## 组合根

应用程序中只有一处位置应该了解依赖注入的任何信息：组合根。这是在使用“穷人版 DI”时构造类的地方，或者在使用控制反转容器时注册接口和类映射的地方。

理想情况下，组合根应尽可能靠近应用程序的入口点。这样可以尽早地引导 DI，为你提供一个明确的位置来查找 DI 配置，并帮助你避免在整个应用程序中泄漏对容器的依赖。这也意味着每种应用程序类型都有不同的组合根。

## 解析根

与组合根密切相关的是解析根。这是构成待解析对象图根部的对象类型。如之前的 WPF 示例所示，解析根甚至可以是一个*实例*，但更常见的是由一个公共基类统一起来的一组类型。

在某些情况下，你需要手动解析解析根，但某些支持依赖注入的应用程序类型——如 MVC——则要求你注册映射，然后由应用程序自行解析这些根。

## ASP.NET MVC

MVC 项目非常适合通过 IoC 容器进行依赖注入。它们具有明确界定的解析根和组合根，并且具有足够的可扩展性，可以支持你可能需要集成到框架中以实现 IoC 的任何库。

MVC 应用程序的解析根是控制器。来自浏览器的所有请求都被发送到路由，这些路由直接映射到控制器上的方法——称为*操作*。当请求进来时，MVC 框架将 URL 映射到控制器名称，找到该名称对应的类型，实例化它，然后对该实例调用操作。图 9-4 通过 UML 序列图描绘了这种交互。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_345_0.png)

**图 9-4** 一个 UML 序列图，展示了 MVC 如何通过工厂构造控制器。

当你使用 IoC 进行依赖注入时，控制器的实例化更准确地说是控制器的*解析*。这意味着你可以轻松地遵循“注册、解析、释放”模式，将 Resolve 调用降到理想的极少数量，也就是只在一个地方调用。

清单 9-25 展示了任务列表应用程序的 ASP.NET MVC 用户界面的组合根。

**清单 9-25** HttpApplication 的 Application_Start 方法在 Web 应用程序中是一个常见的组合根。

```
public class MvcApplication : HttpApplication
{
    public static UnityContainer Container;

    protected void Application_Start()
    {
        AreaRegistration.RegisterAllAreas();

        FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
        RouteConfig.RegisterRoutes(RouteTable.Routes);
        BundleConfig.RegisterBundles(BundleTable.Bundles);

        AutoMapper.Mapper.CreateMap<TaskDto, TaskViewModel>();

        Container = new UnityContainer();
        Container.RegisterType<ISettings, ApplicationSettings>();
        Container.RegisterType<IObjectMapper, MapperAutoMapper>();
        Container.RegisterType<ITaskService, TaskServiceAdo>();
        Container.RegisterType<TaskViewModel>();
        Container.RegisterType<TaskController>();

        ControllerBuilder.Current.SetControllerFactory(new UnityControllerFactory(Container));
    }
}
```

其中一些代码是创建新 MVC 应用程序时默认生成的样板代码。这包括所有 MVC 特定的初始化代码，例如用于注册区域、过滤器、路由和捆绑包的代码。这些都在第一时间执行——即在 Application_Start 方法中。当应用程序在 IIS 中启动后收到第一个请求时，会调用此方法。它位于 Global.asax 的代码隐藏文件中，并包含 HttpApplication 类的特定于应用程序的子类。

除了特定于 MVC 的 TaskController 类之外，其余的服务接口和实现都被复用了。之前的 TaskController 是围绕 WPF 设计的，因此无法在该上下文之外复用。取而代之，新的 TaskController 做的工作大致相同——检索任务并通过 IObjectMapper 将它们转换为更适合视图的格式——但继承自 MVC 的控制器基类。这使它成为应用程序的解析根，因为它继承了 System.Web.Mvc.Controller 类。清单 9-26 展示了这个新的控制器。

