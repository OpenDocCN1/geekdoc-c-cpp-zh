# 216. ADVANCED PROGRAMMING USING VISUAL BASIC 2008

Event handlers/methods

Actions—Pseudocode

| Event handlers/methods | Actions—Pseudocode |
|---|---|
| CommitEditButton Click event | End the current edit.<br>Set the status label to “Record Saved”.<br>Set AddingBoolean and EditingBoolean to False.<br>Set text boxes to ReadOnly.<br>Reset the buttons for normal operation.<br>Set the combo box to no save changes.<br>Reset the combo box index to its previous value. |
| CancelEditButton Click event | If adding or editing CancelAddOrEdit. |
| SalesDataGridView RowLeave event | Reset any grid error messages. |
| StoresBindingSource PositionChanged event | Display the record number in the status bar label. |
| Stor_nameComboBox KeyDown | If adding or editing and Escape key pressed<br>Call CancelAddOrEdit. |
| CancelAddOrEdit | If adding<br>Subtract 1 from previous selected index.<br>Cancel the edit.<br>Set AddingBoolean and EditingBoolean = False<br>Set the text boxes to read only.<br>Reset the buttons for normal operation.<br>Set the combo box to no save changes.<br>Reset the combo box’s selected index to the previous value.<br>Clear the status label. |
| ResetButtonsAfterEdit | Disable the Commit and Cancel buttons.<br>Enable the Add, Edit, and Delete menu items.<br>Enable the sales grid. |
| SaveDataSet | If the dataset has changes<br>End any edits in both tables.<br>Execute the UpdateAll method of the TableAdapterManager. |
| SetButtonsForEdit | Enable the Commit and Cancel buttons.<br>Disable the Add, Edit, and Delete menu items.<br>If adding<br>Set the status label to “Adding”.<br>Else<br>Set the status label to “Editing”. |
| SetComboBoxBinding | If adding or editing<br>Set the data binding to save changes.<br>Set DropDownStyle to Simple.<br>Else<br>Set the data binding to not save changes.<br>Set DropDownStyle to DropDownList. |
| SetControlsReadOnly(Boolean) | Set text boxes’ ReadOnly property to Boolean value. |
| SalesDataGridView DataError event | Set the ErrorText to an error message.<br>Set e.Cancel = True. |
| StoresBindingSource DataError event | If setup complete<br>Display an error message. |