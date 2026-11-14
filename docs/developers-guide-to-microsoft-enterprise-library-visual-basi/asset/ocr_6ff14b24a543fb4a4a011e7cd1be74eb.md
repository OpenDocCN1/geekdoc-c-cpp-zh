In addition, the final example for this block uses the Distributed Transaction Coordinator (DTC) service. This service may not be set to auto-start on your machine. If you receive an error that the DTC service is not available, open the Services MMC snap-in from your Administrative Tools menu and start the service manually; then run the example again.

# READING MULTIPLE DATA ROWS

One of the most common operations when working with a database is reading multiple rows of data. In a .NET application, you usually access these rows as a DataReader instance, or store them in a DataTable (usually within a DataSet you create). In this section we'll look at the use of the ExecuteReader method that returns a DataReader. You will see how to use a DataSet with the Data Access block methods later in this chapter.

# Reading Rows Using a Query with No Parameters

Simple queries consisting of an inline SQL statement or a stored procedure, which take no parameters, can be executed using the ExecuteReader method overload that accepts a CommandType value and a SQL statement or stored procedure name as a string.

The following code shows the simplest approach for a stored procedure, where you can also omit the CommandType parameter. The default is CommandType.StoredProcedure (unlike ADO.NET, where the default is CommandType.Text).

```
' Call the ExecuteReader method by specifying just the stored procedure name.
Using reader As IDataReader = namedDB.ExecuteReader("MyStoredProcName")
    ' Use the values in the rows as required.
End Using
```

To use an inline SQL statement, you must specify the appropriate CommandType value, as shown here.

```
' Call the ExecuteReader method by specifying the command type
' as a SQL statement, and passing in the SQL statement
Using reader As IDataReader = namedDB.ExecuteReader(CommandType.Text, _
    "SELECT TOP 1 * FROM OrderList")
    ' Use the values in the rows as required - here we are just displaying them.
    DisplayRowValues(reader)
End Using
```

The example named Return rows using a SQL statement with no parameters uses this code to retrieve a DataReader containing the first order in the sample database, and then displays the values in this single row. It uses a simple auxiliary routine that iterates through all the rows and columns, writing the values to the console screen.