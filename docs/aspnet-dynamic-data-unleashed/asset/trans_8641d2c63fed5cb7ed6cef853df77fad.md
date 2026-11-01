
## 第4章

## 实体模板

### 本章内容

- 创建实体模板
- 复合实体模板
- 通用实体模板
- 动态实体模板
- 编辑和插入实体模板
- 实体模板查找规则
- 内置实体模板

大多数处理数据的 Web 应用程序都有页面用于显示单个项目的信息，同时允许用户一次创建或修改一个现有项目。图 4.1 显示了此类页面的示例，其中显示了来自 Northwind 示例数据库的单个客户记录。除了明显的视觉精致度不足（由于需要保持代码示例简单）之外，这种页面在当今内部、商业和打包的 Web 应用程序中很常见。你可以在在线零售商网站上轻松找到显示客户资料的类似页面，或在商业 CRM（客户关系管理）系统中找到客户信息。

使用 ASP.NET 实现此类页面非常简单。如图 4.1 所示的典型页面，可以使用数据源控件，例如本示例中的 EntityDataSource，从数据库中检索记录。数据源控件与演示控件关联，例如 FormView，它使用一个或多个数据绑定控件来显示字段值。

在第 3 章“字段模板”中，你看到了 Dynamic Data 如何通过提供 Field Templates（一种特殊类型的用户控件，用于封装不同列类型单个字段值的演示和业务逻辑）使创建数据驱动页面的任务变得更容易。你可以通过向页面添加 DynamicControl 实例并指定其 DataField 属性来使用字段模板，以指示需要字段模板的列。DynamicControl 根据描述列的元数据信息选择合适的字段模板，字段模板使用适当的控件来格式化和显示字段值。

## 创建实体模板

*实体模板* 是 Dynamic Data 使用的一种特殊类型的用户控件，用于封装单个实体或代表数据库表中单行的类的演示逻辑。你可以通过简单地从清单 4.1 中提取突出显示的代码，并将其放置到 Web 项目的 `DynamicData\EntityTemplates` 文件夹中的新用户控件 `Customers.ascx` 中，为 Customers 表创建一个自定义实体模板，这是 Dynamic Data 默认查找实体模板的位置。清单 4.3 显示了新实体模板的标记。

### 清单 4.3 客户实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Customers.ascx.cs"
    Inherits="WebApplication.DynamicData.EntityTemplates.CustomEntityTemplate" %>
<label>ID:</label>
<asp:DynamicControl runat="server" DataField="CustomerID" />
<label>Name:</label>
<asp:DynamicControl runat="server" DataField="ContactName" />
<fieldset><legend>Address</legend>
    <label>Street:</label>
    <asp:DynamicControl runat="server" DataField="Address" /><br />
    <label>City:</label>
    <asp:DynamicControl runat="server" DataField="City" />
    <label>State:</label>
    <asp:DynamicControl runat="server" DataField="Region" />
    <label>Zip:</label>
    <asp:DynamicControl runat="server" DataField="PostalCode" />
</fieldset>
```

除了 `<%@ Control %>` 指令外，新 Customers 实体模板的标记是清单 4.1 中代码的真实复制粘贴。

> **注意**
>
> 请注意控件文件名 Customers.ascx 很重要。文件名（不含扩展名）需要与元数据中描述 Customer 实体的 MetaTable 名称匹配，即 *Customers*（复数）。

用户控件必须继承 Dynamic Data 提供的特殊类 `EntityTemplateUserControl`，如清单 4.4 所示。这个简单的基类提供了多个属性，包括 Table，它返回描述实体的 `MetaTable` 实例，以及 Mode，它可以是只读、插入或编辑。

### 清单 4.4 客户实体模板（代码隐藏）

```csharp
using System.Web.DynamicData;

namespace WebApplication.DynamicData.EntityTemplates
{
    public partial class CustomerEntityTemplate : EntityTemplateUserControl
    {
    }
}
```

在定义了实体模板后，你可以通过用 DynamicEntity 控件替换 FormView 的全部内容来修改客户信息页面以利用它，如清单 4.5 所示。

### 清单 4.5 带实体模板的客户信息页面（标记）

```aspx
<%@ Page Language="C#"
    MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
    Inherits="WebApplication.Samples.Ch04.ReadOnlySamplePage" %>

<asp:Content runat="server" ContentPlaceHolderID="main">
    <asp:ValidationSummary runat="server" />
    <asp:FormView ID="form" runat="server" DataSourceID="dataSource">
        <ItemTemplate>
            <asp:DynamicEntity runat="server" />
        </ItemTemplate>
    </asp:FormView>
    <asp:EntityDataSource ID="dataSource" runat="server"
        ConnectionString="name=NorthwindEntities" AutoGenerateWhereClause="true"
        DefaultContainerName="NorthwindEntities" EntitySetName="Customers">
        <WhereParameters>
            <asp:QueryStringParameter QueryStringField="ID" Name="CustomerID" />
        </WhereParameters>
    </asp:EntityDataSource>
</asp:Content>
```

DynamicEntity 是在 System.Web.DynamicData 命名空间中定义的新控件。在运行时，它会自动确定与其父 FormView 控件关联的 MetaTable，并在 Web 应用程序的 DynamicData\EntityTemplates 文件夹中查找名称匹配的模板。如果匹配的实体模板存在，DynamicEntity 将加载并将其包含在网页中，在本示例中，这使其看起来与图 4.1 所示的页面完全相同。

## 复合实体模板

没有要求每个实体只有一个实体模板。你可以为单个实体创建多个实体模板，其中每个模板包含整个实体的演示或仅其一部分。对于大型实体而言，这特别有用，在这种情况下，将信息呈现在多个页面或单个页面的多个选项卡上是有意义的。你可以通过将联系信息和地址信息分离到单独的实体模板中，进一步分解 Customer 实体模板，分别如清单 4.6 和清单 4.7 所示。

### 清单 4.6 联系实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Contact.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.ContactTemplate" %>

<label>Name:</label>
<asp:DynamicControl runat="server" DataField="ContactName" />
<br />

<label>Company:</label>
<asp:DynamicControl runat="server" DataField="CompanyName" />
<br />

<label>Title:</label>
<asp:DynamicControl runat="server" DataField="ContactTitle" />
<br />
```

如你所见，Contact 实体模板仅包含姓名、公司和职称字段，而 Address 实体模板仅包含地址字段。

### 清单 4.7 地址实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Address.ascx.cs" Inherits="WebApplication.DynamicData.EntityTemplates.AddressTemplate" %>

<fieldset>
<legend>Address</legend>
<label>Street:</label>
<asp:DynamicControl runat="server" DataField="Address" />
<br />

<label>City:</label>
<asp:DynamicControl runat="server" DataField="City" />
<label>State:</label>
<asp:DynamicControl runat="server" DataField="Region" />
<label>Zip:</label>
<asp:DynamicControl runat="server" DataField="PostalCode" />
</fieldset>
```

在将联系和地址字段封装到两个单独的实体模板后，是时候更新主要的 Customers 实体模板以借助 DynamicEntity 控件实例化它们，如清单 4.8 所示

### 清单 4.8 复合客户实体模板（标记）

```
<%@ Control Language="C#" CodeBehind="Customers.ascx.cs"
Inherits="WebApplication.DynamicData.EntityTemplates.CustomerEntityTemplate" %>

<label>ID:</label>
<asp:DynamicControl runat="server" DataField="CustomerID" />

<asp:DynamicEntity runat="server" UIHint="Contact" />
<asp:DynamicEntity runat="server" UIHint="Address" />
```

请注意，由于 Contact 和 Address 实体模板的名称与 Customers 表的名称不匹配，因此你需要通过指定 DynamicEntity 控件的 UIHint 属性来显式引用它们。

## 通用实体模板

如果你注意一下，除了它们显示的字段名称外，没有什么将这些新的 Contact 和 Address 模板与 Customer 实体绑定在一起。不同页面可以利用 DynamicControl 在运行时执行所有初始化任务的事实，通过为任何具有相同名称字段的其他实体重用这些模板。在 Northwind 示例数据库中，Suppliers 表与 Customers 表相似；你可以重用 Contact 和 Address 实体模板来实现 UI，如清单 4.9 所示。

### 清单 4.9 供应商信息页面（标记）

```
<%@ Page Language="C#"
MasterPageFile="~/Site.master" CodeBehind="SamplePage.aspx.cs"
Inherits="WebApplication.Samples.Ch04.GenericTemplates.SamplePage" %>

<asp:Content runat="server" ContentPlaceHolderID="main">
<asp:FormView ID="form" runat="server" DataSourceID="dataSource">
<ItemTemplate>
<asp:DynamicEntity runat="server" UIHint="Contact" />
<asp:DynamicEntity runat="server" UIHint="Address" />
</ItemTemplate>
</asp:FormView>
</asp:Content>
<asp:EntityDataSource ID="dataSource" runat="server"
ConnectionString="name=NorthwindEntities" AutoGenerateWhereClause="true"
DefaultContainerName="NorthwindEntities" EntitySetName="Suppliers">
```
