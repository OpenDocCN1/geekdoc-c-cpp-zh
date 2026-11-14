Command instance from the current Database instance using the GetSqlStringCommand and GetStoredProcCommand methods. You can add parameters to the command before calling the ExecuteScalar method if required. However, to demonstrate the way the method works, the code here simply extracts the complete row set. The result is a single Object that you must cast to the appropriate type before displaying or consuming it in your code.

```
' Create a suitable command type for a SQL statement.
Using sqlCmd As DbCommand _
    = defaultDB.GetSqlStringCommand("SELECT [Name] FROM States")
' Call the ExecuteScalar method of the command.
Console.WriteLine("Result using a SQL statement: {0}", _
    defaultDB.ExecuteScalar(sqlCmd).ToString())
End Using
```

```
' Create a suitable command type for a stored procedure.
' NB: For efficiency, aim to return only a single value or a single row.
Using sprocCmd As DbCommand = defaultDB.GetStoredProcCommand("GetStatesList")
' Call the ExecuteScalar method of the command.
Console.WriteLine("Result using a stored procedure: {0}", _
    defaultDB.ExecuteScalar(sprocCmd).ToString())
End Using
```

You can see the code listed above running in the example Return a single scalar value from a SQL statement or stored procedure. The somewhat unexciting result it produces is shown here.

```
Result using a SQL statement: Alabama
Result using a stored procedure: Alabama
```

# RETRIEVING DATA ASYNCHRONOUSLY

Having looked at all of the main ways you can extract data using the Data Access block, we’ll move on to look at some more exciting scenarios (although many would perhaps fail to consider anything connected with data access exciting...). Databases are generally not renowned for being the fastest of components in an application—in fact many people will tell you that they are major bottleneck in any enterprise application. It’s not that they are inefficient, it’s usually just that they contain many millions of rows, and the queries you need to execute are relatively complex. Of course, it may just be that the query is badly written and causes poor performance, but that’s a different story.

One way that applications can minimize the performance hit from data access is to perform it asynchronously. This means that the application code can continue to execute, and the user interface can remain interactive during the process. Asynchronous data access may not suit every situation, but it can be extremely useful.