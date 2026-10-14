When you are using DI, each type of application requires a different kind of setup. With each, you need to identify the composition root in order to correctly integrate your registration code. The location of the composition root in a WPF application differs from that of a Windows Forms application. Both will differ from that of an ASP.NET MVC application.

In advanced scenarios, the manual composition of classes through Poor Man’s DI and the individual registration of classes through an Inversion of Control container are both too laborious and verbose. By deferring registration to one or more conventions, you can eliminate a lot of boilerplate code but also provide some manual registration, to handle the edge cases when conventions do not suffice.

# The Service Locator anti-pattern

Service locators look very similar to Inversion of Control containers, which is precisely why they are not always thought of as detrimental to the code. Listing 9-20 shows an example of the service locator provided by the Patterns and Practices team at Microsoft.

# LISTING 9-20 The IServiceLocator interface appears to be just another IoC container.

Click here to view code image

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

Note that methods such as TService GetInstance<TService>() could have been taken directly from the IUnityContainer interface—just by swapping the name for Resolve. The problem arises from how a service locator is used, thanks to the static ServiceLocator class, as shown in Listing 9-21.

# LISTING 9-21 This static class is the cause of the anti-pattern.

Click here to view code image

```
/// <summary>
/// This class provides the ambient container for this application. If your
/// framework defines such an ambient container, use ServiceLocator.Current
```