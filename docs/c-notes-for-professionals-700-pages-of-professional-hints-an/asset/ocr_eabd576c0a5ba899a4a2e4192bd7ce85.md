```
public ExampleContext() : base("ExampleContextEntities")
{
}

public virtual DbSet<Widgets> Widgets { get; set; }
}
```

# Executing Entity Framework Queries

Actually executing an Entity Framework query can be quite easy and simply requires you to create an instance of the context and then use the available properties on it to pull or access your data

```
using(var context = new ExampleContext())
{
    // Retrieve all of the Widgets in your database
    var data = context.Widgets.ToList();
}
```

Entity Framework also provides an extensive change-tracking system that can be used to handle updating entries within your database by simply calling the SaveChanges() method to push changes to the database :

```
using(var context = new ExampleContext())
{
    // Grab the widget you wish to update
    var widget = context.Widgets.Find(w => w.Id == id);
    // If it exists, update it
    if(widget != null)
    {
        // Update your widget and save your changes
        widget.Updated = DateTime.UtcNow;
        context.SaveChanges();
    }
}
```

# Section 128.3: ADO.NET Connections

ADO.NET Connections are one of the simplest ways to connect to a database from a C# application. They rely on the use of a provider and a connection string that points to your database to perform queries against.

# Common Data Provider Classes

Many of the following are classes that are commonly used to query databases and their related namespaces :

+   - SqlConnection,SqlCommand,SqlDataReader from System.Data.SqlClient
+   - OleDbConnection,OleDbCommand,OleDbDataReader from System.Data.OleDb
+   - MySqlConnection, MySqlCommand, MySqlDbDataReader from MySql.Data

All of these are commonly used to access data through C# and will be commonly encountered throughout building data-centric applications. Many other classes that are not mentioned that implement the same FooConnection,FooCommand,FooDataReader classes can be expected to behave the same way.

# Common Access Pattern for ADO.NET Connections

A common pattern that can be used when accessing your data through an ADO.NET connection might look as follows :