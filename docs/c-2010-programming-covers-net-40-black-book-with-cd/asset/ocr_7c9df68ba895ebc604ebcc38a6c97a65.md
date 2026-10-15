# Table 26.34: Noteworthy Properties of the AccessDataSource Class

| Property | Description |
|---|---|
| IsViewStateEnabled | Gets a value indicating whether view state is enabled for this control. (Inherited from Control) |
| LoadViewStateByID | Gets a value indicating whether the control participates in loading its view state by ID instead of index. (Inherited from Control) |
| OldValuesParameterFormatString | Gets or sets a format string to apply to the names of any parameters that are passed to the Delete() or Update() method. (Inherited from SqlDataSource) |
| Page | Gets a reference to the Page instance that contains the server control. (Inherited from Control) |
| Parent | Gets a reference to the server control's parent control in the page control hierarchy. (Inherited from Control) |
| ProviderName | Obtains the name of the .NET data provider that the AccessDataSource control uses to connect to a Microsoft Access database |
| SelectCommand | Gets or sets the SQL string that the SqlDataSource control uses to retrieve data from the underlying database. (Inherited from SqlDataSource) |
| SelectCommandType | Gets or sets a value indicating whether the text in the SelectCommand property is an SQL query or the name of a stored procedure. (Inherited from SqlDataSource) |
| SelectParameters | Gets the parameters collection that contains the parameters that are used by the SelectCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. (Inherited from SqlDataSource) |
| Site | Gets information about the container that hosts the current control when rendered on a design surface. (Inherited from Control) |
| SkinID | Gets the skin to apply to the DataSourceControl control. (Inherited from DataSourceControl) |
| SortParameterName | Gets or sets the name of a stored procedure parameter that is used to sort retrieved data when data retrieval is performed using a stored procedure. (Inherited from SqlDataSource) |
| SqlCacheDependency | Specifies a semicolon-delimited string that signifies which database and table to utilize for the Microsoft SQL Server cache dependency |

Now, let's explore the LinqDataSource control.

# The LinqDataSource Control

The LinqDataSource control is a data source control that allows a Web server control to access data located in the relational databases or in the memory data collection, such as an array and context objects. This control enables Web developers to use LINQ, which simplifies the interaction between object-oriented programming and relational data by applying the principles of object-oriented programming to relational data. The LinqDataSource control provides with the capability to connect to data from either a database or an in-memory collection, such as an array. This control enables a user to handle operations, such as insert and delete, without using SQL commands to perform these tasks.

The inheritance hierarchy of the LinqDataSource control is as follows:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.DataSourceControl.QueryableDataSource
      System.Web.UI.WebControls.ContextDataSource
        System.Web.UI.WebControls.LinqDataSource
```

Noteworthy properties of the LinqDataSource class are listed in Table 26.35: