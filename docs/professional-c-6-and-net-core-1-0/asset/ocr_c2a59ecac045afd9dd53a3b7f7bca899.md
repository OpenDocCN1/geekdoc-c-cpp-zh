type: Menu, state: Unchanged, Baked Potato Soup

When you access the entries from the change tracker, by default changes are automatically detected. You configure this by setting the AutoDetectChangesEnabled property of the ChangeTracker. For checking manually to see whether changes have been done, you invoke the method DetectChanges. With the invocation of SaveChangesAsync, the state is changed back to Unchanged. You can do this manually by invoking the method AcceptAllChanges.

# Updating Untracked Objects

Object contexts are usually very short-lived. Using Entity Framework with ASP.NET MVC, with one HTTP request one object context is created to retrieve objects. When you receive an update from the client, the object must again be created on the server. This object is not associated with the object context. To update it in the database, the object needs to be associated with the data context, and the state changed to create an INSERT, UPDATE, or DELETE statement.

Such a scenario is simulated with the next code snippet. The GetMenuAsync method returns a Menu object that is disconnected from the context; the context is disposed at the end of the method (code file MenusSample/Program.cs):

```
private static async Task<Menu> GetMenuAsync()
{
    using (var context = new MenusContext())
    {
        Menu menu = await context.Menus
            .Skip(2)
            .FirstOrDefaultAsync();
        return menu;
    }
}
```

The GetMenuAsync method is invoked by the method ChangeUntrackedAsync. This method changes the Menu object that is not associated with any context. After the change, the Menu object is passed to the method UpdateUntrackedAsync to save it in the database (code file MenusSample/Program.cs):

```
private static async Task ChangeUntrackedAsync()
{
    Menu m = await GetMenuAsync();
    m.Price += 0.7m;
    await UpdateUntrackedAsync(m);
}
```

The method UpdateUntrackedAsync receives the updated object and needs to attach it with the context. One way to attach an object with the context is by invoking the Attach method of the DbSet, and set the state as needed. The Update method does both with one call: attaching the object and setting the state to Modified (code file MenusSample/Program.cs):