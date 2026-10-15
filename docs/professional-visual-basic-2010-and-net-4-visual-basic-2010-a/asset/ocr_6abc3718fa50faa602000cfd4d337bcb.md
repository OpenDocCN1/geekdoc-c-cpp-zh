```
Using conn As New SqlCeConnection(My.Settings.productsConnectionString)
    conn.Open()
    Using cmd As _
        New SqlCeCommand("SELECT ProductName, UnitPrice FROM Products", conn)
        Using reader As SqlCeDataReader = cmd.ExecuteReader
            While reader.Read
                Console.WriteLine("{0}: {1:c}",
                    reader.GetString(0),
                    reader.GetDecimal(1))
            End While
        End Using
    End Using
End Using
```

If you use the provider-agnostic classes, then the code becomes even more like the SQL Server equivalent:

```
Dim fact As DbProviderFactory
Dim prov As String = My.Settings.productsProvider
fact = DbProviderFactories.GetFactory(prov)
Using conn As DbConnection = fact.CreateConnection()
    conn.ConnectionString = My.Settings.productsConnectionString
    conn.Open()
    Using cmd As DbCommand = fact.CreateCommand
        With cmd
            .CommandText = "SELECT ProductName, UnitPrice FROM Products"
            .CommandType = CommandType.Text
            .Connection = conn
            Using reader As DbDataReader = cmd.ExecuteReader
                While reader.Read
                    Console.WriteLine("{0}: {1:c}", _
                        reader.GetString(0), _
                        reader.GetDecimal(1))
                End While
            End Using
        End With
    End Using
End Using
```

The simplest possible way to use a SQL Server Compact database in your application is to use it as a standalone database. While you get none of the benefits of synchronization, you do get the benefit of the simpler (and smaller) deployment for SQL Server Compact. However, the true power of SQL Server Compact comes into play when you use it along with synchronization with a full SQL Server database. This enables you to more easily create applications that work both offline and online.

# Connecting to a SQL Server Compact Database

As with other editions of SQL Server, the key to connecting to a SQL Server Compact database is in the connection string. However, because SQL Server Compact does not have the same features in terms of server and integrated security, different options are used to connect to the database, the most important of which are described in Table 12-1. Only the data source and password values can be set within the IDE.

TABLE 12-1: SQL Server Compact Connection Options

| OPTION | DESCRIPTION |
|---|---|
| Provider name | System.Data.SqlServerCe |
| Data source | Points to the SDF file. As this file is normally included in the project, the value can be written using the DataDirectory shortcut: DataSource=|DataDirectory|\DatabaseName.sdf; |