

提供互操作性，因为 MSIL 代码支持任何类型的 .NET 语言。这意味着在 C# 中创建的 ASP.NET 页面中，你可以添加引用由 Visual Basic 创建的 .dll 文件。

ASP.NET 4.0 的编译架构包含众多功能，具体如下：

- 多语言支持 – 指定你可以在单个 ASP.NET 应用程序中使用不同的语言。在 ASP.NET 4.0 应用程序中，会创建多个程序集，每个程序集支持应用程序中使用的每种语言。因此，对于存储在 App_Code 文件夹中的代码，你可以为每种语言指定一个子文件夹。

- 自动编译 – 在用户首次请求网站资源时，编译 ASP.NET 应用程序及任何依赖资源。按规则，ASP.NET 应用程序为每个应用程序目录创建一个程序集，并为主目录创建一个程序集。

- 灵活部署 – 指定在部署 ASP.NET 应用程序时，你只需将应用程序的源代码复制到 Web 服务器。ASP.NET 提供了两种预编译选项。首先，你可以在部署之前编译网站，或者其次，你可以在部署之后，但在用户向网站发送请求之前编译它。ASP.NET Merge 工具（Aspnet_merge.exe）使你能够组合和管理由 ASP.NET 编译工具（Aspnet_compiler.exe）创建的程序集。该工具使你能够为部署到目标位置（例如生产服务器）的 ASP.NET Web 应用程序进行编译。ASP.NET Merge 工具在由 ASP.NET 版本 2.0 或更高版本创建的程序集上工作。它为目标网站中的每个内容文件夹或内容文件创建一个程序集。它还为部署提供了额外的灵活性。Merge 工具使你能够执行以下任务：

- 为整个网站创建一个程序集
- 为每个网站文件夹创建一个程序集并为程序集名称添加前缀
- 为仅网站 UI 元素（如页面和控件）创建一个单一程序集

使用 Merge 工具的语法如下：

```
aspnet_merge [-?]
              applicationPath
              [-keyfile filename [-delaysign]]
              [-o assemblyname | -w assemblyname | -prefix prefix]
              [-copyattrs [assemblyfile]]
              [-debug]
              [-nologo]
              [-errorstack]
              [-r]
              [-xmldocs]
              [-a]
              [-logfile logfile]
              [-allowattrs textfile]
```

- 可扩展构建系统 – 指自定义 ASP.NET 构建系统以编译自定义资源。BuildProvider 类由 ASP.NET 应用程序用于构建 .aspx 页面（ASP.NET Web 页面）、.ascx 文件（Web 用户控件文件）和全局资源。

## ASP.NET 4.0 中的动态编译

当你创建 ASP.NET 页面时，页面的整个内容会被编译成一个类，该类是 System.Web.UI.Page 类的一个实例。当用户请求该页面时，ASP.NET Framework 首先搜索要执行的 .NET 类。如果找不到该类，则可以将其编译为新的 .NET 类，该类存储在临时 ASP.NET 文件夹中。

如果再次向同一页面发送请求，则页面不会再次编译。已编译的 .NET 类将被执行。不再次编译同一页面的过程称为 ASP.NET 动态编译。如果对 ASP.NET 页面进行任何修改，.NET 类将被自动委派。换句话说，动态编译有助于在部署 Web 应用程序之前修改源代码并重新编译文件，而无需编译代码。

可编译单元。Web.config 文件中 compilation 元素的 codeSubDirectories 元素帮助你实现多语言支持功能，其中每个文件夹可以包含不同编程语言的源代码。例如，你可以通过在 Web.config 文件中使用以下代码片段来配置子文件夹以编译为单独的程序集：

```
<compilation debug="false">
  <codeSubDirectories>
    <add directoryName="CS" />
  </codeSubDirectories>
</compilation>
```

在前面的代码片段中，对 CS 子文件夹的引用不需要任何有关编程语言的信息。

## 优化动态编译

如你所知，如果你对动态编译的 ASP.NET 文件进行任何更改，它会自动使文件的缓存编译程序集失效并触发所有受影响资源的重新编译，例如 .dll 文件。然而，对于大型应用程序而言，即使更改很小，此重新编译过程也可能使应用程序在很长时间内不可用。

你可以通过在 web.config 文件中将 optimizeCompilations 属性设置为 True 来避免这种情况。这意味着在将此属性设置为 True 后，当你实施任何更改时，只有更改的文件会被重新编译。

## 动态编译的缺点

ASP.NET 应用程序中动态编译的缺点如下：

- 用户响应时间慢，因为 ASP.NET 页面和代码必须在首次请求时编译
- 在用户访问网站之前，没有手段识别任何编译时错误
- 没有创建可部署到生产服务器而无需源代码的网站编译版本的 provision

## ASP.NET 4.0 编码模型

通常，Web 表单由控件（如 Label、Button、超链接）和业务逻辑组成。你可以使用 ASP.NET 编码技术来管理这些控件和业务逻辑。ASP.NET 4.0 编码技术是指用于在 Web 应用程序中编写代码的方法。ASP.NET 4.0 提供了两种类型的编码技术，单文件页面模型和代码后置页面模型。在单文件编码方法中，开发人员直接在应用程序的 .aspx 页面中编写代码。单文件代码模型的主要缺点是，在单个文件中编写代码会导致难以阅读的 Web 页面，将表示（HTML）与功能（代码）混合在一起。此缺点在开发复杂应用程序时尤为明显。为了解决单文件页面模型的缺点，ASP.NET 引入了代码后置页面模型。在此模型中，你需要为每个 Web 页面维护单独的代码文件。一个文件存储用 VB 和 C# 等某些编程语言编写的用于实现 Web 页面功能的代码；另一个文件存储 Web 应用程序的 HTML 标记。

## 单文件页面模型

在单文件页面模型中，Web 应用程序的功能和 HTML 标记在同一文件中实现。编程代码位于包含属性 runat="server" 的脚本块中，以将其标记为 ASP.NET 应执行的代码。现在，让我们通过一个名为 SingleFileModelExampleCS 的应用程序来了解单文件页面模型。你可以在列表 13.1 中找到单文件页面模型的 Default.aspx 页面的代码：

### 列表 13.1：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<script runat="server">
void Button1_Click(Object sender, EventArgs e)
{
Label1.Text = "Clicked at " + DateTime.Now.ToString();
}
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Single File Page Model</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label id="Label1" runat="server"></asp:Label>
<asp:Button id="Button1" runat="server" onclick="Button1_Click" Text="Click Me!" />
</div>
</form>
</body>
</html>
```

在列表 13.1 中，我们将按钮的单击事件代码放在开头的 <script> 标签内。应牢记 runat="server" 属性在 <script> 标签内是强制性的，因为它会将页面发布到 Web 服务器。

现在，让我们通过按 F5 键来执行应用程序。应用程序的输出显示在 13.12 中：

![](img/e073a4882197be4ab61103cbe0bcb394_668_0.png)

### 图 13.12：显示应用程序的输出

现在，点击 Click Me! 按钮（图 13.12）。单击事件的结果显示在图 13.13 中：

