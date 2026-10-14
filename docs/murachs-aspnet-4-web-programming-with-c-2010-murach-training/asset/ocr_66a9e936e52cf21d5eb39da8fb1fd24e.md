# A simple list displayed by a DataList control

+   - Austin Powers $79.99
+   - Frankenstein $39.99
+   - Hippie $79.99
+   - JarJar $59.99
+   - Martian $69.99
+   - Superman $39.99

# The aspx code for the DataList control

```
<asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource2">
    <ItemTemplate>
        <asp:Label ID="lblName" runat="server"
            Text='<%# Eval("Name") %>'></asp:Label>
        <asp:Label ID="lblUnitPrice" runat="server"
            Text='<%# Eval("UnitPrice", "{0:C}") %>'></asp:Label>
    </ItemTemplate>
</asp:DataList>
```

# Basic attributes of the DataList control

| Attribute | Description |
|---|---|
| ID | The ID for the DataList control. |
| Runat | Must specify "server." |
| DataSourceID | The ID of the data source to bind the data list to. |

# Description

+   - A *data list* displays a list of items from the data source that it’s bound to. To bind a data list to a data source, use the Choose Data Source command in the control’s smart tag menu.
+   - To define the information to be displayed in a data list, you create one or more *templates*. Visual Studio provides a designer interface you can use to create the templates as shown in the next figure.
+   - To display the data from a column in the data source in a data list, you add a control to a template and then bind that control. See figure 13-14 for more information.
+   - You can use a DataList control for edit operations as well as display operations. However, you’re more likely to use the GridView, DetailsView, FormView, and ListView controls for edit operations.