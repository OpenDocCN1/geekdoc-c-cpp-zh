# Creating the Data Table(s)

A data table object is created from the DataTable class using the standard syntax for creating objects:

```
DataTable variableName = new DataTable()
```

where variableName is any valid variable name.

For example, the following statement creates a data table object for the Employee table, and references it using the variable, dtEmployee.

```
DataTable dtEmployee = new DataTable();
```

# Creating the Data Adapter

A data adapter is created from the DataAdapter class:

```
DataAdapter variableName = new DataAdapter(connectionString, Sql)
```

The first parameter, connectionString, provides the necessary information to connect to the database. To connect to a local database, the syntax of the connection string is

```
@"Data Source = (LocalDB)\MSSQLLocalDB; AttachDbFilename = path\fileName";
```

Here is an example:

```
@"Data Source = (LocalDB)\MSSQLLocalDB; AttachDbFilename = C:\VC\HR2.mdf";
```

If the database is to be accessed from a server, the Data Source would provide the server address. The structure of the connection string may vary with the version of SQL Server you are using. The connection string may include additional information on security, user id and password.

The second parameter, Sql, represents the SQL statement to select data. The syntax to select data from a single table is

```
SELECT fieldNames FROM tableName WHERE criterion
```

In the above statement, fieldNames represents the list of field names separated by commas, tableName represents the table name, and criterion represents the criterion, if any, to select records. If all fields are to be selected, you may replace field names by an asterisk. For example, to select all fields from all records of the Employee table, use the following SQL statement:

```
SELECT * FROM Employee
```

The WHERE clause is discussed briefly later in this section.

Thus, the following code creates a data adapter to access all Employee records, and references it using the variable, daEmployee.

```
string connString = @"Data Source = (LocalDB)\MSSQLLocalDB; AttachDbFilename =
    C\VC\HR2.mdf";
string empSQLStr = "SELECT * FROM Employee";
SqlDataAdapter daEmployee = new SqlDataAdapter(empSQLStr, connString);
```

# Creating the Binding Source

The binding source is created from the BindingSource class:

```
BindingSource variableName = new BindingSource;
```