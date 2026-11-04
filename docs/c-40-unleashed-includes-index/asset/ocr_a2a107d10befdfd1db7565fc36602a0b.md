involve making changes to retrieved data; for example, through some data visualization in a UI control like a data grid. Similarly, records can be inserted into or deleted from the database by manipulating the table objects through the data context:

```
ctx.Products.InsertOnSubmit(new Product() { ProductName = "Visual Studio", ... });

// Deleting an object that was retrieved before, e.g. because the user
// deleted it from a grid control.
Product chai = /* retrieved somehow through a query */;
ctx.Products.DeleteOnSubmit(chai);

// Change tracking through INotifyPropertyChanged tells the context the
// object needs to be updated upon calling SubmitChanges.
Product chang = /* retrieved somehow through a query */;
chang.UnitPrice = chang.UnitPrice * 1.2;

ctx.SubmitChanges();
```

Finally, notice how the relational nature of the database is reflected in the generated objects. You can easily write queries that traverse relationships; for example, querying products by their categories:

```
var beverages = from product in ctx.Products
                where product.Category.CategoryName == "Beverages"
                select product;
```

The query generated for the preceding code involves quite a bit of domain-specific query language knowledge on joins. Without the help of LINQ, the developer would have to figure this out herself, with opportunity for mistakes to sneak in. (For example, the preceding query would likely be parameterized on "Beverages", making plain string concatenation an obvious, but dangerous, choice because of potential SQL injection attacks.) Instead, LINQ to SQL takes care of all of this and generates the following:

```
SELECT [t0].[ProductID], [t0].[ProductName], [t0].[SupplierID],
[t0].[CategoryID], [t0].[QuantityPerUnit], [t0].[UnitPrice],
[t0].[UnitsInStock], [t0].[UnitsOnOrder], [t0].[ReorderLevel],
[t0].[Discontinued]
FROM [dbo].[Products] AS [t0]
LEFT OUTER JOIN [dbo].[Categories] AS [t1]
    ON [t1].[CategoryID] = [t0].[CategoryID]
WHERE [t1].[CategoryName] = @p0
```

Notice the use of parameterization as way to hand over query parameters like "Beverages" in a safe manner so that the database can take care of input checking.