

![](img/36e48639a06772bcb0fa1ea2525b33a3_975_0.png)

**FIGURE 14-17**  Edit DataGridView columns

The major_ID column was removed from the grid using the smart tag **Edit Columns** option. The Last Name was moved up to be displayed in the first column, and the student_ID was moved to the end. As shown in Figure 14-17, the ToolTipText for the column is set here. You enter column headings for the fields into the HeaderText property. Otherwise, the default column names from the database are used as the heading. The Frozen property indicates whether the column moves when the DataGridView control scrolls horizontally. Table 14-7 lists the properties and changes that were made for this application.

Figure 14-18 shows the output produced when the application is run. The form and the DataGridView control were enlarged using the windows resizing handles. The DataGridView was moved to the top-left corner of the form and the DataGridView control's Dock in Parent Container property was set. The Dock in Parent Container property is accessible from the smart tag on the top-right corner of the control.

![](img/36e48639a06772bcb0fa1ea2525b33a3_977_0.png)

FIGURE 14-18 Example using Configuration Tools output

Values were not stored in alphabetical order by last name in the database. The DataGridView control provides the additional functionality of allowing columns to be sorted. The records shown in Figure 14-18 are sorted in ascending order by the last name. Clicking on the column heading for the last name refreshed the display, sorting the records by last name. A second click would rearrange the records in descending order by last name. The sorting capability is available for all of the columns.

## FORMATTING DATAGRIDVIEW CELLS

As noted earlier, when you select Edit Columns from the smart tag on the DataGridView control, the Bound Columns Properties window is displayed for individual columns. As shown in Figure 14-19, the appearance of the column can be formatted by selecting the first listed property, DefaultCellStyle. A CellStyle Builder is opened when you click this property. As shown in the middle window in Figure 14-19, the colors, font, alignment, and format for the cell are set using these properties.

![](img/36e48639a06772bcb0fa1ea2525b33a3_978_0.png)

**FIGURE 14-19** Formatting DataGridView cells

As shown in Figure 14-19, in addition to having numeric, currency, and scientific notation format options, you can also define custom formats for a cell. Nine options are available from the Alignment property, including TopLeft, TopRight, and TopCenter. Similar values (left, right, center) are found with the middle and bottom options. Four values representing the amount of blank space to insert at the left, right, top, and/or bottom can be set using the Padding properties.

Look back at the navigation strip on the form shown in Figure 14-18. This tool strip was automatically added to the form when the table from the **Data Sources** window was dropped onto the form. An object of the **BindingNavigator** class was instantiated; it represents a standardized way to navigate and manipulate data on a form.

## BINDINGNAVIGATOR CONTROL

Another class added to the component tray is the BindingNavigator class. The BindingNavigator control was shown in Figure 14-15. It was one of the five new objects added to the component tray at the bottom of the form when the table from the Data Sources pane was placed on the form. The form and component tray are shown again in Figure 14-20.

![](img/36e48639a06772bcb0fa1ea2525b33a3_979_0.png)

**FIGURE 14-20** BindingNavigator and BindingSource objects

The BindingNavigator control provides a standardized way to move through and process the data. The user interface for the BindingNavigator control includes several buttons and a text box object. The tool strip includes buttons to move first, move backward, move forward, and move to the last records. It also allows you to enter a record number and move directly to that record. The plus symbol inserts a new row so that new values can be entered. The X symbol deletes the row. The tool strip also includes a Save button.

In most cases, a BindingNavigator control is paired with a BindingSource control to move through data records on a form and interact with them. A BindingSource object simplifies binding controls on a form to data. It does this by first attaching the BindingSource control to the data source, then each of the individual controls placed on the form can be bound to the BindingSource object, as opposed to the actual data source.

Much functionality is automatically programmed into the tool strip. When the BindingNavigator control is first instantiated, the navigational move first, last, forward, and backward arrows work properly. This code was also automatically generated when the DataGridView control was dropped onto the form.

### EXAMPLE 14.23

```csharp
private void studentBindingNavigatorSaveItem_Click
    (object sender, EventArgs e)
{
    this.Validate();
    this.studentBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll
        (this.studentDataBaseDataSet.Student);
}
```

> **NOTE**
> 
> The DataGridView is a very rich control that could be programmatically accessed. It has a number of properties and can be treated like a collection of objects stored in a two-dimensional array. DataGridView is a column major structure, which means you would specify the column index first. The following code retrieves the value stored in the first column of the selected row of dataGrid1.
> 
> ```csharp
> dataGrid1[0, dataGrid1.CurrentRow.Index].Value.ToString();
> ```

## TableAdapterManager

The last statement in the method shown in Example 14-23 calls an UpdateAll() method of a TableAdapterManager class. You read earlier in this chapter how a data adapter could be used with a dataset to update a database using a disconnected architecture. The interaction between the dataset and the actual database is controlled through the methods of the data adapter or table adapter objects. Notice that one of the five objects in the component tray, shown in Figure 14-20, is a TableAdapterManager. A TableAdapterManager object is generated when you create a dataset in a project. The TableAdapterManager is extremely useful when an application pulls data from two or more tables. It uses the foreign-key relationships to retrieve and save data in related data tables.

The data or table adapter fills the dataset from the data source (database), and then its update method is used to send the changes back to the database. Data and table adapters read data from a database into a dataset and then write the changed data from the dataset back to the database. They do this using SELECT, INSERT, DELETE, and UPDATE SQL statements.

## TABLEADAPTERS

In the previous discussion about writing program statements to use a dataset and data adapter to update a database, we stated that the CommandBuilder class could be used to generate SQL statements for updates after you set the SelectCommand property of the DataAdapter class. Another approach is to use the TableAdapter SelectCommand, InsertCommand, UpdateCommand, and DeleteCommand properties. The CommandText for each of these properties can be set to a SQL query. For the TableAdapter Update( ) method to work properly, it has to have available SQL INSERT, DELETE, and UPDATE commands. Based on the interaction with the user, one or more of these commands is executed. If data is modified, the UPDATE SQL command is used. When records are deleted, the DELETE SQL command is used. The TableAdapter’s Update( ) method determines which command(s) to use when it is invoked.

When you dropped the DataGridView control onto the form, one of the five objects placed in the component tray was studentTableAdapter. TableAdapters are designer-generated components that are not technically part of ADO.NET, but like data adapters provide a communication link between an application and a database. They provide all of the functionality of a data adapter. They also have a built-in connection object and enable you to configure the InsertCommand, UpdateCommand, and DeleteCommand SQL queries manually in the Properties window.

> **NOTE** If you select the TableAdapter object in the component tray and view its properties, you will not see the SelectCommand, InsertCommand, UpdateCommand, and DeleteCommand properties. You need to use the **DataSet Designer** to view and modify the CommandText for these properties.

## DataSet Designer

The **DataSet Designer** tool is available in Visual Studio to work with DataSet objects. The **DataSet Designer** can be used to extend the functionality of datasets. It is also used to create and modify data and table adapters and their queries. To start the designer, double-click a dataset in the **Solution Explorer** window or right-click the dataset in the **Data Sources** window. A visual representation of the dataset and table adapter is presented, as shown in Figure 14–21.

