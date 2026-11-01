# LISTING 4.13 Continued

```
<tr><td>
<asp:LinkButton runat="server" CommandName="Insert" Text="Insert" />
</td></tr>
</InsertItemTemplate>
<EditItemTemplate>
<asp:DynamicEntity runat="server" Mode="Edit" />
<tr><td>
<asp:LinkButton runat="server" CommandName="Update" Text="Update" />
</td></tr>
</EditItemTemplate>
</asp:FormView>
<asp:EntityDataSource ID="dataSource" runat="server"
EnableInsert="true" EnableUpdate="true"
ConnectionString="name=NorthwindEntities" AutoGenerateWhereClause="true"
DefaultContainerName="NorthwindEntities" EntitySetName="Customers">
<WhereParameters>
<asp:QueryStringParameter QueryStringField="ID" Name="CustomerID" />
</WhereParameters>
</asp:EntityDataSource>
</asp:Content>
```

Similar to field templates, Dynamic Data uses the last part of the template file name to determine its mode. For the Customer page, you might need to have the following three templates in the DynamicData\EntityTemplates folder of the web application:

+   - Customers.ascx, the read-only template
+   - Customers_Edit.ascx, the edit template
+   - Customers_Insert.ascx, the insert template

Creating the Customers_Edit and Customers_Insert entity templates is straightforward; they are nearly identical to the Read-only Customers template (see Listing 4.3) except that the Mode property of the DynamicControl instances is set to Edit and Insert respectively. Listing 4.14 shows the Edit mode template for the Customer entity.

# LISTING 4.14 Customers_Edit Entity Template (Markup)

```
<%@ Control Language="C#" CodeBehind="Customers_Edit.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.CustomerEditEntityTemplate" %>

<label>ID:</label>
<asp:DynamicControl runat="server" DataField="CustomerID" Mode="Edit"/>
<label>Name:</label>
<asp:DynamicControl runat="server" DataField="contactName" Mode="Edit"/>
<fieldset><legend>Address</legend>
```