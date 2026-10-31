container is created. Our application maps a request URL to a page type, and it contains the following generic code that creates new request handlers for a given page type:

```
public RequestHandlerFactory {
    IPicoContainer sessionContainer;

    public Page CreatePage(Type pageType) {
        IImmutablePicoContainer reqContainer = CreateRequestContainer();
        reqContainer.RegisterComponentImplementation(pageType);
        return (Page)reqContainer.GetComponentInstance(pageType);
    }
    private IImmutablePicoContainer CreateRequestContainer() {
        IImmutablePicoContainer pc = new DefaultPicoContainer(sessionContainer);
        pc.RegisterComponentImplementation (typeof(SqlDbConnection));
        /* register all other components here that should be available
           to requests on a per request basis. */
        return pc;
    }
}
```

After the request container is created in the CreatePage() method, the code registers the page type with the request container so that the page itself can use dependency injection. When it retrieves the actual page instance in the third line, the request container tries to create the page but, assuming a ResultPage is required, it cannot resolve the dependency on the Logger class because this has not been registered with the request container. In this situation, it will try to obtain the missing component from its parent, the session container, which also does not contain a logger and thus requests the logger from its parent, the application container. Provided that a logger is registered with that container, all dependencies for the page can be satisfied and it is created by the request container.

The advantage of this approach is that on the one hand components can be registered and shared at the appropriate level, while on the other hand objects that retrieve components from a container only have to deal with one container and can rely on it to find the required components in the chain of containers.

# Service Locator Versus Dependency Injection

At this point we have discussed two different patterns that solve the coupling and instance management issues described at the beginning of this chapter. The question remaining is when to use which pattern.

It is safe to say that the Service Locator pattern is more commonly used today, but this is not necessarily because it is a better match for most applications. Instead, the most likely reason is that the Service Locator pattern has been around for a long time while Dependency Injection is a comparatively new pattern that is not as well known yet. In fact, developers arrived at the Dependency Injection pattern when they tried to improve the Service Locator pattern.

The complete decoupling of the components from the dependency resolution mechanism that is achieved by the Dependency Injection pattern improves testability because the tests do not have to set up specialized versions of a locator to provide stubs or mocked objects. It also helps with reuse