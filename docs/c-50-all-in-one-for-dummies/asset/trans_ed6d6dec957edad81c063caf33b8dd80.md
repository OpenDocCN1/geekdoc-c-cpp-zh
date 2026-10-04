

# 向用户显示内容 679

![](img/6df7bb88e9302e98442acc219cfbd7fc_704_0.png)

**图 3-1：**
这里有文本，还有：

第六卷
第 3 章
体验开发
控制你的

## ## 7. 通过设置 Text 属性，在 Page.Load 事件处理程序中更改标签的值。

新的处理程序应该像这样：

```assembly
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

namespace WebControls
{
    public partial class Text : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Label1.Text = "This is some text from the codebehind";
        }
    }
}
```

## ## 8. 按 <F5> 启动应用程序。

你会看到标签文本是由 C# 代码设置的。

如何在标签和文本之间做选择？这通常很容易。如果文本需要根据用户或服务器的输入发生变化，请使用标签。如果文本是静态的，请使用文本。从数据库加载的条目的描述？那是标签。你 CEO 的简介？那是文本。

# 向用户显示内容

# 图片

在标准网站内容的领域中，图片与文本并列。这是一个复杂的话题，因为很少有程序员是图形艺术家，而且制作出既契合又美观的图片是很困难的。

尽管如此，有时你只是想在页面上显示一张图片。和处理文本一样，你有两种方法可以这一点。（好吧，不止于两种。）你可以使用 HTML `<img>` 标签，也可以使用 ASP.NET Image 控件。

有什么区别吗？和文本是一样的：如果你需要一个可以从 C# 端管理的图像，请使用图像控件——例如产品图片。如果它只是一张静态图片，比如你 CEO 的照片，你可以使用 HTML 标签。

按照以下步骤使用 ASP.Net 的 Image 控件添加图片：

- 1. 右键点击项目并选择“添加：现有项”（Add:Existing Item），向项目添加两张图片。你可以找到图片或下载一些。我用了一架鼓和一个大号。（现在是大学足球赛季！）
- 2. 添加一个名为 Images.aspx 的新页面。
- 3. 将其中一张图片直接拖入表示 div 的框中。你会得到“可访问性属性”（Accessibility Properties）对话框，然后图片就会直接显示。
- 4. 多按几次回键留出一些空间。
- 5. 从工具箱（Toolbox）将一个图像控件拖到光标所在的页面。它应该显示为损坏的图片。没关系。
- 6. 双击页面其他地方获取 Page.Load 事件处理程序并切换到代码视图（Code View）。
- 7. 就像我在 Text 示例中做的那样，设置控件的可见性属性。在这种情况下，它是 ImageUrl。新代码应该像这样：

```assembly
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebControls
{
    public partial class Images : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Image.ImageUrl = "tuba.gif";
        }
    }
}
```

- 8. 在解决方案资源管理器中右键点击 Images.aspx 页面，从上下文菜单中选择“设启动项”（Set As Start）。
- 9. 按 <F5> 查看其运行情况。

到这里你可能已经掌握了思路。你可以使用 HTML 并设置静态值，也可以使用 ASP.NET 控件并设置动态值。在这些示例中，你显然只是“静态”的动态值，但你可以从 Web 服务、数据库，甚至是计算这些值。图片可以从目录列出。文本可以生成并读取到表格中。选项是无尽的。

# 面板和多视图

管理所有这些文本块和图片可能会很困难。ASP.NET 许多工具来帮助，包括以下两种：

- 面板（Panels）只是你可以在后台代码中管理的 div。与你在前一节中添加的文本和图片一样，面板可以在 C# 中命名和控制。服务器会在向浏览器发送 HTML 之前处理更改。这有助于将内容划分为易管理的组。
- 多视图（Multiews）本质上是包含许多面板的容器。你可以将它们用于向导（wizards）和标签分组。它们有助于管理面板，从而帮助管理内容。更多信息请参阅 ASP.NET 的 MSDN。

从客户端的角度来看，面板和多视图实际上是相同的结构，但它们为开发者提供了几个选项。例如，多视图默认只显示它的一种视图，而你必须隐藏未使用的面板。

# 表格

表格的工作与其他 Web 控件类似。在 HTML 中，你有基础的 `<table>`、`<tr>` 和 `<td>` 标签。在 ASP.NET 中，有一个 Table 控件，带有 TableRows 和 TableCells。如果你添加一个 ASP.NET 表格，它看起来像这样：

# 682 从用户获取输入

```asp
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Tables.cs" Inherits="Tables" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/html1/transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Tables</title>
</head>
<body>
<form id="form1" runat="server">
<asp:Table id="Table1" runat="server">
<asp:TableRow>
<asp:TableCell>Header 1</asp:TableCell>
<asp:TableCell>Header 2</asp:TableCell>
</asp:TableRow>
<asp:TableRow>
<asp:TableCell>Cell 1,1</asp:TableCell>
<asp:TableCell>Cell 1,2</asp:TableCell>
</asp:TableRow>
</asp:Table>
</form>
</body>
</html>
```

所以创建表格的方法是什么？嗯，你可以命名行和单元格并在 C# 中管理它们。坦率说，我不建议这样做。表格适用于两个用途——布局和表格数据。布局已经被 CSS 取代。

对于表格数据，表格仍然有效。不过，有一个更好的解决方案。GridView（位于数据部分）同样强大，而且是可以绑定的。我将在本章后面的“数据绑定”部分中详细讨论。

# 从用户获取输入

获取用户输入是 Web 开发者执行最重要的流程之一。数据交互 Web 全是交互性的；Web 2.0 全是交互性的。获取用户信息是一项工作。

# 从用户获取输入 683

你可以有很多方法从用户获取输入，但有一组控件被认为是用户输入。你会经常使用这些控件。

# 使用输入控件

从用户收集数据最明显的形式是文本框，如图 3-2 所示。在 HTML 中，有三个控件：textbox、password 和 textarea。ASP.NET 的 TextBox 控件处理所有这些。TextMode 告诉它如何渲染。

要使用 TextBox 控件，从工具箱将其拖入设计器。你可以在 ASP.NET 标记、属性面板或 C# 代码中更改控件实例——另一个重要的元素。

你最感兴趣的属性包括

- **ID**: 在 C# 代码中引用控件的名称。这需要先设置，才能使用控件。
- **TextMode**: 决定了渲染何种类型的文本框。
- **MaxLength**: 用户在字段可以使用最大字符数。注意，当 TextMode 定义为 TextArea 时，此属性无效。
- **Height 和 Width**: 文本框在页面上显示的尺寸。
- **Css**: 控件渲染时使用的样式表类。必须与样式表配合使用。

