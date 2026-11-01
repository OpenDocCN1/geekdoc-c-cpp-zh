![](bbox=[0.1, 0.15, 0.78, 0.58])

FIGURE 1.13 GridView page with dynamic field columns.

Similar to DynamicControl, DynamicField uses column metadata to automatically select and load an appropriate field template. In other words, pages built with FormView, DetailsView, and GridView controls can reuse the same set of field templates.

Like the DynamicEntity control, which allows you to build a data entry form that includes all columns of a particular table, Dynamic Data offers a similar capability for grid columns. In Listing 1.14, the explicit definitions of fields for ProductName and UnitsInStock have been removed. Instead, the AutoGenerateColumns property of the GridView control is set to true.

# LISTING 1.14 DefaultAutoFieldGenerator Sample (Markup)

```
<%@ Page Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch01.FieldGenerator.SamplePage" %>

<asp:Content ContentPlaceHolderID="main" runat="server">
    <asp:ValidationSummary ID="ValidationSummary1" runat="server" />
    <asp:GridView ID="gridView" runat="server" DataSourceID="dataSource"
DataKeyNames="ProductID" AutoGenerateEditButton="true"
AllowPaging="true" AutoGenerateColumns="true" />
    <asp:EntityDataSource ID="dataSource" runat="server"
ConnectionString="name=NorthwindEntities" EnableUpdate="true"
DefaultContainerName="NorthwindEntities" EntitySetName="Products" />
</asp:Content>
```