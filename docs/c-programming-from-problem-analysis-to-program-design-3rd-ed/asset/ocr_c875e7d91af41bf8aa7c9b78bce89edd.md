![](bbox=[0.171, 0.095, 0.91, 0.523])

Figure 14-21&nbsp;&nbsp;&nbsp; Dataset Designer opened

The Dataset Designer is opened from the **Solution Explorer** window by double-clicking the **StudentDatabaseDataSet.xsd** file. The **Properties** window, shown in Figure 14–21, shows the **StudentTableAdapter** object. The **StudentTableAdapter** object is selected in the DataSet Designer. Notice there are properties named **InsertCommand**, **DeleteCommand**, **UpdateCommand**, and **SelectCommand**. When the **DataGridView** object was dropped on the form, SQL commands were associated with each of these properties.

# Reviewing the TableAdapter's Command Properties

The **StudentTableAdapter** object already has values associated with the SQL commands used to retrieve and update dataset tables. When you expand each of the properties for the four SQL commands (**SelectCommand**, **InsertCommand**, **DeleteCommand**, and **UpdateCommand**), three additional lines are revealed as shown in Figure 14–22. Options of **CommandText**, **CommandType**, and **Parameters** are displayed. You can use the **Query Builder** to edit or write new SQL statements for each of the **CommandTexts**.