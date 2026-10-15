
## Table 26.44: Noteworthy Properties of the EntityDataSource Class

| Property | Description |
|---|---|
| TemplateControl | Gets or sets a reference to the template that contains this control. (Inherited from Control) |
| TemplateSourceDirectory | Gets the virtual directory of the Page or UserControl that contains the current server control. (Inherited from Control) |
| UniqueID | Gets the unique, hierarchically qualified identifier for the server control. (Inherited from Control) |
| UpdateParameters | Obtains the collection of parameters that are used during an update operation |
| ViewState | Gets a dictionary of state information that allows you to save and restore the view state of a server control across multiple requests for the same page. (Inherited from Control) |
| ViewStateIgnoresCase | Gets a value that indicates whether the StateBag object is case-insensitive. (Inherited from Control) |
| Visible | Gets or sets a value indicating whether the control is visually displayed. (Inherited from DataSourceControl) |
| Where | Obtains or sets a value that specifies what conditions must be true for a record to be included in the retrieved data |
| WhereParameters | Obtains the collection of parameters that is used to create the Where clause |

Noteworthy methods of the EntityDataSource class are listed in Table 26.45:

## Table 26.45: Noteworthy Methods of the EntityDataSource Class

| Method | Description |
|---|---|
| DataBind() | Binds the data source control with the database |
| Dispose() | Enables the control to complete the final steps before releasing from the memory |

Noteworthy events of the EntityDataSource class are listed in Table 26.46:

## Table 26.46: Noteworthy Events of the EntityDataSource Class

| Event | Description |
|---|---|
| ContextCreated | Invokes after an instance of the context type object is created |
| ContextCreating | Invokes before an instance of the context type object is created |
| ContextDisposing | Invokes before disposing the context type object |
| DataBinding | Occurs when the server control binds to a data source. (Inherited from Control.) |
| Deleted | Invokes when a delete operation has finished |
| Deleting | Invokes before a delete operation starts |
| Disposed | Occurs when a server control is released from memory, which is the last stage of the server control lifecycle when an ASP.NET page is requested. (Inherited from Control.) |
| Init | Occurs when the server control is initialized, which is the first step in its lifecycle. (Inherited from Control.) |
| Inserted | Invokes when an insert operation has finished |
| Inserting | Invokes before an insert operation starts |

| Event | Description |
|---|---|
| Load | Occurs when the server control is loaded into the Page object. (Inherited from Control.) |
| PreRender | Occurs after the Control object is loaded but prior to rendering. (Inherited from Control.) |
| Selected | Invokes when a data retrieval operation has finished |
| Selecting | Invokes before a data-retrieval operation starts |
| Unload | Occurs when the server control is unloaded from memory. (Inherited from Control.) |
| Updated | Invokes when an update operation has finished |
| Updating | Invokes before an update operation starts |

Now, let’s learn about the SiteMapDataSource control.

## The SiteMapDataSource Control

The SiteMapDataSource control allows you to work with the data stored in the SiteMap configuration file. This control also provides with the capability to customize site navigation by using site map data with data server controls, irrespective of the fact that controls are not navigation controls. The inheritance hierarchy of the SiteMapDataSource control is as follows:

```
System.Object
  System.Web.UI.Control
    System.Web.UI.HierarchicalDataSourceControl
      System.Web.UI.WebControls.SiteMapDataSource
```

Noteworthy properties of the SiteMapDataSource class are listed in Table 26.47:

## Table 26.47: Noteworthy Properties of the SiteMapDataSource Class

| Property | Description |
|---|---|
| ContainsListCollection | Obtains a value indicating whether the data source control contains a collection of data source view objects |
| Context | Gets the HttpContext object associated with the server control for the current Web request. (Inherited from Control.) |
| Controls | Gets a ControlCollection object that represents the child controls for a specified server control in the UI hierarchy. (Inherited from HierarchicalDataSourceControl.) |
| DesignMode | Gets a value indicating whether a control is being used on a design surface. (Inherited from Control.) |
| EnableTheming | Gets a value indicating whether this control supports themes. (Inherited from HierarchicalDataSourceControl.) |
| EnableViewState | Gets or sets a value indicating whether the server control persists its view state, and the view state of any child controls it contains, to the requesting client. (Inherited from Control.) |
| Events | Gets a list of event handler delegates for the control. This property is read-only. (Inherited from Control.) |
| HasChildViewState | Gets a value indicating whether the current server control's child controls have any saved view-state settings. (Inherited from Control.) |
| ID | Gets or sets the programmatic identifier assigned to the server control. (Inherited from Control.) |
| IdSeparator | Gets the character used to separate control identifiers. (Inherited from Control.) |

## Immediate Solutions

## Using the SqlDataSource Control

In this chapter, you have learned that you can display or customize data through data bound controls, such as the GridView control, using any data source controls, such as the SqlDataSource control. The selection of a data source control and data bound control depends on the requirement of an application.

> NOTE
> In this section, we will cover all the data source controls using the GridView control.

Now, let’s understand the SqlDataSource control. Implement the following steps to display data in a GridView control by using the SqlDataSource control:

- 1. Create a Web application and save it as SqlDataSource (available on the CD).

> NOTE
> The applications in this chapter are created using the ASP.NET Empty Web Site template in the New Web Site dialog box. After creating the application, you need to add the Default.aspx page to the application.

- 2. Drag and drop a SqlDataSource control on the Design view of the Default.aspx page. Now, click the Smart Tag, as shown in Figure 26.1:

![](img/e073a4882197be4ab61103cbe0bcb394_1299_0.png)

Figure 26.1: Adding a SqlDataSource Control to the Web Page

> NOTE
> The arrow symbol on the right of the SqlDataSource control in Figure 26.1 represents the Smart Tag.

- 3. Click the Configure Data Source option to configure a data source with the SqlDataSource control, as shown in Figure 26.2:

![](img/e073a4882197be4ab61103cbe0bcb394_1300_0.png)

# Figure 26.2: Configuring Data Source of the SqlDataSource Control

The Configure Data Source wizard appears (Figure 26.3).

- 4. Click the New Connection button, as shown in Figure 26.3:

![](img/e073a4882197be4ab61103cbe0bcb394_1300_1.png)

# Figure 26.3: Clicking the New Connection Button

The Add Connection dialog box appears (Figure 26.4).

5. Select a server name from the Server name combo box and database name from the Select or enter a database name combo box, respectively in the Add Connection dialog box. In this example, we have selected northwnd as the database (Figure 26.4).

6. Click the Test Connection button to test the connection with the database, as shown in Figure 26.4:

![](img/e073a4882197be4ab61103cbe0bcb394_1301_0.png)

# Figure 26.4: Adding a Connection

The Microsoft Visual Studio message box appears that shows the connection with the database is successfully established (Figure 26.5).

7. Click the OK button in the Microsoft Visual Studio message box, as shown in Figure 26.5:

![](img/e073a4882197be4ab61103cbe0bcb394_1301_1.png)

# Figure 26.5: Displaying the Success Message

8. Click the OK button in the Add Connection dialog box. Now, a connection to the northwnd database is created (Figure 26.6).

9. Click the Next button, as shown in Figure 26.6:
