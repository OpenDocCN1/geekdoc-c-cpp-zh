```
SetButtonsForEdit()
PreviousSelectedIndex = Stor_nameComboBox.SelectedIndex
SetComboBoxBinding()
End Sub

Private Sub SaveDatabaseToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SaveDatabaseToolStripMenuItem.Click
' Save the DataSet.

SaveDataSet()
End Sub

Private Sub ExitToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ExitToolStripMenuItem.Click
' Close the application.

Me.Close()
End Sub

' Button event handlers.
Private Sub CommitEditButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CommitEditButton.Click
' Save Updates and Adds to the DataSet.

Try
    StoresBindingSource.EndEdit()
    ToolStripStatusLabel2.Text = "Record Saved"
    AddingBoolean = False
    EditingBoolean = False
    SetControlsReadOnly(True)
    ResetButtonsAfterEdit()
    SetComboBoxBinding()
    Stor_nameComboBox.SelectedIndex = PreviousSelectedIndex
Catch ex As Exception
    ' Catch duplicate records and constraint violations.
    MessageBox.Show("Database error. Duplicate or missing Store ID: " & ex.Message, "Data Error", MessageBoxButtons.OK, MessageBoxIcon.Exclamation)
End Try
End Sub

Private Sub CancelEditButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CancelEditButton.Click
' Cancel an Add or Edit operation.
' Note that this button is the form's Cancel button, so could
' possibly come here when there isn't an Add or Edit in
' progress.

If AddingBoolean Or EditingBoolean Then
    CancelAddOrEdit()
End If
End Sub

' Control event handlers.
Private Sub SalesDataGridView_RowLeave(ByVal sender As Object, ByVal e As System.Windows.Forms.DataGridViewCellEventArgs) Handles SalesDataGridView.RowLeave
' Reset any error messages for an accepted row.
```