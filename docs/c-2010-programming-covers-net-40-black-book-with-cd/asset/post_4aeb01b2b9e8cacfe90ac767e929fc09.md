
# Table 26.32: Noteworthy Properties of the SqlDataSource Class

| Property | Description |
|---|---|
| InsertParameters | Obtains the parameters collection that contains the parameters that are used by the InsertCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. |
| IsChildControlStateCleared | Gets a value indicating whether controls contained within this control have control state. (Inherited from Control) |
| IsTrackingViewState | Gets a value that indicates whether the server control is saving changes to its view state. (Inherited from Control) |
| IsViewStateEnabled | Gets a value indicating whether view state is enabled for this control. (Inherited from Control) |
| LoadViewStateByID | Gets a value indicating whether the control participates in loading its view state by ID instead of index. (Inherited from Control) |
| OldValuesParameterFormatString | Obtains or sets a format string to apply to the names of any parameters that are passed to the Delete() or Update() method. |
| Page | Allows you to get the reference to the Page instance that contains server control. (Inherited from Control) |
| Parent | Gets a reference to the server control's parent control in the page control hierarchy. (Inherited from Control) |
| ProviderName | Obtains or sets the name of the .NET Framework data provider that the SqlDataSource control uses to connect to an underlying data source. |
| SelectCommand | Obtains or sets the SQL string that the SqlDataSource control uses to retrieve data from the underlying database. |
| SelectCommandType | Obtains or sets a value indicating whether the text in the SelectCommand property is an SQL query or the name of a stored procedure. |
| SelectParameters | Obtains the parameters collection that contains the parameters that are used by the SelectCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. |
| Site | Gets information about the container that hosts the current control when rendered on a design surface. (Inherited from Control) |
| SkinID | Gets the skin to apply to the DataSourceControl control. (Inherited from DataSourceControl) |
| SortParameterName | Obtains or sets the name of a stored procedure parameter that is used to sort retrieved data when data retrieval is performed using a stored procedure. |
| SqlCacheDependency | Obtains or sets a semicolon-delimited string that indicates which databases and tables to use for the Microsoft SQL Server cache dependency. |
| TemplateControl | Gets or sets a reference to the template that contains this control. (Inherited from Control) |
| TemplateSourceDirectory | Gets the virtual directory of the Page or UserControl that contains the current server control. (Inherited from Control) |
| UniqueID | Gets the unique, hierarchically qualified identifier for the server control. (Inherited from Control) |
| UpdateCommand | Obtains or sets the SQL string that the SqlDataSource control uses to update data in the underlying database. |
| UpdateCommandType | Obtains or sets a value indicating whether the text in the UpdateCommand property is an SQL statement or the name of a stored procedure. |
| UpdateParameters | Obtains the parameters' collection that contains the parameters that are used by the UpdateCommand property from the SqlDataSourceView control. The SqlDataSourceView control is associated with the SqlDataSource control. |

Noteworthy methods of the SqlDataSource class are listed in the following Table 26.33:

# Table 26.33: Noteworthy Methods of the SqlDataSource Class

| Method | Description |
|---|---|
| Delete() | Deletes the data from the database by using the DeleteCommand SQL string and any parameters that are in the DeleteParameters collection |
| Insert() | Inserts the data in the database by using the InsertCommand SQL string and any parameters that are in the InsertParameters collection |
| Select() | Retrieves the data from the database by using the SelectCommand SQL string and any parameters that are in the SelectParameters collection |
| Update() | Updates the data in the database by using the UpdateCommand SQL string and any parameters that are in the UpdateParameters collection |

Now, let's learn about the AccessDataSource control.

## The AccessDataSource Control

The AccessDataSource control is a data source control that allows a Web server control to access a Microsoft Access database. This control does not support connection strings, but the DataFile property of this control allows you to specify the Access file (.mdb file) that you want to use to access the data. When you add an AccessDataSource control to your ASP.NET page, the following line of code appears in the Source view of page:

```
<asp:AccessDataSource ID="AccessDataSource1" runat="server"></asp:AccessDataSource>
```

The AccessDataSource control does not allow you to provide username and password to access the data. If you need to use a password-protected Access database, select the SqlDataSource control to access the database. The inheritance hierarchy of the AccessDataSource control is as follows:

System.Object
  System.Web.UI.Control
    System.Web.UI.DataSourceControl
      System.Web.UI.WebControls.SqlDataSource
        System.Web.UI.WebControls.AccessDataSource

Noteworthy properties of the AccessDataSource class are listed in Table 26.34:

# Table 26.34: Noteworthy Properties of the AccessDataSource Class

| Property | Description |
|---|---|
| ConnectionString | Obtains the connection string that is used to connect to the Microsoft Access database |
| Context | Gets the HttpContext object associated with the server control for the current Web request. (Inherited from Control) |
| Controls | Gets a ControlCollection object that represents the child controls for a specified server control in the UI hierarchy. (Inherited from DataSourceControl) |
| DataFile | Specifies the path of the Microsoft Access .mdb file |
| DataSourceMode | Gets or sets the data retrieval mode that the SqlDataSource control uses to fetch data. (Inherited from SqlDataSource) |
| DeleteCommand | Gets or sets the SQL string that the SqlDataSource control uses to delete data from the underlying database. (Inherited from SqlDataSource) |
| DeleteCommandType | Gets or sets a value indicating whether the text in the DeleteCommand property is an SQL statement or the name of a stored procedure. (Inherited from SqlDataSource) |
| DeleteParameters | Gets the parameters collection that contains the parameters that are used by the DeleteCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. (Inherited from SqlDataSource) |
| DesignMode | Gets a value indicating whether a control is being used on a design surface. (Inherited from Control) |
| EnableCaching | Gets or sets a value indicating whether the SqlDataSource control has data caching enabled. (Inherited from SqlDataSource) |
| EnableTheming | Gets a value indicating whether this control supports themes. (Inherited from DataSourceControl) |
| EnableViewState | Gets or sets a value indicating whether the server control persists its view state, and the view state of any child controls it contains, to the requesting client. (Inherited from Control) |
| Events | Gets a list of event handler delegates for the control. This property is read-only. (Inherited from Control) |
| FilterExpression | Gets or sets a filtering expression that is applied when the Select() method is called. (Inherited from SqlDataSource) |
| FilterParameters | Gets a collection of parameters that are associated with any parameter placeholders that are in the FilterExpression string. (Inherited from SqlDataSource) |
| HasChildViewState | Gets a value indicating whether the current server control's child controls have any saved view-state settings. (Inherited from Control) |
| ID | Gets or sets the programmatic identifier assigned to the server control. (Inherited from Control) |
| IdSeparator | Infrastructure. Gets the character used to separate control identifiers. (Inherited from Control) |
| InsertCommand | Gets or sets the SQL string that the SqlDataSource control uses to insert data into the underlying database. (Inherited from SqlDataSource) |
| InsertCommandType | Gets or sets a value indicating whether the text in the InsertCommand property is an SQL statement or the name of a stored procedure. (Inherited from SqlDataSource) |
| InsertParameters | Gets the parameters collection that contains the parameters that are used by the InsertCommand property from the SqlDataSourceView object that is associated with the SqlDataSource control. (Inherited from SqlDataSource) |
| IsChildControlStateCleared | Gets a value indicating whether controls contained within this control have control state. (Inherited from Control) |
| IsTrackingViewState | Gets a value that indicates whether the server control is saving changes to its view state. (Inherited from Control) |
