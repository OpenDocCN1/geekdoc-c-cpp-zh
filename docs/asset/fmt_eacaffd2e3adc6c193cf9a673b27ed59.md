
正如你可能猜到的那样，“表格”菜单包含一组工具，允许你在网页中进行插入、删除、选择和修改 HTML 表格。从“表格”菜单中选择“插入表格(Insert Table)”将打开如图 2-24 所示的“插入表格”对话框，允许你指定表格的属性。你可以定义行和列数、单元格内边距和间距以及边框属性。当你点击确定时，Visual Studio 会自动在你的网页中生成相应的表格 HTML。

当你选择网页中现有的表格时，“表格”菜单允许你插入和删除表格行、列和单元格。“修改(Modify)”菜单还允许你将现有单元格拆分为两个独立的单元格，将两个单元格合并为一个单元格，并配置行和列的大小。

“格式”菜单包括基本的元素格式化选项，例如访问元素的 `css` 类；设置前景色和背景颜色、字体和位置；以及将内容转换为不同类型的列表。

# 在 Visual Studio 中处理 CSS

Visual Studio 提供了许多专门设计的工具，让处理 CSS 成为一种极佳的体验。要为你的网页创建一个新样式，只需从“格式”菜单中选择“新样式(New Style)”选项。这将打开“新样式”对话框，如图 2-25 所示。

![](img/67a6707ff505c052edb96c0128fb3096_95_1.png)

图 2-24

![](img/67a6707ff505c052edb96c0128fb3096_95_2.png)

图 2-25

此对话框用于创建新样式。首先，从“选择器(Selector)”下拉列表中选择你想要创建的选择器类型，其中包含所有可用的元素类型。如果你想创建一个类（Class）或 ID 选择器，只需在选择器组合框中输入样式名称即可。

接下来，从“定义在(Define in)”框中选择你想创建样式的位置。你可以选择“当前页面(Current Page)”创建内部样式表，“新样式表(New Style Sheet)”创建外部样式表文件，或“现有样式表(Existing Style Sheet)”将样式插入到现有的样式表文件中。如果你选择“新样式表”或“现有样式表”，则必须为 URL 组合框提供值。

最后，为了使此样式应用于设计面上当前选中的一个或多个元素，请勾选“将新样式应用于文档(Apply New Style to Document)”复选框。

在你选择了要使用的选择器和定义样式的位置后，可以设置样式的属性。只需从“类别(Category)”框中选择属性类别并设置属性值即可。“预览(Preview)”区域为你提供新样式的实时预览。此外，“描述(Description)”区域显示了由 Visual Studio 创建的实际属性语法。点击确定关闭对话框。

在你开始为应用程序创建样式后，你将需要管理并将这些样式应用于应用程序中的元素。Visual Studio 包含了三个工具窗口，你可以用它们来管理样式表、将样式应用于元素，并轻松插入应用到元素的样式属性。

# 管理样式工具窗口

第一个工具是探索“管理样式(Manage Styles)”工具，你可以通过在“菜单(Menu)”视图下的 CSS 子菜单中选择“管理样式”来打开它。该工具如图 2-26 所示，可以为你提供所有样式的全局视图。

如果你检查该工具的内容，你会发现顶部部分包含两个重要的链接：“新样式(New Style)”会打开新样式对话框并允许你如前所述创建新的 CSS 样式；“附加样式表(Attach Style Sheet)”链接允许你将样式表导入网页。使用此选项会让 Visual Studio 在网页中插入 `<link>` 标签。

你必须注意 `<link>` 标签的顺序，以确保样式正确应用。

工具的下一部分包含一个预览区域，允许你查看样式的实时预览。

![](img/67a6707ff505c052edb96c0128fb3096_96_0.png)

最后，工具的底部部分显示附加到页面的样式。样式根据类型使用彩色圆点进行编码：类型选择器为绿色，类选择器绿色，ID 选择器红色。页面内的样式会在彩色圆点周围有一个圆圈。这些样式会被分组，从而很容易判断样式的定义。

此外，如图 2-26 所示，工具窗口允许你通过 CSS 导入语句查看附加到网页的样式。通过展开图中 `light.css` 节点，你可以看到该样式表中的所有样式列表。

图 2-26

# 应用样式工具窗口

帮助你在 Visual Studio 中使用 CSS 的第二个工具是“应用样式(Apply Styles)”工具窗口。配合“管理样式”工具窗口，“应用样式”工具窗口帮助你在 Visual Studio 中使用 CSS。

如图 2-27 所示的应用样式工具窗口显示了锚点标签 `<a>` 的样式。

# CSS 属性工具窗口

最后一个工具是如图 2-28 所示的“CSS 属性(CSS Properties)”窗口。这个实用的窗口向你显示了应用于元素的所有属性。窗口由两部分组成：“应用规则(Applied Rules)”列表和 CSS 属性。

# ASP.NET 控件样式化

由于 ASP.NET 控件简化了 HTML 标记的渲染，使用 CSS 对它们进行样式化非常简单。事实上，默认情况下，控件使用内联样式。你可以通过查看标准的 ASP.NET 按钮控件来观察这一操作。对像按钮这样的 ASP.NET 控件进行样式的标准方法是为暴露的样式属性提供值，如下所示：

![](img/67a6707ff505c052edb96c0128fb3096_97_0.png)

图 2-29

```asp
<asp:Button ID="Button" run="server" BackColor="#3333FF"
BorderColor="Silver" BorderStyle="Double" BorderWidth="3px"
Font-Bold="True" Font-Size="Large" ForeColor="White"
Text="Button" />
```

当 ASP 处理网页内容时，它会将按钮转换为标准的 HTML Input 标签，并且会将你设置的样式转换为 CSS 样式并应用到输入框上。按钮渲染的 HTML 和 CSS 如下：

```html
<input type="submit" name="Button" value="Button" id="Button"
style="color:White;background-color:#3333FF;border-color:Silver;
border-width:3px;
border-style:Double;font-size:Large;font-weight:bold; />
```

直接在 ASP.NET 控件上设置属性是为应用程序中的 ASP.NET 控件设置样的一种快速简单的方法。由于这些是控件上的标准属性，你也可以使用代码在运行时设置它们：

```csharp
protected void Page_Load(object sender, EventArgs e) {
    this.Button.BackColor = System.Drawing.ColorTranslator.FromHtml("#33333FF")
    this.Button.BackColor = System.Drawing.Color.Silver;
    this.Button.BorderStyle = BorderStyle.Double;
    this.Button.BorderWidth = Unit.Pixel(3);
    this.Button.Font.Bold = true;
    this.Button.Font.Size = FontUnit.Large;
    this.Button.ForeColor = System.Drawing.Color.White;
}
```

虽然使用属性为信息设置样式既简单又方便，但它也有一些缺点，特别是当你对重复控件使用相同技术时。一个缺点是，使用内联样式使得在更高、更抽象的层面上控制网站的样式变得困难。如果你想网站上的按钮具有特定的样式，通常你必须在整个网站的每一个 Button 控件上手动设置该样式。主题（Themes）可以帮助解决这个问题，但并不总是好用，特别是当你将 ASP.NET 控件与标准 HTML 控件混合使用时。

另一个缺点是控件会生成大量的重复 HTML，例如 GridView，在迭代的每个元素上使用内联样式会为你的网页添加大量的额外标记。

幸好的是，ASP.NET 服务器控件暴露了 `CssClass` 属性。该属性允许你为控件提供一个或多个类选择器。这种技术非常有帮助，而且通常比让控件渲染内联样式要好，后者你将与运行时渲染的 HTML 作斗争。列表 2-18 显示了你如何使用 `CssClass` 属性为 ASP.NET Button 控件设置样式。

# 列表 2-18：使用 CSS 为标准的 ASP.NET Button 控件设置样式

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head run="server">
<link href="SpringStyles.css" rel="stylesheet" type="text/css" />
<style>
    .search {
        color:White;
        font-weight:bold;
        background-color:Green;
    }
</style>
</head>
<body>
<form id="form1" runat="server">
<asp:Button Id="Button" runat="server" CssClass="search" Text="Button" />
</form>
</body>
</html>
```

# 第 2 章 使用 ASP.NET 进行 HTML5 和 CSS3 设计

列表 2-18（续）

# Visual Studio 2012 中的 HTML 和 CSS 改进

在每个版本的 Visual Studio 中，微软都改进了软件中的 HTML 开发能力。Visual Studio 2012 也不例外。Visual Studio 2012 为 HTML 增加了多项改进，包括但不限于：

- WAI-ARIA，允许元素包含 `role` 属性和其他以 `aria` 开头的属性。

- 匹配的 HTML 和 ASP.NET 服务器控件标签在其中一个重命名时另一个也会被重命名。

- HTML5 元素现在作为 Visual Studio 中的代码片段（snippets）可用。

- `TextBox` ASP.NET 服务器控件已更新，以支持新的 HTML5 输入类型，如 `email` 和 `datetime`。

- `FileUpload` ASP.NET 服务器控件在现代浏览器中支持多个文件上传。

Visual Studio 2012 中对 CSS 也有几项改进，包括但不限于：

- 改进的智能提示（IntelliSense），仅显示可用项目以及 CSS3 规则，例如以 `-moz` 和 `-webkit` 开头的浏览器特定规则。

- 层级缩进，以显示 CSS 规则的逻辑分离（如图 2-30 所示）。

- 注释（使用快捷键）、区域（regions）和代码片段适用于 CSS，就像适用于源代码一样。

- 新的调色板帮助你选择寻找的颜色（如图 2-31 所示）。

![](img/67a6707ff505c052edb96c0128fb3096_99_0.png)

图 2-30

# 在 Visual Studio 中处理 HTML 和 CSS

![](img/67a6707ff505c052edb96c0128fb3096_100_0.png)

图 2-31

# 页面检查器 (Page Inspector)

Page Inspector 是 Visual Studio 2012 自带的一个新工具。该工具允许开发者查看相关服务器端代码的渲染标记。也就是说，当从你的 Web Forms 或 MVC 页面选择控件时，你将看到对应的标记（如图 2-32 所示）。目前，Page Inspector 使用 Internet Explorer 9 或更高版本进行渲染。

![](img/67a6707ff505c052edb96c0128fb3096_100_1.png)

图 2-32

> 注意 第 28 章将介绍如何通过 ASP.NET 4.5 的新功能打包和最小化来进一步优化 CSS。

## 总结

CSS 是为网站添加样式的一种极方法。它是一种强大且方便的机制，结合 HTML5 使用时可以创建复杂的样式和布局。对 CSS 的全面讨论需要更多的时间和空间，因此本章重点向你展示了 HTML 和 CSS 的基本概念，以及 Visual Studio 2012 中的新功能。

本章通过介绍新元素、属性、属性值和 API提供了 HTML5 的概述。你学习了如何在实际情况中使用 HTML5 元素和属性。

接下来，我们提供了 CSS3 的概述，介绍了外部、内部和内联样式表。你学习了 CSS 提供的各种选择器类型以及 CSS 元素的基本布局和定位，包括盒模型如何影响网页元素的位置。你还学习了 HTML5 和 CSS3 的后兼容性。

最后，你回顾了 Visual Studio 中提供的工具，包括使 CSS 操作变得简单的样式管理器和 CSS 属性窗口。你学习了如何将 CSS 用于 ASP.NET 控件。你还学习了 Visual Studio 2012 和 Page Inspector 中 HTML 和 CSS 的若干新功能。

# 第 3 章 ASP.NET Web Forms 结构

本章内容包括：

- 选择应用程序位置和页面结构选项

- 处理页面指令、页面事件和应用程序文件夹

- 选择编译选项

WROX.COM 本章下载

请注意，本章中的所有代码示例均作为本书网站章节下载的一部分。

# 应用程序位置

在 ASP.NET 4.5 中，你可以选择（使用 Visual Studio 2012）创建一个映射到 IIS 虚拟目录的应用程序，或者在 IIS 之外创建一个独立应用程序。虽然早期的 Visual Studio .NET 2002/2003 IDE 强制要求对所有 Web 使用 IIS，但 Visual Studio 2008/2010（以及 Visual Web Developer 2008/2010 Express 版）包含了一个名为 Cassini 的内置 Web 服务器用于开发托管，类似于过去在 ASP.NET WebMatrix 中使用的那种。在 Visual Studio 2012 中，内置 Web 服务器是 IIS Express。

> 注意：IIS Express 是一个轻量级、自包含的 IIS 版本，针对开发和 Visual Studio 进行了优化。关于它的更多信息可以在 www.iis.net 找到。如果你像后文第 35 章讨论的那样下载 WebMatrix，也会安装 IIS。

下面的章节将向你展示如何使用 Visual Studio 2012 自带的 IIS Express。

## 使用文件 (IIS Express)

默认情况下，Visual Studio 2012 使用 IIS Express 构建应用程序。当你在 IDE 中选择“文件(File)->新建(New)->Web 站点(Web Site)”时，可以看到这一点。如果你使用的是 Windows 8，默认的应用程序位置位于 `C:\Users\JasonGaylord\Documents\Visual Studio\WebSites`（如图 3-1 所示）。它不像 Visual Studio .NET 2002/2003 那样位于 `C:\netpub\root`。默认情况下，你构建的任何位于 `C:\Users\JasonGaylord\Documents\Visual Studio 2012\WebSites`（或其他任何文件夹）的站点都使用内置于 Visual Studio 2012 的 IIS Express。如果你使用 Visual Studio 2012 的内置 Web 服务器，并不受限于 Websites 文件夹。相反，你可以创建并使用任何喜欢的文件夹。

要更改此，你有几个选项。点击“新建 Web 站点”对话框中的“浏览(Browse)”按钮。打开的“位置(Location)”对话框如如图 3-1 所示。

![](img/67a6707ff505c052edb96c0128fb3096_103_0.png)

图 3-1

如果你继续使用 Visual Studio 2012 提供的内置 IIS Express，你可以从此对话框中为你的网站选择新位置。要选择新位置，请选择一个新文件夹并将 `.axpx` 页面以及任何其他关联文件保存到此目录。使用 Visual Studio 2012 时，你可以完全从此位置运行你的应用程序。如果你没有 Web 服务器的访问权限，这种处理创建的 ASP.NET 页面的方法是理想的，因为它允许你构建运行不在具有完整版 IIS 机器上的应用程序。

## 文件系统

选择你想要打开的文件夹。

![](img/67a6707ff505c052edb96c0128fb3096_104_0.png)

3-2

创建新网站后，你可以在 Visual Studio 属性窗中修改 IIS Express 设置。图 3-3 所示了一个示例。

## 使用 IIS

从“选择位置(Choose Location)”对话框（如图 3-4 所示），你可以更改应用程序的保存位置以及你采用的 Web 服务器类型。要使用 IIS，请选择对话框中的 IIS 按钮。这将更改文本区域的结果，向你显示机器上所有的虚拟应用程序根列表。

![](img/67a6707ff505c052edb96c0128fb3096_104_1.png)

图 3-3

> 注意：如果你想查看本地 IIS 实例，需要以管理员用户身份运行 Visual Studio。
