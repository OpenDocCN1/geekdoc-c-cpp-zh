Then you made a simple LINQ query to list all the stores' information:

```
var query = from store in db.Stores
            orderby store.Name
            select store;
```

The code to print out the results of the query is very straightforward because it simply deals with objects and collections, no database-specific code:

```
WriteLine("Bookstore Inventory Report:");
foreach (var store in query)
{
    WriteLine($"{store.Name} located at {store.Address}");
    foreach (Stock stock in store.Inventory)
    {
        WriteLine($"-- Title: {stock.Item.Title}");
        WriteLine($"-- Copies in Store: {stock.OnHand}");
        WriteLine($"-- Copies on Order: {stock.OnOrder}");
    }
}
```

To print the inventory under each store, you simply use a foreach loop like with any collection.

# HANDLING MIGRATIONS

Inevitably as you develop your code, you are going to change your mind. You will come up with a better name for one of your properties, or you will realize you need a new class or relationship. If you change the code in a class connected to a database, via the Entity Framework, you will encounter the Invalid Operation Exception shown in Figure 21-14 when you first run the changed program.

![](bbox=[0.15, 0.72, 0.5, 0.82])

FIGURE 21-14

Keeping the database up to date with your changed classes is complicated, but again the Entity Framework steps in with a facility to make it relatively easy. As the error message suggests, you need to add the Code First Migrations package to your program.

To do this, go to Tools ⌘ NuGet Package Manager ⌘ Package Manager Console. This brings up a command window as shown in Figure 21-15.

To enable automatic migration of your database to your updated class structure, enter this command in the Package Manager Console at the PM> prompt:

```
Enable-Migrations -EnableAutomaticMigrations
```