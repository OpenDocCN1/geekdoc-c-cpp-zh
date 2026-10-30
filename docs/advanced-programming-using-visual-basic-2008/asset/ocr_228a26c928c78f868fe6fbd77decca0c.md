```
Me.Validate() ' Causes validation of the control losing focus.
Me.StoresBindingSource.EndEdit()
Me.SalesBindingSource.EndEdit()
Me.TableAdapterManager.UpdateAll(Me.PubsDataSet)
```

STEP 5: Run the project just to make sure that the form's controls all fill correctly. You can step through the store records, but don't make any changes yet. You have some work to do first.

# Commit Added Parent Records before Adding Child Records

If a user adds a new parent record (a new store) and then wants to add a sale for the new store, a constraint violation could occur since the dataset would not yet hold the store record. You can commit the store record when the user switches to the sales grid.

STEP 1: In the Code Editor, drop down the Class Name list and select SalesDataGridView. Drop down the Method Name list and select GotFocus.

STEP 2: In the SalesDataGridView_GotFocus event procedure, add this code, which will commit any unfinished edit in the store record and reset the Stor_id text box to be ReadOnly:

```
Private Sub SalesDataGridView_GotFocus(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles SalesDataGridView.GotFocus
' Make sure that a new store is committed to the dataset before
' allowing a new sale to be added.

Try
    StoresBindingSource.EndEdit()
    Stor_idTextBox.ReadOnly = True
Catch Ex As Exception
    MessageBox.Show("Unable to save the changes. " & _
    & Ex.Message, "Data Error")
End Try
End Sub
```

# Add the Save Query for Exit

The user can click the Save button to save the in-memory copy of the dataset to the original data source. We also want to check for unsaved changes when the user closes the application.

STEP 1: Create a new event handler for the form's FormClosing event and add the following code. If the user chooses to save the changes, we will call the Save button's event handler.

```
' Check for unsaved changes.
If PubsDataSet.HasChanges Then
    Dim ResponseDialogResult As DialogResult
    ResponseDialogResult = MessageBox.Show("Save the database changes?", _
    "Unsaved Changes", MessageBoxButtons.YesNoCancel, _
    MessageBoxIcon.Question)
    Select Case ResponseDialogResult
    Case Windows.Forms.DialogResult.Yes
        StoresBindingNavigatorSaveItem_Click(sender, e)
```