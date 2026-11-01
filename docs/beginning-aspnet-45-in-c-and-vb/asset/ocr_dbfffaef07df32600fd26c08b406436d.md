6. Click Next and then Finish to finalize the Configure Data Source wizard.

7. Select the new SqlDataSource (called SqlDataSource2) in Design View and change its ID to GenresDataSource using the Properties Grid so it's easier to recognize in the page.

8. Switch to Markup View, locate the InsertItemTemplate for the GenreId of the DetailsView, and remove its contents (the TextBox control). At the place where you removed the TextBox, add a DropDownList by dragging it from the Toolbox into Markup View. Your code looks like this:

```
<asp:TemplateField HeaderText="GenreId" SortExpression="GenreId">
    <asp:EditItemTemplate>
        <asp:TextBox ID="TextBox4" runat="server"
        Text='<%# Bind("GenreId") %>'></asp:TextBox>
    </asp:EditItemTemplate>
    <asp:InsertItemTemplate>
        <asp:DropDownList ID="DropDownList1" runat="server">
        </asp:DropDownList>
    </asp:InsertItemTemplate>
    ...
</asp:TemplateField>
```

9. Switch to Design View, right-click the DetailsView, and choose Edit Template ▸ Field[4] - GenreId, as shown in Figure 13-20. If you don't see this menu item, you may need to click one of the rows with controls—such as the summary row—first to put the focus on the DetailsView correctly.

![](bbox=[0.12, 0.66, 0.7, 0.88])

FIGURE 13-20