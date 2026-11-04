
这个控件通过提供框架来协助你。你仍然需要提供地图。通常，人们会使用单独的图像。

- **日历：** 日历控件只是一个文本框，可帮助用户正确设置日期格式。它运行良好。它还有大量格式设置选项——可在属性面板中查看它们。

还有其他控件。我可能已经介绍了你将在工具箱中看到的所有内容，但外面还有更多。你需要记住的是基础知识——它们是具有 ASP.NET 实现和 HTML 输出的可见控件。你可以使用属性面板、标记或 C# 代码来更改属性。并且你可以将它们绑定到代码中的对象——我们将在本章后面讨论。

## 使用提交按钮提交输入

将所有输入放入表单后，你需要用户将其发送给你。基本方法是通过提交按钮。

在第 1 章中，我讨论了 PostBack 事件，以及 Microsoft 如何使用 JavaScript 改变将表单回发到服务器的工作方式。提交按钮就是实现这一点的方式。

明确一点——任何控件都可以导致回发。如果你为控件中的某个事件设置了事件处理程序，它就会导致回发。一旦表单数据返回到服务器，你可以在任何时候保存它。我们使用提交按钮，因为这是用户所习惯的。

ASP.NET 默认控件有三个按钮。

- **Button** 正如其名——HTML 中 type 为 submit 的输入。
- **ImageButton** 是一个按钮控件，具有用于图像的内置 src 属性。
- **LinkButton** 只是显示一个 HTML 锚点，并将其当作按钮对待。

在我们接受用户输入的几乎每个页面中，都会使用其中之一。大多数时候，用户期望如此。

## 数据绑定

将数据放入 Web 页面中的控件还不够。在数据输入后，需要某种方式来持久保存（保存以便重用）该信息。数据绑定就是答案。

数据绑定告诉控件从基础类的哪个成员获取数据。例如，如果你有一个 Apple 对象集合，其中有一个 Color 属性，你想在文本框中显示它，可以将值 Apple.Color 绑定到 Text 属性。

但事情会变得更有趣。假设你想提供一个颜色列表，并允许用户选择相关对象的颜色。你可以通过将集合列表和选定值绑定到列表控件的 SelectedItem 属性来实现。如果你想显示颜色本身，可以绑定到文本控件的 FontColor 属性。

## 为绑定设置标记

回到 Active Server Page 时代，你只需将数据打印到页面上，就能把所有数据放在那里。听起来简单，但它有很多问题。最重要的是，你的表单必须非常了解它正在显示的数据。这是一件坏事。不管怎样，这样做所用的格式是

```
<%= ThisIsWhatIWantToPrint %>
```

如果你需要列表，就在周围的代码中循环。如果你需要方法结果，就直接把方法放在那里。所见即所得。

数据绑定是将数据显示到屏幕上的更开明的方式。ASP.NET 内置的控件知道如何自行处理数据，只要该数据满足一些基本的具体要求。

数据绑定通过将控件的属性设置为基础类的成员来完成。对于单个控件（如文本框），只需设置相关属性，如下所示：

```
<asp:Label ID="Label1" runat="server" Text='<%# IAmBindingToThisVariable %>' />
```

如果要绑定到重复控件（如 Grid 或 ListBox），则设置 DataSource 属性。我将在下一节“代码中的绑定”中向你展示如何操作。

你绑定到的变量需要位于代码隐藏文件中，并且是公共的。如果不是，你将遇到运行时错误。这也是为什么在代码中绑定是个好主意，我们将在下一节中这样做。

现在，我们来谈谈标记中的绑定。要设置用于绑定的标记，你需要做的就是：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_696_0.png)

1. 在我们一直向其添加带控件页面的 Chapter 3 Web 项目中，右键单击并依次选择“添加新项”和“类”。
我将自己的类命名为 Show。

2. 单击“确定”，然后将这个简单的数据类放入其中。这个类只是示例——它可以是数据库、数据类或实体框架模型。

```csharp
using System;

namespace Chapter_3
{
public class Show
{
public int ID { get; set; }
public String ShowTitle { get; set; }
public String EpisodeTitle { get; set; }
public DateTime ScheduledTime { get; set; }
public int Channel { get; set; }
}
}
```

3. 打开 Chapter 3 项目中的 Text.aspx 文件。

4. 双击设计界面以转到代码隐藏文件。
如果 Page_Load 中已经出现任何代码，你可以将其删除。

5. 向 Page_Load 添加代码以创建模拟的 Show 对象。
在真实项目中，你会从数据库或服务层获取此对象。对于此示例，我只使用模拟代码：

```csharp
Show show = new Show { ID = 1, Channel = 5,
EpisodeTitle = "ASP.NET Databinding", ScheduledTime
= new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle =
"The C# Show" };
```

6. 我们需要告诉页面我们将要进行数据绑定。在 Page_Load 末尾添加 Page.DataBind() 调用。
完成后的方法如下所示：

```csharp
protected void Page_Load(object sender, EventArgs e)
{
Show show = new Show { ID = 1, Channel = 5, EpisodeTitle =
"ASP.NET Databinding", ScheduledTime = new DateTime(2009, 4, 12, 12,
0, 0), ShowTitle = "The C# Show" };
Page.DataBind();
}
```

7. 在设计器中切换到标记。

8. Text 字段获得绑定的标记。我们可以直接给它属性，如下所示：

```aspx
<asp:Label ID="Label1" runat="server" Text="<%# show.EpisodeTitle %>"></asp:Label>
```

这不是绑定事物的有趣方式。它很好，因为你可以编辑绑定而无需重新编译，但有趣的方式是在 C# 代码中。在 C# 代码中完成它更可读、更易管理。有时会分别使用这两种方式，但这是一本 C# 书。我们至少可以关注代码隐藏文件，对吧？

## 使用代码隐藏文件进行数据绑定

与其在标记中直接设置属性，我们可以在代码隐藏文件中将其设置为等于某个值。对于重复控件，我们可以在该控件的 C# 代码中设置 DataSource 属性。然后，当我们绑定页面时，它会使用该值从代码隐藏文件中加载正确的值。

不过请记住，对于 Label 的 Text 属性（例如），这只是简单的数据绑定。我只是在设置一个值。

让我们用前面的示例来试试。只需按照以下步骤操作：

1. 保持标签文本简单——只需去掉 Text 属性，如下所示：

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Text.aspx.cs" Inherits="Chapter_3.Text" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
This is some text.<br />
<asp:Label ID="Label1" runat="server" />
</div>
</form>
</body>
</html>
```

2. 在代码隐藏文件中，将 Text 属性设置为等于你要绑定到的控件上的属性。

注意，页面没有 DataBind 命令：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
```

```csharp
namespace Chapter_3
{
    public partial class Text : System.Web.UI.Page
    {
        public Show show;
        protected void Page_Load(object sender, EventArgs e)
        {
            show = new Show { ID = 1, Channel = 5, EpisodeTitle = "*ASP.NET DataBinding*", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" };
            Label1.Text = show.EpisodeTitle;
        }
    }
}
```

3. 运行应用程序以查看值被设置。

这运行良好，但请记住，这只是简单的数据绑定。它只是在设置值。完整的数据绑定适用于具有重复属性的控件。

## 使用常用绑定控件

在讲了这么多关于标签的内容之后，我们来谈谈数据绑定真正擅长什么——集合。数据绑定非常适合处理项组，并绑定到 HTML 中的重复结构。

数据绑定的典型示例是 DataGrid 控件。如果一切设置正确，你就可以对网格的外观进行出色的控制。如果命名不正确，你仍然可以选择以默认样式显示所有数据。那么让我们开始吧。要创建数据绑定网格，请按照以下步骤操作：

1. 向项目添加一个名为 `Grid.aspx` 的新 ASPX 文件。
2. 切换到设计视图。
3. 打开工具箱的“数据”部分，并将 `GridView` 拖到设计界面上。
4. 双击设计界面以切换到代码视图，并获取页面加载事件处理程序。
5. 在页面加载事件处理程序中创建一个模拟的 *节目* 集合。我使用了 *Show* 的泛型列表。

```csharp
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "*ASP.NET DataBinding*", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "*ASP.NET Styling*", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "*Inheritance*", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "*Learning C#*" });
}
```
