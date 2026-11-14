the database type at some later stage. However, it means that you can only use the features available across all of the possible database types (the methods and properties defined in the **Database** class).

Some features are only available in the concrete types for a specific database. For example, the **ExecuteXmlReader** method is only available in the **SqlDatabase** class. If you want to use such features, you must cast the database type you instantiate to the appropriate concrete type. The following code creates an instance of the **SqlDatabase** class.

```
' Resolve a SqlDatabase object from the container using the default database.
Dim SqlServerDB As Database _
    = TryCast(EnterpriseLibraryContainer.Current.GetInstance(Of Database)()), _
    SqlDatabase)
```

In addition to using configuration to define the databases you will use, the Data Access block allows you to create instances of concrete types that inherit from the **Database** class directly in your code, as shown here. All you need to do is provide a connection string that specifies the appropriate ADO.NET data provider type (such as **SqlClient**).

```
' Assume the method GetConnectionString exists in your application and
' returns a valid connection string.
Dim myConnectionString As String = GetConnectionString()
Dim db As SqlDatabase = New SqlDatabase(myConnectionString)
```

# THE EXAMPLE APPLICATION

Now that you have your new **Database** object ready to go, we'll show you how you can use it to perform a variety of tasks. You can download an example application (a simple console-based application) that demonstrates all of the scenarios you will see in the remainder of this chapter. You can run this directly from the bin\debug folder, or open the solution named **DataAccess** in Microsoft Visual Studio® to see all of the code as you run the examples.

The two connection strings for the database we provide with this example are:

```
Data Source=.\SQLEXPRESS;
AttachDbFilename=|DataDirectory|\DataAccessExamples.mdf;
Integrated Security=True;User Instance=True
Data Source=.\SQLEXPRESS;Asynchronous Processing=true;AttachDbFilename=
|DataDirectory|\DataAccessExamples.mdf;
Integrated Security=True;User Instance=True
```

If you have configured a different database using the scripts provided with the example, you may find that you get a different error when you run this example. It is likely that you have an invalid connection string in your App.config file for your database. In addition, use the Services MMC snap-in in your Administrative Tools folder to check that the SQL Server (SQLEXPRESS) database service (the service is named **MSSQL$SQLEXPRESS**) is running.