
```
True
id: 17, current: Sample, original: Sample, modified: False
user 2 update failed with user 2 wins
user 2 error: Database operation expected to affect 1 row(s) but actually affected 0 row(s).
Data may have been modified or deleted since entities were loaded.
See http://go.microsoft.com/fwlink/?LinkId=527962 for information on understanding and handling optimistic concurrency exceptions.
user 2 wins 0.0.0.0.0.1.1.209.
id: 17, current: user 2 wins, original: sample book, modified: True
id: 17, current: Sample, original: Sample, modified: False
updated: user 1 wins
```

When using concurrency tokens and handling the `DbUpdateConcurrencyException`, you can deal with concurrency conflicts as needed. You can, for example, automatically resolve concurrency issues. If different properties are changed, you can retrieve the changed record and merge the changes. If the property changed is a number where you do some calculations—for example, a point system—you can increment or decrement the values from both updates and just throw an exception if a limit is reached. You can also ask the user to resolve the concurrency issue by giving the user the information that’s currently in the database and ask what changes he or she would like to do. Just don’t ask too much from the user. It’s likely that the only thing the user wants is to get rid of this rarely shown dialog, which means he or she might click OK or Cancel without reading the content. For rare conflicts, you can also write logs and inform the system administrator that an issue needs to be resolved.

## Using Transactions

Chapter 37 introduces programming with transactions. With every access of the database using the Entity Framework, a transaction is involved, too. You can use transactions implicitly or create them explicitly with configurations as needed. The sample project used with this section demonstrates transactions in both ways. Here, the Menu, MenuCard, and MenuContext classes are used as shown earlier with the MenusSample project. This sample application makes use of the following dependencies and namespaces:

### Dependencies

```
NETStandard.Library
Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.SqlServer
```

### Namespaces

```
Microsoft.EntityFrameworkCore
Microsoft.EntityFrameworkCore.Storage
System.Linq
System.Threading
System.Threading.Tasks
static System.Console
```

### Using Implicit Transactions

An invocation of the `SaveChangesAsync` method automatically resolves to one transaction. If one part of the changes that need to be done fails—for example, because of a database constraint—all the changes already done are rolled back. This is demonstrated with the following code snippet. Here, the first `Menu` (`m1`) is created with valid data. A reference to an existing `MenuCard` is done by supplying the `MenuCardId`. After the update succeeds, the `MenuCard` property of the `Menu` `m1` is filled automatically. However, the second `Menu` created, `mInvalid`, references an invalid menu card by supplying a `MenuCardId` that is one value higher than the highest ID available in the database. Because of the defined foreign key relation between `MenuCard` and `Menu`, adding this object will fail (code file `TransactionsSample/Program.cs`):

```
private static async Task AddTwoRecordsWithOneTxAsync()
{
    WriteLine(nameof(AddTwoRecordsWithOneTxAsync));
    try
    {
        using (var context = new MenusContext())
        {
            var card = context.MenuCards.First();
            var m1 = new Menu
            {
                MenuCardId = card.MenuCardId,
                Text = "added",
                Price = 99.99m
            };

            int highestCardId = await context.MenuCards.MaxAsync(c => c.MenuCardId);
            var mInvalid = new Menu
            {
                MenuCardId = ++highestCardId,
                Text = "invalid",
                Price = 999.99m
            };
            context.Menus.AddRange(m1, mInvalid);

            int records = await context.SaveChangesAsync();
            WriteLine($"{records} records added");
        }
    }
    catch (DbUpdateException ex)
    {
        WriteLine($"{ex.Message}");
        WriteLine($"{ex?.InnerException.Message}");
    }
    WriteLine();
}
```

After running the application invoking the method AddTwoRecordsWithOneTxAsync, you can verify the content of the database to see that not a single record was added. The exception message as well as the message of the inner exception gives the details:

```
AddTwoRecordsWithOneTxAsync
An error occurred while updating the entries. See the inner exception for details.
The INSERT statement conflicted with the FOREIGN KEY constraint "FK_Menu_MenuCard_MenuCardId".
The conflict occurred in database "MenuCards",
table "mc.MenuCards", column 'MenuCardId'.
```

In case writing the first record to the database should be successful even if the second record write fails, you have to invoke the SaveChangesAsync method multiple times as shown in the following code snippet. In the method AddTwoRecordsWithTwoTxAsync, the first invocation of SaveChangesAsync inserts the m1 Menu object, whereas the second invocation tries to insert the mInvalid Menu object (code file TransactionsSample/Program.cs):

```
private static async Task AddTwoRecordsWithTwoTxAsync()
{
    WriteLine(nameof(AddTwoRecordsWithTwoTxAsync));
    try
    {
        using (var context = new MenusContext())
        {
            var card = context.MenuCards.First();
            var m1 = new Menu
            {
                MenuCardId = card.MenuCardId,
                Text = "added",
                Price = 99.99m
            };
            context.Menus.Add(m1);

            int records = await context.SaveChangesAsync();
            WriteLine($"{records} records added");

            int highestCardId = await context.MenuCards.MaxAsync(c => c.MenuCardId);
            var mInvalid = new Menu
            {
                MenuCardId = ++highestCardId,
                Text = "invalid",
                Price = 999.99m
            };
            context.Menus.Add(mInvalid);

            records = await context.SaveChangesAsync();
            WriteLine($"{records} records added");
        }
    }
    catch (DbUpdateException ex)
    {
        WriteLine($"{ex.Message}");
        WriteLine($"{ex?.InnerException.Message}");
    }
    WriteLine();
}
```

When you run the application, adding the first INSERT statement succeeds, but of course the second one results in a DbUpdateException. You can verify the database to see that one record was added this time:

```
AddTwoRecordsWithTwoTxAsync
1 records added
An error occurred while updating the entries. See the inner exception for details.
The INSERT statement conflicted with the FOREIGN KEY constraint "FK_Menu_MenuCard_MenuCardId".
The conflict occurred in database "MenuCards",
table "mc.MenuCards", column 'MenuCardId'.
```

### Creating Explicit Transactions

Instead of using implicitly created transactions, you can also create them explicitly. This gives you the advantage of also having the option to roll back in case some of your business logic fails, and you can combine multiple invocations of SaveChangesAsync within one transaction. To start a transaction that is associated with the DbContext derived class, you need to invoke the BeginTransactionAsync method of the DatabaseFacade class that is returned from the Database property. The transaction returned implements the interface IDbContextTransaction. The SQL statements done with the associated DbContext are enlisted with the transaction. To commit or roll back, you have to explicitly invoke the methods Commit or Rollback. In the sample code, Commit is done when the end of the DbContext scope is reached; Rollback is done in cases where an exception occurs (code file TransactionsSample/Program.cs):

```
private static async Task TwoSaveChangesWithOneTxAsync()
{
    WriteLine(nameof(TwoSaveChangesWithOneTxAsync));
    IDbContextTransaction tx = null;
    try
    {
        using (var context = new MenusContext())
        using (tx = await context.Database.BeginTransactionAsync())
        {
            var card = context.MenuCards.First();
            var m1 = new Menu
            {
                MenuCardId = card.MenuCardId,
                Text = "added with explicit tx",
                Price = 99.99m
            };
            context.Menus.Add(m1);
            int records = await context.SaveChangesAsync();
            WriteLine($"{records} records added");
            int highestCardId = await context.MenuCards.MaxAsync(c => c.MenuCardId);
            var mInvalid = new Menu
            {
                MenuCardId = ++highestCardId,
                Text = "invalid",
                Price = 999.99m
            };
        }
    }
    ...
}
```
