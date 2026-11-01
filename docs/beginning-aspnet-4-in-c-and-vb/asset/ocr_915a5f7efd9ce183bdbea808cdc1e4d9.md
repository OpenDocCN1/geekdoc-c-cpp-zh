or one-to-many relationship with Customer and Order because the CustomerID with the Order table is defined as Nullable in the database schema.

![](bbox=[0.12, 0.2, 0.7, 0.48])

# FIGURE 31-6

You access the customers and their orders with two iterations shown here. First the Customer objects are accessed, and the value of the CompanyName property is written to the console. Then all orders are accessed by using the Orders property of the Customer class. The related orders are lazy loaded to access the property because with the ObjectContext the ContextOptions.LazyLoadingEnabled property is set to true:

```
```csharp
using (var data = new NorthwindEntities())
{
    foreach (Customer customer in data.Customers)
    {
        Console.WriteLine("{0}", customer.CompanyName);

        foreach (Order order in customer.Orders)
        {
            Console.WriteLine("\t{0} {1:d}", order.OrderID, order.OrderDate);
        }
    }
}
```
```

code snippet NorthwindDemo/Program.cs

Behind the scenes, the RelationshipManager class is used to access the relationship. The RelationshipManager instance can be accessed by casting the entity object to the interface IEntityWithRelationships as you can see in the designer-generated property Orders from the class Customer. This interface is explicitly implemented by the class EntityObject. The RelationshipManager property returns a RelationshipManager that is associated with the entity object at one end. The other end is defined by invoking the method GetRelatedCollection(). The first parameter NorthwindModel.FK_Orders_Customers is the name of the relationship; the second parameter Orders defines the name of the target role:

```
```csharp
public EntityCollection<Order> Orders
{
    get
    {
        return ((IEntityWithRelationships)this).RelationshipManager.
            GetRelatedCollection<Order>("NorthwindModel.FK_Orders_Customers",
            "Orders");
    }
    set
```
```