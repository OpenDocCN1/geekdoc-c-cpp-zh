```
var query = from s in context.Suppliers
             select new { s.CompanyName, s.City };
foreach (var item in query)
    Console.WriteLine(item.CompanyName + " " + item.City );
```

An anonymous type is declared in-place, with property names inferred from the names of the Supplier properties that provide the values. It serves as a Data Transfer Object (DTO) that holds Supplier property values in place of the actual Supplier instances. This particular code could be also rewritten to use an explicitly defined DTO class, like so:

```
class SupplierProjection
{
    public string CompanyName;
    public string City;
}

var query = from s in context.Suppliers
            select new SupplierProjection
            {
                CompanyName = s.CompanyName,
                City = s.City
            };
```

As you can see, the version based on the anonymous type is much more concise and closely resembles the SQL syntax. However, visibility of anonymous types is limited to the methods where they are defined. You need to declare the projection classes explicitly if you need to pass the DTOs to another function for further processing.

> **NOTE**
> 
> Projection objects are not entity instances. They do not participate in the identity management process of the ObjectContext and cannot be used to change the underlying database records.

# Sorting

The orderby LINQ keyword can be used to sort query results. Here is how you could sort the list of Products in the order of UnitPrice, from highest to lowest:

```
var query = from p in context.Products
            orderby p.UnitPrice descending
            select p;
```

By default, orderby acts like its counterpart in SQL: Sorting is performed in ascending order. To reverse the sort order for a property, use the descending LINQ keyword after the