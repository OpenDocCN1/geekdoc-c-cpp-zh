# Two constructors for the SqlConnection class

new SqlConnection()
SqlConnection(connectionString)

# Common properties and methods of the SqlConnection class

| Property | Description |
| --- | --- |
| ConnectionString | Provides information for accessing a SQL Server database |
| Method | Description |
| Open () | Opens the connection using the specified connection string |
| Close () | Closes the connection |

# Common values used in the ConnectionString property for SQL Server

| Name | Description |
| --- | --- |
| Data source/Server | The name of the instance of SQL Server you want to connect to |
| Initial catalog/Database | The name of the database you want to access |
| Integrated security | Determines whether the connection is secure. Valid values are True, False, and SSPI. SSPI uses Windows integrated security and is equivalent to True |
| User ID | The user ID's used to log in to SQL Server |
| Password/Pwd | The password that's used to log in to SQL Server |
| Persist security info | Determines whether sensitive information, such as the password, is returned as part of the connection. The default is False |
| Workstation ID | The name of the workstation that's connecting to SQL Server |

# A connection string for the SQL Server provider

```
Data Source=localhost\SqlConnection;Initial Catalog=MMBooks;Integrated
Security=True
```

# A connection string for the JET OLE DB provider

```
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Databases\MMBooks.mdb
```

# Code that creates, opens and closes a connection

```
string connectionString = =
"Data Source=localhost\SqlConnection;Initial Catalog=MMBooks;" + 
"Integrated Security=True";
SqlConnection connection = new SqlConnection(connectionString)
connection.Open();
...
connection.Close();
```

# Description

+   - You can set the ConnectionString property after you create a connection or as you create
it by passing the string to the constructor of the connection class.
- The values you specify for the ConnectionString property depend on the type of data-base you're connecting to.

Figure 20-1  How to create and work with connections