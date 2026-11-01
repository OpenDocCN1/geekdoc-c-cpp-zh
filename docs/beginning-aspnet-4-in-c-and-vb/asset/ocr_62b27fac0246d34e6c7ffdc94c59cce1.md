(continued)

| CONTROL | DESCRIPTION |
|---|---|
| Substitution | Specifies a section of a web page that isn't cached along with other output. This is an advanced topic related to ASP.NET caching behavior, which you won't be looking at in this book. |
| Localize | Exactly like Literal, but enables text to be localized by using project resources to specify the text to display for various locales. |

# Data Web Server Controls

The data web server controls are divided into three types:

+   - **Data source controls** (`SqlDataSource`, `AccessDataSource`, `LinqDataSource`, `EntityDataSource`, `ObjectDataSource`, `XmlDataSource`, and `SiteMapDataSource`)
+   - **Data display controls** (`GridView`, `DataList`, `DetailsView`, `FormView`, `ListView`, `Repeater`, and `DataPager`)
+   - **Dynamic data controls** (`DynamicControl` and `DynamicDataManager`)

In general, you will place one of the (nonvisual) data source controls on a page to link to a data source; and then you will add a data display control that binds to a data source control to display that data. Some of the more advanced data display controls, such as GridView, also allow you to edit data.

All the data source controls derive from either System.Web.UI.DataSource or System.Web.UI.HierarchicalDataSource. These classes expose methods such as GetView() or GetHierarchicalView() to give access to internal data views and skinning capabilities.

The following table describes the various data source controls. Note that there is less detail about properties in this section than in others — mainly because configuration of these controls is best done graphically or through wizards. Later in this chapter, you will see some of these controls in action.

| CONTROL | DESCRIPTION |
|---|---|
| SqlDataSource | Acts as a conduit for data stored in a SQL Server database. By placing this control on a page, you can manipulate SQL Server data using a data display control. You will see this control in action later in this chapter. |
| AccessDataSource | Like SqlDataSource, but it works with data stored in a Microsoft Access database. |
| LinqDataSource | This control allows you to manipulate objects in a LINQ-enabled data model. |
| EntityDataSource | This control allows you to manipulate ADO.NET Entity Data Model objects. |
| ObjectDataSource | This control allows you to manipulate data stored in objects that you have created, which may be grouped in a collection class. This can be a very quick way to expose custom object models to an ASP.NET page. |
| XmlDataSource | Enables you to bind to XML data. This works well in binding to for, example, a TreeView control (one of the Navigation controls). You can also transform XML data using an XSL style sheet using this control if desired. |
| SiteMapDataSource | Allows binding to hierarchical site map data. See the section on navigation web server controls in Chapter 41 for more information. |

The following table displays the data display controls. Several of these are available to suit various needs. Some are more fully functional than others, but often you can go with simplicity (for example, when you don't need to be able to edit data items).