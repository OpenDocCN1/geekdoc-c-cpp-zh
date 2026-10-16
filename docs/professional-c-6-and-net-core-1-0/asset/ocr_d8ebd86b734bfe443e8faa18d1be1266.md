System.Linq

System.Threading

System.Threading.Tasks

static System.Console

# Using Implicit Transactions

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