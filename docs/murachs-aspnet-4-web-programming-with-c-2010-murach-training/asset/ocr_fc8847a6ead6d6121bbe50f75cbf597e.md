# The EditItem template for the ListView control in figure 16-1

```
```aspx
<EditItemTemplate>
    <tr style="">
        <td>
            <asp:Button ID="UpdateButton" runat="server"
                CommandName="Update" Text="Update" />
            <asp:Button ID="CancelButton" runat="server"
                CommandName="Cancel" Text="Cancel" /></td>
        <td>
            <asp:Label ID="CategoryIDLabel1" runat="server"
                Text='<%# Eval("CategoryID") %>' /></td>
        <td>
            <asp:TextBox ID="ShortNameTextBox" runat="server"
                Text='<%# Bind("ShortName") %>' /></td>
        <td>
            <asp:TextBox ID="LongNameTextBox" runat="server"
                Text='<%# Bind("LongName") %>' /></td>
    </tr>
</EditItemTemplate>
```
```

# The InsertItem template for the ListView control in figure 16-1

```
```aspx
<InsertItemTemplate>
    <tr style="">
        <td>
            <asp:Button ID="InsertButton" runat="server"
                CommandName="Insert" Text="Insert" />
            <asp:Button ID="CancelButton" runat="server"
                CommandName="Cancel" Text="Clear" /></td>
        <td>
            <asp:TextBox ID="CategoryIDTextBox" runat="server"
                Text='<%# Bind("CategoryID") %>' /></td>
        <td>
            <asp:TextBox ID="ShortNameTextBox" runat="server"
                Text='<%# Bind("ShortName") %>' /></td>
        <td>
            <asp:TextBox ID="LongNameTextBox" runat="server"
                Text='<%# Bind("LongName") %>' /></td>
    </tr>
</InsertItemTemplate>
```
```

# Description

+   - The EditItem template determines how an item in the ListView control is rendered in edit mode. By default, it includes a label for each column in the data source that can’t be modified and a text box for each column in the data source that can be modified. These controls are bound to the columns of the data source using the Eval and Bind methods.
+   - The InsertItem template is similar to the EditItem template. It determines the content that’s rendered for a new item that’s being inserted.
+   - The EditItem template also includes update and cancel buttons by default, and the InsertItem template includes insert and cancel buttons.

Figure 16-14  How to work with the EditItem and InsertItem templates