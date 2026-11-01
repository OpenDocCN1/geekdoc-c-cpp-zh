
Click Next to go to the Configure Data Selection screen, shown in Figure 14-11. From the EntitySetName drop-down list, choose PhotoAlbums.

![](img/eadab2ccd79b253c01a3fdff2321202d_566_0.png)

FIGURE 14-11

- 7. For this exercise, you need insert behavior, so check off the Enable Automatic Inserts check box. Click Finish to close the Configure Data Source wizard.

- 8. If you don’t see the Id and Name columns in the DetailsView, but a general Databound Column instead, click the Refresh Schema link on the control’s Smart Tasks panel. Enable inserting for the DetailsView control by checking the Enable Inserting item on the same Smart Tasks panel.

- 9. Open the DetailsView control’s Properties Grid and change the DefaultMode from ReadOnly to Insert.

- 10. Switch to Markup View, locate the BoundField for the Id property of the PhotoAlbum, and set its InsertVisible property to false so you don’t get a text box for the ID when inserting a new photo album.

```
<asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" InsertVisible="false" />
```

- 11. Select the EntityDataSource control in Design View, open its Properties Grid, and switch to the Events tab. Double-click the Inserted event, visible in Figure 14-12.

all the available templates that you can add as direct children of the ListView control in the markup of the page.

| TEMPLATE | DESCRIPTION |
|---|---|
| `<LayoutTemplate>` | Serves as a container. It enables you to define a location where the individual data items are placed. The data items, presented through the `ItemTemplate` and `AlternatingItemTemplate`, are then added as children of this container. |
| `<ItemTemplate>`<br>`<AlternatingItemTemplate>` | Define the read-only mode for the control. When used together, they enable you to create a "zebra effect," where odd and even rows have a different appearance (usually a different background color). |
| `<SelectedItemTemplate>` | Enables you to define the look and feel of the currently active, or selected, item. |
| `<InsertItemTemplate>`<br>`<EditItemTemplate>` | These two templates enable you to define the user interface for inserting and updating items in the list. You typically place controls like text boxes, drop-down lists, and other server controls in these templates and bind them to the underlying data source. |
| `<ItemSeparatorTemplate>` | Defines the markup that is placed between the items in the list. Useful if you want to add a line, an image, or any other markup between the items. |
| `<EmptyDataTemplate>` | Displayed when the control has no data to display. You can add text or other markup and controls to it to tell your users there's no data to display. |
| `<GroupTemplate>`<br>`<GroupSeparatorTemplate>`<br>`<EmptyItemTemplate>` | Used in advanced presentation scenarios where data can be presented in different groups. |

Although this long list of templates seems to suggest you need to write a lot of code to work with the ListView, this is not always the case. First of all, VS creates most of the code for you based on the data that is exposed by controls such as the EntityDataSource. Secondly, you don't always need all templates, enabling you to minimize the code for the control.

Besides the numerous templates, the control has the following properties that you typically set to influence its behavior.

| PROPERTY | DESCRIPTION |
|---|---|
| `ItemPlaceholderID` | The ID of a server-side control placed within the LayoutTemplate. The control referred to by this property is replaced by all the repeated data items when the control is displayed on-screen. It can be a true server control like an `<asp:PlaceHolder>` or a simple HTML element with a valid ID and its runat attribute set to server (for example, `<ul runat="server" id="MainList"></ul>`). If you don't set this property, ASP.NET tries to find a control with an ID of itemPlaceholder and uses that control instead. |
| `DataSourceID` | The ID of a data source control on the page, such as an EntityDataSource or a SqlDataSource control. |
| `InsertItemPosition` | The enumeration for this property contains three property values — None, FirstItem, and LastItem — to determine the position of the InsertItemTemplate: either at the beginning or end of the list, or not visible at all. |

Just like the other data-bound controls, the ListView has a number of events that fire at specific moments during the control's lifetime. For example, it has ItemInserting and ItemInserted events that fire right before and after an item has been inserted in the underlying data source. Similarly, it has events that trigger right before and after you update or delete data. You see more about handling these kinds of events in the next chapter.

Besides the templates, properties, and events you just saw, the ListView has more to offer. For a detailed explanation of the ListView control and all of its members and behavior, check out the MSDN documentation at http://bit.ly/dCAooK.

The next exercise shows you how to put all of this information together. You see how to define the various templates and set the relevant properties to control the look and feel of the ListView control.

## TRY IT OUT  Inserting and Deleting Data with the ListView Control

Inserting items with the ListView can be just as easy as with the DetailsView: You point the control to a data source and let VS create the necessary templates for you. However, in many real-world web sites, these default templates won't cut it. You may want to display fewer fields than are available in the data source, validate data before it gets sent to the database, or store data at a different location than the database. For example, you may want to store uploaded images on disk rather than in the database and then store only a reference to the file in the database table. The next exercise shows you how to customize the ListView templates and handle the Inserting event of the EntityDataSource when you build functionality to add pictures to your photo albums.

This exercise has you work with a lot of code that is generated automatically by VS. Most of what you need to do in this exercise is remove code instead of add new code. If you get lost somewhere, or you feel your code does not look like it should, remember this chapter comes with the full source code that you can download from the Wrox website, so you can compare your code with mine.

- 1. In the root of the website, create a new Web Form based on your custom template. Call it `ManagePhotoAlbum.aspx`, set its `Title` to `Manage Photo Album`, and switch it into Design View.

- 2. From the Data category of the Toolbox, drag a `ListView` control onto the page in the `cpMainContent` placeholder and then hook it up to an `EntityDataSource` control by choosing `<New data source>` in the Choose Data Source drop-down list on the Smart Tasks panel (just as you did with the `DetailsView` earlier). Click the Entity icon, click OK, choose `PlanetWroxEntities` as the named connection, and click Next.

    In the Configure Data Selection dialog box of the `EntityDataSource` control's wizard, visible in Figure 14-11, choose `Pictures` from the EntitySetName drop-down list.

- 3. Check the first and the last check box of the three at the bottom of the screen to give the `EntityDataSource` insert and delete support. Finally, click Finish to close the Configure Data Source wizard.

- 4. Back in Design View, select the `EntityDataSource` control, open its Properties Grid, locate the `Where` property, and open its Expression Editor by clicking the ellipsis for that property. You may recall that the `ManagePhotoAlbum.aspx` page receives the photo album ID through the query string, so you'll need to set up a `QueryStringParameter` in this step to filter the `ListView` to those pictures belonging to the designated photo album. To do this, enter `it.PhotoAlbum.Id = @photoAlbumId` in the Where Expression box at the top of the dialog box. Then click Add Parameter, enter `PhotoAlbumId` as the name, choose QueryString from the Parameter Source drop-down, and enter `PhotoAlbumId` as the QueryStringField. Next, click the Show Advanced Properties link and change the Type property of the parameter to `Int32`. Your dialog box should now look like Figure 14-13. When you're done, click OK to dismiss the dialog box.

![](img/eadab2ccd79b253c01a3fdff2321202d_572_0.png)

FIGURE 14-13
