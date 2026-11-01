

![](img/11b373b78859e17d318fd76939a0df9d_143_0.png)

## 图 4.3 由动态实体模板生成的供应商信息页面

清单 4.10 展示了动态实体模板的标记。

## 清单 4.10 默认实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Default.ascx.cs"
Inherits="WebApplication.DynamicData.EntityTemplates.DefaultEntityTemplate" %>

<asp:EntityTemplate runat="server" ID="entityTemplate">
    <ItemTemplate>
        <tr>
            <td><asp:Label runat="server" OnInit="Label_Init" /></td>
            <td><asp:DynamicControl runat="server" OnInit="DynamicControl_Init" /></td>
        </tr>
    </ItemTemplate>
</asp:EntityTemplate>
```

动态实体模板利用了 Dynamic Data 提供的元数据信息，包括已注册数据模型中每个表的所有列的列表。此标记中使用的 EntityTemplate 控件是一个轻量级模板化控件，类似于 ASP.NET 的 Repeater。清单 4.11 中显示的 OnLoad 方法使用它以编程方式为每个实体列创建一个 Label 和一个 DynamicControl。由于所有列都使用同一个模板，DynamicControl 的 DataField 属性和 Label 的 Text 属性在各自的 OnInit 事件处理程序中以编程方式初始化。

## 清单 4.11 默认实体模板（代码隐藏）

```
using System;
using System.Collections.Generic;
using System.Web.DynamicData;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.EntityTemplates
{
    public partial class DefaultEntityTemplate : EntityTemplateUserControl
    {
        private MetaColumn currentColumn;

        protected override void OnLoad(EventArgs e)
        {
            IEnumerable<MetaColumn> scaffoldColumns = this.Table.GetScaffoldColumns(
                this.Mode, this.ContainerType);
            foreach (MetaColumn column in scaffoldColumns)
            {
                this.currentColumn = column;
                NamingContainer container = new NamingContainer();
                this.entityTemplate.ItemTemplate.InstantiateIn(container);
                this.entityTemplate.Controls.Add(container);
            }
        }

        protected void Label_Init(object sender, EventArgs e)
        {
            ((Label)sender).Text = this.currentColumn.DisplayName;
        }

        protected void DynamicControl_Init(object sender, EventArgs e)
        {
            ((DynamicControl)sender).DataField = this.currentColumn.Name;
        }
    }
}
```

## 注意

注意，NamingContainer 是一个自定义控件，直接继承自内置的 Control，并实现 INamingContainer 标记接口。ASP.NET 运行时依赖该接口来确定命名边界，并生成在整个页面中唯一的控件 ID。

显示在由实体模板动态生成的 Label 控件中，并在报告验证错误时显示在 ValidationSummary 控件中。清单 4.12 中的 Supplier 示例为 ContactName、ContactTitle、CompanyName 以及其他几个列指定了显示名称。

您可以通过将 DisplayAttribute 的 AutoGenerateField 属性设置为 false，完全阻止显示特定列。或者，要达到相同的结果，可以将 ScaffoldColumnAttribute 应用于实体属性，并将其 Scaffold 属性值指定为 false。清单 4.12（Supplier 示例）展示了如何使用此方法隐藏 HomePage 列。

> **注意**
> ScaffoldColumnAttribute 是在 ASP.NET Dynamic Data 的第一个版本中引入的，该版本作为 .NET Framework 3.5 Service Pack 1 的一部分发布。DisplayAttribute 是在第二个版本（随 .NET Framework 4 发布）中引入的，同时保留了 ScaffoldColumnAttribute 以实现向后兼容。

## 清单 4.12 Supplier 元数据特性

```
using System.ComponentModel.DataAnnotations;

namespace DataModel
{
    [MetadataType(typeof(Supplier.Metadata))]
    partial class Supplier
    {
        public class Metadata
        {
            [Display(Name = "Name", Order = 1)]
            public object ContactName { get; set; }

            [Display(Name = "Title", Order = 2)]
            public object ContactTitle { get; set; }

            [Display(Name = "Company", Order = 3)]
            public object CompanyName { get; set; }

            [Display(Order = 4)]
            public object Phone { get; set; }

            [Display(Order = 5)]
            public object Fax { get; set; }

            [Display(Name = "Street")]
            public object Address { get; set; }

            [Display(Name = "State")]
            public object Region { get; set; }

            [Display(Name = "Zip")]
            public object PostalCode { get; set; }

            [ScaffoldColumn(false)]
            public object HomePage { get; set; }
        }
    }
}
```

## 编辑和插入实体模板

除了迄今已讨论的只读实体模板外，Dynamic Data 还支持 Edit 和 Insert 模式的实体模板。考虑清单 4.13 中的 FormView 控件，除了前面使用的只读 ItemTemplate 之外，它还定义了 EditItemTemplate 和 InsertItemTemplate 部分。这三个部分都使用 DynamicEntity 控件，根据与 FormView 关联的 MetaTable 和 Mode 属性（可以是 Insert、Edit 或 ReadOnly（默认值））动态加载适当的实体模板。

## 清单 4.13 支持编辑和插入模式的客户信息页面

```
<%@ Page Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch04.EditTemplates.SamplePage" %>

<asp:Content runat="server" ContentPlaceHolderID="main">
    <asp:ValidationSummary runat="server" />
    <asp:FormView ID="form" runat="server" DataSourceID="dataSource"
        DataKeyNames="CustomerID">
        <ItemTemplate>
            <asp:DynamicEntity runat="server" />
            <tr><td>
                <asp:LinkButton runat="server" CommandName="Edit" Text="Edit" />
                <asp:LinkButton runat="server" CommandName="New" Text="New" />
            </td></tr>
        </ItemTemplate>
        <InsertItemTemplate>
            <asp:DynamicEntity runat="server" Mode="Insert" />
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

与字段模板类似，Dynamic Data 使用模板文件名的最后一部分来确定其模式。对于 Customer 页面，您可能需要在 Web 应用程序的 DynamicData\EntityTemplates 文件夹中放置以下三个模板：

- Customers.ascx，只读模板
- Customers_Edit.ascx，编辑模板
- Customers_Insert.ascx，插入模板

创建 Customers_Edit 和 Customers_Insert 实体模板非常简单；它们与只读 Customers 模板（见清单 4.3）几乎相同，只是 DynamicControl 实例的 Mode 属性分别设置为 Edit 和 Insert。清单 4.14 显示了 Customer 实体的 Edit 模式模板。

## 清单 4.14 Customers_Edit 实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Customers_Edit.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.CustomerEditEntityTemplate" %>

<label>ID:</label>
<asp:DynamicControl runat="server" DataField="CustomerID" Mode="Edit"/>
<label>Name:</label>
<asp:DynamicControl runat="server" DataField="contactName" Mode="Edit"/>
<fieldset><legend>Address</legend>
```

