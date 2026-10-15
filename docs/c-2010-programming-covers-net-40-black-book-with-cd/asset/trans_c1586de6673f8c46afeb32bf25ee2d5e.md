

## 创建 SiteMapPath

我们在本章的深入部分中已经提到，SiteMapPath 控件可以自动配置到 SiteMapDataSource 控件，该控件反过来可以读取 Web.sitemap 文件以在应用程序上显示数据。我们创建了一个名为 SiteMapPathControl 的应用程序。你可以在 CD-ROM 上找到该应用程序，名称为 SiteMapPathControlCS。

要在 SiteMapPathControl 应用程序中创建 Web.sitemap，右键单击项目名称。会出现一个上下文菜单。从上下文菜单中选择添加新项选项。会出现添加新项对话框框，如图 15.14 所示。选择可用的选项中的站点地图。这将在项目中创建一个新的 Web.sitemap 文件。

Web.sitemap 文件包含应用程序的导航详细信息。你可以使用 Web.sitemap 文件为每个页面设置标题、URL 和其他信息。在 Web.sitemap 文件中添加清单 15.14 所示的代码：

### 清单 15.14：显示 Web.sitemap 文件的代码

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
  <siteMapNode url="default.aspx" title="Home Page" description="" >
    <siteMapNode url="page1.aspx" title="Section 1" description="" />
    <siteMapNode url="page2.aspx" title="Section 2" description="" />
  </siteMapNode>
</siteMap>
```

你还需要在该应用程序的 Default.aspx 页面中添加清单 15.15 所示的代码：

### 清单 15.15：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>SiteMapPath Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="SiteMapDataSource Example"/><br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : " PathDirection="CurrentToRoot">
<PathSeparatorStyle Font-Bold="True" ForeColor="#5D7B9D" />
<CurrentNodeStyle ForeColor="#333333" />
<NodeStyle Font-Bold="True" ForeColor="#7C6F57" />
<RootNodeStyle Font-Bold="True" ForeColor="#5D7B9D" />
</asp:SiteMapPath>
<br />
<br />
<asp:HyperLink ID="HyperLink1" runat="server" NavigateUrl="~/Page1.aspx">Go to Page 1</asp:HyperLink>
<asp:HyperLink ID="HyperLink2" runat="server" NavigateUrl="~/Page2.aspx">Go to Page 2</asp:HyperLink><br />
</div>
</form>
</body>
</html>
```

现在，在项目中添加两个 Web 表单，命名为 Page1.aspx 和 Page2.aspx，并在 SiteMapPathControl 应用程序的 Page1.aspx 页面中添加清单 15.16 所示的代码：

### 清单 15.16：显示 Page1.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Page1.aspx.cs" Inherits="Page1" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>SiteMapPath Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="SiteMapDataSource Example"></asp:Label><br />
<br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : ">
<PathSeparatorStyle Font-Bold="True" ForeColor="#5D7B9D" />
<CurrentNodeStyle ForeColor="#333333" />
<NodeStyle Font-Bold="True" ForeColor="#7C6F57" />
<RootNodeStyle Font-Bold="True" ForeColor="#5D7B9D" />
</asp:SiteMapPath>
&nbsp;<br />
<br />
<asp:HyperLink ID="HyperLink2" runat="server" NavigateUrl="~/Page2.aspx">Go to Page 2</asp:HyperLink><br />
</div>
</form>
</body>
</html>
```

现在，在 SiteMapPathControl 应用程序的 Page2.aspx 页面中添加清单 15.17 所示的代码：

### 清单 15.17：显示 Page2.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Page2.aspx.cs" Inherits="Page2" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>SiteMapPath Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="SiteMapDataSource Example"></asp:Label><br />
<br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : ">
<PathSeparatorStyle Font-Bold="True" ForeColor="#5D7B9D" />
<CurrentNodeStyle ForeColor="#333333" />
<NodeStyle Font-Bold="True" ForeColor="#7C6F57" />
<RootNodeStyle Font-Bold="True" ForeColor="#5D7B9D" />
</asp:SiteMapPath>
<br />
<br />
<asp:HyperLink ID="HyperLink1" runat="server" NavigateUrl="~/Page1.aspx">Go to Page 1</asp:HyperLink><br />
</div>
</form>
</body>
</html>
```

> 注意
> 在运行应用程序之前，将 Default.aspx 页面设为起始页面。

现在，执行功能完整的 SiteMapPath 控件。输出如图所示 15.19：

![](img/e073a4882197be4ab61103cbe0bcb394_779_0.png)

图 15.19：显示 SiteMapPath 控件示例

## 摘要

在本章中，描述了 ASP.NET 4.0 的三个导航控件——TreeView 控件、Menu 控件和 SiteMapPath 控件。你学习了导航控件的基础类以及其属性、方法和事件。此外，你还学习了在即时解决方案部分中这些导航控件的实现。

在下一章中，我们将讨论 ASP.NET 4.0 中可用的登录和 Web Parts 控件。

## ASP.NET 4.0 中的登录和 Web Parts 控件

| 如果你需要即时解决方案： | 请参见页码： |
|--------------------------------------|-----------|
| 使用 Login 和 LoginView 控件 | 791 |
| 使用 LoginName 和 LoginStatus 控件 | 798 |
| 使用 CreateUserWizard 控件 | 800 |
| 使用 PasswordRecovery 和 ChangePassword 控件 | 802 |
| 在代码中创建 WebPartManager 控件 | 808 |
| 在代码中创建 WebPartZone 控件 | 811 |
| 在代码中创建 CatalogZone 控件 | 813 |
| 在代码中创建 EditorZone 控件 | 815 |
| 创建自定义 Web Parts | 817 |
| 在代码中创建 ConnectionsZone 控件 | 821 |

## 深入

在当前情况下，互联网正成为执行各种任务的最广泛使用的媒介，例如交换数据和信息以及进行网上购物和银行交易。除了普通用户之外，大多数政府组织和企业完全依赖这种媒介来传输和接收关键信息并开展日常业务。所有这些信息和数据都需要防止来自非法和恶意来源的未经授权访问。网站的安全性主要通过两个过程实现，即身份验证和授权。身份验证是指识别用户身份的过程；而授权则是向已通过身份验证的用户提供访问数据库和打印机等各种资源的过程。

过去，你需要编写大量代码来创建用于对用户进行身份验证的表单和用户界面（UI），并根据用户被赋予的角色或权限显示所需页面。然而，使用标准的 ASP.NET 服务器控件创建此类表单或用户界面既繁琐又耗时。微软意识到这个问题并开发了一系列新的服务器控件，称为登录控件。要在你的网站中使用登录控件，你只需将它们拖放到 Web 表单上，这意味着无需在代码隐藏文件中编写冗长的代码。登录控件帮助你确保只有经过身份验证的用户才能访问你的网站。登录控件具有内置功能（称为 Membership 服务），用于处理与用户身份验证和授权相关的所有任务。登录控件于 ASP.NET 2.0 引入，并在 ASP.NET 的后续版本中也可用，例如 3.0、3.5 和 4.0。

ASP.NET 中的 Web Parts 控件是一组协同工作的控件，使你能够创建一个 Web 页面，最终用户可以通过更改用户界面的外观和行为来修改该页面。换句话说，Web Parts 控件使你能够构建可在运行时动态定制的灵活网站。Web Parts 是 Web 表单的对象，用户可以在其上执行多种功能，例如打开、关闭、最小化或根据需要修改 Web Parts 控件的内容、行为或外观。使用门户框架创建具有多个 Web Parts 控件的 Web 页面。

在本章中，你将学习登录控件，例如 Login、LoginView、LoginStatus、LoginName、CreateUserWizard、Password 和 ChangePassword 控件。你还将学习 Web Parts 控件，例如 WebPartManager、ProxyWebPartManager、WebPartZone、CatalogZone 和 EditorZone 控件。

### 介绍登录控件

身份验证和授权是两种不同的功能，用于确保用户安全登录网站。身份验证是识别用户的机制，而授权是为已通过身份验证的用户指定访问网站上安全资源的访问级别的机制。这些机制由一组特定的 ASP.NET 4.0 控件实现，称为登录控件。登录控件为 Web 应用程序的用户提供全方位的登录解决方案。登录控件会自动与 ASP.NET 成员资格服务交互，验证用户的凭据，并在用户通过身份验证时授予或拒绝访问权限。

Membership 服务是 ASP.NET 的重要功能，有助于你在应用程序中验证和存储用户凭据。为了对用户进行身份验证，登录控件使用 Membership 服务，其中每个用户都提供唯一的用户名和密码。在使用登录控件的 Web 应用程序中，会自动配置默认的 Membership 提供程序。换句话说，ASP.NET Membership 服务和登录控件同时工作以注册和验证用户。Membership API 可以用两个新类来描述：Membership 和 MembershipUser。Membership 类自行提供 Membership 服务，并提供创建用户、验证用户等功能。MembershipUser 类描述单个用户，并提供用于更改密码和检索最后登录日期的方法和属性。

ASP.NET Membership 服务帮助你在应用程序中实现以下功能：

- 创建新用户和密码

