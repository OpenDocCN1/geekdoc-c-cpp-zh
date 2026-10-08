A DI container behaves like a registry of interface-class associations, named class instances. Before using the container to resolve a specific interface, you must first register that interface with a concrete implementation.

# Service Locator Pattern

The Service Locator Pattern centralizes distributed service object lookups, provides a centralized point of control, and may act as a cache that eliminates redundant lookups. Used in software development to encapsulate the processes involved in obtaining a service with a strong abstraction layer.

In a decoupled system, you do not have the knowledge of the environment in which your code will run, or you may want to create a component that may be able to run in several environments. For example, you may need a component that can be used both in a web application and in a Windows service. In the latter case, you do not have access to a valid HttpClient instance, but you can have a dependency on some interface implementation like an IEmailSenderService.

A Service Locator implementation provides a singleton instance of itself, and it requires only a one-time registration of the DI container that holds the registry data.

Listing 18-4 shows how a service can be resolved using a ServiceLocator implementation for Unity.

# LISTING 18-4: BookService Class Using ServiceLocator to Resolve Another Service

```
```
public class BookService{
    public SendMailAboutNewBooks ({
        var emailSenderService = ServiceLocator.Current;
        GetInstance<IEmailSenderService>();
    }
}
```
```

# Extensibility in MVC

The MVC framework was built with extensibility in mind. The design patterns play an important role in the extensibility features of MVC. With these features, you can customize the whole framework to your taste.

Internally, MVC is built as a coherent set of independent components that can be replaced by other components. You have a default implementation of MVC components that you can use with your application. However, if you need something more sophisticated than the default implementation, you have two options:

+   - You can inherit from the classes representing MVC components and implement your own components with more control — or on the contrary, simplify them (for example, using default values).