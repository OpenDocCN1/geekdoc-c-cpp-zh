# SQL Server Database Programming with C#

To view each record, you can click the forward arrow on the top of the form to scan all records from the top to the bottom of the Faculty table.
If you only want to display some columns from the Faculty table, go to the Data Source window and select the Faculty table. Expand the table to display the individual columns, and drag the desired column from the Data Source window onto the DataGridView. For each column, an individual data-bound control is created on the DataGridViewForm, with an appropriately titled label control. When you run this project, the first record with columns will be retrieved and displayed on the form, and you can scan all records by clicking the forward arrow. One special column, family name, is shown at the bottom of Figure 5-2.
Well, the DataGridView is a powerful tool and allows users to view all data from a table. Generally, we do not want to perform this kind of view as an in-line SQL statement. The SQL statement must be already defined in full before your project runs. In others, you can add any parameter to the query statement and all query parameters must be defined before your project runs. But running SQL statements dynamically is a very popular style for today's database operations, and in the following sections we will implement this technology and LINQ to perform the data query from five tables in the database CSE_DEPT with SelectWizard Project.

# 5. USE DATA DESIGNER TO EDIT THE STRUCTURE OF A DATASET

After a data source is added to a new project, the next step is to edit the DataSet structure based on your applications you want to develop a dynamic SQL statement. The following DataSet Structures can be edited using the DataSet Designer:

+   - Build user-defined query in an SQL statement format
- Modify the method of the TableAdapter to match the users' preference

Now let's begin to develop a dynamic SQL statement or a user-defined query with a real example. We will use the same project SelectWizard Project developed in the previous sections. Before we start the Login table,
Open the Data Source and right-click any place inside the window, select Edit DataSet Designer. Locate the Login table and right-click on the last item, with two methods - Fill() and GetData() - displayed, and select the Add Item query from the popup menu. Or, you can also select Configure to modify an existing query. Right now, however, we do not want to configure any existing query; we just want to add a new query to perform without data query.
On the opened TableConfiguration Wizard, perform the following operations to build our dynamic query:

+   1) Keep the default selection, Use SQL statements, and click on the Next.
2) In the next wizard, Choose a Query Type, keep the top selection, SELECT which returns rows, and click on the Next button since we need to complete a row.
3) In the next wizard, just click on the Query button to open the Query Builder wizard to build our dynamic query.

The opened Query Builder wizard is shown in Figure 5.37.
Query Builder provides a graphical user interface (GUI) for creating SQL queries, and it is composed of graphical panes and test panes. The top two panes are graphical panes and the third pane is the text pane. You can select columns from the top graphical pane, and each column selected will be added into the second graphical pane, you can