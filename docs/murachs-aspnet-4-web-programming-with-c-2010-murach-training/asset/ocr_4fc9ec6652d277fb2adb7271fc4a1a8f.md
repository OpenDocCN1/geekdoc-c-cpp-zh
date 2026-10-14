# The Item template generated for a FormView control

```
```aspx
<asp:FormView ID="FormView1" runat="server" DataKeyNames="ProductID"
    DataSourceID="SqlDataSource2">
    <ItemTemplate>
        ProductID:
            <asp:Label ID="ProductIDLabel" runat="server"
                Text='<%# Eval("ProductID") %>' /><br />
        Name:
            <asp:Label ID="NameLabel" runat="server"
                Text='<%# Bind("Name") %>' /><br />
        ShortDescription:
            <asp:Label ID="ShortDescriptionLabel" runat="server"
                Text='<%# Bind("ShortDescription") %>' /><br />
        LongDescription:
            <asp:Label ID="LongDescriptionLabel" runat="server"
                Text='<%# Bind("LongDescription") %>' /><br />
        CategoryID:
            <asp:Label ID="CategoryIDLabel" runat="server"
                Text='<%# Bind("CategoryID") %>' /><br />
        ImageFile:
            <asp:Label ID="ImageFileLabel" runat="server"
                Text='<%# Bind("ImageFile") %>' /><br />
        UnitPrice:
            <asp:Label ID="UnitPriceLabel" runat="server"
                Text='<%# Bind("UnitPrice") %>' /><br />
        OnHand:
            <asp:Label ID="OnHandLabel" runat="server"
                Text='<%# Bind("OnHand") %>' /><br />
    </ItemTemplate>
    .
    .
    .
</asp:FormView>
```
```

# Description

+   - When you bind a FormView control to a data source, the Web Forms Designer generates an Item template that includes heading text and a bound label for each column in the data source.
+   - The Item template is rendered whenever the FormView control is displayed in ReadOnly mode.
+   - The Item template uses the Eval and Bind methods to create binding expressions for the columns in the data source (see figure 13-15 in chapter 13).
+   - If the data source includes Update, Delete, and Insert commands, the generated Item template will include Edit, Delete, and New buttons.
+   - The Web Forms Designer also generates an EditItem template and an InsertItem template, even if the data source doesn’t include an Update or Insert command. For more information, see the next figure.
+   - You can modify a generated template so you can use CSS to control the format and layout of the data that’s rendered for that template.

Figure 15-13 How to work with the Item template