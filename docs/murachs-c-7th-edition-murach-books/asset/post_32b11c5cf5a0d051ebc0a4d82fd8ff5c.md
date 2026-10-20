
## Code that handles database exceptions

```
private void btnDelete_Click(object sender, EventArgs e)
{
    DialogResult result =
        MessageBox.Show("Delete " + selectedCustomer.Name + "?",
        "Confirm Delete", MessageBoxButtons.YesNo, MessageBoxIcon.Question);
    if (result == DialogResult.Yes)
    {
        try
        {
            context.Customers.Remove(selectedCustomer);
            context.SaveChanges(true);
            this.ClearControls();
        }
        catch (DbUpdateException ex)
        {
            string errorMessage = "";
            var sqlException = (SqlException)ex.InnerException;
            foreach (SqlError error in sqlException.Errors)
            {
                errorMessage += "ERROR CODE:  " + error.Number + "  " + error.Message + "\n";
            }
            MessageBox.Show(errorMessage);
        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message, ex.GetType().ToString());
        }
    }
}
```

## A using directive for the SQL Server data provider

```
using Microsoft.Data.SqlClient;
```

## Description

- The DbUpdateException is thrown by the DB context when changes can’t be saved to the database.
- When you catch the DbUpdateException, you must cast it to the appropriate exception type for the database you’re using. Then, you can use the InnerException property of that type to get the actual exception that occurred.
- The InnerException property contains a collection of one or more errors. You can refer to this collection using the Errors property, and you can get a count of the errors using the Count property of the Errors property.
- One way to handle the DbUpdateException is to iterate through the collection of errors and display information about each error. To do that, you can use properties of each error like the Number and Message properties shown above.
- Another way to handle the DbUpdateException is to check for specific error numbers. Although this is more cumbersome, it allows you to display your own custom messages.

## How concurrency affects insert, update, and delete operations

When using EF, a common problem is the conflict that can occur when two or more users retrieve data in the same row of a table and then try to update that row. This is called a concurrency conflict. It’s possible because once a program retrieves data from a database, the connection to that database is dropped. As a result, the database management system can’t manage the update process.

To illustrate, consider the diagram shown in figure 20-13. Here, two users have retrieved the Products table from a database, so a copy of the Products table is stored on each user’s computer. These users could be using the same program or two different programs. Now, suppose that user 1 modifies the unit price in the row for product CPLS and updates the Products table in the database. Then, suppose that user 2 modifies the description in the row for the same product and attempts to update the Products table in the database. What will happen? That depends on the concurrency control’s used by the programs.

When you use EF core, you have two main choices for concurrency control. By default, a program uses the last in wins technique, which works the way its name implies. Since no checking is done with this technique, the row that’s updated by the last user overwrites any changes made to the row by a previous user. For the example above, the row updated by user 2 overwrites changes made by user 1, which means that the description is right but the unit price is wrong.

To prevent data errors like this, many programs use a technique known as optimistic concurrency that checks whether a row has been changed since it was retrieved. If so, it doesn’t save the data. Instead, it throws a concurrency exception. Then, the program can handle the concurrency exception.

If you know that concurrency conflicts will be a problem, you can use a couple of programming techniques to limit concurrency exceptions. One technique is to update the database frequently so other users can retrieve the current data. The program should also refresh its entity collections frequently so it contains the recent changes made by other users. To do that, you simply create a new instance of the DB context. Then, the next time you retrieve rows, they’ll be retrieved from the database.

Another way to avoid concurrency exceptions is to retrieve and work with just one row at a time. That way, it’s less likely that two users will update the same row at the same time. By contrast, if two users retrieve the same table, they will of course retrieve the same rows. Then, if they both update the same row in the table, even though it may not be at the same time, a concurrency exception will occur when they try to update the database.

Because most database applications are multi-user applications, you have to add code to them to deal with concurrency conflicts. In the topics that follow, then, you’ll learn how to configure entities so they use optimistic concurrency. Then, you’ll learn how to handle concurrency exceptions when they occur.

You should also be aware of a third technique, pessimistic concurrency, that assumes conflicts will happen (it’s pessimistic about them) and locks the database to avoid them. Since pessimistic concurrency is rarely used, this book only shows how to work with optimistic concurrency.

## Two users who are working with copies of the same data

![](img/844f608d10a44654833ea5efc8a2e7a7_683_0.png)

## What happens when two users try to update the same row?

- When two or more users retrieve the data in the same row of a database table at the same time, it is called a concurrency conflict. Because EF Core uses a disconnected data architecture, the database management system can’t prevent this from happening.
- If two users try to update the same row in a database table at the same time, the second user’s changes could overwrite the changes made by the first user. Whether or not that happens, though, depends on the concurrency control that the programs use.
- By default, EF Core uses last in wins. This means that the program doesn’t check whether a row has been changed before an update or delete operation takes place. Instead, the operation proceeds without throwing an exception. This can lead to errors in the database.
- With optimistic concurrency, the program checks whether the database row that’s going to be updated or deleted has been changed since it was retrieved. If it has, a concurrency exception occurs and the update or delete operation is refused. Then, the calling program should handle the exception.

## How to avoid concurrency conflicts

- For many applications, concurrency conflicts rarely occur. As a result, optimistic concurrency is adequate because the users will rarely have to resubmit an update or deletion that is refused.
- If concurrency conflicts are likely to be a problem, a program can be designed so it updates the database and refreshes the entity collections frequently. That way, concurrency errors are less likely to occur.
- Another way to avoid concurrency conflicts is to design a program so it retrieves and updates just one row at a time. That way, there’s less chance that two users will retrieve and update the same row at the same time.
- A program can also use pessimistic concurrency, which assumes that concurrency conflicts will happen and avoids them by locking a database record while it’s being updated. Since locking database records creates its own problems, most applications don’t use pessimistic concurrency.

## How to configure a concurrency token with attributes

```
public class Customers {
    public int CustomerId { get; set; }
    public string Name {get; set; }

    [ConcurrencyCheck]
    public string Address {get; set; }
    .
    .
}
```

## How to configure a rowversion property with attributes

```
public class Customers {
    public int CustomerId { get; set; }
    public string Name { get; set; }
    public string Address { get; set; }
    .
    .
    [Timestamp]
    public byte[] RowVersion { get; set; }
}
```

## How to simulate a concurrency conflict

```
var c = context.Customers.Find(1);    // get a customer from the database

context.Database.ExecuteSqlRaw(
    "UPDATE Customers " +
    "SET Address = '1 Main St' " +
    "WHERE CustomerId = 1");    // change address in the database

c.Address = "26 Duffie Drive";    // change address in entity
context.SaveChanges();
```

## Description

- To check an individual property for a concurrency conflict, you configure the property with a *concurrency token*. To do that, you add the ConcurrencyCheck attribute to the property.
- To check all the properties in an entity for conflicts, you use a *rowversion property*. To use a rowversion property with a SQL Server database, you must first add a column with the rowversion data type to the corresponding database table. Then, the rowversion property will be generated for you when you generate the DB context. However, you may need to manually add the TimeStamp attribute to this property.
- To simulate a concurrency conflict so you can test your exception handling code, you can use the ExecuteSQLRaw() method of the DbContext class’s Database property. This command lets you execute a query against the database. You can use it to update or delete a row that you’ve previously retrieved into the DB context. Then, when you update that row or mark it for deletion and save the changes to the database, a concurrency exception will occur.
