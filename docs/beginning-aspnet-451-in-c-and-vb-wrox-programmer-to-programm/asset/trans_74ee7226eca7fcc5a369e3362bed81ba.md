

## 理解默认文档

在 URL 的上下文中，你也应该了解默认文档。当你访问像 www.domain.com 这样的站点时，你可能会神奇地看到一个页面出现。这是如何运作的呢？每个 Web 服务器都有所谓的默认文档，这是一份在没有提供显式文档时可以提供给浏览器的文档名称列表。因此，当你访问 www.domain.com 时，Web 服务器会扫描请求的目录（在本例中为根文件夹），并处理从找到的默认列表中的第一个文件。在大多数 ASP.NET 场景中，Web 服务器被设置为使用 `Default.aspx` 作为默认文档。因此，当你在 ASP.NET 服务器上访问 www.domain.com 时，你实际上获得的是 www.domain.com/Default.aspx 页面。

在你创建的链接中，如果不需要，通常应该省略 `Default.aspx`。这可以减小页面大小，更重要的是，它让用户更容易输入地址。

现在你已经学会了如何使用 URL 指向文档和其他文件，是时候查看一些利用这些 URL 的更高级控件了：ASP.NET 导航控件。

## 使用导航控件

ASP.NET 4.5.1 提供了三个实用的导航工具：SiteMap、TreeView 和 Menu。图 7-2 显示了这三个导航控件的示例，没有应用任何样式。

左侧的 SiteMap 显示用户到当前页面的路径。这有助于想要在层次结构中移动一级或多个级别的用户。它帮助他们理解自己所处的位置。TreeView 可以显示你的站点结构，并允许你展开和折叠不同的节点；图 7-2 显示了展开的树。右侧的 Menu 最初只显示 Home（首页）菜单项。然而，一旦将鼠标移动到菜单项上，子菜单就会出现。图 7-2 中这些元素之一是 Items，它反过来又有子元素。

![](img/9e033e3b9560597824f8b22941d6d8bb_280_0.png)

图 7-2

尽管在行为和外观上非常不同，但这三个导航控件在设计上是有共同点的。

> 注意：在第 2 章中，我提到过导航控件与 Bootstrap 等框架配合得并不好。如果你使用这些框架之一，最好不要使用导航控件，而是依靠这些框架的导航功能（例如菜单）。

## 导航控件的体系

为了方便使用 Menu、TreeView 或 SiteMap 在你的站点中显示相关页面，ASP.NET 使用了一个基于 XML 的文件来描述你网站的逻辑结构。默认情况下，该文件名为 `sitemap`。然后，该文件被你站点中的导航控件使用，以组织化的方式呈现相关链接。通过将其中一个导航控件连接到 `Web.sitemap`，你可以创建复杂的用户界面，如折叠菜单或树视图。

## 检查 Web.sitemap 文件

默认情况下，你应该将站点地图文件名为 `Web.sitemap`。这使得控件能够自动找到正确的文件。对于更高级的场景，你可以拥有多个不同名称站点文件，并在 `Web.config` 文件中使用配置设置将这些额外文件暴露给系统。在大多数情况下，单个站点地图文件就足够了。站点地图文件的基本版本如下：

```xml
<xml version="1.0" encoding="UTF-8"?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode url="/Home.aspx" description="Go to the homepage">
    <siteMapNode title="Reviews" description="Reviews published on the site" />
    <siteMapNode url="/About.aspx" title="About" description="About this site" />
  </siteMapNode>
</siteMap>
```

站点地图文件包含 `siteMapNode` 元素，这些元素构成了你站点的逻辑结构。例如，有一个根节点 Home，它反过来包含两个元素 Reviews 和 About。

## Web.sitemap 文件的关键元素

每个 `siteMap` 都有许多子节点（但 `siteMap` 元素下只能有一个 `siteMap`），这允许你创建一个既宽又深的站点结构。示例中的 `siteMapNodes` 有三个属性被设置了：`url`、`title` 和 `description`。`url` 属性应该指向你网站中的有效页面。你可以使用上一节中看到的语法来引用基于应用程序根的 URL。ASP.NET 运行时不允许你多次指定相同的 URL，但你可以通过添加查询字符串使 URL 变得唯一来绕过这一点。例如，`~/Login.aspx` 和 `~/Login.aspx?type=Admin` 被视为两个不同的页面。你将在本章后面看到更多关于查询字符串的内容。

`title` 属性用于导航控件中显示页面名称。当你处理 Menu、TreeView 和 SiteMap 控件时，你会看到更多此类信息。`description` 属性用作导航元素的工具提示（tooltip）。7-2 显示了 By Genre（类型）元素的工具提示。

导航控件与 ASP.NET 机制协同工作。你可以自动隐藏用户没有访问权限的如 Menu 等控件元素。安全性将在第 16 章中更详细地描述。

显示面包屑导航（本章稍后将讨论）的 SiteMap 控件能够找到 `Web.sitemap` 文件。对于另外两个，SiteMap 控件能够找到 `Web.sitemap` 文件。SiteMap 控件能够找到 `Web.sitemap` 文件。

要创建一个 `Web.sitemap`，你需要向站点添加内容。

## 尝试创建 Web.sitemap

在本次练习中，你向站点中添加内容。

1. 右键点击解决方案管理器（Solution Explorer），选择“新建项”（New Item），并将默认名称设置为 `Web.sitemap`。
2. 修改 sitemap 文件使其包含以下代码：
   ```xml
   <xml version="1.0" encoding="UTF-8"?>
   <siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
     <siteMapNode url="/Home.aspx" description="Go to the homepage">
       <siteMapNode title="Reviews" description="Reviews published on the site" />
       <siteMapNode url="/About.aspx" title="About" description="About this site" />
     </siteMapNode>
   </siteMap>
   ```
3. 保存文件；你现在已经完成了。

## 常见错误

确保你输入的代码与所示完全一致。注意某些项（例如 Home 元素）包含其他子元素并在下方有闭合标签。相比之下，像 By Genre 的项使用自闭标签且没有子元素。

## 工作原理

尽管你没有在 `Web.sitemap` 文件中添加惊艳的代码，但有些点值得讨论。首先，请注意站点只包含一个根节点 Home。这是 `Web.sitemap` 文件强制要求的，它不允许有多个根节点。缺点是，这个根节点将成为你的 Menu 和 TreeView 控件的根节点。在图 7-2 中，你可以看到 TreeNode 的所有子菜单都在 Home 节点之下。然而，在大多数网站中，Home 项与其他处于同一水平更为常见。因此，在本次练习中，你在父节点下直接添加了一个 Home 节点，以便与 Reviews、About 和 Login 项对齐。在稍后的练习中，你将看到如何从控件中隐藏根元素，从而只显示根的“第一个子节点”及其子节点。为了解决 `siteNode` 元素中的 URL 需要唯一的问题，你将其中一个设置为 `~/`，另一个设置为 `~/Default.aspx`。由于 Web 服务器处理默认文档的方式，它们最终指向同一个文件。

`Web.sitemap` 文件本身并没有什么用。你需要向站点添加导航控件来使用站点地图。在下一节中，你将看到如何使用 Menu 控件。后面的章节将深入探讨 TreeNode 和 SiteMap 控件。

## 使用 Menu 控件

Menu 控件非常容易使用和调整。要创建一个基础菜单，你只需要在页面上添加它，并将其连接到 SiteMapDataSource 控件就完成了。但同时，该控件非常有灵活性，拥有约 80 个公共属性（包括所有控件共享的属性），允许你微调控件的每个视觉方面。下表列出了与 Menu 最常用的属性。请参考 MSDN 在线帮助以获取该控件的完整描述。

