After learning about the LingDataSource control, let’s learn about the SiteMapDataSource control.

# The SiteMapDataSource Control

The SiteMapDataSource control allows you to work with the data stored in the SiteMap configuration file. This control also provides the capability to customize site navigation by using site map data with data server controls, irrespective of the fact that controls are not navigation controls. Table 6.11 lists some noteworthy properties of the SiteMapDataSource class:

| Table 6.11: Noteworthy Properties of the SiteMapDataSource Class |  |
|---|---|
| **Property** | **Description** |
| `ContainsListCollection` | Obtains a value indicating whether the SiteMapDataSource control contains a collection of data source view objects |
| `Context` | Gets the HttpContext object associated with the server control for the current Web request. |
| `Controls` | Gets a ControlCollection object that represents the child controls for a specified server control in the user interface hierarchy. |
| `DesignMode` | Gets a value indicating whether a control is being used on a design surface. |
| `EnableTheming` | Gets a value indicating whether this control supports themes. |
| `EnableViewState` | Gets or sets a value indicating whether the server control persists its view state, and the view state of any child controls it contains, to the requesting client. |
| `Events` | Gets a list of event handler delegates for the control. This property is read-only. |
| `HasChildViewState` | Gets a value indicating whether the current server control’s child controls have any saved view-state settings. |

Table 6.12 lists some noteworthy methods of the SiteMapDataSource class:

| Table 6.12: Noteworthy Methods of the SiteMapDataSource Class |  |
|---|---|
| **Method** | **Description** |
| `GetList` | Gets a list of datasource controls that can be used as sources of lists of data |
| `GetView` | Gets a named view on the site map data of the site map provider according to the starting node and other properties of the datasource |
| `GetViewNames` | Gets a collection of named views for the datasource control |

Let’s learn how to use the SiteMapDataSource control in a Web application by performing the following steps:

+   1. *Click* **Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010.**
+   2. Select **File→New→Web Site** from the menu bar.
+      The New Web Site dialog box appears.
+   3. Select **Visual C#→ASP.NET Web Site** from the middle templates pane.
+   4. *Set* the name of the Web site as **SitemapdatasourceControl**.
+   5. Click the **OK** button.
+      The **SitemapdatasourceControl** application is created.
+   6. *Drag and drop* the **SiteMapDataSource** control on the **Default.aspx** page.
+   7. *Add* a **Web.sitemap** file in the application as done earlier (in chapter 3 of this section) and add the code, shown in Listing 6.3, in it:

**Listing 6.3:** Showing the Code for the Web.sitemap File

```
```xml
<siteMapNode url="" title="My Favourite" description="Favourite">
    <siteMapNode url="" title="Books" description="" />
    <siteMapNode url="" title="C#" description="" />
</siteMapNode>
```
```