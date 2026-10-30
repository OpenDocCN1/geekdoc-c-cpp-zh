```
' Move to the next record.
With PublishersBindingSource
    If .Position = .Count - 1 Then
        .MoveFirst()
    Else
        .MoveNext()
    End If
End With

' Move to the previous record.
With PublishersBindingSource
    If .Position = 0 Then
        .MoveLast()
    Else
        .MovePrevious()
    End If
End With

' Move to the first record.
PublishersBindingSource.MoveFirst()

' Move to the last record.
PublishersBindingSource.MoveLast()
```

# Binding Source Update Methods

You can use the methods of the binding source to maintain table data (Table 5.5). Use the AddNew method to begin the operation to add a new record to the dataset. When you execute the AddNew method for data displayed in a grid, the last line in the grid (the one with the asterisk) is activated so the user can enter a new row. If you execute AddNew for individually bound fields, the field contents are cleared so that the user can enter the new record. When the user moves off of the new record, the EndEdit method is executed automatically; or you can explicitly execute the method, perhaps in response to a button click. If the user wishes to cancel the add or edit, you can call the CancelEdit method. You also can use CancelNew for an add in progress, which has the same effect as CancelEdit. But always remember that the dataset is disconnected, so any new records are added to the dataset in memory and not saved to the original data source until you execute the Update or UpdateAll method.

# Editing Methods of the BindingSource Object

# Table 5.5

| Method | Purpose |
|---|---|
| AddNew | Clears bound fields to allow new data to be entered. Adds a new row to the table. |
| Insert | Adds a record at the specified index. |
| CancelNew | Cancels the record being added. |
| CancelEdit | Cancels the edit currently being processed. |
| EndEdit | Completes the current edit and saves the changes in the dataset. |
| RemoveAt | Deletes the row at the specified index from the table. |
| RemoveCurrent | Deletes the current record. |