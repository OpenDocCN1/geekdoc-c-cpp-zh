
## The dialog box for entering a custom Select statement

![](img/c024ccf88e28c30c07dd410d4342288f_438_0.png)

### Description

- To use custom statements with a SQL data source, select the SQL Statement option and then enter the statement into the text box. You can enter Select, Update, Insert, and Delete statements by selecting the appropriate tab.
- You can also generate custom statements using the Query Builder as shown in figure 13-9.
- To use stored procedures with a SQL data source, select the Stored Procedure option and then select the stored procedure you want to use from the drop-down list that's displayed.
- When you use custom statements, Visual Studio doesn't generate Update, Insert, and Delete statements from the Select statement you enter. Because of that, you have to enter each of these statements yourself or use the Query Builder to generate them.

## How to create a Select statement with the Query Builder

The Query Builder makes it easy to generate SQL statements without even knowing the proper syntax for them. Even if you do know the proper syntax, it can be much easier to use the Query Builder than to enter your own custom statements. In this topic, I’ll show you how to use the Query Builder to create a Select statement. You can use similar techniques to create other SQL statements.

When the Query Builder window opens, the Add Table dialog box is displayed. This dialog box, which isn’t shown in this figure, lists all of the tables and views in the database that the data source is connected to. You can use this dialog box to add one or more tables to the diagram pane of the Query Builder window so you can use them in your query. In this figure, for example, the Products table has been added to the diagram pane.

In the grid pane, you can see the columns that will be included in the query. To add columns to this pane, you just check the boxes before the column names in the diagram pane. You can also enter an expression in the Column column of the grid pane to create a calculated column, and you can enter a name in the Alias column to give the calculated column a name.

Once the columns have been added to the grid pane, you can use the Sort Type column to identify any columns that should be used to sort the returned rows and the Sort Order column to give the order of precedence for the sort if more than one column is identified. The Query Builder uses these specifications to build the Order By clause for the Select statement.

You can use the Filter column to establish the criteria to be used to select the rows that will be retrieved by the query. For the query in this figure, a parameter named @CategoryID is specified for the CategoryID column. As a result, only the products whose CategoryID field matches the value of the @CategoryID parameter will be retrieved.

Notice in this figure that the Output column for the CategoryID column in the grid pane isn’t selected. That means that this column won’t be included in the query output. However, it’s included in the grid pane so it can be used to specify the filter criteria.

## The Query Builder dialog box

![](img/c024ccf88e28c30c07dd410d4342288f_440_0.png)

### Description

- The *Query Builder* is displayed if you choose to enter a custom SQL statement, and then click the Query Builder button in the dialog box that follows.
- The Query Builder lets you build a Select statement by choosing columns from one or more tables and views and specifying the sort order and filter criteria for each column.
- When you first start the Query Builder, a dialog box is displayed that lets you select the database tables you want to include in the query. Each table you select is displayed in the *diagram pane* at the top of the Query Builder window.
- If you add two related tables to the diagram pane, the Query Builder automatically joins the two tables by including a Join phrase in the From clause.
- To include a column from a table, use the check box that appears next to the column in the diagram pane. This adds the column to the *grid pane*. Then, you can specify any sorting or filtering requirements for the column.
- You can use a parameter in an expression in the Filter column to create a parameterized query. If you use one or more parameters in the query, the Data Source Configuration Wizard lets you specify the source of each parameter value, as described in figure 13-10.
- As you select columns and specify sort and selection criteria, the Query Builder builds the Select statement and displays it in the *SQL pane*.
- To display the results of the query in the *results pane*, click the Execute Query button. If the query includes parameters, you will be asked to enter the value of each parameter.

Figure 13-9 How to create a Select statement with the Query Builder

## The dialog box for defining parameters

![](img/c024ccf88e28c30c07dd410d4342288f_442_0.png)

### Parameter sources

| Source | Description |
|---|---|
| Control | The parameter's value comes from a control on the page. |
| QueryString | The parameter's value comes from a query string in the URL used to request the page. |
| Form | The parameter's value comes from an HTML form field. |
| Session | The parameter's value comes from an item in session state. |
| Profile | The parameter's value comes from a profile property. |
| Cookie | The parameter's value comes from a cookie. |

### Description

- If you specify one or more parameters when you use the Query Builder to define a Select statement, the next dialog box lets you define those parameters.
- To define a parameter, you specify the source of the value for each parameter.

## How to use the DataList control

A DataList control displays items from a repeating data source such as a data table. In the topics that follow, you’ll learn how the DataList control works, you’ll learn how to create the templates that define a DataList control, and you’ll learn how to format a DataList control.

Before I present the DataList control, though, you should know that you can also create a list using the Repeater control. The Repeater control has one major drawback, however. That is, you can’t define it using a visual interface. Instead, you have to enter code directly into the .aspx file. Because of that, we won’t present the Repeater control in this book.

### How the DataList control works

Figure 13-11 shows a simple *data list* that consists of two columns of data. To create a list like this, you use the DataSourceID attribute of the DataList control to bind the control to a data source. Then, you define one or more *templates* within the control that define the content and format of the list.

In the .aspx code shown in this figure, you can see that the source of data for the data list is a SQL data source control named SqlDataSource2. You can also see that a single Item template is used to create this list. This template includes two label controls that are bound to the Name and UnitPrice columns of the data source. You’ll learn about the expressions you use to accomplish this binding later in this chapter.

### A simple list displayed by a DataList control

- Austin Powers $79.99
- Frankenstein $39.99
- Hippie $79.99
- JarJar $59.99
- Martian $69.99
- Superman $39.99

### The .aspx code for the DataList control

```
<asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource2">
    <ItemTemplate>
        <asp:Label ID="lblName" runat="server"
            Text='<%# Eval("Name") %>'></asp:Label>
        <asp:Label ID="lblUnitPrice" runat="server"
            Text='<%# Eval("UnitPrice", "{0:C}") %>'></asp:Label>
    </ItemTemplate>
</asp:DataList>
```

### Basic attributes of the DataList control

| Attribute | Description |
|---|---|
| ID | The ID for the DataList control. |
| Runat | Must specify "server". |
| DataSourceID | The ID of the data source to bind the data list to. |

### Description

- A *data list* displays a list of items from the data source that it’s bound to. To bind a data list to a data source, use the Choose Data Source command in the control’s smart tag menu.
- To define the information to be displayed in a data list, you create one or more *templates*. Visual Studio provides a designer interface you can use to create the templates as shown in the next figure.
- To display the data from a column in the data source in a data list, you add a control to a template and then bind that control. See figure 13-14 for more information.
- You can use a DataList control for edit operations as well as display operations. However, you’re more likely to use the GridView, DetailsView, FormView, and ListView controls for edit operations.
