```
"server=(localdb)\MSSQLLocalDb;database=SampleDatabase;trusted_connection=true""EntityFramework.MicrosoftSqlServer"
```

The `dbcontext` command enables you to list `DbContext` objects from the project, as well as create `DBContext` objects. The command `scaffold` creates `DbContext`-derived classes as well as model classes. The `dnx ef dbcontext scaffold` needs two required arguments: the connection string to the database and the provider that should be used. With the statement shown earlier, the database `SampleDatabase` was accessed on the `SQL Server (localdb)\MSSQLLocalDb`. The provider used was `EntityFramework.MicrosoftSqlServer`. This NuGet package as well as the NuGet package with the same name and the `Design` postfix need to be added to the project.

After running this command, you can see the `DbContext` derived classes as well as the model types generated. The configuration of the model by default is done using the fluent API. However, you can change that to using the data annotations supplying the `-a` option. You can also influence the generated context class name as well as the output directory. Just check the different available options using the option `-h`.

# Working with Object State

After creating the database, you can write to it. In the first sample you’ve written to a single table. What about writing a relationship?

# Adding Objects with Relations

The following code snippet writes a relationship, a `MenuCard` containing `Menu` objects. Here, the `MenuCard` and `Menu` objects are instantiated. The bidirectional associations are assigned. With the `Menu`, the `MenuCard` property is assigned to the `MenuCard`, and with the `MenuCard`, the `Menus` property is filled with `Menu` objects. The `MenuCard` instance is added to the context invoking the `Add` method of the `MenuCards` property. When you add an object to the context, by default all objects are added to the tree with the state added. Not only the `MenuCard` but also the `Menu` objects are saved. `IncludeDependents` is set. With this option, all the associated `Menu` objects are added to the context as well. Invoking `SaveChanged` on the context now creates four records (code file `MenusSample/Program.cs`):

```
private static async Task AddRecordsAsync()
{
    // etc.
    using (var context = new MenusContext())
    {
        var soupCard = new MenuCard();
        Menu[] soups =
        {
            new Menu
            {
                Text ="Consomm&eacute; C&eacute;lestine (with shredded pancake)",
                Price = 4.8m,
```