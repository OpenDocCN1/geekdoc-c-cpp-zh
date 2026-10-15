
records in various ways on the Web page without affecting the dataset. When you drag a QueryExtender control to the page, the following code appears in the Source view of the page:

```
<asp:QueryExtender ID="QueryExtender1" runat="server"></asp:QueryExtender>
```

The inheritance hierarchy of the QueryExtender control is as follows:

System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.QueryExtender

Noteworthy properties of the QueryExtender class are listed in Table 26.28:

| Table 26.28: Noteworthy Properties of the QueryExtender Class |
| Property | Description |
| ClientIDMode | Generates ClientID property for the control (Inherited from the control) |
| EnableViewState | Decides whether the control save its view state automatically or not (Inherited from the control) |
| TargetControlID | Saves the id of the target control |
| ViewStateMode | Determines whether the view state is enabled for the chart control or not |
| Visible | Decides whether the control should be visible or not |

Noteworthy events of the QueryExtender class are listed in Table 26.29:

| Table 26.29: Noteworthy Events of the QueryExtender Class |
| Event | Description |
| Disposed | Invokes when the control is disposed |
| Init | Invokes when the Web page is initialized |
| Load | Invokes when the Web page is loaded |
| Unload | Invokes when the Web page is unloaded |

Noteworthy methods of the QueryExtender class are listed in Table 26.30:

| Table 26.30: Noteworthy Methods of the QueryExtender Class |
| Method | Description |
| ApplyStyleSheetSkin() | Applies the styles to the control defined in the style sheet |
| DataBind() | Binds the data source control with the database |
| Dispose() | Enables the control to complete the final steps before releasing from the memory |
| FindControl() | Searches the server control with the help of the its id |
| Focus() | Sets the focus on the control |
| HasControls() | Determines the child server control in the parent server control |

Noteworthy expressions of the QueryExtender class are listed in Table 26.31:

| Table 26.31: Noteworthy Expressions of the QueryExtender Class |
| Expressions | Description |
| SearchExpression | Searches the string value and compare with the given string value |
| RangeExpression | Defines the range using the pair of values |
| PropertyExpression | Compares the value of a column in a table with the given string value |
| OrderByExpression | Sorts the data by a particular column |
| CustomExpression | Provides the LINQ expression that can be customized |
| DynamicFilterExpression | Filters the data dynamically in dynamic data Web site |
| ControlFilterExpression | Filters the control in dynamic data Web site |

## The SqlDataSource Control

The SqlDataSource control is a data source control that allows a server control, such as the GridView control, to access data located in a relational database, such as Microsoft SQL Server and Oracle. This control also generates a connection string to interact with the data in an ASP.NET page. These connection strings are generated through the Configure Data Source wizard. A connection string contains information about the server, database, and security you are working with in your application, for example:

```
Data Source=.\sqlexpress; Initial Catalog=Northwnd; Integrated Security=True
```

### NOTE

To learn more about the Configure Data Source Wizard in detail, refer to the Immediate Solutions section of this chapter.

The SqlDataSource control automatically opens a database connection, which is provided in the connection string, executes the SQL queries, and then closes the connection. When you add a SqlDataSource control to an ASP.NET page, the following code appears in the Source view of a page:

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"></asp:SqlDataSource>
```

The inheritance hierarchy of the SqlDataSource control is as follows:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.DataSourceControl
      System.Web.UI.WebControls.SqlDataSource
```

Noteworthy properties of the SqlDataSource class are listed in Table 26.32:

## Table 26.32: Noteworthy Properties of the SqlDataSource Class

| Property | Description |
|---|---|
| CacheDuration | Obtains or sets the length of time, in seconds, for which the data source control caches data that is retrieved by the Select() method. |
| CacheExpirationPolicy | Obtains or sets the cache expiration behavior that, when combined with the duration, describes the behavior of the cache that the data source control uses. |
| CacheKeyDependency | Obtains or sets a user-defined key dependency that is linked to all data cache objects that are created by the data source control. All cache objects explicitly expire when the key expires. |
| CancelSelectOnNullParameter | Obtains or sets a value indicating whether a data retrieval operation is canceled when any parameter that is contained in the SelectParameters collection evaluates to null reference. |
| ChildControlsCreated | Gets a value that indicates whether the server control's child controls have been created. (Inherited from Control) |
| ClientID | Gets the server control identifier generated by ASP.NET. (Inherited from DataSourceControl) |
| ClientIDSeparator | Gets a character value representing the separator character used in the ClientID property. (Inherited from Control) |
| ConflictDetection | Obtains or sets the value indicating how the SqlDataSource control performs, updates, and deletes when data in a row in the underlying database changes during the time of the operation. |
| ConnectionString | Obtains or sets the ADO.NET provider-specific connection string that the SqlDataSource control uses to connect to an underlying database. |
| Context | Gets the HttpContext object associated with the server control for the current Web request. (Inherited from Control) |
| Controls | Gets a ControlCollection object that represents the child controls for a specified server control in the UI hierarchy. (Inherited from DataSourceControl) |
| DataSourceMode | Obtains or sets the data retrieval mode such as DataSet and DataReader that the SqlDataSource control uses to fetch data. |
| DeleteCommand | Obtains or sets the SQL string that the SqlDataSource control uses to delete the data from the underlying database. |
| DeleteCommandType | Obtains or sets a value indicating whether the text in the DeleteCommand property is an SQL statement or is the name of a stored procedure. |
| DeleteParameters | Obtains the parameters collection that contains the parameters that are used by the DeleteCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. |
| DesignMode | Gets a value indicating whether a control is being used on a design surface. (Inherited from Control) |
| EnableCaching | Obtains or sets a value indicating whether the SqlDataSource control has data caching enabled. |
| EnableTheming | Gets a value indicating whether this control supports themes. (Inherited from DataSourceControl) |
| EnableViewState | Gets or sets a value indicating whether the server control persists its view state, and the view state of any child controls it contains, to the requesting client. (Inherited from Control) |
| Events | Gets a list of event handler delegates for the control. This property is read-only. (Inherited from Control) |
| FilterExpression | Obtains or sets a filtering expression that is applied when the Select() method of data source is called. |
| FilterParameters | Obtains a collection of parameters that are associated with any parameter placeholders that are in the FilterExpression string. |
| HasChildViewState | Gets a value indicating whether the current server control's child controls have any saved view-state settings. (Inherited from Control) |
| ID | Gets or sets the programmatic identifier assigned to the server control. (Inherited from Control) |
| IdSeparator | Gets the character used to separate control identifiers. (Inherited from Control) |
| InsertCommand | Obtains or sets the SQL string that the SqlDataSource control uses to insert data into the underlying database. |
| InsertCommandType | Obtains or sets a value indicating whether the text in the InsertCommand property is an SQL statement or the name of a stored procedure. |
