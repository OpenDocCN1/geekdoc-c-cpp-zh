
Other points to note about asynchronous data access are the following:

- **Threading** namespace, such as wait handles and manual reset events, to manage asynchronous execution of the Data Access block methods. You can also cancel a pending or executing command by calling the **Cancel** method of the command you used to initiate the operation. For more information, see “Asynchronous Command Execution in ADO.NET 2.0” on MSDN at http://msdn.microsoft.com/en-us/library/ms379553(VS.80).aspx.

- The **BeginExecuteReader** method does not accept a **CommandBehavior** parameter. By default, the method will automatically set the **CommandBehavior** property on the underlying reader to **CloseConnection** unless you specify a transaction when you call the method. If you do specify a transaction, it does not set the **CommandBehavior** property.

- Always ensure you call the appropriate **EndExecute** method when you use asynchronous data access, even if you do not actually require access to the results, or call the **Cancel** method on the connection. Failing to do so can cause memory leaks and consume additional system resources.

- Using asynchronous data access with the Multiple Active Results Set (MARS) feature of ADO.NET may produce unexpected behavior, and should generally be avoided.

- Asynchronous data access is only available if the database is SQL Server 7.0 or later. Also, for SQL Server 7.0 and SQL Server 2000, the database connection must use TCP. It cannot use shared memory. To ensure that TCP is used for SQL Server 7.0 and SQL Server 2000, use **localhost**, **tcp:server_name**, or **tcp:ip_address** for the server name in the connection string.

Asynchronous code is notoriously difficult to write, test, and debug for all edge cases, and you should only consider using it where it really can provide a performance benefit. For guidance on performance testing and setting performance goals see “patterns & practices Performance Testing Guidance for Web Applications” at http://perftesting.codeplex.com/.

## Retrieving Row Set Data Asynchronously

The following code shows how you can perform asynchronous data access to retrieve a row set from a SQL database. The code creates a **Command** instance and adds two parameters, and then calls the **BeginExecuteReader** method of the **Database** class to start the process. Although you can use complex Lambda expressions in Visual Studio 2010 and Visual Basic 10, you cannot do so if you are using Visual Basic version 9 in Visual Studio 2008. Instead, you can create a separate callback function and specify it when you call the **BeginExecuteReader** method, as shown here.

```
Try
    ' Create command to execute stored procedure and add parameters.
    Dim cmd As DbCommand = asyncDB.GetStoredProcCommand("ListOrdersSlowly")
    asyncDB.AddInParameter(cmd, "state", DbType.String, "Colorado")
    asyncDB.AddInParameter(cmd, "status", DbType.String, "DRAFT")

    ' Execute the query asynchronously specifying the command and
    ' the callback to execute when data access completes.
    asyncDB.BeginExecuteReader(cmd, AddressOf ExecuteReadData, asyncDB)

Catch ex As Exception
    Console.WriteLine("Error while starting data access: {0}", ex.Message)
End Try
...

' Callback executed when the data access completes.
Sub ExecuteReadData(ByVal asyncResult As IAsyncResult)
    Try
        ' Extract Database instance from async state passed to callback
        Dim db As Database = CType(asyncResult.AsyncState, Database)
        Using reader As IDataReader = db.EndExecuteReader(asyncResult)
            DisplayRowValues(reader)
        End Using
    Catch ex As Exception
        Console.WriteLine("Error after data access completed: {0}", ex.Message)
    End Try
End Sub
```

The Lambda expression then calls the **EndExecuteReader** method to obtain the results of the query execution.

The **AsyncState** parameter can be used to pass any required state information into the callback routine. For example, when you use a separate callback, you would pass a reference to the current **Database** instance as the **AsyncState** parameter so that the callback code can call the **EndExecuteReader** (or other appropriate **End** method) to obtain the results. If you use a Lambda expression instead, the current **Database** instance is available within the expression and, therefore, you do not need to populate the **AsyncState** parameter.

The callback executes the **EndExecuteReader** method to obtain the results of the query. At this point you can consume the row set in your application or, as the code above does, just display the values. Notice that the callback expression should handle any errors that may occur during the asynchronous operation.

The example **Execute a command that retrieves data asynchronously** uses the code shown above to fetch two rows from the database and display the contents. As well as the code above, it uses a simple routine that displays a “Waiting...” message every second as the code executes. The result is shown here.

```
Database supports asynchronous operations
Waiting... Waiting... Waiting... Waiting... Waiting...

Id = 1
Status = DRAFT
CreatedOn = 01/02/2009 11:12:06
Name = Adjustable Race
LastName = Abbas
FirstName = Syed
ShipStreet = 123 Elm Street
ShipCity = Denver
ShipZipCode = 12345
ShippingOption = Two-day shipping
State = Colorado

Id = 2
Status = DRAFT
CreatedOn = 03/02/2009 01:12:06
Name = All-Purpose Bike Stand
LastName = Abel
FirstName = Catherine
ShipStreet = 321 Cedar Court
ShipCity = Denver
ShipZipCode = 12345
ShippingOption = One-day shipping
State = Colorado
```

Of course, as we don't have a multi-million-row database handy to query, the example uses a stored procedure that contains a WAIT statement to simulate a long-running data access operation. It also uses ManualResetEvent objects to manage the threads so that you can see the results more clearly. Open the sample in Visual Studio, or view the Program.vb file, to see the way this is done.

## Retrieving Data as Objects Asynchronously

You can also execute data accessors asynchronously when you want to return your data as a sequence of objects rather than as rows and columns. The example Execute a command that retrieves data as objects asynchronously demonstrates this technique. You can create your accessor and associated mappers in the same way as shown in the previous section of this chapter, and then call the BeginExecute method of the accessor. This works in much the same way as when using the BeginExecuteReader method described in the previous example.

You pass to the BeginExecute method the lambda expression or callback to execute when the asynchronous data access process completes, along with the AsyncState and an array of Object instances that represent the parameters to apply to the stored procedure or SQL statement you are executing. The lambda expression or callback method can obtain a reference to the accessor that was executed from the AsyncState (casting it to an instance of the DataAccessor base type so that the code will work with any accessor implementation), and then call the EndExecute method of the accessor to obtain a reference to the sequence of objects the accessor retrieved from the database.

## UPDATING DATA

So far, we've looked at retrieving data from a database using the classes and methods of the Data Access block. Of course, while this is typically the major focus of many applications, you will often need to update data in your database. The Data Access block provides features that support data updates. You can execute update queries (such as INSERT, DELETE, and UPDATE statements) directly against a database using the ExecuteNonQuery method. In addition, you can use the ExecuteDataSet, LoadDataSet, and UpdateDataSet methods to populate a DataSet and push changes to the rows back into the database. We'll look at both of these approaches here.

## Executing an Update Query

The Data Access block makes it easy to execute update queries against a database. By update queries, we mean inline SQL statements, or SQL statements within stored procedures, that use the UPDATE, DELETE, or INSERT keywords. You can execute these kinds of queries using the ExecuteNonQuery method of the Database class.

Like the ExecuteReader method we used earlier in this chapter, the ExecuteNonQuery method has a broad set of overloads. You can specify a CommandType (the default is StoredProcedure) and either a SQL statement or a stored procedure name. You can also pass in an array of Object instances that represent the parameters for the query. Alternatively, you can pass to the method a Command object that contains any parameters you require. There are also Begin and End versions that allow you to execute update queries asynchronously.

The following code from the example application for this chapter shows how you can use the ExecuteNonQuery method to update a row in a table in the database. It updates the Description column of a single row in the Products table, checks that the update succeeded, and then updates it again to return it to the original value (so that you can run the example again). The first step is to create the command and add the required parameters, as you've seen in earlier examples, and then call the ExecuteNonQuery method with the command as the single parameter. Next, the code changes the value of the command parameter named description to the original value in the database, and then executes the compensating update.

```
Dim oldDescription As String _
    = "Carries 4 bikes safely; steel construction, fits 2"" receiver hitch."
Dim newDescription As String = "Bikes tend to fall off after a few miles."
' Create command to execute stored procedure and add parameters.
Dim cmd As DbCommand = defaultDb.GetStoredProcCommand("UpdateProductsTable")
defaultDb.AddInParameter(cmd, "productID", DbType.Int32, 84)
defaultDb.AddInParameter(cmd, "description", DbType.String, newDescription)
```
