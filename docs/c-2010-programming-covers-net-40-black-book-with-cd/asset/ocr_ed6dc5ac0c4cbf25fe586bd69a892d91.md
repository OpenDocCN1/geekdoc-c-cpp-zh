# Table 26.38: Noteworthy Properties of the ObjectDataSource Class

| Property | Description |
|---|---|
| Parent | Gets a reference to the server control's parent control in the page control hierarchy. (Inherited from Control) |
| SelectCountMethod | Obtains or sets the name of the method or function that the ObjectDataSource control invokes to retrieve a row count. |
| SelectMethod | Obtains or sets the name of the method or function that the ObjectDataSource control invokes to retrieve data. |
| SelectParameters | Obtains the parameters collection that contains the parameters that are used by the method specified by the SelectMethod property. |
| Site | Gets information about the container that hosts the current control when rendered on a design surface. (Inherited from Control) |
| SkinID | Gets the skin to apply to the DataSourceControl control. (Inherited from DataSourceControl) |
| SortParameterName | Obtains or sets the name of the business object that the SelectMethod parameter uses to specify a sort expression for data source sorting support. |
| SqlCacheDependency | Obtains or sets a semicolon-delimited string that indicates which databases and tables to use for the Microsoft SQL Server cache dependency. |
| StartRowIndexParameterName | Obtains or sets the name of the data retrieval method parameter that is used to indicate the value of the identifier of the first record to retrieve for data source paging support. |
| TemplateControl | Gets or sets a reference to the template that contains this control. (Inherited from Control) |
| TemplateSourceDirectory | Gets the virtual directory of the Page or UserControl that contains the current server control. (Inherited from Control.) |
| TypeName | Obtains or sets the name of the class that the ObjectDataSource object represents. |
| UniqueID | Allows the server control to get the unique, hierarchically qualified identifier. (Inherited from Control) |
| UpdateMethod | Obtains or sets the name of the method or function that the ObjectDataSource control invokes to update data. |
| UpdateParameters | Obtains the parameters collection that contains the parameters that are used by the method that is specified by the UpdateMethod property. |

Noteworthy methods of the ObjectDataSource class are listed in Table 26.39:

# Table 26.39: Noteworthy Methods of the ObjectDataSource Class

| Method | Description |
|---|---|
| Delete() | Deletes the data from the database by calling the method that is identified by the DeleteMethod property with any parameters that are in the DeleteParameters collection |
| Insert() | Inserts the data in the database by calling the method that is identified by the InsertMethod property and any parameters in the InsertParameters collection |
| Select() | Retrieves the data from the database by calling the method that is identified by the SelectMethod property with the parameters in the SelectParameters collection |
| Update() | Updates the data in the database by calling the method that is identified by the UpdateMethod property and any parameters that are in the UpdateParameters collection |