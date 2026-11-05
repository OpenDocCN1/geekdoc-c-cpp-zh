
on the form can be bound to the BindingSource object, as opposed to the actual data source.

Much functionality is automatically programmed into the tool strip. When the BindingNavigator control is first instantiated, the navigational move first, last, forward, and backward arrows work properly. This code was also automatically generated when the DataGridView control was dropped onto the form.

### Example 14-23

```csharp
private void studentBindingNavigatorSaveItem_Click(object sender, EventArgs e)
{
    this.Validate();
    this.studentBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll(this.studentDataBaseDataSet.Student);
}
```

## TableAdapterManager

The last statement in the method shown in Example 14-23 calls an UpdateAll() method of a TableAdapterManager class. You read earlier in this chapter how a data adapter could be used with a dataset to update a database using a disconnected architecture. The interaction between the dataset and the actual database is controlled through the methods of the data adapter or table adapter objects. Notice that one of the five objects in the component tray, shown in Figure 14-20, is a TableAdapterManager. With Visual Studio 2010, a TableAdapterManager object is generated when you create a dataset in a project. The TableAdapterManager is extremely useful when an application pulls data from two or more tables. It uses the foreign-key relationships to retrieve and save data in related data tables.

The data or table adapter fills the dataset from the data source (database), and then its update method is used to send the changes back to the database. Data and table adapters read data from a database into a dataset and then write the changed data from the dataset back to the database. They do this using SELECT, INSERT, DELETE, and UPDATE SQL statements.

## TableAdapters

In the previous discussion about writing program statements to use a dataset and data adapter to update a database, we stated that the CommandBuilder class could be used to generate SQL statements for updates after you set the SelectCommand property of the DataAdapter class. Another approach is to use the TableAdapter SelectCommand, InsertCommand, UpdateCommand, and DeleteCommand properties. The CommandText for each of these properties can be set to a SQL query. For the TableAdapter.Update() method to work properly, it has to have available SQL INSERT, DELETE, and UPDATE commands. Based on the interaction with the user, one or more of these commands is executed. If data is modified, the UPDATE SQL command is used. When records are deleted, the DELETE SQL command is used. The TableAdapter's Update() method determines which command(s) to use when it is invoked.

When you dropped the DataGridView control onto the form, one of the five objects placed in the component tray was studentTableAdapter. TableAdapters are designer-generated components that are not technically part of ADO.NET, but like data adapters provide a communication link between an application and a database. They provide all of the functionality of a data adapter. They also have a built-in connection object and enable you to configure the InsertCommand, UpdateCommand, and DeleteCommand SQL queries manually in the Properties window.

![](img/e33ae760e23d89eac66541252ad65de8_909_0.png)

If you select the TableAdapter object in the component tray and view its properties, you will not see the SelectCommand, InsertCommand, UpdateCommand, and DeleteCommand properties. You need to use the DataSet Designer to view and modify the CommandText for these properties.

## DataSet Designer

The Dataset Designer tool is available in Visual Studio to work with DataSet objects. The Dataset Designer can be used to extend the functionality of datasets. It is also used to create and modify data and table adapters and their queries. To start the designer, double-click a dataset in the Solution Explorer window or right-click the dataset in the Data Sources window. A visual representation of the dataset and table adapter is presented, as shown in Figure 14-21.

![](img/e33ae760e23d89eac66541252ad65de8_910_0.png)

Figure 14-21 Dataset Designer opened

The Dataset Designer is opened from the **Solution Explorer** window by double-clicking the **StudentDatabaseDataSet.xsd** file. The **Properties** window, shown in Figure 14-21, shows the **StudentTableAdapter** object. The **StudentTableAdapter** object is selected in the DataSet Designer. Notice there are properties named **InsertCommand**, **DeleteCommand**, **UpdateCommand**, and **SelectCommand**. When the **DataGridView** object was dropped on the form, SQL commands were associated with each of these properties.

## Reviewing the TableAdapter's Command Properties

The **StudentTableAdapter** object already has values associated with the SQL commands used to retrieve and update dataset tables. When you expand each of the properties for the four SQL commands (**SelectCommand**, **InsertCommand**, **DeleteCommand**, and **UpdateCommand**), three additional lines are revealed as shown in Figure 14-22. Options of **CommandText**, **CommandType**, and **Parameters** are displayed. You can use the **Query Builder** to edit or write new SQL statements for each of the **CommandTexts**.

![](img/e33ae760e23d89eac66541252ad65de8_911_0.png)

Figure 14-22 Updating the SelectCommand

As shown in Figure 14-22, the first property, **CommandText**, holds the SQL statement. The SQL statement can be typed directly into this box, or it can be generated using the **Query Builder**. To open the **Query Builder**, click in the **CommandText** value box. An ellipsis will appear. The Builder is started when you click the ellipsis.

## Query Builder

Clicking the value box beside any of the command properties opens up a drop-down list with options of **Current**, **New**, and **None**. The Query Builder can be launched from both **Current** and **New**. If you select **New**, and then click the ellipsis in the **CommandText** box, you are first prompted to select the table from which the data is to be retrieved. This is shown in Figure 14-23.

![](img/e33ae760e23d89eac66541252ad65de8_912_0.png)

Figure 14-23 Identify the table for the update

After you add the Student table and close the dialog box shown in Figure 14-23, you build the query. You can type the SQL statement into the SQL pane or use the Diagram pane to select the columns you want to update. Normally, all of the columns are selected for an update. The Grid pane in the center is used to filter and enter parameterized expressions.

## Parameters

To indicate that the column is to be set by entering a value at run time, a parameterized query can be created. For values that might be provided at run time while the form is being displayed, an “at” symbol (@) is placed in front of an identifier for SQL Server data sources. A question mark (?) is used instead of the @ symbol for Access. No identifier can follow the ? with Access.

Figure 14-24 shows the SELECT statement created with the Query Builder. Only records that had major_ID = 'CS' were retrieved.

![](img/e33ae760e23d89eac66541252ad65de8_913_0.png)

Figure 14-24 CommandText property value for the SelectCommand

The CommandText for the SelectCommand is shown in Example 14-24. Instead of using the Diagram or Grid pane, this SQL statement was typed directly into the SQL pane.

### Example 14-24

```sql
SELECT  student_ID, student_FirstName, student_LastName, major_ID,
        student_Phone
FROM Student
WHERE (major_ID = 'CS')
```

Inside the Query Builder, you can test your SQL statements by selecting the Execute Query button. If you have parameterized values, a dialog box is displayed requesting values for the arguments. The results of the query are displayed back on the **Results** pane in the **Query Builder** window.

You can insert new rows, modify the existing data, and delete one or more rows. Figure 14-25 shows some snapshots of the user interface as the application is running.

![](img/e33ae760e23d89eac66541252ad65de8_914_0.png)

**Figure 14-25** Example using Configuration Tools final output

As illustrated in Figure 14-25, Joshua Binkley’s name was changed. Two records (Adam Jones and Brenda Shepherd) were deleted, yet Francisco and Manuel Alberto were inserted. Clicking the **Save** button caused the `tableAdapterManager.UpdateAll()` method to be called, which used the table adapter’s `InsertCommand`, `DeleteCommand`, and `UpdateCommand` `CommandText` SQL statements to make changes back to the database. Figure 14-26 shows the updated Access table.

![](img/e33ae760e23d89eac66541252ad65de8_914_1.png)

Code generators often add more code than is necessary. The **UpdateCommand**'s **CommandText** was shortened to `UPDATE Student SET student_ID = ?, student_FirstName = ?, student_LastName = ?, major_ID = ?, student_Phone = ? WHERE (student_ID = ?)`. None of the other **CommandText** properties were modified for the final ConfigToolsExample solution.
