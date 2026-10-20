# How to work with columns and events

As mentioned earlier in this chapter, the DataGridView controls in most production applications don’t provide for adding, modifying, and deleting data directly in the grid. However, you can add columns that contain buttons for modifying and deleting rows. Then, when a user clicks on one of these buttons, you can handle the event that occurs to execute custom code that performs the modify or delete operation. You can also provide a button outside of the DataGridView control that lets the user add new rows.

# How to add and remove columns

Figure 22-6 shows how to add a button column to a DataGridView control. To start, you use the constructor for the DataGridViewButtonColumn class to create a column that contains a button. Then, you can use the properties of this class to determine how the column is formatted. Finally, you can use the Add() method to add the column to the end of the Columns collection. Alternatively, you can use the Insert() method to insert the column at a specific index.

The first example in this figure shows how this works. Here, the first statement creates the column. Then, the second statement sets the HeaderText property to an empty string so nothing is displayed in the column header. Next, the UseColumnTextForButtonValue is set to true. That way, the value of the Text property is displayed on each button in the column, and the Text property is set to “Delete”. Finally, the Add() method adds the column to the end of the Columns collection. The column that’s created by this code is shown in the grid at the top of this figure. This grid also includes a button column with Modify buttons that’s created using similar code.

In addition to adding button columns, you can add columns that provide other types of controls including text boxes, checkboxes, and images. For more information on how to use these types of columns, see the online documentation.

This figure also shows how to delete a column from a grid. You might want to that, for example, if the grid is bound to an entity collection and the entity contains one or more properties that define relationships with other tables. Then, you can use the Remove() or RemoveAt() method to delete those columns.