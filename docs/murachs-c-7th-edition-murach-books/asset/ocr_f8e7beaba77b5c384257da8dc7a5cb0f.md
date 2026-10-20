# .NET data provider core objects

| Object | Description |
|---|---|
| Connection | Establishes a connection to a database. |
| Command | Represents an individual SQL statement that can be executed against the database. |
| Data reader | Provides read-only, forward-only access to the data in a database. |

# Three data providers for .NET

| Provider | Namespace | Description |
|---|---|---|
| SQL Server | Microsoft.Data.SqlClient | Lets you access SQL Server databases. |
| OLE DB | System.Data.OleDb | Lets you access any database that supports OLE DB. |
| ODBC | System.Data.Odbc | Lets you access any database that supports ODBC. |

# Class names for the data providers

| Object | SQL Server | OLE DB | ODBC |
|---|---|---|---|
| Connection | SqlConnection | OleDbConnection | OdbcConnection |
| Command | SqlCommand | OleDbCommand | OdbcCommand |
| Data reader | SqlDataReader | OleDbDataReader | OdbcDataReader |

# A using directive for the SQL Server data provider namespace

```
using Microsoft.Data.SqlClient;
```

# Description

+   - The .NET data providers provide the ADO.NET classes that are responsible for working directly with a database. In addition to the core classes shown above, classes are provided for other functions such as passing parameters to commands or working with transactions.
+   - To use the Microsoft.Data.SqlClient namespace, you must install its NuGet package. To do that, you can use the instructions presented in figure 20-2 to search for and install the Microsoft.Data.SqlClient NuGet package.
+   - To make it easy to use a .NET data provider in a program, you can add a using directive for the appropriate namespace. Otherwise, you’ll have to qualify each class you refer to with the namespace.
+   - The SQL Server data provider is optimized for working with a SQL Server database. As a result, you should use that data provider if you’re using a SQL Server database.
+   - Many database vendors have developed .NET data providers that are optimized for use with their databases. For example, MySQL and Oracle have developed optimized .NET data providers.