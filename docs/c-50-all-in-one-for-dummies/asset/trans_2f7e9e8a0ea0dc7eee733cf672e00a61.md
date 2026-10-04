

# 712 保护 ASP.NET

需要记录的是，没有设置权限级别的站点默认为“完全（Full）”，这显然高于上述任何一个级别。

# 更改信任度

要更改类的信任度，你需要在 ASP.NET 应用中为该类装饰一个托管权限，如下所示：

```csharp
using System;
using System.Web;
using System.Security.Permissions;

[NetHostingPermission(SecurityAction.Demand, Level=AspNetPermissionLevel.High)]
public class ApplicationClass
{
    // 我的代码在这里。
}
```

因此，这段代码使用了 High（高）级别。其他还有 None（无）、Minimal（最小）、Low（低）、Medium（中）和 Unrestricted（无限制）。表 4-1 显示了详细分类。

| 表 4-1 | ASP.NET 权限级别 |
|---|---|
| AspHostingPermissionLevel | 说明 |
| None | 哪里也去不了。别问。 |
| Minimal | 代码可以执行，但它什么也做不了。 |
| Low | 你对某些受限信息（如 请求本身）具有只读访问权限。非常粗略。 |
| Medium | 多多可以查看任何内容——数据库、网络、任何东西。没有写入权限。 |
| High | 对任何托管代码具有读/写权限，但不能运行未托管（原生）代码。 |
| Unrestricted | 完全开箱运行。 |

# 解决问题

最常见的问题是将 None 或 Minimal 作为权限级别。我甚至不知道微软为什么要提供这些选择。如果你将类设置为 Minimal，据我目前所了解的，没有任何东西可以访问任何东西。在受信任的环境中坚持使用 High，共享服务器上使用 Medium。

# 使用站点地图（Site Maps）进行导航

站点地图是一个 XML 文件，用于帮助 Web 设计工具制定动态导航。最近，它们有了更有趣的用途：它们被搜索引擎用于更好地索引你的网站。

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_0.png)

Webmasters.bing.com 是微软的一款新产品，它可以让你的套件更容易地被 Bing 用户发现。它利用站点地图文件使你的网站更具索引性。去看看吧！

搜索引擎优化（SEO）是今天的一个大话题，而站点地图可以让你的生活变得简单得多。搜索引擎设置了读取器来检查站点地图，然后利用它来遍历文件结构并确保指向网站的链接准确无。

## 添加站点地图

要创建站点地图，请遵循以下步骤：

+   1. 右键点击项目并选择添加（Add）-> 新项（New Item）。
2. 从右键菜单中选择 Site Map，如图 4-3 所示。

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_1.png)

**图 4-3：** 添加站点地图。

![](img/6df7bb88e9302e98442acc219cfbd7fc_738_2.png)

# 714 使用站点地图进行导航

# 3. 接受默认名称 Web.SiteMap。以下是默认代码：

Visual Studio 构建了一个模板站点地图。

```xml
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description="" />
  <siteMapNode url title="" description="" />
  <siteMapNode url title="" description="" />
</siteMap>
```

模板文件为你展示了网站导航的指南。如果你在 About（关于）部分内有多个文件，你可以创建一个 About 的 SiteMapNode，然后在它内部（在 <sitemapnode> 之前）添加该部分中的页面，例如“联系我们”或“我们的故事”。

但是，对于这个示例，网站没有分区域划分。分区域划分在第 5 章中。在当前情况下，你可以让它扁平化运行：

# 4. 为我们的三页扁平化结构设置站点地图，如下：

```xml
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode title="" description="" />
  <siteMapNode url title="" description="" />
  <siteMapNode url title="" description="" />
</siteMap>
```

注意，根据规范，SiteMapNode 具有两层深度。

# 5. 像这样添加三个名称和 URL：



```xml
<xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0">
  <siteMapNode url="Cookies.aspx" title="Learn all About Cookies" />
  <siteMapNode url="Default.aspx" title="Home" description="The page" />
  <siteMapNode url="Request.aspx" title="Request" description="Coding" />
</siteMap>
```

如果你不是根据书中的示例代码进行操作，你需要向项目添加 Cookies.aspx 文件。

# 使用 SiteMap 导航网站

一旦在应用中安全地安装了 web.semanticweb 文件，IIS 现在拥有了一个 SiteMap 集合，其中包含了你在此创建的 XML 文件。

# 管理文件 715

内存。如果你需要确定用户正在查看的页面还有哪些其他相关页面，你可以这样做。遵循以下步骤：

+   1. 打开当前项目中的 Default.aspx 页面。
2. 将一个空的 ListBox 控件拖入页面。
3. 进入代码视图（Code View）。

+   4. 遍历 SiteMap 集合中的项并将项添加到 listbox 中。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // 引用父节点获取对象
            string baseNode = SiteMap.CurrentNode.Title;

            // 检查是否有子节点
            if (SiteMap.CurrentNode.HasChildNodes)
            {
                foreach (SiteMapNode sitemapKids in SiteMap.CurrentNode.Children)
                {
                    // 将标题放入列表
                    ListBox1.Items.Add(new ListItem(sitemapKids.Title));
                }
            }
        }
    }
}
```

如果你感兴趣，在调试器中循环并查看 SiteMap。单单包含了从客户端发送的数据。表单使用的是 multipart 格式。

# 741

# 716 管理文件

ASP.NET 使用两部分计划将文件传递给你。请记住，你可以手动完成，但这都源于 ASP.NET 的理念。前端的控件，后端的系统。

我们将从设计视图开始。遵循以下步骤设置：

+   1. 在项目中创建一个名为 FileUpload.aspx 的新 Web 表单。
2. 从工具箱拖入一个 FileUpload 控件到设计表面。
3. 在表面拖入一个按钮。

FileUpload 控件上的按钮用于选择你文件系统中的项。你仍然需要表单回传（postback）。

这提供了一个良好的开始。FileUpload 有一个文本框和一个按钮，让你访问本地文件系统。按钮提供了提交函数。

+   4. 双击设计表面上的提交按钮以获取 Button1_Click 事件处理器。

+   5. 设置保存文件的路径。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    string localPath = Server.MapPath("~/UploadedFiles/");
}
```

+   6. 在处理程序中添加一些代码来检查表单中是否有文件。新代码在：

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    string localPath = Server.MapPath("~/UploadedFiles/");
}
```

+   7. 在 if 语句体中，让 FileUpload 控件帮助你保存文件。

```csharp
string localPath = Server.MapPath("~/UploadedFiles/");
if (FileUpload1.HasFile)
{
    try {
        FileUpload1.PostedFile.SaveAs(localPath + FileUpload1.FileName);
```

