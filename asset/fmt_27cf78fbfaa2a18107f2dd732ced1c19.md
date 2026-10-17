
为了在 C# 代码中设置属性，我将引用在属性面板中设置的 ID。如果我使用默认值（请勿在实际案例中这样做，请为控件命名真实的名称），配置第一个文本框可能像这样：

```csharp
public class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs args)
    {
        TextBox1.MaxLength = 20;
        TextBox1.Height = 22;
        TextBox1.Width = 135;
        TextBox1.Enabled = true;
    }
}
```

## 685 获取用户输入

### 使用单项选择控件

在收集了文本后，下一种常见的用户输入收集操作是要求他们从列表中选择一个项目。在 HTML 中，你可以使用复选框、单选按钮或下拉列表来实现（参见图 3-3）。

ASP.NET 提供了所有这些项目：

- **布尔复选框：** 这只是一个复选框，答案为“是”或“否”。尽管只有一个项目可选择，但它仍然被视为单项选择，并用于在 C# 代码中表示布尔值。它由复选框控件表示。
- **单选按钮列表：** 单选按钮的好处在于，它们可以防止用户在看到所有选项的同时选择多个项目。列表是一个非常有意思的野兽，因为它们可以绑定到集合上。我将在稍后的“数据绑定”章节中介绍这一内容。该控件是 `RadioButtonList`。
- **下拉列表：** 由下拉控件表示，这种列表允许用户选择查看并选取一个项目，然后列表会关闭。它也可以绑定到集合上。

![](img/6df7bb88e9302e98442acc219cfbd7fc_710_0.png)

图 3-3：单项选择器。

## 686 获取用户输入

这是这三者的代码。注意，下拉列表（`todolist`）和单选按钮（`radiobutton`）使用列表控件来渲染项目。

```asp
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="SingleItem.aspx.cs"
Inherits="WebControls.SingleItem %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<div id="form" runat="server">
<br />
1. The Checkbox<br />
<asp:CheckBox Id="Checkbox" runat="server" />
<br />
2. The Radio Button List<br />
<asp:RadioButtonList Id="RadioButtonList1" runat="server">
<asp:ListItem>
<asp:ListItem Text="1"></asp:ListItem>
<asp:ListItem Text="2"></asp:ListItem>
<asp:ListItem Text="3"></asp:ListItem>
<asp:ListItem Text="4"></asp:ListItem>
</asp:ListItem>
</asp:RadioButtonList>
<br />
3. The dropdownlist<br />
<asp:DropDownList Id="DropDownList1" runat="server">
<asp:ListItem>
<asp:ListItem Text="1"></asp:ListItem>
<asp:ListItem Text="2"></asp:ListItem>
<asp:ListItem Text="3"></asp:ListItem>
<asp:ListItem Text="4"></asp:ListItem>
</asp:ListItem>
</asp:DropDownList>
</</div>
</body>
</html>
```

### 多项选择控件

有时，你希望用户能够从列表中选择多个可用项目。HTML 有两个控件可以处理这种情况：列表框（`listbox`）和复选框列表（`checkbox list`）（参见图 3-4）。

ASP.NET 重复了这些控件，如下：

- *列表框：* 这个列表类似于下拉列表，区别在于不需要展开——直接使用展开的列表并滚动即可。要选择多个项目，用户通常需要在点击时按住 Ctrl 键或 Command 键。
- *复选框列表：* 这正如其名所示：复选框列表。它看起来和单选按钮列表一样，只是换成了复选框。你可以在图 3-4 中看到出我的意思。

## 687 获取用户输入

![](img/6df7bb88e9302e98442acc219cfbd7fc_712_0.png)

图 3-4：多项选择控件。

这些是控件的代码。对于列表框，使用 `listItem`（列表项）来显示项目。如果是数据绑定的，则列表项将不再如此——它们将在运行时从数据源渲染。

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>title</title>
</head>
<body>
<form id="form1" runat="server">
<div>
1. <asp:ListBox Id="ListBox1" runat="server">
<asp:ListItem>Item 1</asp:ListItem>
<asp:ListItem>Item 2</asp:ListItem>
<asp:ListItem>Item 3</asp:ListItem>
</asp:ListBox>
<br />
2. <asp:ListBox Id="ListBox2" runat="server">
<asp:ListItem>Item 1</asp:ListItem>
<asp:ListItem>Item 2</asp:ListItem>
<asp:ListItem>Item 3</asp:ListItem>
<asp:ListItem>Item 4</asp:ListItem>
</asp:ListBox>
</div>
</form>
</body>
</html>
```

## 688 获取用户输入

### 使用其他输入类型

ASP.NET 提供了许多其他输入类型（参见图 3-5）。它们包括：

- *文件上传（FileUpload）：* 这正如其名。它为你创建一个类型为 multipart/form-data 的 HTML 输入。
- *图像映射（Imagemaps）：* 图像映射几乎是一个旧时代。基本上，它们允许你标记图像区域并分配 URL 或操作。
- *日历（Calendars）：* 日历控件就是一个可以帮助用户格式化日期的文本框。效果非常好。有很多格式选项——请在面板中查看。

![](img/6df7bb88e9302e98442acc219cfbd7fc_713_0.png)

*TextArea（文本区域）

## 689 数据绑定

还有其他的。可能已经涵盖了工具箱中看到的所有内容，但还有很多。你需要记住基础知识——你可以使用面板、标记和 C# 代码来更改属性。你可以将它们绑定到对象——我们将在后续章节讨论。

### 使用提交按钮提交输入

当你从表单获取这些输入后，你需要用户将其发送给你。实现此操作的基本方法是通过提交按钮。

在本书的第一章中，我讨论了 PostBack 事件，微软使用 JavaScript 改变了回传的方式。提交按钮就是实现这种操作的方法。

让我们——任何控件都可以触发回传。如果你为控件的某个事件设置了事件处理程序，它就会触发回传。一旦数据返回服务器，你就可以保存数据区域。我使用提交按钮是因为用户习惯了它。

ASP.NET 默认控件有三种：

- 按钮（Button）：正如其名——一个在 HTML 中提交的 Button 类型输入。
- 图像按钮（ImageButton）：这是一个带有内置 src 属性的用于图像的按钮控件。
- 链接按钮（LinkButton）：几乎在每个接受输入的页面上都会显示。大多数情况下，用户将其视为按钮。

# 690 数据绑定

但事情比这更有趣。假设你想提供一个颜色列表，并允许用户选择某个对象的颜色。你可以通过将集合列表和选定值绑定到列表控件的 `SelectedItem` 属性来实现这一点。如果你想自己显示颜色，可以绑定到文本控件的 `FontColor` 属性。

## 设置用于绑定的标记语言

在早期的 Active Server Page 时代，你通过打印将所有数据输出到页面上。这听起来很简单，但有很多问题。最重要的是，你的表单必须对它显示的数据有大量的了解。而现在情况有所不同。总之，这种操作的格式是：

```
<% ThisWhatIWantPrint %>
```

如果你需要一个列表，就在周围的代码中进行循环。如果你需要一个方法的结果，只需将方法放在那里即可。你看到什么就得到什么。

数据绑定是在屏幕上获取数据的一种更具启发性的形式。ASP.NET 内置的控件知道如何处理数据，以便你的数据满足某些特定要求。

数据绑定是通过将控件的属性设置为底层类的一个成员来实现的。对于单个控件（如文本框），你可以像这样设置相关属性：

```
<asp:Label Id='Label1' runat='server' Text='<%DataBindingToThisVariable %>' />
```

如果你正在绑定到重复控件（如 Grid 或 ListBox），则需要设置 `DataSource` 属性。我将在下一节向你展示如何操作。

你需要的变量需要在代码后台（code-behind）中并且是公共的。如果它们不是的，你将得到运行时错误。这就是为什么在代码中绑定是一个好主意，我将在下一节中演示。

现在，我将讨论在标记语言中绑定。以下是设置绑定标记语言所需的所有步骤：

- 1. 在第 3 章添加了控件页的 Web 项目中，右键点击并选择“添加（Add）”、“新建项（New Item）”，然后创建一个名为 `Show` 的类。
- 2. 点击“确定”，然后将这个简单的数据类放在其中。

这个类仅用于示例——它可以是一个数据库、一个数据类或 Entity Framework 模型。

![](img/6df7bb88e9302e98442acc219cfbd7fc_715_0.png)

```csharp
using System;
namespace WebControls
{
    public class Show {
        public int ID { get; set; }
        public String ShowTitle { get; set; }
        public String EpisodeTitle { get; set; }
        public DateTime ScheduledTime { get; set; }
        public int Channel { get; set; }
    }
}
```

- 3. 打开第 3 章项目中的 `Text.aspx` 文件。
- 4. 双击设计表面进入代码后台。如果 `Page.Load` 中已经出现了任何代码，你可以将其删除。
- 5. 在 `Page.Load` 中添加代码以创建一个 Mock Show 对象。

在项目中，你会从数据库或服务器层获取此对象。对于此示例，只需使用模拟代码即可：

```csharp
Show show = new Show { ID = 1, Channel = 5,
EpisodeTitle = "ASP.NET DataBinding",
ScheduledTime = new DateTime(2009, 4, 12, 0, 0),
ShowTitle = "C# Show" 
}
```

- 6. 在 `Page.Load` 的末尾添加 `Page.DataBind()` 调用，告诉页面你将进行数据绑定。

完成后的方法如下：

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    Show show = new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET DataBinding", ScheduledTime = new DateTime(2009, 4, 12, 0, 0), ShowTitle = "C# Show" };
    Page.DataBind();
}
```

- 7. 回到设计器中的标记语言。`Text` 字段被赋予了属性文本，例如：
- 8. 你可以直接编写代码来绑定项。

```asp
<asp:Label ID="Label" runat="server" Text="<%#show.EpisodeTitle %>"/>
```

这并不是绑定项的有趣方法。它的好处在于你无需重新编译即可编辑绑定，而有趣的方法是在 C# 代码中。在 C# 代码中操作更具可读且易于管理。每种方法都有其使用场景，但这是 C# 代码。我能做的至少是关注代码后台，对吧？

## 692 数据绑定

## 使用代码绑定进行数据绑定

与其直接在标记语言中设置属性，不如在代码绑定中将其赋值为一个值。对于重复控件，你可以在 C# 代码中为控件设置 `DataSource` 属性。然后，当你绑定页面时，它将使用该值从代码绑定中加载正确的值或多个值。

但请记住，对于 Label 的 `Text` 属性（例如），这只是数据绑定。我只是设置了一个值。

尝试一下 Show 示例。只需遵循以下步骤：

- 1. 保持标签文本简单——只需丢掉 `Text` 属性，如：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/html1/transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" Language="C#" AutoEventBack="true" CodeBehind="Text.aspx.cs" Inherits="Chapter_3.Text">
<head runat="server">
  <title></title>
</head>
<body>
  <form id="form" runat="server">
    <div>
      This is some text. <br />
      <asp:Label Id="Label" runat="server" />
    </div>
  </form>
</body>
</html>
```

- 2. 在代码绑定中将 `Text` 属性设置为要绑定的控件属性。注意页面中的 `DataBind` 命令：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;
namespace Chapter_3
{
    public partial class Text : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Show show = new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET DataBinding", ScheduledTime = new DateTime(2009, 4, 12, 0, 0), ShowTitle = "C# Show" };
            Label.Text = show.EpisodeTitle;
        }
    }
}
```

- 3. 运行以查看设置的值。这运行良好，但请记住，这只是简单的数据绑定。完整的数据绑定是针对重复属性的。

## 693 使用常用控件

在这些标签之后，我将讨论数据绑定的含义——数据绑定非常适合处理项的集合。数据绑定的典型示例是 DataGrid。如果一切设置正确，你对网格样式有很好的控制。要创建一个网格，请遵循以下步骤：

- 1. 在项目中添加一个新的 `Grid.aspx` 文件。
- 2. 切换到设计视图。
- 3. 从工具箱中将 `Grid` 拖到设计表面。
- 4. 双击设计表面切换到代码视图并获取 `Page_Load` 事件处理程序。
- 5. 在 `Page_Load` 事件处理程序中创建一个 Show 列表：

```csharp
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show (ID = 1, Channel = 5, EpisodeTitle = "ASP_NET Binding", ScheduledTime = new DateTime(2009, 4, 12, 0, 0), ShowTitle = "C# Show"));
```
