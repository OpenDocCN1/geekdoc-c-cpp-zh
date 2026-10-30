
The Factory Isolation pattern replaces the common Create method, which returns an instance of a factory product, instead providing a With method, which accepts a lambda method that has the factory product as a parameter.

The advantage here is that the lifetime of the factory product is explicitly linked to the lambda method’s scope. This succinctly communicates to the client that it is not in control of the product’s lifetime. The factory implementation itself is very simple, as shown in Listing 12-19.

**LISTING 12-19** Creating an isolating factory is simple.

```
public class IsolationConnectionFactory : IConnectionIsolationFactory
{
    public void With(Action<IDbConnection> do)
    {
        using(var connection = CreateConnection())
        {
            do(connection);
        }
    }
}
```

The With method can construct a fluid object graph of decorators, adapters, and composites—just as SOLID suggests—and manage their lifetimes without the calling client concerning itself with anything but using the final product.

## Beyond simple injection

This section covers some more advanced topics of dependency injection.

Dependency injection can be implemented in many different ways, by using a variety of different frameworks. Some patterns out there are benevolent, supporting and enhancing DI while reinforcing what it aims to accomplish. Other patterns do the opposite: they detract from the underlying purpose of DI, actively undermining it and detracting from the whole point.

Two such patterns are particularly insidious. The Service Locator anti-pattern is, unfortunately, all too common. It is used in many frameworks and libraries—sometimes, it is the only way to create a hook to use dependency injection. Worse than the Service Locator is an anti-pattern with an unfortunate moniker that I shall eschew in favor of something a bit more sanitized: *Illegitimate injection*. This is a middle ground where dependency injection is used “sometimes,” allowing the construction of services, controllers, and similar entities without properly providing their dependencies.

When using DI, each type of application requires a different kind of setup. With each, you need to identify the composition root to correctly integrate your registration code. The location of the composition root in a WPF application differs from that of a Windows Forms application. Both will differ from that of an ASP.NET MVC application.

In advanced scenarios, the manual composition of classes through Poor Man's DI and the individual registration of classes through an Inversion of Control container might be too laborious and too verbose. You can eliminate a lot of boilerplate code by deferring registration to one or more conventions. You can also provide some manual registration to handle the edge cases when conventions do not suffice.

## The Service Locator anti-pattern

Service locators look very similar to Inversion of Control containers, which is precisely why they are not always thought of as detrimental to the code. Listing 12-20 shows an example of the service locator provided by the Patterns and Practices team at Microsoft.

LISTING 12-20 The IServiceLocator interface appears to be just another IoC container.

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

Note that methods such as TService GetInstance<TService>() could have been taken directly from the IUnityContainer interface—just by swapping the name for Resolve. The problem arises from how a service locator is used, thanks to the static ServiceLocator class, as shown in Listing 12-21.

LISTING 12-21 This static class is the cause of the anti-pattern.

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
}
```

```
public static void SetLocatorProvider(ServiceLocatorProvider newProvider)
{
    currentProvider = newProvider;
}
```

The comment hints at the problem. The concept of an ambient container implies a leak of knowledge that a container exists. Although there is a laudable decoupling of the specific implementation of the service locator behind an interface, the problem is the acknowledgement—inside any class other than the composition root—of the service locator or container. Listing 12-22 shows how the TaskListController would look if it was rewritten to use the ServiceLocator.

# LISTING 12-22 A service locator allows classes to retrieve anything at all, whether appropriate or not.

```
public class TaskListController : INotifyPropertyChanged
{
    public void OnLoad()
    {
        var taskService = ServiceLocator.Current.GetInstance<ITaskService>();
        var taskDtos = taskService.GetAllTasks();
        var mapper = ServiceLocator.Current.GetInstance<IObjectMapper>();
        AllTasks = new ObservableCollection<TaskViewModel>(mapper.Map<IEnumerable<TaskViewModel>>((taskDtos));
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

    public event PropertyChangedEventHandler PropertyChanged = delegate {};

    private ObservableCollection<TaskViewModel> allTasks;
}
```

Now there is no constructor, nor is there constructor injection. Instead, when required, the class makes a call to the static ServiceLocator class and returns the service requested. Recall that static classes like this are skyhooks—a code smell.

Worse still, the class is able to retrieve anything and everything from the service locator. You are no longer following the "Hollywood Principle" of dependency injection: Don't call us, we'll call you. Instead, you are directly asking for the things you need, rather than having them handed to you. How can you tell what dependencies this class needs? With the service locator, you have to examine the code, searching for capricious calls that retrieve a required service. Constructor injection allowed you to view dependencies—all of them—with a glance at the constructor, or at a distance, via IntelliSense.

The problem is not necessarily one of unit testing. The service locator allows you to set an IServiceLocator implementation before use, which means that it can be mocked and the classes can be unit tested. At least it does not prevent that. It just seems absurd to register classes and map them to their interfaces—a significant undertaking—only to pollute controllers, services, and other classes with infrastructural code such as this. It is doubly absurd when there is no problem to be solved—constructor injection did not need to be circumvented in this way.

An adapter for the service locator is provided for Unity. Listing 12-23 shows how this is registered after the mappings have been set up.

# LISTING 12-23 The service locator will delegate directly to the UnityContainer instance to resolve instances.

```
private void OnApplicationStartup(object sender, StartupEventArgs e)
{
    CreateMappings();

    container = new UnityContainer();
    container.RegisterType<ApplicationSettings>();
    container.RegisterType<ObjectMapper, MapperAutoMapper>();
    container.RegisterType<ITaskService, TaskServiceAdo>();
    container.RegisterType<TaskListController>();
    container.RegisterType<TaskListView>();

    ServiceLocator.SetLocatorProvider(() => new UnityServiceLocator(container));

    MainWindow = container.Resolve<TaskListView>();
    MainWindow.Show();

    ((TaskListController)MainWindow.DataContext).OnLoad();
}
```

This looks remarkably similar to the prior versions except for setting the locator provider. The call to Resolve, though, does not truly "resolve" the object graph; there are no longer any dependencies to inject into the TaskListView. They are all fetched individually as and when needed within the methods of the class.

The Service Locator anti-pattern is a good example of literal irony applied to a programming context, in that what is claimed is contrary to the reality. It is claimed that classes do not have dependencies, due to their default constructor, but that is simply not the case: they do have dependencies, otherwise you wouldn't be trying to fetch them from a service locator!

Unfortunately, the service locator is sometimes an unavoidable anti-pattern. In some application types—particularly Windows Workflow Foundation—the infrastructure does not lend itself to constructor injection. In these cases, the only alternative is to use a service locator. This is better than not injecting dependencies at all. For all my vitriol against the anti-pattern, it is better than instantiating new classes directly. After all, it still enables those all-important extension points provided by interfaces that allow decorators, adapters, and similar benefits.
