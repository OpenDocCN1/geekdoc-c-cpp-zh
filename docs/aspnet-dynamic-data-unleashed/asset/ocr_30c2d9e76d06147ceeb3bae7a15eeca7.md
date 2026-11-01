![](bbox=[0.15, 0.12, 0.92, 0.62])

# FIGURE 6.5 Prefiltered List page.

The List page template is implemented in List.aspx, located in the DynamicData/PageTemplates folder of the web application. Listing 6.5 shows the markup of the built-in template after some cleanup to improve readability and highlight important sections in bold.

The structure of the List page template is actually quite similar to the structure of the Details page template. It also includes DynamicDataManager, EntityDataSource, and QueryExtender controls. The only significant differences are the GridView control, which this template uses to display entities, and the QueryableFilterRepeater used to generate the filter controls.

# LISTING 6.5 List Page Template (Markup)

```
```aspx
<%@ Page Language="C#" MasterPageFile="~/Site.master" CodeBehind="List.aspx.cs" Inherits="WebApplication.DynamicData.PageTemplates.List" %>
<%@ Register Src="~/DynamicData/Controls/GridViewPager.ascx" TagName="GridViewPager" TagPrefix="dd" %>
<asp:Content ContentPlaceHolderID="main" runat="Server">
    <asp:DynamicDataManager runat="server">
        <DataControls>
            <asp:DataControlReference ControlID="gridview" />
        </DataControls>
    </asp:DynamicDataManager>
```
```