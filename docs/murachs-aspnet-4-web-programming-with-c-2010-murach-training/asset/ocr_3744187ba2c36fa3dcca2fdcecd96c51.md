# How to update GridView data

Another impressive feature of the GridView control is its ability to update data in the underlying data source with little additional code. Before you can set that up, though, you must configure the data source with Update, Delete, and Insert statements, as described in the last chapter. Once you’ve done that, you can set up a GridView control so it calls the Update and Delete statements, which you’ll learn how to do next. Then, you’ll learn how to insert a row into a GridView control.

# How to work with command fields

A command field is a GridView column that contains one or more command buttons. Figure 14-9 shows five of the command buttons that you can include in each row of a GridView control. Please note, however, that the Update and Cancel buttons are displayed only when a user clicks the Edit button to edit a row. You can’t display these buttons in separate command fields.

When the user clicks a Delete button, the GridView control calls the data source control’s Delete method, which deletes the selected row from the underlying database. Then, the GridView control redisplays the data without the deleted row.

When the user clicks the Edit button, the GridView control places the selected row in edit mode. In this mode, the labels used to display the editable bound fields are replaced by text boxes so the user can enter changes. Also, the row is formatted using the style attributes provided by the EditRowStyle element. Finally, the Edit button itself is replaced by Update and Cancel buttons. Then, if the user clicks the Update button, the GridView control calls the data source control’s Update method, which updates the underlying database. But if the user clicks Cancel, any changes made by the user are discarded and the original values are redisplayed.

The Select button lets the user select a row. Then, the selected row is displayed with the settings in the SelectedRowStyle element. Also, the SelectedIndex and SelectedRow properties are updated to reflect the selected row. The Select button is most often used in combination with a FormView or DetailsView control to create pages that show the details for an item selected from the GridView control. You’ll learn how this works in chapter 15.

The two tables in this figure show the attributes of a CommandField element. For instance, you can set the ShowEditButton attribute to True to display an Edit button in a command field. And you can use the EditText attribute to set the text that’s displayed on that button.

Although a single command field can display more than one button, it’s common to create separate command fields for Select, Edit, and Delete buttons. It’s also common to set the CausesValidation attribute of the Select and Delete buttons to False since the operations these buttons perform don’t require any data validation. On the other hand, you’ll usually leave the CausesValidation attribute of the Edit button set to True so that validation is performed when the user clicks the Update button. Later in this chapter, you’ll learn how to use validation controls with the Edit button by creating template fields.