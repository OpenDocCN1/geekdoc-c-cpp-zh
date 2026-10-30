After all registration is complete, you need to get an instance of your resolution root: the TaskListView. The Resolve method of the container will examine the constructor of this class and try to instantiate any dependencies by examining their constructors and trying to instantiate their dependencies, and so on down the chain. Eventually, when there are no more classes to instantiate, the Resolve method is able to call the constructors that it found by passing in the instances it has created so far. This is exactly the same process that you follow when using Poor Man’s DI, but with that approach you examine the constructors manually and instantiate the classes directly.

# The Register, Resolve, Release pattern

All Inversion of Control containers reduce to a simple interface with only three methods, as shown in Listing 12-8. Unity is no exception to this and follows a similar pattern.

# LISTING 12-8 Although each implementation will embellish it, this is the general interface for all IoC containers.

```
public interface IContainer : IDisposable
{
    void Register<TInterface, TImplementation>()
        where TImplementation : TInterface;

    TImplementation Resolve<TInterface>();

    void Release();
}
```

The purpose of each of the three methods is explained in the following list:

+   - **Register** This method is called first, at application initialization. It will be called many times to register many different interfaces to their implementations. The where clause enforces the constraint that the TImplementation type must implement the TInterface type. Other permutations of this method allow you to register an already-constructed instance of a class and a type without a specific interface. (Such a type will be registered against all the interfaces it implements.)

+   - **Resolve** This method is called during the running of the application. It is common for a particular family of classes to be resolved as the top-level object of the graph. For example, this would be the controllers in an ASP.NET Model-View-Controller (MVC) application, the viewmodels in a ViewModel-first WPF application, and the views in a Windows Forms Model-View-Presenter (MVP) application. The call to this method should be an infrastructural concern. That is, you should not call Resolve inside your application’s classes for controllers, views, presenters, services, domain, business logic, or data access.

+   - **Release** At some point, the classes will no longer be needed and their resources can be released. This might happen at the end of the application, but it also could happen at a more opportune moment during the application’s lifetime. In a web scenario, for example, it is common for resources to live only per-request. Thus, Release could be called at the end of each request. This sort of object lifetime concern is discussed in more detail later.