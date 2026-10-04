# Data Source Configuration Wizard

![](bbox=[0.118, 0.99, 0.831, 0.517])

FIGURE 13-9 to close the dialog box and finishing up the data source for the drop-down list.

+   9. Click OK to close the dialog box and finishing up the data source for the drop-down list.
10. With theDownList control still selected in Design View, Press F4 to open up its Properties grid and set the property AppendDataBoundItems to True. To switch to Markup View, and if the static ListItem instructs your users to select an item does not have a Value attribute, add it manually and set it to an empty string. Your final code should look like this:

```
<asp:DropDownList ID="DropDownList1" runat="server" DataSourceID="SqlDataSource1"
DataTextField="Name" DataValueField="Id" AppendDataBoundItems="true"
AutoPostBack="True">
<asp:ListItem Value="--">Make a selection:--</asp:ListItem>
</asp:DropDownList>

<asp:SqlDataSource ID="SqlDataSource1" runat="server"
ConnectionString="{ConnectionStrings:PlanetWroxConnectionString}"
SelectCommand="SELECT [Id], [Name] FROM [Genre] ORDER BY [SortOrder]" />
```

+   11. Save all your changes and press Ctrl+F to open the page in the browser. Now you should see a drop-down list with all the genres in the database ordered by their SortOrder column. once you choose a new genre from the list, the page posts back to server. Nothing else happens because you didn't tie any logic to the DropDownList control, but you see how to do this in the next exercise.