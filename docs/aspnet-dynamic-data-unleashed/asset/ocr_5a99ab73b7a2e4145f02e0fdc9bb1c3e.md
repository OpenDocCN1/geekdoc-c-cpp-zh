```
<h2>Entry from table <%= ordersTable.DisplayName %></h2>
<asp:FormView runat="server" ID="formView" DataSourceID="formDataSource">
    <ItemTemplate>
        <asp:DynamicEntity runat="server" />
        <div class="DFormActions">
            <asp:DynamicHyperLink runat="server" Action="Edit" Text="Edit" />
            <asp:DynamicHyperLink runat="server" Action="Delete" Text="Delete" />
            <asp:DynamicHyperLink runat="server" Action="List" Text="List" />
        </div>
    </ItemTemplate>
</asp:FormView>

<asp:EntityDataSource ID="formDataSource" runat="server"/>

<asp:QueryExtender TargetControlID="formDataSource" runat="server">
    <asp:DynamicRouteExpression />
</asp:QueryExtender>
</td>

<td>

<h2><%= itemsTable.DisplayName %></h2>
<asp:GridView ID="gridView" runat="server" DataSourceID="gridDataSource"
    AutogenerateColumns="false" AllowSorting="True">
    <Columns>
        <asp:DynamicField DataField="Product" />
        <asp:DynamicField DataField="UnitPrice" />
        <asp:DynamicField DataField="Quantity" />
        <asp:TemplateField>
            <ItemTemplate>
                <asp:DynamicHyperLink runat="server" Action="Edit" Text="Edit" />
                <asp:DynamicHyperLink runat="server" Action="Delete" Text="Delete" />
                <asp:DynamicHyperLink runat="server" Action="Details" Text="Details" />
            </ItemTemplate>
        </asp:TemplateField>
    </Columns>
</asp:GridView>

<asp:EntityDataSource ID="gridDataSource" runat="server"
    ConnectionString="name=NorthwindEntities"
    DefaultContainerName="NorthwindEntities"
    EntitySetName="Order_Details" Include="Product"
    OnSelected="GridDataSource_Selected" />
<asp:QueryExtender TargetControlID="gridDataSource" runat="server">
    <asp:DynamicRouteExpression />
</asp:QueryExtender>
```