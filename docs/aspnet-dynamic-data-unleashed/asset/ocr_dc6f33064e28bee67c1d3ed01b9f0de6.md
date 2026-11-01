Notice that the FilteredObjectSet constructor takes the original ObjectSet instance as a parameter and stores it in the private field. Most of the properties and methods, such as AddObject, simply call the same method on the original instance. However, the Expression, ElementType, and Provider properties that implement the IQueryable interface are different; they also take into account the CustomQueryAttribute that might be applied to the entity type. Instead of delegating their implementation directly to the original ObjectSet, these properties delegate to the object returned by the GetQueryable method, which returns the original if the entity type has no CustomQueryAttribute or the modified query if it does.

# NOTE

By having FilteredObjectSet class reimplement the IObjectSet interface instead of inheriting from the built-in ObjectSet class, you lose the ability to access some of the additional APIs the Entity Framework provides on top of the plain LINQ, such as the Include method discussed in Chapter 2, "Entity Framework." Although it is usually possible to work around the loss of this particular extension and others, you might find this approach impractical if your application uses them pervasively.

With the FilteredObjectSet implemented and the T4 template modified to generate object set properties based on it, you now have row-level security available in any application using the NorthwindEntities object context. For instance, the following pseudo-code returns just one Customer entity when the current user of the application is in the Customer role and all entities when the current user is a Manager or an Employee:

```
using (var context = new NorthwindEntities())
{
    var customers = context.Customers;
}
```

The automatic filtering will work with LINQ queries as well, so the following pseudo-code will not allow a customer from New York to access records of customers in London:

```
using (var context = new NorthwindEntities())
{
    var customers = context.Customers.Where(c => c.City == "London");
}
```

However, just like authorization of Read access discussed in the previous section, this limited implementation of row-level security can be circumvented by LINQ queries that do not use the Customers object set directly. Queries that return Customer information via navigation properties or projection allow unrestricted access, and if you plan to take advantage of this functionality in your applications, keep in mind you cannot rely on it exclusively.