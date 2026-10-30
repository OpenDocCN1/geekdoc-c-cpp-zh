
# Set Up the Form Controls

+   STEP 1: In the Data Sources window, change the sales table to Details and set the stor_id field to a combo box.
+   
+   STEP 2: Drag the sales table to the form. Notice that the component tray now holds a DataSet, SalesTableAdapter, SalesBindingSource, SalesBindingNavigator, and TableAdapterManager.
+   
+   STEP 3: Drag the stores node from the Data Sources window and drop it on top of the stor_id combo box. This will set up the combo box bindings so that the store name from the stores table displays, instead of the stor_id. Two new components are added to the component tray: StoresTableAdapter and StoresBindingSource.
+   
+   STEP 4: Change the DropDownStyle property of the combo box to Simple and resize the box, if necessary, to make it match the text boxes. This step removes the drop-down arrow from the combo box to eliminate the possibility of the user navigating from the store name.
+   
+   STEP 5: Run the program. Using the navigation bar, step through the sales records. The store names should display for each sale. Stop program execution.

## What Happened?

It’s time to examine what happened behind the scenes. When you dropped the stores table on top of the combo box, the combo box properties were modified automatically. The DataSource property is set to the BindingSource of the table that contains the value to display (StoreBindingSource to display the store name). The DisplayMember is set to the column name, stor_name, and the ValueMember property is the primary key from the original table.

Although the bindings for the combo box changed, the bindings for the rest of the form’s controls are unchanged. You can verify that by expanding the DataBindings property from another control; the binding is still set to the SalesBindingSource.

The properties of the combo box are set according to the following table:

| Property | Setting | Purpose | Example |
|---|---|---|---|
| DataSource | BindingSource of the related table. | Determines the table from which to select the data. | StoresBindingSource |
| DisplayMember | Field name for the value from the related table. | The field value that you want to display. | stor_name |
| ValueMember | The primary key from the original table. | The link to connect the code in the primary table with the key in the secondary table. | stor_id |

## Look Up a Second Field

Notice that the sales data still hold a code for the title. The sales table holds a title_id field, and the database has a titles table that has a title_id primary key and title field. You can use most of the same steps that you used above to display the full title for each sale. Figure 4.10 shows the completed exercise; the steps to accomplish this task appear in the following step-by-step exercise.

## Figure 4.10

The completed lookup step-by-step exercise. The complete store name and title display instead of the stor_id and title_id fields for each sale.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_182_0.png)

+   STEP 1: In the Data Sources window, click the Configure DataSet with Wizard button.
+   STEP 2: Expand the Tables node and the titles table. Select the title_id and title fields and click Finish.
+   STEP 3: In the Form Designer, delete the text box and label for title_id. In the Data Sources window, for the sales table, change the control type for title_id to a combo box and drag only that field to the form. Fix the spacing of the controls and change the identifying label to "Title".
+   STEP 4: Drag the titles table from the Data Sources window and drop it on top of the title_id combo box. This should set the bindings for the combo box.
+   STEP 5: Change the DropDownStyle property of the combo box to Simple and resize the box to match the text boxes. This step removes the dropdown arrow from the combo box to eliminate the possibility of the user navigating from the title.
+   STEP 6: Test it. Does it work?

## Feedback 4.2

+   1. What Fill method statements are created for a relationship for Customers and Orders? Assume that the project contains two TableAdapters called CustomersTableAdapter and OrdersTableAdapter as well as a DataSet called NorthwindDataSet.
+   2. How can you view the relationship between two tables?
+   3. Describe the necessary steps to display the job description from the jobs table rather than the job id when displaying the employee table.

## Queries and Filters

If you want to retrieve the records that match a specific value, you can use a parameterized query or a filter. A parameterized query creates a new DataSet; a filter selects records from an existing DataSet. When you already have the complete DataSet, the best choice is to use a filter, rather than return to the original data source and create a new DataSet.

You will choose a filter or a parameterized query depending on the needs of the specific application. To use a filter, you select records from an existing DataSet. For a parameterized query, you send a new request (query) to the database. You may have a huge database and do not want the entire database loaded in memory. On the other hand, your needs may require you to limit the number of requests to the database, therefore limiting the number of queries. You need to be able to write an application either way, depending on the situation.

## Using a Parameterized Query

A parameterized query is a SQL statement that retrieves selected record(s) from the database based on a value that the user enters at run time. The fact that the user supplies the value, called the parameter, is the basis for the term parameterized query.

You have seen that a TableAdapter property holds the query for selecting a DataSet’s data. Actually, a TableAdapter can hold multiple queries, so we can add queries for various purposes. In the step-by-step exercise in this section, you will create an application that allows the user to enter a job_id. You will then execute a parameterized query that selects only the records that match that job_id from the database and creates a new DataSet from the result.

## Selecting Specific Records

When you want your DataSet to contain only selected record(s), you can modify the SQL SELECT statement used by the TableAdapter. Use a WHERE clause in a SQL query to specify which records to select, called the criteria.

Here are some example SELECT statements with WHERE clauses:

```
SELECT Title, Author, ISBN FROM Books
WHERE Title = 'Romeo and Juliette'
```

```
SELECT Name, AmountDue FROM OverdueAccounts
WHERE AmountDue > 100
```

```
SELECT emp_id, Iname, fname FROM employee
WHERE Iname = 'Jones'
```

However, you usually don’t know until run time the value that you want to include in the WHERE clause. In that case, you can use a wildcard in place of the actual value and supply the value as a parameter in code:

```
SELECT emp_id, Iname, fname FROM employee
WHERE Iname = @Iname
```

You can type the SQL SELECT statements yourself, or use the Query Builder, which generates the correct SQL when you enter a value in the Filter column. The exercise that follows uses the Query Builder.

> TIP
> In the SQL version used by Access, the WHERE clause should read: WHERE Iname = ?

## Creating a Parameterized Query—Step-by-Step

In this program, the user enters a job id. The program displays a grid of matching employees.

STEP 5: A FillByJobID toolstrip is added to your form. Move the grid, if necessary, to see both toolbars.

## Run the Program

+   STEP 1: Run the program.
+   
+   STEP 2: Type “5” in the text box on the search toolstrip.
+   
+   STEP 3: Click on the FillByJobID button on the toolstrip. The grid should fill with all of the employees with 5 for the Job ID (Figure 4.12). Try some other values; the Job IDs range from 2 to 14.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_185_0.png)

## Figure 4.12

> Enter “5” for the job_id and click the FillByJobID button; the grid fills with matching employee records.

## Make Modifications

STEP 1: You can make the form look more professional. You might change the text on the toolstrip buttons, set the grid’s column widths, dock the grid to the form, remove the editing buttons from the navigation toolbar, or even remove the navigation toolbar entirely.

> **TIP**
> 
> You can undock both toolbars and align them to be side-by-side.

## Examine the Code

Display the form’s code: The FillByJobIDToolStripButton has a click event handler. A FillByJobID method for the EmployeeTableAdapter is enclosed in a Try / Catch block. And still another program with all of its code has been generated automatically!

Every time the user clicks the FillByJobID button, a new DataSet is created, holding only the records that match the selection criteria.

## Filtering a DataSet

You can select rows from an existing DataSet by using a filter. In Chapter 3, you used the Sort method of a BindingSource; here you will learn to use the BindingSource’s Filter method.

```
’ Filter an existing DataSet based on a combo box selection.
SelectionString = JobComboBox.SelectedValue.ToString
With BindingSource1
    .DataMember = "employee"
    .Filter = "job_id = " & SelectionString
    .Sort = "Name"
End With
```
