
## PCSDemoSite 中的主题

PCSDemoSite 网站包含三个主题，您可以在 `/Configuration/Themes/Default.aspx` 页面上选择——前提是您以 `RegisteredUser` 或 `SiteAdministrator` 角色的成员身份登录。此页面如图 41-6 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1269_0.png)

图 41-6

此处使用的主题是 DefaultTheme，但您可以从此页面的其他选项中选择。图 41-7 显示了 BareTheme 主题。

![](img/d7d2ffa0a76feaab821930e95daace93_1269_1.png)

图 41-7

```
Page.Theme = Session["SessionTheme"] as string;
}
else
{
    Page.Theme = "DefaultTheme";
}

// base call
base.OnPreInit(e);
}
```

代码片段 PCDemoSite/App_Code/MyPageBase.cs

此事件处理程序检查会话状态中 SessionTheme 的条目，如果存在则应用所选主题；否则使用 DefaultTheme。

同样请注意，此类继承自通常的页面基类 Page。这是有必要的，因为否则页面将无法作为 ASP.NET 网页运行。

要使其正常工作，还必须为所有网页指定此基类。有几种方法可以做到这一点，最明显的是在页面的 <%@ Page %> 指令中或在页面的代码隐藏中执行。前一种策略对于简单页面来说是可以的，但排除了为页面使用自定义代码隐藏，因为页面将不再使用其自己的代码隐藏文件中的代码。另一种选择是在代码隐藏文件中更改页面继承的类。默认情况下，新页面继承自 Page，但您可以更改它。在前面显示的主题选择页面的代码隐藏文件中，您可能已经注意到以下代码：

```
public partial class _Default : MyPageBase
{
    ...
}
```

代码片段 PCDemoSite/Configuration/Themes/Default.aspx.cs

在这里，MyPageBase 被指定为 Default 类的基类，因此在 MyPageBase.cs 中重写的方法将被使用。

## Web 部件

ASP.NET 包含一组称为 Web Parts 的服务器控件，旨在使用户能够个性化网页。您可能已经在行动中看到过，例如在基于 SharePoint 的网站或 My MSN 主页上：http://my.msn.com/。当您使用 Web Parts 时，其产生的功能如下：

- 用户会看到您提供的默认页面布局。该布局由多个组件 Web Parts 组成，每个 Web Part 都有标题和内容。
- 用户可以更改页面上 Web Parts 的位置。
- 用户可以自定义页面上 Web Parts 的外观或完全将其从页面中移除。
- 用户可以获得一个 Web Parts 目录，可以将其添加到页面。
- 用户可以从页面导出 Web Parts，然后在不同的页面或站点上导入它们。
- Web Parts 之间可以存在连接。例如，一个 Web Part 中显示的内容可能是另一个 Web Part 中显示的内容的图形表示。
- 用户所做的任何更改都会在站点访问之间保留。

ASP.NET 提供了完整的框架来实现 Web Parts 功能，包括管理和编辑控件。

Web Parts 的使用是一个复杂的话题，本节并未描述所有可用功能或列出 Web Part 组件提供的所有属性和方法。然而，您可以看到足够的内容来了解 Web Parts 的概况并理解可能的基本功能。

### Web Parts 应用组件

工具箱中的 Web Parts 部分包含 13 个控件，如下表所述。该表还介绍了 Web Parts 页面的一些关键概念。

| 控制 | 描述 |
|---|---|
| WebPartManager | 使用 Web Parts 的每个页面必须有一个（且只有一个）WebPartManager 控件的实例。您可以在母版页上放置它，如果您这样做，则应仅在您希望在页面上使用 Web Parts 时使用母版页。此控件负责大部分 Web Parts 功能，它在几乎无需干预的情况下提供这些功能。根据您需要的功能，您可能不需要做更多的事情，只需将其放置在网页上即可。对于更高级的功能，您可以使用此控件公开的大量属性和事件。 |
| ProxyWebPartManager | 如果您将 WebPartManager 控件放置在母版页上，则在单个页面上配置它会很困难——并且无法以声明方式进行配置。这对于 Web Parts 之间静态连接的定义尤其相关。ProxyWebPartManager 控件使您能够在网页上以声明方式定义静态连接，从而解决了无法在同一页面上拥有两个 WebPartManager 控件的问题。 |
| WebPartZone | WebPartZone 控件用于定义可以包含 Web Parts 的页面区域。您通常会在页面上使用多个此类控件。例如，您可能在页面上的三列布局中使用三个控件。用户可以在 WebPartZone 区域之间移动 Web Parts 或在单个 WebPartZone 内重新定位它们。 |
| CatalogZone | CatalogZone 控件使用户能够向页面添加 Web Parts。此控件包含派生自 CatalogPart 的控件，其中提供了三个——下表中的接下来的三个条目描述了这些控件。CatalogZone 控件及其包含的控件是否可见取决于 WebPartManager 设置的当前显示模式。 |
| DeclarativeCatalogPart | DeclarativeCatalogPart 控件使您能够内联定义 Web Part 控件。这些控件随后将通过 CatalogZone 控件提供给用户。 |
| PageCatalogPart | 用户可以移除（关闭）页面上显示的 Web Parts。为了检索它们，PageCatalogPart 控件提供了一个已关闭 Web Parts 的列表，可以将其放回页面。 |
| ImportCatalogPart | ImportCatalogPart 控件使已从页面导出的 Web Parts 能够通过 CatalogPart 接口导入到另一个页面。 |
| EditorZone | EditorZone 控件包含控件，使用户能够根据其包含的控件编辑 Web Part 显示和行为的各个方面。它可以包含派生自 EditorPart 的控件，包括下表接下来的四行中列出的四个控件。与 CatalogZone 一样，此控件的显示取决于当前的显示模式。 |
| AppearanceEditorPart | 此控件使用户能够修改 Web Part 控件的外观和大小，以及隐藏它们。 |
| BehaviorEditorPart | 此控件使用户能够通过使用各种属性来配置 Web Parts 的行为，这些属性控制例如 Web Part 是否可以关闭或 Web Part 标题链接到的 URL。 |
| LayoutEditorPart | 此控件使用户能够更改 Web Part 的布局属性，例如它包含的区域以及它是否以最小化状态显示。 |
| PropertyGridEditorPart | 这是最通用的 Web Part 编辑器控件，使您能够为自定义 Web Part 控件定义可编辑的属性。用户随后可以编辑这些属性。 |
| ConnectionsZone | 此控件使用户能够在公开连接功能的 Web Parts 之间创建连接。与 CatalogZone 和 EditorZone 不同，此控件内部没有要放置的控件。此控件生成的用户界面取决于页面上可用于连接的控件。控件的可见性取决于显示模式。 |

您可能会注意到，此控件列表不包括任何 Web Parts。这是因为您自己创建这些。您放入 WebPartZone 区域的任何控件都会自动成为 Web Part——包括（最重要的是）用户控件。通过使用用户控件，您可以将其他控件组合在一起以提供 Web Part 控件的用户界面和功能。

### Web Parts 示例

为了说明 Web Parts 的功能，您可以查看本章下载代码中的另一个示例网站，名为 PCSWebParts。此示例使用与 PCSAuthenticationDemo 示例相同的数据库。它有两个用户名为 User 和 Administrator 的用户，两者的密码均为 Pa$$w0rd。您可以以用户身份登录，操作页面上的 Web Parts，注销，以另一用户身份登录，并以完全不同的方式操作 Web Parts。两个用户的个性化设置在站点访问之间得以保留。

登录站点后，初始显示（用户已登录）如图 41-8 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1273_0.png)

图 41-8
