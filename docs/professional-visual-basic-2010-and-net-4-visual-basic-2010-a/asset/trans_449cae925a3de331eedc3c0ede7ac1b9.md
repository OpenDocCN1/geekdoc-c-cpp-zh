

## 在母版页中提供默认内容

之前，你已经了解了如何使用基本的 ContentPlaceHolder 控件。除了按所示方式使用外，你还可以创建包含默认内容的 ContentPlaceHolder 控件：

```
<asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
    Here is some default content!
</asp:ContentPlaceHolder>
```

对于默认内容，你同样可以使用任何你想要的元素，包括任何其他 ASP.NET 服务器控件。使用包含这些 ContentPlaceHolder 控件之一的主页的内容页，可以覆盖默认内容——只需指定其他内容（这会覆盖主页中声明的原始内容）——也可以保留控件中包含的默认内容。

## 导航

开发者很少会构建单页 Web 应用程序。相反，应用程序通常由多个以某种方式相互关联的页面组成。有些应用程序有一个工作流，终端用户可以逐页操作，而另一些应用程序则有一个导航结构，允许在页面间自由漫游。有时站点的导航结构会变得复杂，管理这种复杂性可能相当繁琐。

ASP.NET 提供了一种管理 Web 应用程序导航结构的方式：在 XML 文件中定义导航结构，然后将 XML 数据绑定到专注于导航的服务器控件上。你可以在单个文件中维护导航结构，数据绑定机制可确保任何更改都会立即在整个应用程序中得到反映。

本书附带的示例项目包含一个名为 Navigation 的网站项目。你可以打开这个项目，并跟随现有代码一起操作，也可以在学习过程中构建自己的项目。

使用 ASP.NET 导航系统的第一步是创建站点地图文件，即包含完整站点结构的 XML 文件。例如，假设你想要以下导航结构：

- 首页
  - 书籍
  - 杂志
    - 美国杂志
    - 欧洲杂志

该站点结构有三个层级，最底层有多个项目。你可以在 web.sitemap 文件中如下反映这一结构：

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
    <siteMapNode url="default.aspx" title="Home"
        description="The site homepage">
        <siteMapNode url="books.aspx" title="Books"
            description="Books from our catalog" />
        <siteMapNode url="magazines.aspx" title="Magazines"
            description="Magazines from our catalog">
            <siteMapNode url="magazines_us.aspx" title="U.S. Magazines"
                description="Magazines from the U.S." />
            <siteMapNode url="magazines_eur.aspx" title="European Magazines"
                description="Magazines from Europe" />
        </siteMapNode>
    </siteMapNode>
</siteMap>
```

![](img/d99870e80390742f93963da7be0b2e61_764_0.png)

在 Visual Studio 中创建站点地图文件时，请转到“添加新项”对话框并选择“站点地图”选项。你可以将前面的内容放入此文件中。要在层次结构中向下移动一层，可将 `<siteMapNode>` 元素嵌套在其他 `<siteMapNode>` 元素中。一个 `<siteMapNode>` 元素可以包含多个不同的属性，如表 22-1 中所定义。

## 表 22-1：siteMapNode 元素属性

| 属性 | 说明 |
|---|---|
| Title | 提供链接的文本描述。此处使用的 String 值就是用于链接的文本。 |
| Description | 此属性不仅提醒你该链接的用途，还用于链接的 ToolTip 属性。ToolTip 属性是当用户将光标悬停在链接上几秒钟时出现在链接旁边的黄色小框。 |
| Url | 描述文件在解决方案中的位置。如果文件在根目录中，则直接使用文件名，如 default.aspx。如果文件位于子文件夹中，请确保用于此属性的 String 值中包含文件夹，例如 MySubFolder/MyFile.aspx。 |
| Roles | 如果启用了 ASP.NET 安全裁剪，你可以使用 Roles 属性定义哪些角色被允许查看和点击导航中提供的链接。 |

## 使用 SiteMapPath 服务器控件

可绑定到站点地图的可用服务器控件之一是 SiteMapPath 控件。该控件提供了许多互联网网站上常见的流行结构。这种功能有时被称为面包屑导航，在 ASP.NET 中实现起来非常简单。

为了查看此控件的实际工作示例，我们需要一个位于站点地图结构底部的页面。在包含站点地图文件的项目中，创建一个名为 magazines_us.aspx 的 Web 窗体（此页面名称包含在站点地图文件中），并将工具箱“导航”部分中的 SiteMapPath 控件拖放到该窗体上。此控件的标记如下所示：

```
<asp:SiteMapPath ID="SiteMapPath1" runat="server"></asp:SiteMapPath>
```

要让此控件正常工作，你还需要做什么？什么都不用。只需生成并运行该页面，即可看到如图 22-8 所示的结果。

![](img/d99870e80390742f93963da7be0b2e61_765_0.png)

### 图 22-8

SiteMapPath 控件定义了终端用户在应用程序站点结构中的位置。它显示用户当前所在的页面（美国杂志），以及层次结构中位于其上方的两个页面。

SiteMapPath 控件不需要 DataSource 控件，因为它会自动绑定到项目中找到的任何 .sitemap 文件；你无需做任何事即可实现这一点。SiteMapPath 的智能标记还允许你自定义控件的外观，因此你可以生成其他结果，如图 22-9 所示。

![](img/d99870e80390742f93963da7be0b2e61_766_0.png)

图 22-9

此版本 SiteMapPath 控件的代码如下：

```
<asp:SiteMapPath ID="SitePath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : ">
  <CurrentNodeStyle ForeColor="#333333" />
  <NodeStyle Font-Bold="True" ForeColor="#284E98" />
  <PathSeparatorStyle Font-Bold="True" ForeColor="#507CD1" />
  <RootNodeStyle Font-Bold="True" ForeColor="#507CD1" />
</asp:SiteMapPath>
```

代码片段来自 magazines_us.aspx

此示例说明了 SiteMapPath 控件可以使用许多样式元素和属性。你可以使用大量选项来创建独特的、独一无二的面包屑导航。

## Menu 服务器控件

另一个导航控件允许应用程序的终端用户根据 web.sitemap 文件中存储的信息在页面间导航。Menu 服务器控件生成一个紧凑的导航系统，当用户将鼠标悬停在某个选项上时会弹出子选项。当 Menu 服务器控件绑定到站点地图时，其结果如图 22-10 所示。

![](img/d99870e80390742f93963da7be0b2e61_766_1.png)

图 22-10

要查看这一点，请检查名为 magazines_eur.aspx 的 Web 窗体。该页面上同时具有 Menu 和 SiteMapDataSource 控件：

```
<asp:SiteMapDataSource ID="SiteMapDataSource1" runat="server" />
<asp:Menu ID="Menu1" runat="server" DataSourceID="SiteMapDataSource1">
</asp:Menu>
```

代码片段来自 magazines_eur.aspx

SiteMapDataSource 控件自动与应用程序的 web.sitemap 文件配合工作，Menu 控件绑定到 SiteMapDataSource（就像 GridView 可以绑定到 SqlDataSource 一样）。与 ASP.NET 中的许多其他可视控件一样，你可以通过单击控件智能标记中的“自动套用格式”链接轻松修改 Menu 控件的外观。选择“经典”会产生如图 22-11 所示的结果。

![](img/d99870e80390742f93963da7be0b2e61_767_0.png)

### 图 22-11

与其他控件一样，许多子元素共同构成了控件样式外观的改变：

```
<asp:Menu ID="Menu1" runat="server" DataSourceID="SiteMapDataSource1"
BackColor="#B5C7DE" DynamicHorizontalOffset="2" Font-Names="Verdana"
Font-Size="0.8em" ForeColor="#284E98" StaticSubMenuIndent="10px">
<DynamicHoverStyle BackColor="#284E98" ForeColor="White" />
<DynamicMenuItemStyle HorizontalPadding="5px" VerticalPadding="2px" />
<DynamicMenuStyle BackColor="#B5C7DE" />
<DynamicSelectedStyle BackColor="#507CD1" />
<StaticHoverStyle BackColor="#284E98" ForeColor="White" />
<StaticMenuItemStyle HorizontalPadding="5px" VerticalPadding="2px" />
<StaticSelectedStyle BackColor="#507CD1" />
</asp:Menu>
```

代码片段来自 magazines_eur.aspx

## 使用 ASP.NET 提供程序模型

从 ASP.NET 诞生之初，用户就希望能够通过除三种传统存储模式（InProc、StateServer 和 SQLServer）之外的其他方式来存储会话。其中一个请求是新增一种可在 Oracle 数据库中存储会话的存储模式。这看起来像是合乎逻辑的添加，但如果团队为 Oracle 添加了存储模式，他们很快就会收到为其他数据库和数据存储方法添加更多模式的请求。出于这个原因，ASP.NET 团队没有为特定场景构建存储模式，而是通过设计一个可插拔的提供程序模型使系统具有可扩展性，使任何人都能根据需要添加新模式。

除了会话状态之外，ASP.NET 还包含其他几个需要某种状态存储的功能。此外，许多此类功能不是以脆弱模式记录状态（默认情况下会话的存储方式），而是要求其状态存储在更具体的数据存储中，例如数据库或 XML 文件。这也使得访问应用程序的用户能够获得更持久的状态——这些新系统的另一项需求。

