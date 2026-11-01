version of the Customer entity templates, and you can solve it using the exact same approach. Listing 10.4 shows the markup of the dynamic Edit mode template.

# LISTING 10.4 Edit-Mode Dynamic Entity Template (Markup)

```
<%@ Control Language="C#" CodeBehind="Default_Edit.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.DefaultEditEntityTemplate" %>
<table class="DDDetailsTable">
<asp:EntityTemplate runat="server" ID="entityTemplate">
<ItemTemplate>
<tr>
<td class="DDLightHeader">
<asp:Label runat="server" OnInit="Label_Init" OnPreRender="Label_PreRender"/>
</td>
<td>
<asp:DynamicControl runat="server" ID="DynamicControl" Mode="Edit" OnInit="DynamicControl_Init" />
</td>
</tr>
</ItemTemplate>
</asp:EntityTemplate>
</table>
```

As you can see, the Default_Edit entity template hardcodes the Edit value for the Mode property of the DynamicControl instances. The Default_Insert entity template hardcodes the Insert value, and the Default (Read-only) template leaves the default, ReadOnly value. Aside from this, there are no other significant differences between the three dynamic templates, and you can replace them with the single multimode template shown in Listing 10.5.

# LISTING 10.5 Multimode Dynamic Entity Template (Markup)

```
<%@ Control Language="C#" CodeBehind="Default.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.DefaultEntityTemplate" %>
<table class="DDDetailsTable">
<asp:EntityTemplate runat="server" ID="entityTemplate">
<ItemTemplate>
<tr>
<td class="DDLightHeader">
<asp:Label runat="server" OnInit="Label_Init" OnPreRender="Label_PreRender" />
</td>
<td>
<asp:DynamicControl runat="server" ID="dynamicControl"
```