# 472 SQL Server Database Programming with C#

C. The selected image is converted to a byte array img[], and furthermore converted to a String with a Base64String format.

D. Finally, String is formatted and assigned to the ImageUrl property of the Faculty Image box, PhotoBox, to be displayed.

Now let's concentrate on the coding for our data insertion actions. However, before we can continue building our codes to insert a new record into our database with the LINQ to SQL method, let's have a discussion about a key component, the DataContext class, with its methods to provide us a clear picture about DataContext and its implementations.

# 8.7.4.3 The DataContext Class and its Implementations

As discussed in Chapter 4, the DataContext is the source of all entities mapped over a database connection. It tracks changes that you made to all retrieved entities and an identity code that guarantees entities more than one are represented by using the same object instance.

In general, a DataContext is designed to last one unit of work; however, your application defines that. A DataContext is lightweight and not expensive to create. A LINQ to SQL application creates DataContext instances at method scope or as a map of short-lived classes that represent a logical set of related database operations.

Four constructors are involved with this class, the DataContext class contains 30 methods, the most popular methods are listed in Figure 8.64. Among these popular, the following methods are most important in the LINQ to SQL implementations:

+   * ExecuteCommand()
* ExecuteQuery()

FIGURE 8.63 Constructors of the DataContext class.

| Constructor | Functions |
|---|---|n| DataContext(Connection) | Initializes a new instance of the DataContext class by referencing the connection used by the .NET Framework. |
| DataContext(Connection, Source) | Initializes a new instance of the DataContext class by referencing a connection and a mapping source. |
| DataContext(String) | Initializes a new instance of the DataContext by referencing a file source. |
| DataContext(String, Source) | Initializes a new instance of the DataContext by referencing a file source and a mapping source. |

| Methods | Functions |
|---|---|n| CreateDatabase() | Dynamically creates a new database on the server. |
| DatabaseExists() | Determines whether the associated database can be opened. |
| DeleteDatabase() | Deletes the associated database. |
| ExecuteCommand(String, Object[1]) | Executes SQL commands directly on the database. |
| ExecuteQuery(Type, String, Object[1]) | Executes SQL queries directly on the database. |
| ExecuteQuery<TResult>(String, Object[1]) | Determines whether the associated database can be opened. |
| SubmitChanges() | Computes the set of modified objects to be inserted, updated, or deleted, and executes the appropriate command to implement the changes to the database. |
| ToString() | Returns a string that represents the current object (Inherited from Object). |

FIGURE 8.64 Most popular methods in the DataContext class.