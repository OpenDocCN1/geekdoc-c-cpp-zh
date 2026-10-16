```
private static async Task UpdateUntrackedAsync(Menu m)
{
    using (var context = new MenusContext())
    {
        ShowState(context);

        // EntityEntry<Menu> entry = context.Menus.Attach(m);
        // entry.State = EntityState.Modified;

        context.Menus.Update(m);
        ShowState(context);

        await context.SaveChangesAsync();
    }
}
```

When you run the application with the ChangeUntrackedAsync method, you can see that the state is modified. The object was untracked at first, but because the state was explicitly updated, you can see the Modified state:

```
type: Menu, state: Modified, Cheddar Broccoli Soup
```

# Conflict Handling

What if multiple users change the same record and then save the state? Who will win with the changes?

If multiple users accessing the same database work on different records, there’s no conflict. All users can save their data without interfering with data edited by other users. If multiple users work on the same record, though, you need to give some thought to conflict resolution. You have different ways to deal with this. The easiest one is that the last one wins. The user saving the data last overwrites changes from the user that did the changes previously.

Entity Framework also offers a way for letting the first one win. With this option, when saving a record, a verification is needed if the data originally read is still in the database. If this is the case, saving data can continue as no changes occurred between reading and writing. However, if the data changed, a conflict resolution needs to be done.

Let’s get into these different options.

# The Last One Wins

The default scenario is that the last one saving changes wins. To see multiple accesses to the database, the BooksSample application is extended.

For an easy simulation of two users, the method ConflictHandlingAsync invokes the method PrepareUpdateAsync two times, makes different changes to two Book objects that reference the same record, and invokes the UpdateAsync method two times. Last, the book ID is passed to the CheckUpdateAsync method, which shows the actual state of the book from the database (code file