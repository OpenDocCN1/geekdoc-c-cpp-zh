
在当今的开发中，`Response.Write` 主要用于执行你希望在每个满足特定条件的页面上执行的操作，无论该页面由谁编写。你可以将其添加到母版页的代码隐藏文件中（第 5 章将详细讨论），并确保站点的输出流会被直接修改。

## 保护 ASP.NET 安全

第 III 册第 1 章涵盖了 .NET 安全性，而且有一整本关于安全性的书你应该读——由 Michael Howard 和 David LeBlanc 合著的 *编写安全代码（第二版）*（Microsoft Press）。我在本章只讨论安全性，是因为 `AspNetHostingPermission` 位于 `System.Web` 命名空间中，我想给它一点展示机会。

ASP.NET 安全性是一个复杂的话题。由于网站访问者是匿名的，绕过 Windows 安全系统的情况经常发生。这种绕过——称为*模拟*——允许 IIS 代表用户执行操作，即使 Windows 实际上并不认识该用户。请记住，仅仅因为你输入了用户名和密码，并不意味着 Windows 认可你的凭据。

![](img/80ff26f06fc9ab951e1cd4257b867366_736_0.png)

因此，ASP.NET 网站通常以 IIS 服务运行时所用的权限运行。正常情况下，该服务是一个权限相当受限的帐户，称为 Network Service。但事实是，你实际上根本不知道权限会是什么，因为托管公司很可能会管理这些权限。据你所知，你的用户可能拥有管理员权限。

你可以在代码中有意限制用户的权限。这可以防止有人通过你的代码逻辑找到方法来调用你不希望他们能够调用的方法。

相信我，这种情况确实会发生。

总体思路是不信任任何人，我在第 III 册第 1 章中反复强调这一点。你要假装大多数将要运行你的代码的人都是敌人。我知道这并不好玩。但在今天这是必要的。有一些预构建的脚本可以侵入网页——甚至不需要真人在那里实施入侵。

MSDN 文档是这样说的：

> “对于受信任的站点，建议将 trust 配置元素的 level 属性设置为 High。对于不受信任的站点，例如托管运行外部客户代码的网站的 Web 服务器，建议将 trust 配置元素的 level 属性设置为 Medium。”

郑重说明一下，未设置权限级别的站点默认使用 Full，这显然高于上述两个级别。

### 更改信任级别

要更改类的信任级别，你需要在 ASP.NET 应用程序中使用宿主权限来修饰该类，如下所示：

```csharp
using System;
using System.Web;
using System.Security.Permissions;

[AspNetHostingPermission(SecurityAction.Demand, Level=AspNetHostingPermissionLevel.High)]
public class ApplicationClass
{
    //My Code is here.
}
```

因此这段代码使用 High 级别。其他级别包括 None、Minimal、Low、Medium 和 Unrestricted。表 4-1 显示了大致分类。

| 表 4-1 | ASP.NET 权限级别 |
|---|---|
| AspNetHostingPermissionLevel | 描述 |
| None | 无法访问任何内容。别问了。 |
| Minimal | 代码可以执行，但什么也做不了。 |
| Low | 你对某些受限信息（例如 Request 本身）具有只读访问权限。非常粗略。 |
| Medium | 或多或少可以查看任何内容——数据库、网络等等。没有写访问权限。 |
| High | 对任何托管代码具有读/写权限，但不能运行非托管（本机）代码。 |
| Unrestricted | 完全控制这台机器。 |

### 解决问题

最常见的问题是使用 None 或 Minimal 作为权限级别。我甚至不知道 Microsoft 为什么提供这些选项。如果你将类设置为 Minimal，据我所知，什么都无法访问。对于受信任的环境，请坚持使用 High；对于共享服务器，请使用 Medium。

### 3. 接受默认名称 Web.SiteMap。

Visual Studio 会生成一个模板站点地图。以下是默认代码：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
  <siteMapNode url="" title="" description="">
    <siteMapNode url="" title="" description="" />
    <siteMapNode url="" title="" description="" />
  </siteMapNode>
</siteMap>
```

该模板文件向你展示了添加站点导航的指导原则。如果你在 About 部分中有多个文件，你可以为 About 创建一个 SiteMapNode，然后在其内部（在结束标签 </sitemap-node> 之前）添加该部分中的页面，例如 Contact Us 或 Our Story。

不过，对于这个示例，站点没有分区划分。第 5 章中会有分区。在当前情况下，你将其设为扁平结构并以此进行操作。

### 4. 为我们的三页扁平结构设置站点地图，如下所示：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
<siteMapNode>
  <siteMapNode url="" title="" description="" />
  <siteMapNode url="" title="" description="" />
  <siteMapNode url="" title="" description="" />
</siteMapNode>
</siteMap>
```

请注意，按照规范，SiteMapNode 必须有两层深度。

### 5. 添加三个页面名称和 URL，如下所示：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
<siteMapNode url="Cookies.aspx" title="Cookies" description="Learn all about Cookies" />
<siteMapNode url="Default.aspx" title="Home" description="The main page" />
<siteMapNode url="Request.aspx" title="Request" description="Coding for the Request" />
</siteMapNode>
</siteMap>
```

如果你不是使用本书的示例代码，则需要将 Cookies.aspx 文件添加到项目中。

## 使用 SiteMap 导航站点

将 web.sitemap 文件安全地安装到应用程序中后，IIS 现在拥有一个 SiteMap 集合，其中包含你刚刚在内存中创建的 XML 文件。如果你需要弄清楚还有哪些页面与用户正在查看的页面相关，你可以做到。请按照以下步骤操作：

- 1. 在当前项目中打开 Default.aspx 页面。
- 2. 将一个空的 ListBox 控件拖到页面中。
- 3. 转到“代码”视图。
- 4. 循环遍历 SiteMap 集合中的项，并将项添加到列表框中。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Chapter_4
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // Reference the parent node to keep the object model happy.
            string baseNode = SiteMap.CurrentNode.Title;

            // Check to make sure there are subpages.
            if (SiteMap.CurrentNode.HasChildNodes)
            {
                foreach (SiteMapNode sitemapKids in
                    SiteMap.CurrentNode.ChildNodes)
                {
                    // Put the node name in the listbox.
                    ListBox1.Items.Add( new ListItem(sitemapKids.Title));
                }
            }
        }
    }
}
```

如果你感兴趣，可以在循环中放置一个调试器，并查看那个 SiteMap 对象。它是一个很好的集合，包含 Web.sitemap 文件中已引用的页面。尽管这项技术不能解决每个站点上的所有导航问题，但它是 System.Web 中一个很好但未被充分使用的部分。

## 管理文件

forms 集合包含从客户端发回的所有数据。这包括使用 multipart-data 格式上传的任何文件。

ASP.NET 使用一个由两部分组成的方案将文件数据提供给你。请记住，你可以完全手动完成所有这些操作，但这一切都回归到 ASP.NET 模型背后的理念：前端是控件，后端是 System.Web 相关内容。

我将从“设计”视图开始。用户只需选择一个本地文件，浏览器就会负责对文件进行编码并将其发送到服务器。文件编码标准内置于协议中，就像 HTML 本身一样。请按照以下步骤设置上传：

- 1. 在第 4 章项目中创建一个名为 FileUpload.aspx 的新 Web 窗体。
- 2. 从“工具箱”中将 FileUpload 控件拖到设计图面上。
- 3. 将一个按钮拖到图面上。

FileUpload 控件上的按钮仅用于选择文件系统中的一个项。你仍然需要回发该窗体。

这为你提供了一个良好的开端。FileUpload 有一个文本框和一个按钮，可让你访问本地文件系统。该按钮提供提交功能。

在此示例中，所有神奇之处都发生在后端。浏览器会为你处理文件上传。服务器端则由你负责。

4. 在设计图面上双击提交按钮，以获取 Button1_Click 事件处理程序。

5. 设置保存文件的路径。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    String localPath = Server.MapPath("~/UploadedFiles/");
}
```

6. 向处理程序添加一些代码，以检查窗体中是否有文件。新增代码以粗体显示。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    String localPath = Server.MapPath("~/UploadedFiles/");
}
```

7. 在 if 语句的主体中，让 FileUpload 控件帮助我们保存文件。

新增代码以粗体显示。

```csharp
protected void Button1_Click(object sender, EventArgs e)
{
    String localPath = Server.MapPath("~/UploadedFiles/");
    if (FileUpload1.HasFile)
    {
        try
        {
            FileUpload1.PostedFile.SaveAs(localPath + FileUpload1.FileName);
        }
    }
}
```
