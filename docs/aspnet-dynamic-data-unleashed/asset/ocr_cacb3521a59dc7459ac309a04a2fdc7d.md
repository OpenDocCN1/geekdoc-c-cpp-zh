```
Category wines = context.Categories
.FirstOrDefault(c => c.CategoryName == "Wines");
if (wines == null)
{
    wines = new Category() { CategoryName = "Wines" };
    context.Categories.AddObject(wines);
}

Product p = new Product() { ProductName = "Mukuzani", Category = wines };
context.Products.AddObject(p);

context.SaveChanges();
transaction.Complete();
}
```

In this new version of the code, the TransactionScope class from the System.Transactions assembly and namespace is being used. By creating a new instance of this class, you start a database transaction (think of it as of the BEGIN TRANSACTION statement in SQL for now) and by calling the Complete method, you are committing it (COMMIT TRANSACTION). The TransactionScope class implements the IDisposable interface so that when a transaction scope instance is disposed and the Complete method has not been called, the transaction is automatically rolled back. By placing the TransactionScope instance inside of the using statement you guarantee that if any exceptions are thrown while you are manipulating the Category and Product instances and the Complete method doesn't get called, the entire transaction will be rolled back (ROLLBACK TRANSACTION) before control leaves this code.

TransactionScope instances can be hierarchical. If your method creates a transaction scope and calls another method that creates its own, by default this second transaction scope becomes a part of the first one, and any changes performed within it are executed as part of the same database transaction. TransactionScope also supports distributed transactions that span multiple databases or servers. Simply place all relevant code inside of a single TransactionScope, and it will automatically escalate the transaction from a single server to the Microsoft Distributed Transaction Coordinator (DTC) to perform a two-phase commit.

# Read-Only ObjectContext

Preserving object identity and keeping track of changes are great features when you are writing code that needs to not only retrieve data from the database, but also make changes. However, it requires the ObjectContext to check every database row against the internal dictionary of previously materialized objects and store both original and current values of all entity properties. This comes at the cost of additional CPU resources required to perform the lookup and increased memory consumption to store the additional property values. The tradeoff is usually well justified in a typical rich-client application that