# # A method that handles a concurrency exception

```
```csharp
private void btnModify_Click(object sender, EventArgs e)
{
    // code that retrieves and updates a Customers object
    try
    {
        context.SaveChanges();
        this.DisplayCustomer();
    }
    catch (DbUpdateConcurrencyException ex)
    {
        ex.Entries.Single().Reload();
        if (context.Entry(customer).State == EntityState.Detached)
        {
            MessageBox.Show("Another user has deleted that customer.",
                "Concurrency Error");
            this.ClearControls();
        }
        else
        {
            string message = "Another user has updated that customer.\n" +
                "The current database values will be displayed.";
            MessageBox.Show(message, "Concurrency Error");
            this.DisplayCustomer();
        }
    }
    catch (DbUpdateException ex) {...}
    catch (Exception ex) {...}
}
```
```



+   - The DbUpdateConcurrencyException is thrown when a concurrency conflict occurs.
+   - To get a collection of the entities that caused the concurrency exception, you use the Entries property of the DbUpdateConcurrencyException class.
+   - You can use a loop to iterate over the Entries collection. Or, if you're updating or deleting a single entity, you can use the Single() method to get an EntityEntry object for that entity.
+   - You can use the Reload() method of the EntityEntry object to load the current database values into the entity.
+   - You can use the Entry() method of the DB context to check whether the entity is detached. If it is, you know that row has been deleted in the database.
+   - Because DbUpdateConcurrencyException is a subclass of DbUpdateException, you must catch this exception before you catch DbUpdateException.

> Figure 20-15 How to handle concurrency exceptions