```
    string sql = "SELECT * FROM Employees;";
    OleDbCommand command = new OleDbCommand(sql, connection);
    OleDbDataReader reader = command.ExecuteReader();
    while (reader.Read())
    {
        Console.WriteLine($"Name: {reader["Name"]}, Age: {reader["Age"]}, Department: {reader["Department"]}");
    }

    connection.Close();
```

# ## Odbc Data Provider

The Odbc data provider is used to connect to ODBC data sources, such as MySQL or Oracle databases. It is included in the System.Data.Odbc namespace. This data provider provides a generic way to connect to a wide range of data sources using the Open Database Connectivity (ODBC) standard.

To use the Odbc data provider, you need to create an instance of the OdbcConnection class and pass in a connection string that specifies the data source, driver, and authentication credentials. You can then use the OdbcCommand class to execute SQL commands against the data source.

Here's an example of using the Odbc data provider to connect to a MySQL database and execute a SQL command:

```
    string connectionString = "Driver={MySQL ODBC 8.0 Unicode Driver};Server=MyServer;Database=MyDatabase;Uid=myUsername;Pwd=myPassword;";
    OdbcConnection connection = new OdbcConnection(connectionString);
    connection.Open();

    string sql = "SELECT * FROM Employees;";
    OdbcCommand command = new OdbcCommand(sql, connection);
    OdbcDataReader reader = command.ExecuteReader();
```