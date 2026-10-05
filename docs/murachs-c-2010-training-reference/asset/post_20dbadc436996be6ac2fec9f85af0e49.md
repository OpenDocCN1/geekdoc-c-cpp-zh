
# The Query

Query Builder

| Column | Alias | Output | Sort Type | Sort Order | Filter | Or... |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| CustomerID | Customers | | Ascending | | | |
| Name | | | | | | |

Diagram pane

Grid pane

SQL pane

```sql
SELECT
FROM
ORDER BY Name
CustomerID, Name, Address, City, State, ZipCode
```

Results pane

![](img/3148667e42d4db35b3d08576aaa1fa01_594_0.png)

# Description

- To display the Query Builder for the main query, select the table adapter that contains the query and then click on the ellipsis to select the CommandText of the SelectCommand object in the Properties window.
- By default, the current table is displayed in the diagram pane. To add a related table to this pane, right-click in the pane, select Add Table, and select the table from the dialog box's displayed. Then, a join is added to the query.
- To include a column in a query, click on the box to its left. Then, that column is added to the grid pane. Or, select all the columns by checking the * (All Columns) items.
- To create a calculated column, enter an expression in the Column column and then enter the name you want to use for the Alias column.
- To sort the returned rows by one or more columns, select the Ascending or Descending option from the Sort Type for those columns in the sequence you wanted. You can also use the Sort Order to set the sort sequence.
- To specify selection criteria (like a specific value that the column must contain to be selected), enter it in the Filter column.
- To use a column for sorting or for specifying criteria without including it in the query results, remove the check mark from the Output column.
- As you select columns and specify sort and selection criteria, the Query Builder builds the SQL statement and displays it in the SQL pane.
- To display the results of a query in the results pane, click the Execute Query button.
- When you accept a query, a dialog box will be displayed if you want to update the Insert, Update, and Delete queries that are generated from the main query.

Figure 18-17 How to use the Query Builder

# How to preview the data for a query

After you create a query, you can use the Dataset Designer to preview the data it retrieves. To do that, you use the Preview Data dialog box as shown in figure 18-18. Here, the data returned by the Fill query for the Customers table adapter is being previewed.

To preview the data for a query, you just click the Preview button. When you do, the data will be displayed in the Results grid, and the number of columns and rows returned by the query will be displayed just below the grid. In this example, the query retrieved 6 columns and 697 rows.

In the next chapter, you'll learn how to create queries that use parameters. For those queries, you must enter a value for each parameter in the Value column of the Parameters grid before you can preview its data. For example, suppose you want to retrieve the data for a customer with a specific customer ID. Then, you have to enter that customer ID in the Parameters grid to retrieve the data for that customer.

# Preview Data dialog box

![](img/3148667e42d4db35b3d08576aaa1fa01_596_0.png)

# Description

- To display the Preview Data dialog box for a query, right-click on the query in the Dataset Designer and select the Preview Data command, or select the query and then use the Data→Preview Data command.
- To preview the data, click the Preview button. When you do, the data will be displayed in the Results grid, and the number of columns and rows returned by the query will be displayed just below the Results grid.
- If a query requires parameters, you must enter a value for each parameter in the Value column of the Parameters grid. Check chapter 19 for more information on query parameters.

Figure 18-18 How to preview the data for a query

# How to interpret the generated SQL statements

The Fill method of a table adapter uses the SQL Select statement's stored in the SelectCommand object for the Fill query of the table adapter to retrieve data from a database. Similarly, the UpdateAll manager uses the SQL Insert, Update, and Delete statements that are stored in the InsertCommand, UpdateCommand, and DeleteCommand objects of the table adapter to add, update, and delete from the database.

To help you understand what these statements form, figure 18-19 presents the Select for the Customer maintenance form and the Insert, Update, and Delete statements that were generated from this statement. Although these statements may look complicated, the information presented here will give you a good idea of how they work.

To start, notice that the Insert statement is formed by a Select statement that retrieves the row that was just added to the database. That may be necessary in cases where the database generates some of the data for the new row. When a customer row is added to the database, for example, the database generates the value of the CustomerID column. Then, the Select statement in this figure uses the SQL Server SCOPE_IDENTITY function to retrieve the row with this ID. If the database doesn't generate or calculate any of the column values, however, this Select statement, as well as the one after the Update statement, isn't.

Also notice that the Update and Delete statements use optimistic concurrency. Because of that, code is added to the Where clauses these statements to check whether any of the column values have changed since they were retrieved from the database. This code compares the current value of each column in the database against the original value of the column, which is stored in the dataset. If none of the values have changed, the operation is performed.

Finally, notice that most of the statements in this figure use one or more parameters. Parameters are used in the Values clause of the Insert statement and the Set clause of the dataset to refer to the current values of the columns in the dataset. Parameters are also used in the Where clauses of the Update and Delete statements to refer to the original values of the columns in the dataset. And one is used in the Where clause of the Select statement after the Update statement to refer to the current row. The wizard inserts these parameters when it creates the command objects for a table adapter. Then, before each statement is executed, Visual Studio substitutes the appropriate value for each variable.

This should give you more perspective on how the dataset is refreshed and how optimistic concurrency is provided when you use ADO.NET. Because of the disconnected data architecture, these features can't be provided by the database management system or by ADO.NET. Instead, they are provided by the SQL statements that are generated by the Data Source Configuration Wizard.

# SQL that retrieves customer rows

```sql
SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
```

# SQL that inserts a customer row and refreshes the dataset

```sql
INSERT INTO Customers
(Name, Address, City, State, ZipCode)
VALUES (@Name, @Address, @City, @State, @ZipCode);

SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE (CustomerID = SCOPE_IDENTITY())
```

# SQL that updates a customer row and refreshes the dataset

```sql
UPDATE Customers
SET Name = @Name,
    Address = @Address,
    City = @City,
    State = @State,
    ZipCode = @ZipCode
WHERE (CustomerID = @Original_CustomerID) AND
  (Name = @Original_Name) AND
  (City = @Original_City) AND
  (State = @Original_State) AND
  (ZipCode = @Original_ZipCode);

SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE (CustomerID = @CustomerID)
```

# SQL that deletes a customer row

```sql
DELETE FROM Customers
WHERE (CustomerID = @Original_CustomerID) AND
  (Name = @Original_Name) AND
  (City = @Original_City) AND
  (State = @Original_State) AND
  (ZipCode = @Original_ZipCode);
```

# Description

- By default, the Data Source Configuration Wizard adds code to the Where clause of the Update and Delete statements checks that the data hasn't changed since it was retrieved.
- By default, the Data Source Configuration Wizard adds a Select statement after the Insert and Update statement to refresh the new or modified row in the dataset.
