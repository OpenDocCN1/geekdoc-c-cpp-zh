
```csharp
if (!Request.IsAuthenticated) {
    Response.Redirect("login.aspx");
}
```

另一方面，有时你需要告诉用户这里根本就不是他们该来的地方。当你不得不更改网站结构时，`RedirectPermanently` 特别有用，它会告诉搜索引擎蜘蛛：“不，这里已经没有这个页面了。去那边更新你的索引吧。”

例如，假设你有一个产品线被移动到了一个全新的 URL。你可以检查 QueryString 中的产品线声明，如果找到它，就永久重定向该链接。

```csharp
if (Request.QueryString["ProductLineId"] == 4) {
    Response.RedirectPermanently("http://newproduct.com");
}
```

## 直接修改请求或响应

有时你只是想直接更改某些东西。

`Response.Write`、`Response.WriteFile` 和 `Response.WriteSubstitution` 都是为了让你能够做到这一点而设计的。在过去（调试器出现之前），我们不得不使用 `Response.Write` 将错误写入 HTML，然后用 ViewSource 查看。如果你在使用 MVC，那里仍然有它的用武之地。

在今天的开发中，`Response.Write` 主要用于在满足特定条件的每个页面上执行你想要的操作，无论这些页面是谁编写的。你可以将它添加到母版页的代码隐藏文件中（第 5 章会更多介绍），从而直接修改站点的输出流。

## 使用 ASP.NET 保障安全

第三卷涵盖了安全性，而且还有一整本关于安全的书你应该读一读——Steve McConnell 的《代码大全》。我在本章只涉及一部分安全内容，因为 `AspNetHostingPermission` 位于 System.Web 命名空间中，我想稍微介绍一下它。

ASP.NET 安全性是一个复杂的主题。由于网站访问者是匿名的，因此经常绕过 Windows 安全系统。这种绕过被称为“模拟”（impersonation），它允许 IIS 代表用户执行操作，即使 Windows 并不真正认识这个用户。请记住，仅仅因为你输入了用户名和密码，并不代表 Windows 认可你的凭据。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_716_0.png)

因此，ASP.NET 网站通常使用 IIS 服务运行时所拥有的任何权限来运行。在正常情况下，该服务是一个受限程度相当高的帐户，称为 Network Service。然而事实上，你根本无法预知这些权限会是什么，因为托管公司很可能会管理这些设置。说不定你的用户就拥有管理员权限呢。

你可以在代码中有意限制用户的权限。这可以防止有人通过你的代码逻辑找到调用你本不希望他们调用的方法的方式。

相信我，这种事确实存在。

总体思路是不要信任任何人，这一点我在第三卷的“安全”章节中一直在强调。你要假设大多数会运行你代码的人都是敌人。我知道这并不有趣，但在今天却是必要的。现在已有现成的脚本可以闯入网页——甚至都不需要真人在那里操作就能攻破。

MSDN 文档是这样说明的：

> “建议对受信任的站点将 trust 配置元素的 level 属性设置为 High。对于不受信任的站点，例如托管运行外部客户代码的网站的 Web 服务器，建议将 trust 配置元素的 level 属性设置为 Medium。”

顺便说明一下，未设置权限级别的站点默认为 Full，这显然比上述两种级别都高。

### 更改信任级别

要更改某个类的信任级别，你需要在 ASP.NET 应用程序中使用宿主权限对该类进行修饰，如下所示：

```csharp
using System;
using System.Web;
using System.Security.Permissions;

[AspNetHostingPermission(SecurityAction.Demand, Level=AspNetHostingPermissionLevel.High)]
public class ApplicationClass
{
    // My Code is here.
}
```

所以这段代码使用的是 High 级别。其他级别包括 None、Minimal、Low、Medium 和 Unrestricted。表 4-1 展示了总体的划分。

**表 4-1** ASP.NET 权限级别

| AspNetHostingPermissionLevel | 描述 |
| --- | --- |
| None | 哪里也访问不了。别问了。 |
| Minimal | 代码可以执行，但不能执行任何操作。 |
| Low | 你可以对某些受限信息（如 Request 本身）进行只读访问。非常受限。 |
| Medium | 基本上可以查看任何内容——数据库、网络等。但没有写入权限。 |
| High | 可以对任何托管代码进行读/写，但不能运行非托管（本机）代码。 |
| Unrestricted | 对整台机器拥有完全运行权限。 |

### 解决问题

最常见的问题是使用 None 或 Minimal 作为权限级别。我甚至不知道为什么微软会提供这些选项。根据我的经验，如果你将类设置为 Minimal，那什么也无法访问。在受信任环境中坚持使用 High，在共享服务器上使用 Medium。

## 使用站点地图导航

站点地图是一个 XML 文件，可帮助 Web 设计工具制定动态导航。不过，最近它们有了一个更有趣的用途：搜索引擎利用它们来更好地为你的站点编制索引。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_717_0.png)

Webmasters.bing.com 是微软的一个新产品，它能让你的套件更容易被 Bing 用户使用。它利用站点地图文件使你的网站更易于索引。去看看吧！

搜索引擎优化（SEO）是当下的一大主题，而站点地图能让你的工作轻松很多。搜索引擎已经设置了读取器来检查站点地图，然后利用它遍历文件结构，并确保站点的链接准确无误。

### 添加站点地图

要创建站点地图，请按照以下步骤操作：

- 1. 右键单击项目，然后选择“添加新项...”。
- 2. 从上下文菜单中选择“站点地图”，如图 4-3 所示。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_718_0.png)

图 4-3：添加站点地图。

- 3. 接受默认名称 Web.SiteMap。

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

模板文件为你提供了添加站点导航的指导。如果你在“关于”（About）部分中有多个文件，你可以创建一个 About 的 SiteMapNode，然后在其中（在结束的 `</siteMapNode>` 之前）添加该部分中的页面，例如“联系我们”或“我们的故事”。

不过，在我们的示例中，站点没有分区结构。第 5 章中会有。在当前这种情况下，我们将其设为扁平结构，然后进行演示。

- 4. 为我们的三页扁平结构设置站点地图，如下所示：

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

请注意，根据规范，SiteMapNode 必须至少有两层深度。

- 5. 添加三个页面名称和 URL，如下所示：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
    <siteMapNode>
        <siteMapNode url="Cookies.aspx" title="Cookies" description="Learn all about Cookies" />
        <siteMapNode url="Default.aspx" title="Home" description="The main page" />
        <siteMapNode url="Request.aspx" title="Request" description="Coding for the Request" />
    </siteMapNode>
</siteMap>
```

### 使用 SiteMap 导航站点

当 web.sitemap 文件被安全地安装到应用程序中后，IIS 现在就有了一个 SiteMap 集合，其中包含我们直接在内存中创建的 XML 文件。如果你需要找出与用户正在查看的页面相关的其他页面，你可以做到。请按照以下步骤操作：

- 1. 打开当前项目中的 Default.aspx 页面。
- 2. 将一个空的 ListBox 控件拖到页面中。
- 3. 切换到代码视图。
- 4. 遍历 SiteMap 集合中的项，并将各项添加到列表框中。

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
                foreach (SiteMapNode sitemapKids in SiteMap.CurrentNode.ChildNodes)
                {
                    // Put the node name in the listbox.
                    ListBox1.Items.Add( new ListItem(sitemapKids.Title));
                }
            }
        }
    }
}
```

