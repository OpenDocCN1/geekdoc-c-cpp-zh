
Additionally, you see that the numerous child elements of the table (table rows and anchor elements) all have different style settings applied. For example, odd and even rows now have the following style applied:

```
<tr style="background-color:#EFF3FB;"> ... </tr>
<tr style="background-color:White;"> ... </tr>
```

Close the source document and click the headers of the GridView a few times. The header changes color to indicate the column is now sorted.

## How It Works

The different style elements you created in step 5 are converted into their CSS and HTML equivalents. For example, RowStyle and AlternatingRowStyle have their BackColor set to a different background color:

```
<RowStyle BackColor="#EFF3FB" />
<AlternatingRowStyle BackColor="White" />
```

When the control renders its HTML, it applies these backgrounds to the table row of the items and alternating items:

```
<tr style="background-color:#EFF3FB;"> ... </tr>
<tr style="background-color:White;"> ... </tr>
```

The same principle is applied to the other styles in the GridView.

If you look at the source of the page in the browser, you see a lot of page bloat, because each individual row has its properties set. This increases the page size, especially with larger results displayed in the GridView. To decrease the page size and improve the performance of the page, you could move the style definitions to a page theme and then use CSS and jQuery instead. You see how to do this next.

## Combining Styles, Themes, and Skins

Chapter 6 discussed how to create consistent-looking web pages using master pages, themes, and skins. With the basic theme infrastructure set up, it's now easy to add a new theme that applies to the entire Management section. Earlier you saw how to create a skin file to change the appearance of a button; in the following exercise you see how to reuse this concept to create a skin file for the GridView, enabling you to style all GridView controls in the Management folder in one fell swoop.

## TRY IT OUT  Creating Advanced Style Solutions

In this Try It Out, you move the various Style properties from the Genres.aspx page into a separate .skin file. You also move the inline style information to a separate CSS file. You then use some jQuery to separate data and appearance of the page even further.

- 1. On the Solution Explorer, right-click the App_Themes folder, choose Add ▸ Add ASP.NET Folder ▸ Theme, and type Management as the new theme name.
- 2. Right-click this new folder and choose Add → Add New Item. Add a skin file called GridView.skin. You should end up with a Solution Explorer looking like Figure 15-5.

![](img/eadab2ccd79b253c01a3fdff2321202d_605_0.png)

FIGURE 15-5
- 3. Open the Genres.aspx page in Markup View and delete all the style elements you created in the previous exercise except the HeaderStyle, the PagerStyle, the SortedAscendingHeaderStyle, and the SortedDescendingHeaderStyle. From the four remaining styles, remove all attributes and replace them with a single CssClass attribute named after the style and prefixed with GridView. You should end up with the following styles:

```
<HeaderStyle CssClass="GridViewHeaderStyle" />
<PagerStyle CssClass="GridViewPagerStyle" />
<SortedAscendingHeaderStyle CssClass="GridViewSortedAscendingHeaderStyle" />
<SortedDescendingHeaderStyle CssClass="GridViewSortedDescendingHeaderStyle" />
```

Don't worry if VS adds red error lines under the CSS class names. Because the CSS classes aren't defined yet, it can't find them. Later, you add them to the theme's CSS file, where VS still can't find them. They'll work fine at run time, though, so don't worry.
- 4. Select the styles in the code editor and then cut them to the clipboard using Ctrl+X. Switch to the GridView.skin file, delete all existing code (the comment text you saw earlier), and paste the styles into the skin file.
- 5. Wrap the styles in an <asp:GridView> element with its runat attribute set to server and its CssClass attribute set to GridView. Don't add an ID attribute, because skin files don't need this. You should end up with this code:

```
<asp:GridView runat="server" CssClass="GridView">
  styles go here
</asp:GridView>
```

- 6. Open the resources folder for this chapter (located at C:\BegASPNET\Resources\Chapter 15 if you followed the instructions in the Introduction section of this book) in File Explorer (Windows Explorer in Windows 7), select the Images folder and the Management.css file, and press Ctrl+C to copy them. Switch back to VS, click the Management folder under App_Themes, and press Ctrl+V. Just as the two other themes do, the management theme now has its own style sheet and Images folder, shown in Figure 15-6.

![](img/eadab2ccd79b253c01a3fdff2321202d_605_1.png)

FIGURE 15-6

The two images are used to change the header for sorted columns in the GridView, as you will see later.
- 7. Open the Web.config file for the Management folder in the root that you added earlier and set the theme to Management:

```
<system.web>
  <pages theme="Management" />
</system.web>
```

- 8. Open the Management.master file from the MasterPages folder, switch to Markup View, and below the ContentPlaceHolder in the <head> section of the page, drag the jquery-1.7.2.min.js file from the Scripts folder. VS inserts the following <script> element for you:

```
<asp:ContentPlaceHolder>
<script src="../Scripts/jquery-1.7.2.min.js"></script>
</head>
```

- 9. Go back to Genres.aspx and in Markup View, under the Columns element of the GridView control, delete the bound field for the Id column. Users typically don't need to see the IDs of items in the user interface because they are often meaningless to them. By removing the Id column, you reduce the noise in the page. Set the ItemStyle-Width for the CommandField to 100px and for the Name column to 200px. Finally, set ShowSelectButton of the CommandField to False, and set the HeaderText of the SortOrder field to Sort Order with a space between the words. You should end up with this GridView:

```
<asp:GridView ID="GridView1" runat="server" AllowPaging="True" AllowSorting="True" AutoGenerateColumns="False" DataKeyNames="Id" DataSourceID="SqlDataSource1" GridLines="None" CellPadding="4" ForeColor="#333333" EmptyDataText="There are no data records to display.">
  <Columns>
    <asp:CommandField ShowDeleteButton="True" ShowEditButton="True" ShowSelectButton="False" ItemStyle-Width="100px" />
    <asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" ItemStyle-Width="200px" />
    <asp:BoundField DataField="SortOrder" HeaderText="Sort Order" SortExpression="SortOrder"></asp:BoundField>
  </Columns>
</asp:GridView>
```

- 10. Scroll down to the end of the page in Markup View and, right before the closing </asp:Content> tag, add the following jQuery code wrapped in a <script> block:

```
<script type="text/javascript">
$(function()
{
  $('.GridView tr:odd:not(.GridViewPagerStyle)').addClass('GridViewAlternatingRowStyle');
});
</script>
```

- 11. Save all your changes by pressing Ctrl+Shift+S and then open Genres.aspx in the browser. You should now see the list of genres that was presented in Figure 15-2, except for the disabled Delete links, which you add later. Click the header of the Name or Sort Order columns to order the data in the GridView. Notice how the GridView now shows a little glyph beside the name to indicate the sort direction.
- 12. Click Manage Reviews in the main Management menu to open the Reviews page. Select a genre from the drop-down list to display a list of reviews. Note that the Reviews list — visible in Figure 15-7 — now also has the same styles applied as the Genres list you saw earlier, except for the alternating row styles applied by jQuery.

## The ASP.NET Page and Control Life Cycles Revisited

In Chapter 6 you learned about the stages in a page's life. You learned about different events such as `PreInit`, `Load`, `PreRender`, and `Unload`. Besides these events that are raised by the ASPX page, all the other controls in your ASPX pages can raise their own events. These events can be as simple as a Button control's `Click` event (triggered by a user action) or be more complex events, such as `Inserting`, which is raised by controls like the `EntityDataSource` and the `SqlDataSource`, or the `DataBound` event that is raised by various data-bound controls. You see many of these events in the next exercise.

## TRY IT OUT   Seeing the Page and Control Life Cycles at Work

To give you an idea of the different events that you can hook into during a page or control's life cycle and the order in which they fire, this Try It Out shows you how to set up a page that displays some data from the `Genres` table using an `EntityDataSource`. You also add a button to the page that you can use to trigger a postback to see how influences things. You then hook up a number of event handlers to a few interesting events of the controls on the page so you can see in what order things are called. You can apply the concepts you learn in this exercise to any other page or control that raises events to get a better understanding of how they operate.

- 1. Inside the `Demos` folder, create a new file called `Events.aspx`. Make sure it's based on your custom page template so it inherits from `BasePage`. Set the page's `Title` to `Events Demo`.
- 2. Switch the page to Design View, drop a `GridView` into the `cpMainContent` placeholder, and then hook it up to a new `EntityDataSource` control using the `GridView`'s Smart Tasks panel. Use `PlanetWroxEntities` as the Named Connection and bind the `EntityDataSource` control to the `Genres` entity set. There's no need to set up insert, update, or delete behavior, nor do you need to select specific columns or add a `Where` clause.
- 3. Back on the `GridView` control's Smart Tasks panel, click Refresh Schema if the `GridView` doesn't show the columns for the `Id`, `Name`, and `SortOrder`. Then enable sorting by selecting the second check box. When you're done, your code should look like this:

```
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataKeyNames="Id" DataSourceID="EntityDataSource1" AllowSorting="True">
  <Columns>
    <asp:BoundField DataField="Id" HeaderText="Id" ReadOnly="True" SortExpression="Id" />
    <asp:BoundField DataField="Name" HeaderText="Name" SortExpression="Name" />
    <asp:BoundField DataField="SortOrder" HeaderText="SortOrder" SortExpression="SortOrder" />
  </Columns>
</asp:GridView>
<asp:EntityDataSource ID="EntityDataSource1" runat="server" EntitySetName="Genres" ConnectionString="name=PlanetWroxEntities" EnableFlattening="False" DefaultContainerName="PlanetWroxEntities">
</asp:EntityDataSource>
```
