```
id = .Cells(1).Text
task = CType(.Cells(2).Controls(0), TextBox)
complete = CType(.Cells(3).Controls(0), CheckBox)
End With

ctx.UpdateTask(id, task.Text, complete.Checked)
' turn off edit
TaskGrid.EditIndex = -1
BindGrid()

Catch ex As DataServiceRequestException
    statusMessage = "Unable to connect to the table storage server." &
    ex.Message
End Try
Me.Message.Text = statusMessage
End Sub
```

Code snippet from CloudToDoWithQueue

The RowCancelingEdit and RowEditing methods are relatively simple methods used to switch the desired row of the GridView into or out of edit mode. The bulk of the update is in the RowUpdating method. This is called when the user clicks the Update link on the row while editing. In this method, the code reads the new values from the edit controls on the GridView and submits them to a new UpdateTask method that will be created in a moment. It then sets the GridView not to display the edit functionality and redisplays the current data.

The next step is to add the method to update the data in the table storage:

```
Public Sub UpdateTask(ByVal id As String,
                    ByVal name As String,
                    ByVal isComplete As Boolean)

    Try
        ' get existing task by name
        Dim t As Task = (From f In Me.Tasks
                         Where f.TaskID = id
                         Select f).FirstOrDefault
        ' update properties
        With t
            .Name = name
            .IsComplete = isComplete
        End With
        If isComplete Then
            ' send to the Worker role
            ProcessTask(t)
        End If
        ' save
        MyBase.UpdateObject(t)
        MyBase.SaveChanges()
    Catch ex As Exception
        Trace.WriteLine(ex.Message, "Error")
    End Try
End Sub
```

Code snippet from CloudToDoWithQueue

As this code will update an existing task, the first step is to retrieve the current values. This uses LINQ to query the underlying data service to retrieve the item by ID. You then set the new values and call UpdateObject to mark it for submission when SaveChanges is called.

The ProcessTask method will add the task to the queue if the task is being marked complete: