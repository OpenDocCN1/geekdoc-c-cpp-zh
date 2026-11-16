```
Description = "A brand new product"
};
context.Products.Add(newProduct);
context.SaveChanges();
}
```

In this code snippet, we create a new Product object, set its properties, add it to the Products DbSet, and then call SaveChanges() to persist the changes to the database.

# **Read: Retrieving Data**

The Read operation involves fetching data from the database. EF Core provides a rich set of querying capabilities, including LINQ support, to retrieve data based on various criteria.

Let's see how to retrieve all products from the database:

C#

```
using (var context = new ApplicationDbContext())
{
    var products = context.Products.ToList();
    foreach (var product in products)
    {
        Console.WriteLine($"{product.Name} - {product.Price}");
    }
}
```