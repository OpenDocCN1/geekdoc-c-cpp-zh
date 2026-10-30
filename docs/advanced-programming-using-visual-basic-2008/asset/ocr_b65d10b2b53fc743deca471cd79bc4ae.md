# The Code for the Edit Button

```
Private Sub EditButton_Click(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles EditButton.Click
    ' Allow editing to the current record.
    EditingBoolean = True
    SetNavigation(False)
    SetControlsReadOnly(False)
    SetButtonsForEdit()
End Sub
```

# A Complete Update Program

Here is the code for the complete update program that uses navigation buttons and updates the data source after each change (Ch05DetailsViewUpdateNavigation). Refer to Figure 5.6 for the form.

```
'Program: Ch05DetailsViewUpdateNavigation
'Date: June 2009
'Programmer: Bradley Millsbaugh
'Class: ContactForm
'Description: Update a single table in a details view in a single-tier application. Uses buttons for navigation.
' Saves each change back to the original data source as
' it occurs.

Imports System.Data

Public Class ContactForm
    ' Module-level variables.
    Private AContactsDataSet As ContactsDataSet
    Private APublishersTableAdapter _
    As ContactsDataSetTableAdapters.PublishersTableAdapter
    Private WithEvents APublishersBindingSource As BindingSource

    Private AddingBoolean As Boolean = False
    Private EditingBoolean As Boolean = False

    Private Sub ContactForm_Load(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles MyBase.Load
        ' Load the DataSet.
        Try
            ' Set up and fill the DataSet.
            AContactsDataSet = New ContactsDataSet
            APublishersTableAdapter = New ContactsDataSetTableAdapters.PublishersTableAdapter
            APublishersTableAdapter.Fill(AContactsDataSet.Publishers)
            ' Set up the binding source.
            APublishersBindingSource = New BindingSource
            With APublishersBindingSource
                .DataSource = Me.AContactsDataSet
                .DataMember = "Publishers"
```