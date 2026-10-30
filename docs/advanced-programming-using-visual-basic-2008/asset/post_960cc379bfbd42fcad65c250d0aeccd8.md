
ToolStripStatusLabel2.Text = "Record Saved"
AddingBoolean = False
EditingBoolean = False
SetNavigation(True)
SetControlsReadOnly(True)
ResetButtonsAfterEdit()
Catch ex As Exception
    ' Catch duplicate records and constraint violations.
    MessageBox.Show(ex.Message)
End Try
End If
End Sub

Private Sub DeleteCancelButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles DeleteCancelButton.Click
' Delete the current record after confirming or cancel an Add or Edit.
Dim DeleteDialogResult As DialogResult

Try
    If DeleteCancelButton.Text = "&Delete" Then
        DeleteDialogResult = MessageBox.Show("Delete this record?", _
            "Confirm Delete", MessageBoxButtons.YesNo, _
            MessageBoxIcon.Question)
        If DeleteDialogResult = Windows.Forms.DialogResult.Yes Then
            APublishersBindingSource.RemoveCurrent()
            APublishersTableAdapter.Update(_
                AContactsDataSet.Publishers)
            ToolStripStatusLabel2.Text = "Record deleted"
        End If
    Else
        ' Cancel button clicked.
        APublishersBindingSource.CancelEdit()
        AddingBoolean = False
        EditingBoolean = False
        SetNavigation(True)
        SetControlsReadOnly(True)
        ResetButtonsAfterEdit()
    End If
Catch ex As Exception
    Dim MessageString As String
    MessageString = "Unable to complete the delete/cancel operation: " _
        & ex.Message
    MessageBox.Show(MessageString, "Delete/Cancel", _
        MessageBoxButtons.OK, MessageBoxIcon.Exclamation)
End Try
End Sub

Private Sub EditButton_Click(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles EditButton.Click
' Allow editing to the current record.

EditingBoolean = True
SetNavigation(False)
SetControlsReadOnly(False)
SetButtonsForEdit()
End Sub

Private Sub SetControlsReadOnly(ByVal ValueBoolean As Boolean)
' Lock or unlock the controls.
NameTextBox.ReadOnly = ValueBoolean
CompanyNameTextBox.ReadOnly = ValueBoolean
AddressTextBox.ReadOnly = ValueBoolean
CityTextBox.ReadOnly = ValueBoolean
StateTextBox.ReadOnly = ValueBoolean
ZipTextBox.ReadOnly = ValueBoolean
TelephoneTextBox.ReadOnly = ValueBoolean
FaxTextBox.ReadOnly = ValueBoolean
End Sub

Private Sub SetButtonsForEdit()
' Set up the buttons for an Add or Edit operation.

AddSaveButton.Text = "&Save"
DeleteCancelButton.Text = "&Cancel"
EditButton.Enabled = False
If AddingBoolean Then
    ToolStripStatusLabel2.Text = "Adding"
Else
    ToolStripStatusLabel2.Text = "Editing"
End If
End Sub

Private Sub ResetButtonsAfterEdit()
' Reset the buttons after an Add or Edit operation.

AddSaveButton.Text = "&Add"
DeleteCancelButton.Text = "&Delete"
EditButton.Enabled = True
ToolStripStatusLabel2.Text = String.Empty
End Sub

Private Sub SetNavigation(ByVal ValueBoolean As Boolean)
' Set the Enabled property of the navigation buttons.

FirstRecordButton.Enabled = ValueBoolean
LastRecordButton.Enabled = ValueBoolean
NextRecordButton.Enabled = ValueBoolean
PreviousRecordButton.Enabled = ValueBoolean
End Sub

Private Sub FirstRecordButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles FirstRecordButton.Click
' Move to the first record.

APublishersBindingSource.MoveFirst()
End Sub

Private Sub PreviousRecordButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles PreviousRecordButton.Click
' Move to the previous record.

With APublishersBindingSource
    If .Position = 0 Then
        .MoveLast()
    Else
        .MovePrevious()
    End If
End With
End Sub

Private Sub NextRecordButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles NextRecordButton.Click
' Move to the next record.

With APublishersBindingSource
    If .Position = .Count - 1 Then
        .MoveFirst()
    Else
        .MoveNext()
    End If
End With
End Sub

Private Sub LastRecordButton_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles LastRecordButton.Click
' Move to the last record.

APublishersBindingSource.MoveLast()
End Sub
End Class

## Navigating from a Combo Box Selection

The update program must change somewhat for a program that allows the user to select a record from a combo box, rather than navigate using buttons. The logic of an add, delete, or update is essentially the same, but the combo box introduces additional complications. Refer to Figures 5.7 and 5.8 for the form. You can see the complete program in Ch05DetailsViewUpdate.

### During Navigation

When the user is navigating using the combo box, the text box portion of the combo box must not allow the user to enter any keystrokes that would change the displayed value. Also, the combo box text binding should be set to DataSourceUpdateMode.Never.

You can change the DataSourceUpdateMode for the combo box using the DataBindings collection. Recall that you set the initial mode in the DataBindings.Add method:

```
NameComboBox.DataBindings.Add("text", ABindingSource, "Name", _
False, DataSourceUpdateMode.Never)
```

The DataBindings.Add statement adds the text binding to the DataBindings collection. You can change the binding at run time using the bang (!) notation to refer to the text element in the DataBindings collection:

```
NameComboBox.DataBindings!text.DataSourceUpdateMode = _
DataSourceUpdateMode.OnValidation
```

### During an Add or Edit

The state of the combo box must change during an Add or Edit in regards to navigation. The user must not be allowed to make a new selection from the combo box, but instead be able to type text into the text portion of the box. You can prevent the user from dropping down the combo box by setting its DropDownStyle to Simple during an Add or Edit. After the user has completed the Add or Edit by selecting Save or Cancel, you must change the combo box's DropDownStyle back to DropDownList.

```
NameComboBox.DropDownStyle = ComboBoxStyle.Simple
```

or

```
NameComboBox.DropDownStyle = ComboBoxStyle.DropDownList
```

### The Combo Box Code

Write the code to handle the combo box binding and drop-down behavior in a general procedure and call it from the Add, Edit, Save, and Cancel routines.

```
Private Sub SetComboBoxBinding()
    ' Set the combo box to save changes.
    ' Saves for Add or Edit; does not save during navigation.
    ' Sets the combo box to not allow drop-down during an Add or an Edit.
    With NameComboBox
        If (AddingBoolean Or EditingBoolean) Then
            .DataBindings!Text.DataSourceUpdateMode = _
            DataSourceUpdateMode.OnValidation
            .DropDownStyle = ComboBoxStyle.Simple
        Else
            .DataBindings!Text.DataSourceUpdateMode = _
            DataSourceUpdateMode.Never
            .DropDownStyle = ComboBoxStyle.DropDownList
        End If
    End With
End Sub
```

### Additional Requirements for Combo Box Navigation

You must guard against another potential problem. During an Add or Edit, if the focus is on the combo box and the user presses the Escape key, the keystroke is lost. So you must handle the Escape key yourself.

```
Private Sub NameComboBox_KeyDown(ByVal sender As Object, _
ByVal e As System.Windows.Forms.KeyEventArgs) _
Handles NameComboBox.KeyDown
    ' Cancel the Add or Edit if the Escape key is pressed.
    If (AddingBoolean Or EditingBoolean) And _
    e.KeyData = Keys.Escape Then
        DeleteCancelButton_Click(sender, e)
    End If
End Sub
```

## Feedback 5.3

- 1. You want to delete a record from a dataset and the original data source. Are these statements in the correct order?
  - AuthorsBindingSource.RemoveCurrent()
  - AuthorsTableAdapter.Update(NorthwindDataSet)
- 2. What steps are required to set up the form to allow a record to be added?

## Validating User Input Data

As your user enters data, some fields need to be validated. You may need to check constraints, such as required fields or the data type. Your application also may contain business rules for validating the data. Validating the data before sending it back to the database can reduce the number of round trips between your application and the database. You can perform field-level or record-level validation in the code for the form or for the dataset. The recommended practice is to place validation code in the dataset.

### Checking for Nulls

A common problem for programming database updates relates to null fields. What should happen if the user does not enter data in a required field? When and how should the validation occur? If the user does not enter data in a field that does not permit nulls and you send the record to the database, an exception occurs, which probably is not the desired behavior.

You can check to see which fields allow nulls in two ways in the VS IDE. If you display the DataSet Designer, you can click on each individual field and view its AllowDBNull property, which is a Boolean value. Or you can view the settings for an entire table by using the Server Explorer (or the Database Explorer in the VB Express Edition). Select View / Server Explorer (or Database Explorer) to see the window, which generally docks with the Toolbox window. Expand the node for your connection and its Tables collection to find the name of the table. Right-click on the table name and select Open Table Definition, which displays the column names, data types, and whether nulls are allowed for each field. In Figure 5.9, you can see that for the Publishers table, nulls are

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_235_0.png)

### Figure 5.9

View and modify the table definition by selecting Open Table Definition from the table's context menu in the Server Explorer or Database Explorer.
