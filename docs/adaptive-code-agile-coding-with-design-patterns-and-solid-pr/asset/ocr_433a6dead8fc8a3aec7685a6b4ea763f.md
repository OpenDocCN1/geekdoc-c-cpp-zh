Even with this change, the controller from the multiple implementation example is sufficient: it correctly asks for each interface as a separate constructor parameter. What needs to change is how you construct the controller and supply it with those parameters. This is shown in Listing 10-19.

# LISTING 10-19 Although it might look unusual, this is an expected side effect of interface segregation.

```
public OrderController CreateSingleService()
{
    var crud = new CreateReadUpdateDelete<Order>();
    return new OrderController(crud, crud, crud);
}
```

First, you only need a single instance of the CreateReadUpdateDelete class. It implements all three interfaces, so it suffices for all three constructor parameters.

As unusual as that might look—passing in the same instance three times—it makes sense because each parameter requires a different facet of the class. This is a common side effect of the interface segregation principle.

Of the two variations explored, this single implementation for a suite of related—but segregated—interfaces is not as versatile as having multiple implementations. It is most commonly used for the leaf implementation of the interfaces—that is, the implementation that is neither decorator nor adapter. It is the one that does the actual work. The reason for this is that the context is the same across all implementations. Whether you are using NHibernate, ADO.NET, Entity Framework, or some other persistence framework, the leaf implementation is the one that directly uses these libraries. In each case—reading, saving, or deleting—that same library will be used to do the main work.

Some decorators and adapters also apply to the full suite of segregated interfaces, but it is more common for these to be implemented individually only on the appropriate interface.

# The Interface Soup anti-pattern

A common mistake is to take the segregated interfaces and reunify them in an aggregate interface for some reason, as Listing 10-20 demonstrates. This is usually done to avoid the odd-looking multiple injection shown earlier.

# LISTING 10-20 Interface segregation is wrongly circumvented when all interfaces are thrown together to form a soup.

```
interface IInterfaceSoupAntiPattern<TEntity> : IRead<TEntity>, ISave<TEntity>, IDelete<TEntity>
{
}
```