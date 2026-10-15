that while this stored procedure is executing, you can perform other tasks in your Windows Forms application. Here is the SQL code for the usp_Long_Running_Procedure stored procedure:

```
CREATE PROCEDURE usp_Long_Running_Procedure
AS
SET NOCOUNT ON
WAITFOR DELAY '00:00:20'
EXEC usp_authors_Get_All
```

Code snippet from Examples.sql

The last line of code in the Button's Click event handler is the call to BeginExecuteReader. In this call, the first thing you are passing in is a delegate method (Me.AsyncCallback) for the System.AsyncCallback delegate type. This is how the .NET Framework calls you back once the method is finished running asynchronously. You then pass in your initialized SqlCommand object so that it can be executed, as well as the CommandBehavior value for the DataReader. In this case, you pass in the CommandBehavior.CloseConnection value so that the connection to the database will be closed once the DataReader has been closed. You will look at the DataReader in more detail in the next section.

Now that you have initiated the asynchronous call, and have defined a callback for your asynchronous call, let's look at the actual method that is being called back, the AsyncCallback method:

```
Private Sub AsyncCallback(ByVal ar As IAsyncResult)
    ' Get the command that was passed from the AsyncState of the IAsyncResult.
    Dim command As SqlCommand = CType(ar.AsyncState, SqlCommand)
    ' Get the reader from the IAsyncResult.
    Dim reader As SqlDataReader = command.EndExecuteReader(ar)
    ' Get a table from the reader.
    Dim table As DataTable = Me.GetTableFromReader(reader, "Authors")
    ' Call the BindGrid method on the Windows main thread,
    ' passing in the table.
    Me.Invoke(New BindGridDelegate(AddressOf Me.BindGrid),
        New Object() {table})
End Sub
```

Code snippet from AdoNetFeaturesTest project

The first line of the code is simply retrieving the SqlCommand object from the AsyncState property of the IAsyncResult that was passed in. Remember that when you called BeginExecuteReader earlier, you passed in your SqlCommand object. You need it so that you can call the EndExecuteReader method on the next line. This method gives you your SqlDataReader. On the next line, you then transform the SqlDataReader into a DataTable (covered later when the DataSet is discussed).

The last line of this method is probably the most important. If you tried to just take your DataTable and bind it to the grid, it would not work, because right now you are executing on a thread other than the main Windows thread. The helper method named BindGrid can do the data binding, but it must be called only in the context of the Windows main thread. To bring the data back to the main Windows thread, it must be marshaled via the Invoke method of the Form object. Invoke takes two arguments: the delegate of the method you want to call and (optionally) any parameters for that method. In this case, you define a delegate for the BindGrid method, called BindGridDelegate. Here is the delegate declaration:

```
Private Delegate Sub BindGridDelegate(ByVal table As DataTable)
```

Notice how the signature is exactly the same as the BindGrid method shown here:

```
Private Sub BindGrid(ByVal table As DataTable)
    ' Clear the grid.
    Me._authorsGridView.DataSource = Nothing
    ' Bind the grid to the DataTable.
    Me._authorsGridView.DataSource = table
End Sub
```