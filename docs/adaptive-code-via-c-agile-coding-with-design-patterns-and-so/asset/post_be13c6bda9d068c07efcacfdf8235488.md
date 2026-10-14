
```
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
return allTasks;
}
}
```

The ISettings interface abstracts away from this class the details of retrieving the connection string. An implementation that is an adapter for the Microsoft .NET Framework’s ConfigurationManager class is provided. It is not hard to imagine that the settings could end up being stored elsewhere at some point, which justifies the use of an interface. Another problem is that the ConfigurationManager class is static and, thus, hard to mock. Using it directly would not only limit your options for retrieving application settings such as connection strings, it would also make the TaskServiceAdo class less testable.

## Constructing the object graph

Often in this book, it has been an accepted fact that interfaces are injected into constructors. Eventually, of course, interfaces prove to be insufficient, and you must commit to an implementation. There are two main options for accomplishing this: Poor Man’s Dependency Injection and using an Inversion of Control container. In order to exemplify how dependency injection works, this section will first look at Poor Man’s DI.

## Poor Man’s Dependency Injection

This pattern is so named because it does not require any external dependencies in order to function. It involves constructing the necessary object graph for the controller ahead of time. Listing 9-4 shows how to construct the refactored TaskListController and provide it to the TaskListView, which is the application’s main window.

### LISTING 9-4 Poor Man’s DI is verbose but flexible.

Click here to view code image

```
public partial class App : Application
{
    private void OnApplicationStartup(object sender, StartupEventArgs e)
    {
```

```
CreateMappings();

var settings = new ApplicationSettings();
var taskService = new TaskServiceAdo(settings);
var objectMapper = new MapperAutoMapper();
controller = new TaskListController(taskService, objectMapper);
MainWindow = new TaskListView(controller);
MainWindow.Show();

controller.OnLoad();
}

private void CreateMappings()
{
    AutoMapper.Mapper.CreateMap<TaskDto, TaskViewModel>();
}

private TaskListController controller;
}
```

This code is the entry point to your application. The OnApplicationStartup method is an event handler that is called by internal WPF code to inform you that you can initialize things. In different types of applications, the entry point varies in style but is always a good place to put your dependency injection code.

The process of bootstrapping the application is very simple. The target is to construct a TaskListView, because that is the view class that acts as the resolution root of the application. Resolution roots are covered later in this chapter. In order to construct that class, you need a TaskListController instance. But that class requires both an ITaskService and an IObjectMapper, so you instantiate classes for both—this is where you are committing to the implementations. The TaskServiceAdo, in turn, requires an ISettings implementation, so you commit to the ApplicationSettings, which is an adapter for the ConfigurationManager .NET Framework class. Figure 9-3 clarifies this with a class diagram.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_320_0.png)

## FIGURE 9-3 The interfaces, their implementations, and their dependencies, all of which make up the Task List application.

Each class requires one or more dependencies as sockets that are implemented by other classes that might also require dependencies. It is common for an implementation to be an adapter, such as the MapperAutoMapper and the ApplicationSettings classes. These simply fulfil the interface required of the dependency but delegate the actual work to another class. Even if the class is not an adapter, it is likely to have some dependencies of its own to which it delegates some of the work, like the TaskServiceAdo, which uses ADO .NET for the real retrieval of data. Other implementations of the ITaskService could get the task list from anywhere—a TaskServiceNHibernate class would be an alternative implementation that delegated much of the work to NHibernate. A TaskServiceOutlook class could depend on the Microsoft Outlook Add-In framework and read the tasks directly from the built-in task list of Outlook. It is imperative to note that, because the interface does not tie itself to any of these technologies, anything could be the source of tasks, assuming that it can fulfil the interface.

Poor Man’s DI is verbose. When this application is extended to support adding new tasks, editing tasks, or perhaps notifying of an imminent due date, it is clear that these few lines of construction code will grow significantly, to the point where they are no longer easily understood. However, Poor Man’s DI is flexible. Whatever complex object graph you want to construct, the way to construct it is obvious because there is only one way: manually creating instances of everything and passing them to classes that aggregate their functionality, repeating until you reach the resolution root. You can implement any number of decorators for the interfaces that each class depends on; Poor Man’s DI allows you to meticulously construct the resulting graph.

## Method injection

The constructor isn’t the only option for providing dependencies to classes. Methods and properties can also be used, and they both have different use cases when compared to constructors.

Listing 9-5 shows part of the TaskListController that has been rewritten to furnish the ITaskService with its ISettings dependency as a parameter on the GetAllTasks method. This requires the interface for the method to be altered.

### LISTING 9-5 The task service now accepts the settings as a method parameter instead of a constructor parameter.

Click here to view code image

```
public class TaskListController : INotifyPropertyChanged
{
    public TaskListController(ITaskService taskService, IObjectMapper mapper,
    ISettings
        settings)
    {
        this.taskService = taskService;
        this.mapper = mapper;
        this.settings = settings;
    }

    public void OnLoad()
    {
        var taskDtos = taskService.GetAllTasks(settings);
        AllTasks = new
        ObservableCollection<TaskViewModel>(mapper.Map<IEnumerable<TaskViewModel>>
        (taskDtos));
    }
}
```

This is useful when the method being called is the only one that requires the dependency. Constructor dependencies indicate that sufficient behavior in the class requires delegation to the dependency, but if only a small percentage of methods truly use the dependency, it might make more sense to pass it in to those methods specifically. The downside of method injection is that it requires the clients who call the method to “acquire” an instance of the dependency. They can do so either through a constructor parameter or through a method parameter that causes clients to pass the parameter down the call stack until it is used by the target class.

## Inversion of Control

Throughout this book, the examples have focused on developing classes that delegate to abstractions. These abstractions are then implemented by other classes, which delegate some work to more abstractions. Eventually, a class is so small and directed that it need not delegate any further, and the chain of dependency is ended. In order to construct the dependent classes, first their dependencies are constructed and then injected in as dependencies. You have learned how this dependency injection can be implemented by manually constructing classes and passing instances into the constructors. Though this elevates you from a situation in which dependent implementations cannot be swapped or decorated to one in which they can, the object graph is still constructed statically: which part goes where is known at compile time. Inversion of Control (IoC) allows you to defer this construction to run time.

IoC is most well known in the context of IoC *containers*. These systems allows you to link the interfaces of your application to their implementations and retrieve an instance of a class by *resolving* all of the dependencies.

The code in Listing 9-7 shows the application entry point rewritten to use the Unity IoC container. The first step is to instantiate a new UnityContainer instance. Note that when you are bootstrapping the IoC container like this, there is no alternative but to directly create instances of infrastructural components.

**LISTING 9-7** With an IoC container, instead of manually constructing implementations, types are mapped to interfaces.

[Click here to view code image](#code-image)

```
public partial class App : Application
{
    private IUnityContainer container;
    private void OnApplicationStartup(object sender, StartupEventArgs e)
    {
        CreateMappings();

        container = new UnityContainer();
        container.RegisterType<ISettings, ApplicationSettings>();
        container.RegisterType<IObjectMapper, MapperAutoMapper>();
        container.RegisterType<ITaskService, TaskServiceAdo>();
        container.RegisterType<TaskListController>();
        container.RegisterType<TaskListView>();

        MainWindow = container.Resolve<TaskListView>();
        MainWindow.Show();

        ((TaskListController)MainWindow.DataContext).OnLoad();
    }
}
```
