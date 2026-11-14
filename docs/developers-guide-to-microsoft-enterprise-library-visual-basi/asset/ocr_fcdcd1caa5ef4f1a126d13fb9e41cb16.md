object by using two methods of the **Database** class: **GetSqlStringCommand** and **GetStoredProcCommand**. These methods return an instance of the appropriate command class for the configured database as a provider-independent **DbCommand** type reference.

After you create the appropriate type of command, you can use the many variations of the **Database** methods to manipulate the collection of parameters. You can add parameters with a specific direction using the **AddInParameter** or **AddOutParameter** method, or by using the **AddParameter** method and providing a value for the **Parameter Direction** property. You can change the value of existing parameters already added to the command using the **GetParameterValue** and **SetParameterValue** methods.

The following code shows how easy it is to create a command, add an input parameter, and execute both a SQL statement and a stored procedure. Notice how the code specifies the command to which the **Database** class should add the parameter (there could be more than one connection defined for the database), the name, the data type, and the value of the new parameter.

```
' Read data with a SQL statement that accepts one parameter.
Dim sqlStatement As String
 _
 = "SELECT TOP 1 * FROM OrderList WHERE STATE LIKE @state"
' Create a suitable command type and add the required parameter.
Using sqlCmd As DbCommand = defaultDB.GetSqlStringCommand(sqlStatement)
    defaultDB.AddInParameter(sqlCmd, "state", DbType.String, "New York")

    ' Call the ExecuteReader method with the command.
    Using sqlReader As IDataReader = namedDB.ExecuteReader(sqlCmd)
        DisplayRowValues(sqlReader)
    End Using
End Using

' Now read the same data with a stored procedure that accepts one parameter.
Dim storedProcName As String = "ListOrdersByState"

' Create a suitable command type and add the required parameter.
Using sprocCmd As DbCommand = defaultDB.GetStoredProcCommand(storedProcName)
    defaultDB.AddInParameter(sprocCmd, "state", DbType.String, "New York")

    ' Call the ExecuteReader method with the command.
    Using sprocReader As IDataReader = namedDB.ExecuteReader(sprocCmd)
        DisplayRowValues(sprocReader)
    End Using
End Using
```