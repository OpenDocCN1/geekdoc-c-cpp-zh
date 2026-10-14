# A Master/Detail page typically contains:

+   - A control that lets the user choose an item to display, such as a drop-down list or a GridView control.
+   - A data source that retrieves all of the items to be displayed in the list. The control that contains the list of data items should be bound to this data source.
+   - A DetailsView control that displays data for the item selected by the user.
+   - A data source that retrieves the data for the item selected by the user. The DetailsView control should be bound to this data source. To retrieve the selected item, this data source can use a parameter that’s bound to the SelectedValue property of the control that contains the list of data items.

# A SqlDataSource control with a parameter that’s bound to a drop-down list

```
<asp:SqlDataSource ID="SqlDataSource2" runat="server"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnection %>"
    SelectCommand="SELECT [ProductID], [Name], [ShortDescription], [LongDescription], [CategoryID], [ImageFile], [UnitPrice], [OnHand] FROM [Products] WHERE ([ProductID] = @ProductID)">
    <SelectParameters>
        <asp:ControlParameter ControlID="ddlProducts" Name="ProductID" PropertyName="SelectedValue" Type="String" />
    </SelectParameters>
</asp:SqlDataSource>
```

# Description

+   - A Master/Detail page is a page that displays a list of items from a database along with the details of one item from the list. The DetailsView control is often used to display the details portion of a Master/Detail page.
+   - The list portion of a Master/Detail page can be displayed by any control that contains a list of data items, including a drop-down list or a GridView control.
+   - A Master/Detail page usually includes two data sources, one for the master list and the other for the DetailsView control.