# The Default.aspx file

```
<ItemTemplate>
    <div id="itemtemplate">
        <p class="name">
            <asp:Label ID="NameLabel" runat="server" Text='<%# Eval("Name") %>' />
        </p>
        <div class="info">
            <p class="label">Category:</p>
            <p class="control">
                <asp:Label ID="CategoryLabel" runat="server" Text='<%# Eval("Category") %>' />
            </p>
            <p class="label">Short Description:</p>
            <p class="control">
                <asp:Label ID="ShortDescriptionLabel" runat="server" Text='<%# Eval("ShortDescription") %>' />
            </p>
            <p class="label">Long Description:</p>
            <p class="control">
                <asp:Label ID="LongDescriptionLabel" runat="server" Text='<%# Eval("LongDescription") %>' />
            </p>
            <p class="label">Unit Price:</p>
            <p class="control">
                <asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice", "{0:c}") %>' />
            </p>
            <p class="label">On Hand:</p>
            <p class="control">
                <asp:Label ID="OnHandLabel" runat="server" Text='<%# Eval("OnHand") %>' />
            </p>
        </div>
    </div>
</ItemTemplate>
```