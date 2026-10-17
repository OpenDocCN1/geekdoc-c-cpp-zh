
## 验证服务器控件客户端行为控制

在许多情况下，验证服务器控件会为客户端自动提供客户端验证（如果请求的容器恰当处理生成的 JavaScript），你有时需要一种方法来控制这种行为。关闭这些控件的客户端功能是完全可能的，这样它们就不会独立地向请求者发送客户端功能。例如，你可能希望所有的验证都在服务器上完成，无论请求的容器提供什么功能。

你可以通过以下几种方法来关闭此功能。

### 控件级别控制

每个验证服务器控件都有一个 `EnableClientScript` 属性。该属性默认设置为 `True`，但将其设置为 `False` 可以防止控件向客户端发送用于验证的 JavaScript 函数。相反，验证将在服务器上进行。其用法在列表 4-20 所示。

# 第 4 章：验证服务器控件

```html
<title>验证组</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<h1>St. Louis .NET 用户组</h1>
<asp:Username>
<asp:TextBox ID="TextBox1" runat="server"/></asp:TextBox>&nbsp; 密码:
<asp:TextBox ID="TextBox2" runat="server" TextMode="Password"/></asp:TextBox>&nbsp;
<asp:Button ID="Button1" runat="server" Text="登录" ValidationGroup="Login" />
<br />
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" Text="您必须提交用户名!" ControlToValidate="TextBox1" ValidationGroup="Login"></asp:RequiredFieldValidator>
<br />
<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" Text="您必须提交密码!" ControlToValidate="TextBox2" ValidationGroup="Login"></asp:RequiredFieldValidator>
<p>
我们的会议几乎总是安排在每个月的最后一个周一举行。有时我们会遇到假期或极端情况，会将时间改到另一个晚上，但这种情况非常罕见。请查看网站主页获取详情。演讲兴趣小组会在该月的其他时间开会。请查看 SIG 页面并访问各自的网站获取更多信息。
您也可以查看我们的日历页面获取活动摘要。<br />
</p>
<h2>电子邮箱：</h2>
<asp:Email>
<asp:TextBox ID="TextBox3" runat="server"/></asp:TextBox>&nbsp;
<asp:Button ID="Button2" runat="server" Text="注册" ValidationGroup="Newsletter" />
<br />
<asp:RegularExpressionValidator ID="RegularExpressionValidator1" runat="server" Text="您必须提交格式正确的电子邮箱地址" ControlToValidate="TextBox3" ValidationGroup="Newsletter" ValidationExpression="^([\w-\.]+)@([\w-]+\.)+[a-z]{2,4}$"></asp:RegularExpressionValidator>
<br />
<asp:RequiredFieldValidator ID="RequiredField3" runat="server" Text="您忘记输入邮箱地址了!" ControlToValidate="TextBox3" ValidationGroup="Newsletter"></asp:RequiredFieldValidator>
</p>
</div>
</form>
</body>
</html>
```

此页面上的 `ValidationGroup` 属性以粗体形式显示。你可以看到该属性接受一个字符串值。请注意，不仅是验证控件具有此新属性。核心服务器控件也拥有 `ValidationGroup` 属性，因为像按钮这样的控件可以与特定的验证组关联。

在此示例中，每个按钮都有不同的验证组分配。Login 表单上的第一个按钮使用 `"Login"` 作为值，而表单上的第二个按钮使用 `"Newsletter"` 作为值。然后，每个验证控件都与这些验证组之一关联。由于当用户点击页面上的登录按钮时，ASP.NET 会识别出它应该只与具有相同验证组的服务器控件一起工作。ASP.NET 会忽略分配给其他验证组的验证控件。

使用此增强功能，你可以拥有多组验证规则，这些规则仅在你希望它们触发时触发。

验证控件的另一个强大功能是名为 `SetFocusError` 的属性。该属性接受一个布尔值，如果在提交表单时抛出验证错误，该属性会将焦点放在接收错误的元素上。`SetFocusError` 属性在以下示例中使用：

```asp
<asp:RequiredFieldValidator Id="RequiredValidator1" Runat="server" Text="* 您必须提交用户名!" ControlToValidate="TextBox1" ValidationGroup="Login" SetFocusError="True"></asp:RequiredFieldValidator>
```

如果 `RequiredFieldValidator` 因为最终用户没有在 `TextBox1` 中输入值而抛出错误，页面将重绘并将焦点置于 `TextBox1`。

如果你在页面上有多个 `SetFocusOnError` 属性设置为 `True` 的验证控件，并且发生了多个验证错误，则具有验证错误的最上方表单元素将获得焦点。在上一个示例中，如果用户名框 `TextBox1` 和密码框 `TextBox2` 都关联了验证错误，则页面焦点将分配给用户名框，因为它是表单上第一个带有错误的控件。

## 总结

验证控件对于从 Server Pages 迁移到 ASP.NET 的开发者来说是一个受欢迎的补充。它们在一个简单易用的包中带来了许多功能，就像 .NET 世界中的大多数事物一样，你可以轻松地让它们的外观和行为完全符合你的设想。

记住，在应用程序中使用表单的目的是收集数据，但如果数据无效，这种数据收集就没有意义。这意味着你必须建立验证规则，并通过一系列不同的控件——验证服务器控件——在你的表单中实现这些规则。

本章详细介绍了各种验证控件，包括：

- `RequiredFieldValidator`
- `CompareValidator`
- `RangeValidator`
- `RegularExpressionValidator`
- `CustomValidator`
- `ValidationSummary`

除了查看基础验证控件外，本章还讨论了如何应用客户端验证和服务器端验证。

# 第 5 章：使用主页

视觉继承是母页的一大优势。本章将介绍如何使用母页来减少代码重复并保持你网站的一致性。

## 为什么你需要主页？

大多数网站都有公共元素，例如页眉、页脚和导航栏。与其在每个页面上重复这些元素，你可以在母页中定义一次它们。单个页面随后使用母页，这使得维护和更新你的网站变得容易得多。

## 主页的优势

主页允许你创建复杂且动态的网站设计。你可以在母页中定义网站的布局，然后在各个页面上填充内容。这确保了你的网站具有统一的外观。

## 如何使用主页

要使用主页，你首先需要创建一个定义公共元素的母页文件。然后创建使用母页的内容页。这允许你专注于每个页的内容，而无需担心重复的代码。

以前使用包含文件的问题是，它们必须考虑到头部包含文件中的新的 HTML 标签。这些标签必须添加到主文档中或包含文件中。你可以使用：

```html
<!--#include file="header.asp" -->
```

这允许你将头部文件的内容包含到页面中。然而，主页提供了一种更强大、更有结构的方法来管理跨越网站的公共元素。

# 第 5 章：使用主页 Master Pages

随着 2000 年 ASP.NET 1.0 的引入，开发者开始使用用户控件来封装 Web 页面的公共部分。例如，你可以通过简单地拖放每个所需的这些代码部分，来构建一个包含页眉、导航和页脚部分的 Web 页面。

这种技术行之有效，但也带来了一些问题。到了 Visual Studio 2005 和 ASP.NET 2.0，用户控件引起了与包含文件类似的问题。当你在 Web 页面的设计视图中工作时，Visual Studio .NET 2002 和 2003 中的页面公共区域仅以灰色框的形式显示。这使得构建页面变得更加困难。在编译并在浏览器中运行页面之前，你无法直观地看到正在构建的页面外观。用户控件也面临与包含文件相同的问题——你必须在两个单独文件中匹配 HTML 标签的开始和结束。

针对包含文件和用户控件的问题，ASP.NET 团队开发了主页的概念——这是一种将模板应用于应用程序的卓越方式。它们反转了开发者解决问题的方法。主页存在于你开发的页面之外，而用户控件存在于页面内部，并注定会重复。这些主页在你在页面间携带的公共区域与每个页面独有的内容区域之间划出了一条清晰的界限。

## 主页的基础

主页提供模板的一种简单方法，该模板可以供应用程序中任意数量的 ASP.NET 页面使用。通过使用主页，你创建一个主文件，该文件是子页面或内容页面引用的模板。主页使用 `.master` 文件扩展名，而内容页面使用你熟悉的 `.aspx` 文件扩展；内容页面在该文件的指令中进行此类声明。

你可以将任何想要包含在 `.master` 文件模板中的内容。这可以包括整个 Web 应用程序使用的页眉、导航和页脚部分。内容页面包含主页元素之外的所有内容。在运行时，ASP.NET 引擎会将这些元素合并成一个单一页面供最终用户。

使用主页的好处之一是，当你创建内容页面时，可以在 IDE 中直观地看到模板。由于你可以在工作时看到整个页面，因此作为模板开发内容页面要容易得多。当你处理内容页面时，所有模板化项目都显示为灰色且不可编辑。唯一可以更改的项目在模板中清晰显示。这些可操作区域被称为内容区域，它们最初定义在主页本身。在主页内部，你指定了内容页面可以使用区域。如果你愿意，你的主页中可以有多个内容区域。

## 编写主页

现在看之前图 5-3 所示的主页。你可以在文本的编辑器中创建它，也可以使用 Visual Studio 2008。在本章中，你将看到如何操作。主页以与 `.aspx` 相同的方式添加到你的项目中——当你添加新文件时，选择“主页”，如图 5-4 所示。

由于与任何其他 `.aspx` 页面非常相似，“添加新建项”对话允许你从内联编码模型选择，或将其放在单独文件中。不将代码放在单独文件中意味着你将为创建的页面使用内联模型。选择在单独文件中使用代码意味着你使用关联的 `.master.vb` 或 `.master.cs` 文件。你还有将主页嵌套另一个主页的选项，这在本章也会涵盖。使用内联模型的示例主页如代码 5-1 所示。

# 代码 5-1：示例主页

```asp
<%@ Master Language="VB" %>

<script runat="server">
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>My Company Page</title>
<asp:ContentPlaceholder id="head" runat="server">
</asp:ContentPlaceholder>
</head>
<body>
<form id="form1" runat="server">
<table cellpadding="3" border="1">
<tr bgcolor="silver">
<td colspan="2">
<h1>My Company Home Page</h1>
</td>
</tr>
<tr>
<td>
<asp:ContentPlaceholder ID="ContentPlaceholder1" runat="server">
</asp:ContentPlaceholder>
</td>
</tr>
<tr>
<td>
<asp:ContentPlaceholder ID="ContentPlaceholder2" runat="server">
</asp:ContentPlaceholder>
</td>
</tr>
<tr>
<td colspan="2">
Copyright 2008 - My Company
</td>
</tr>
</table>
</form>
</body>
</html>
```

这是一个简单的主页。在 Visual Studio 2008 中创建主页的伟大之处在于，你可以在代码视图中处理主页，也可以切换到设计视图像创建其他 ASP.NET 页面一样创建主页。

首先查看主页的代码。第一行是指令：

```asp
<%@ Master Language="VB" %>
```
