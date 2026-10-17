
ASP.NET 的演进仍在！从 Active Server Pages 3.0 到 ASP.NET 1.0 的跨越至少可以说是革命性的。现在，随着 ASP.NET 最新版本——版本 3.5 的发布，这场革命仍在继续。ASP.NET 1.0 的最初引入从根本上改变了 Web 编程模型。而 ASP.NET 3.5 在提高您的工作效率方面，也具有同样的革命性意义。长期以来，ASP.NET 的首要目标是让您能够使用最少的代码构建强大、安全的动态应用程序。尽管此本书涵盖了 ASP.NET 3.5 提供的新功能，但它也涵盖了 ASP.NET 技术的所有内容。

如果你是 ASP.NET 的新手，并首次在 ASP.NET 3.5 中构建你的第一组应用程序，你可能会被它提供的大量精良服务器控件感到惊讶。你可能会对它能够让您通过一系列数据提供程序更有效地处理数据而惊叹。你可能会对您能够多很好地构建安全性和个性化功能而印象深刻。

然而，ASP.NET 3.5 的卓越能力并不仅于此。本章将介绍许多方便处理 ASP.NET 页面和应用程序的令人兴奋的选项。作为开发者，启动项目时应该采取的第一步之一是熟悉你正在在此构建的基础以及用于自定义该基础的可用选项。

# 应用位置选项

通过 ASP.NET 3.5，您有一个选项——使用 `Visual Studio 2008`——创建一个具有映射到 `IIS` 的虚拟目录的应用程序，或者在 `IIS` 范围之外创建一个独立应用程序。早期的 `Visual Studio .NET 2002/2003` IDE 强制开发者对所有 Web 应用程序使用 `IIS`，而 `Visual Studio 2008`（确切地说，还包括 `Visual Web Developer 2008 Express`）包含了一个内置的 Web 服务器，你可以将其用于开发，就像过去在使用 `ASP.NET Web Matrix` 时使用的那样。

## 第 1 章：应用程序与页面框架

此内置 Web 服务器之前向开发者展示过一个名为 `Cassini` 的代码示例。事实上，这个微型 Web 服务器的代码可以从 `www.asp.net` 上的 ASP.NET 网站免费下载。

接下来的部分将展示如何使用 `Visual Studio 2008` 自带的内置 Web 服务器。

### 内置 Web 服务器

默认情况下，`Visual Studio 2008` 在不使用 `IIS` 的情况下构建应用程序。如果你使用 Windows Vista，当你选择 `C:\Bill\Documents\Visual Studio 2008\WebSites` 时，可以看到这一点（如图 1-1 所示）。它不是 `Visual Studio .NET 2002/2003` 中那样的 `C:\inetpub\wwwroot`。默认情况下，您在 `C:\Users\Bill\Visual Studio 2008\WebSites`（或您创建的任何文件夹）内部构建并保留的站点都使用 `Visual Studio 2008` 的内置 Web 服务器。如果你使用 `Visual Studio 2008` 的内置 Web 服务器，你就不被限于 `Websites` 文件夹，你可以创建任何

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_62_0.png)

要更改此默认设置，你有几个选项。点击“新建 Web站点”`New Web Site` 对话框中的“浏览”`Browse` 按钮，这将弹出“选择位置”`Choose Location` 对话框，如图 1-2 所示。

如果你继续使用 `Visual Studio 2008` 提供的内置 Web 服务器，你可以从此对话框为你的 Web 应用程序选择一个新位置。要选择新位置，请选择新文件夹并将你的 `.aspx` 页面以及其他关联文件保存到此目录。使用 `Visual Studio 2008` 时，你可以完全从此位置运行你的应用程序。这种处理你创建的 ASP.NET 页面的方法对于没有 Web 服务器访问权限的人是理想的——它使你能够构建不驻在具有 `IIS` 机器上的应用程序。这意味着你可以在 Windows XP 家庭版等操作系统上开发 ASP.NET 应用程序。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_63_0.png)

图 1-2

### IIS

从“选择位置”对话框中，你也可以更改应用程序的保存位置以及你的应用程序采用的 Web 服务器类型。要使用 `IIS`（你可能在你在使用 `Visual Studio .NET 2002/2003` 时已经这样做过），请点击对话框中的 `IIS` 按钮。这将更改文本区域的结果，向你显示机器上所有虚拟应用程序根的列表。如果你想使用本地 `IIS`，则需要以管理员身份运行 `Visual Studio`。

要为你的应用程序创建一个虚拟根，请突出显示默认站点 `Default Web Site`。对话框顶部会出现两个可访问的按钮（见图 1-3）。从左到右看，对话框右上角的第一个按钮用于创建“新应用程序”`New application`——或虚拟根。此按钮显示为框内的地球图标。第二个按钮允许你为你创建的任何虚拟根创建虚拟目录。第三个按钮是“删除”`Delete` 按钮，它允许你删除服务器上的任何选定目录或虚拟根。

在你创建了虚拟目录后，点击“打开”`Open` 按钮。`Visual Studio 2008` 将通过标准过程创建你的应用程序。然而，现在，你的应用程序将不再依赖 ASP.NET 3.5 的内置 Web 服务器，而是将使用 `IIS`。

当你调用应用程序时，它包含像 `http://localhost/MyWeb/Default.aspx` 这样的 URL。

### FTP

`FTP` 不仅可以在“选择位置”对话框中决定应用程序的保存位置以及你的应用程序采用的 Web 服务器类型。

## 第一章：应用程序与页面框架

### 列表 1-1：一个典型的 ASP.NET 1.0/1 .aspage 文件

```vb
<%@ Language="vb" AutoEventWireup="false" CodeBehind="WebForm.aspx.vb"
Inherits="Web.Application.WebForm" %>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html
<Head>
  <title>WebForm</title>
  <meta name="GENERATOR" content="Microsoft Visual Studio .NET 7.1*">
  <meta name="CODE_LANGUAGE" content="Visual Basic .NET 7.1*">
  <meta name="defaultClientScript" content="JavaScript">
  <meta name="vs_targetSchema" content="schemas.microsoft.com/intellellisense/ie5">
</Head>
<body
  <form id="Form" method="post" runat="server">
    <p>What is your name?<br>
    <asp:TextBox id="TextBox1" runat="server"></asp:TextBox><br>
    <asp:Button id="Button1" runat="server" Text="Submit"></asp:Button></p>
    <p><asp:Label id="Label" runat="server"></asp:Label></p>
  </form>
</body>
</html>
```

在 `Visual Studio .NET 2002/2003` 中为 `.aspx` 页面创建的代码后台文件如列表 1-2 所示。

### 列表 1-2：一个典型的 ASP.NET 1.0/1 .asx/.aspx.cs 页面

```vb
Public Class WebForm
Inherits System.Web.UI.Page
```
