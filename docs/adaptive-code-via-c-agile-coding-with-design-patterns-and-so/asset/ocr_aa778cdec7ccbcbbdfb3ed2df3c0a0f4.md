This is due to the relative dependencies involved. One decorator depends on the IEventPublisher interface, whereas the other depends on the AuditInfo class. It would be better instead to separate those implementations into their own assemblies with their own dependency chains.

# Client construction

The design of interfaces—segregated or otherwise—affects the classes that implement the interfaces and also the clients that use the interfaces. If clients are to use interfaces, they must in some way be supplied them. This chapter will continue, for the most part, to manually construct the implementations and provide them to clients via constructor parameters. For an alternative option, see the next chapter, which covers dependency injection.

The manner in which you supply the implementations to clients is partly dictated by the number of implementations of the segregated interfaces. If each interface is given its own implementation, each of those implementations needs to be constructed and supplied to the client. Alternatively, if all of the interfaces are implemented in a single class, a single instance is sufficient for all of the related dependencies on the client.

# Multiple implementations, multiple instances

Continuing the CRUD example, assume that the IRead, ISave, and IDelete interfaces have all been implemented by different, distinct classes. A client needing to use these interfaces will, because of segregation, require three interfaces whereas it previously only required one. Such a client is shown in Listing 8-15.

LISTING 8-15 The order-specific controller requires each facet of CRUD as a separate dependency.

Click here to view code image

```
public class OrderController
{
    private readonly IRead<Order> reader;
    private readonly ISave<Order> saver;
    private readonly IDelete<Order> deleter;

    public OrderController(IRead<Order> orderReader, ISave<Order> orderSaver, IDelete<Order> orderDeleter)
    {
        reader = orderReader;
        saver = orderSaver;
        deleter = orderDeleter;
    }

    public void CreateOrder(Order order)
    {
        saver.Save(order);
    }
}
```