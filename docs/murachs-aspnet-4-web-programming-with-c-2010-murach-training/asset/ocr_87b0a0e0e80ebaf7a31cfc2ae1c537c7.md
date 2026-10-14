# The Default.aspx file

```
<asp:GridView ID="GridView1" runat="server"
    AutoGenerateColumns="False" DataKeyNames="CategoryID"
    DataSourceID="SqlDataSource1" ForeColor="Black">
    <Columns>
        <asp:BoundField DataField="CategoryID" HeaderText="ID"
            ReadOnly="True" >
            <HeaderStyle HorizontalAlign="Left" />
            <ItemStyle Width="100px" />
        </asp:BoundField>

        <asp:TemplateField HeaderText="Short Name">
            <EditItemTemplate>
                <asp:TextBox ID="txtGridShortName" runat="server"
                    Width="125px" MaxLength="15"
                    Text='<%# Bind("ShortName") %>'>
                </asp:TextBox>
                <asp:RequiredFieldValidator
                    ID="RequiredFieldValidator4" runat="server"
                    ControlToValidate="txtGridShortName"
                    ErrorMessage="Short Name is a required field."
                    ForeColor="White"
                    ValidationGroup="Edit">*
                </asp:RequiredFieldValidator>
            </EditItemTemplate>
            <ItemTemplate>
                <asp:Label ID="lblGridShortName" runat="server"
                    Text='<%# Bind("ShortName") %>'>
                </asp:Label>
            </ItemTemplate>
            <HeaderStyle HorizontalAlign="Left" />
            <ItemStyle Width="150px" />
        </asp:TemplateField>
        <asp:TemplateField HeaderText="Long Name">
            <EditItemTemplate>
                <asp:TextBox ID="txtGridLongName" runat="server"
                    Width="180px" MaxLength="50"
                    Text='<%# Bind("LongName") %>'>
                </asp:TextBox>
                <asp:RequiredFieldValidator
                    ID="RequiredFieldValidator5" runat="server"
                    ControlToValidate="txtGridLongName"
                    ErrorMessage="Long Name is a required field."
                    ForeColor="White"
                    ValidationGroup="Edit">*
                </asp:RequiredFieldValidator>
            </EditItemTemplate>
            <ItemTemplate>
                <asp:Label ID="lblGridLongName" runat="server"
                    Text='<%# Bind("LongName") %>'>
                </asp:Label>
            </ItemTemplate>
            <HeaderStyle HorizontalAlign="Left" />
            <ItemStyle Width="200px" />
        </asp:TemplateField>
    </Columns>
</asp:GridView>
```

Figure 14-17  The aspx code for the template version of the Category Maintenance application (part 1 of 2)