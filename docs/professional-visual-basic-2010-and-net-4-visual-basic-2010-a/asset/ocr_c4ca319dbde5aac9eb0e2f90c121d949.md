```
```vb
Dim cmd As SqlCommand
Dim result As Integer
Dim cmdString As String = _
    String.Format("UPDATE roysched SET royalty={0} where royalty={1}", _
                  newPercent, _
                  currentPercent)
'update to match the location of pubs on your computer
Using conn As New SqlConnection("Server=(local)\\sqlexpress; " & _
                               "database=pubs;Integrated Security=true;")
    conn.Open()
    'display the record before updating
    DisplayData(conn, "before")
    cmd = New SqlCommand(cmdString, conn)
    result = cmd.ExecuteNonQuery()
    'display the record after updating
    DisplayData(conn, "after")
End Using

Return result
End Function
Private Sub DisplayData(ByVal conn As SqlConnection, _
                        ByVal direction As String)
    Dim cmdString As String = "SELECT * FROM roysched ORDER BY title_id"
    Dim cmd As New SqlCommand(cmdString, conn)

    Console.WriteLine("Displaying data ({0})", direction)
    Using reader As SqlDataReader = cmd.ExecuteReader
        While reader.Read
            Console.WriteLine("Title: {0} {1}-{2} Royalty: {3}%", _
                              reader.GetString(0), _
                              reader.GetInt32(1), _
                              reader.GetInt32(2), _
                              reader.GetInt32(3))
        End While
    End Using
End Sub
End Module
```
```

This update function changes the royalty percentage for authors from 10% to 8%. This is done with the SQL command string. The great thing about these update capabilities is that you can capture the number of records that were updated by assigning the result of the ExecuteNonQuery command to the records variable. The total number of affected records is then returned by the function.

Notice that in this case the connection was wrapped in a Using statement. The Using statement creates a scope for an object, and the object is properly disposed of at the close of the statement. This guarantees that the connection will be closed when the Using clause completes.

# Deleting Data

Along with reading, inserting, and updating data, you sometimes need to delete data from the data source. Deleting data is a simple process of using the SQL command string and then the ExecuteNonQuery command as you did in the update example. The following bit of code illustrates this:

```
```vb
Imports System.Data.SqlClient

Module Main

    Sub Main()
        Dim deletes As Integer
```
```