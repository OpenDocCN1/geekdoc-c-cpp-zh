
```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta runat="server">
<title>MultipleSelection</title>
</head>
<body>
<form id="form1" runat="server">
<div>
  1. Checkbox List<br />
  <asp:CheckboxList ID="CheckboxList1" runat="server">
    <asp:CheckBoxItem Text="Item 1" Value="1"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 2" Value="2"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 3" Value="3"></asp:CheckBoxItem>
    <asp:CheckBoxItem Text="Item 4" Value="4"></asp:CheckBoxItem>
  </asp:CheckboxList>
  <br />
  <br />
  2. Listbox<br />
  <asp:ListBox ID="ListBox1" runat="server" Multiple="True">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:ListBox>
  <br />
</div>
</form>
</body>
</html>
```

### 694

## 从用户获取输入 669

```html
2. Listbox<br />
  <asp:ListBox ID="ListBox1" runat="server" Multiple="True">
    <asp:ListItem Item="Item1"</asp:ListItem>
    <asp:ListItem Item="Item2"</asp:ListItem>
    <asp:ListItem Item="Item3"</asp:ListItem>
    <asp:ListItem Item="Item4"</asp:ListItem>
  </asp:ListBox>
</div>
</form>
</body>
</html>
```

## 使用其他类型的输入控件

ASP.NET 提供了许多其他输入类型，它们是上述类型的组合，或者是非位置输入（见图 3-5）。它们都是特殊控件，你需要将它们放入工具箱中，以便在需要时使用。

- `FileUpload`：`FileUpload` 正如其名。它创建一个类型为 `File` 的 HTML 输入，并将表单 `enctype`（编码类型）设置为 `multipart/form-data`。这允许 Web 服务器接收长二进制数据流，你可以通过流器来捕获它。

- `Imagenaps`：图像映射几乎是过去的遗迹了。基本上，它们允许你在图像上按像素标记地图，然后将地图中的区域分配给 URL 或其他操作。

# 670 数据绑定

此控件通过为你提供框架来提供帮助。你仍然需要提供映射关系。通常，人们会使用单独的。

- 日历控件：日历控件只是一个文本框，帮助用户正确地格式化日期。它运行良好。此外还有大量的格式化选项——可以在属性面板中查看它们。

还有其他控件。我可能涵盖了你在工具箱中会看到的所有内容，但那里还有更多选择。你需要记住基础知识——它们是具有 ASP.NET 实现和 HTML 输出的可见控件。你可以使用属性面板、标记语言和 C# 代码来更改属性。你还可以将它们绑定到代码中的对象上——我们将在本章稍后部分讨论。

# 使用 Submit 按钮提交输入

在将所有输入获取到表单后，你需要将它们发送给你。实现此点的基本方法是通过 Submit 按钮。

在第 1 章中，我讨论了 `PostBack` 事件，以及微软如何使用 JavaScript 来将表单提交回服务器的工作原理。Submit 按钮就是实现此操作的方法。

让我们明确一点——任何控件都可以引起 `postback`。如果你为某个事件设置了事件处理程序，它就会导致 `postback`。一旦数据返回服务器，你可以在任何时候保存表单数据。我们使用 Submit 按钮是因为用户习惯于这样做。

ASP.NET 默认控件有三种按钮。

- `Button`（按钮）顾如其名——HTML 中类型为 `submitted` 的输入。

- `ImageButton`（图片按钮）是一个具有内置 `src` 属性的控件。

- `LinkButton`（链接按钮）显示 HTML 锚点并将其视为按钮处理。

在几乎每个接受用户输入的页面中，我们都会使用这些控件之一。大多数情况下，用户期望看到它。

# 数据绑定

将数据放入 Web 页面的控件中是不够的。在输入数据后，需要某种方式来持久化（保存以便重用）这些信息。数据绑定就是答案。

# 数据绑定告诉控件底层类的成员从哪里获取数据。例如，如果你有一个 `Apple` 对象集合，其中包含一个你想在文本框中显示的属性 `Color`，你可以将 `Apple.Color` 的值绑定到 `Text` 属性。

但情况会变得更有趣。假设你想提供颜色列表，并允许用户选择相关对象的颜色。你可以通过将集合列表和选中的值绑定到列表控件的 `SelectedItem` 属性来实现。如果你想显示颜色本身，可以绑定到文本控件的 `FontColor` 属性。

# 为绑定设置标记

在过去的 Active Server Page (ASP) 时代，你只需简单的打印就能将所有数据放在页面上。听起来简单，但有很多问题。首先，你的表单必须对它所显示的数据有大量的了解。这是一个事事。总之，它的格式是：

```
<%= ThisIsWhatIWantToPrint % %>
```

如果你需要列表，就在周围的代码中进行循环。如果你需要方法的结果，只需将方法放在那里即可。你看到的即是所得。

数据绑定是获取屏幕上数据的一种更明智的形式。ASP.NET 内置的控件知道如何处理数据，只要数据符合某些基本规范。

数据绑定通过将控件的属性设置为底层类的成员来实现。对于单个控件（如文本框），你设置相关的属性，例如：

```
<asp:Label ID="Label" runat="server" Text='<%# IAmBindingToThisVariable %>' />
```

如果你正在绑定一个重复控件（如 Grid 或 List），则需要设置 `DataSource` 属性。我将在下一节“代码中的绑定”中向你展示如何操作。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_696_0.png)

你需要的变量需要在代码后（code-behind）中并且必须是公共的。如果它们不是，你将得到运行时错误。这就是为什么在代码中进行绑定是一个好主意，我们将在下一节进行操作。

现在，让我们讨论在标记中进行绑定。以下是设置绑定标记所需的所有内容：

# 672 数据绑定

1. 在我们一直在添加了带有控件的页面的第 3 章 Web 项目中，右键点击并选择“Add New（添加新建）”，然后选择“Class（类）”。

我将我的类命名为 `Show`。

2. 点击确定，然后将这个简单的数据类放在那里。这个类仅用于示例——它可以是一个数据库类、数据类或 Entity Framework 模型。

```
using System;
namespace Chapter_3 {
    public class Show {
        public int ID { get; set; }
        public String ShowTitle { get; set; }
        public String EpisodeTitle { get; set; }
        public DateTime ScheduledTime { get; set; }
        public int Channel { get; set; }
    }
}
```

3. 打开第 3 项目中的 `Text.aspx`。

4. 双击设计表面以获取代码后代码。

如果 `Page.Load` 中已经出现任何代码，你可以删除它们。

5. 向 `Page.Load` 中添加代码以创建一个模拟对象（Mock Object）。

在实际项目中，你将从数据库或服务器层获取此对象。对于此示例，我仅使用模拟代码：

```csharp
protected void Page_Load(object sender, EventArgs e) {
    Show show = new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET Databinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" };
    Page.DataBind();
}
```

6. 我们需要告诉页面我们将进行数据绑定。在 `Page_Load` 的末尾添加 `Page.DataBind()`。

完成后的方法所示：

7. 更改设计器中的标记。

8. `Text` 字段获得了用于绑定的标记。我们可以直接给它该属性，如下：

```html
<asp:Label ID="Labell" run="server" Text='<%# show.EpisodeTitle %>'" />
</asp:Label>
```

这并不是绑定内容的有趣方式。它的好处是你可以在不重新编译的情况下编辑绑定，但有趣的方式是代码。有趣的方式是绑定内容。它的好处是你可以在不重新编译的情况下编辑绑定，但有趣的方式是代码。

# 数据绑定 675

```csharp
shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle = 'Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0), ShowTitle = "Learning C#") ;
shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle = 'Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0), ShowTitle = "Learning C#") );
```

## 6. 在页面加载底部添加数据源并执行 DataBind。

我绑定了代码中添加的行：

```csharp
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show (ID = 1, Channel = 5, EpisodeTitle = '*ASP.NET Binding', ScheduledTime = new DateTime(2009, 4, 12, 13, 0), ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 2, Channel = 5, EpisodeTitle = '*ASP.NET Styling', ScheduledTime = new DateTime(2009, 4, 12, 13, 0), ShowTitle = "The C# Show");
    shows.Add(new Show (ID = 3, Channel = 8, EpisodeTitle = '*Inheritance', ScheduledTime = new DateTime(2009, 4, 16, 9, 0), ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 4, Channel = 8, EpisodeTitle = '*Partial Classes', ScheduledTime = new DateTime(2009, 4, 17, 9, 0), ShowTitle = "Learning C#");
    shows.Add(new Show (ID = 5, Channel = 8, EpisodeTitle = '*Operator Overloading.', ScheduledTime = new DateTime(2009, 4, 18, 0, 0), ShowTitle = "Learning C#"));
    Gridview1.DataSource = shows;
    Page.DataBind();
}
```

## 7. 刷新 `<F5>` 以查看应用程序运行。

如图 3-6 所示，来自数据库的控件会自动绑定到 HTML 表格中。

这些都很好，但如果你不想显示 ID，或者想按照自己的喜好绑定某些列怎么办？你可以这样做，但这需要多花一点精力。

`gridview` 自动显示表中所有列的能力是由一个属性处理的：`AutoGenerateColumns`。我们需要做的第一件事是将其设置为 `False`。这告诉 ASP.NET 我们将手动获取所有列。

接下来，我们需要告诉它我们要使用哪些列。这可以在 ASP.NET 代码中完成，但这是 C# 代码。让我们在 C# 代码中来实现。

我们需要向网格添加列——假设是 Channel 和 Episode。为了实现这一点，我们需要定义并设置两个 `BoundColumn` 对象。然后，我们需要将它们添加到网格中。这在我们在标记中添加 `datacolumn` 标签时会在后台发生。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_700_0.png)

# 676 数据绑定

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_701_0.png)

图 3-6：这里的电视节目列已绑定到网格上。

这是生成的标记。我将添加到页面事件处理程序中的代码行进行了**加粗**：

```csharp
List<Show> show = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    show.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET DataBinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "ASP.NET Styling", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "C# Show" });
    show.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 19, 0, 0), ShowTitle = "C# Show" });
}
```

```csharp
GridView.DataSource = show;
GridView.AutoGenerateColumns = false;

BoundField channelColumn = new BoundField();
channelColumn.DataField = "Channel";
channelColumn.HeaderText = "Channel";
GridView.Columns.Add(channelColumn);

BoundField episodeColumn = new BoundField();
episodeColumn.DataField = "EpisodeTitle";
episodeColumn.HeaderText = "Episode";
GridView.Columns.Add(episodeColumn);

Page.DataBind();
```

# 为你的控件设置样式

当控件中已有数据时，你需要让控件看起来具有特定的样式。这里有很多选项。所有带有属性的控件都可以在此处设置。

# 辅助功能控制特性

大多数 ASP.NET 控件在适用情况下都符合一组特定的无障碍功能列表。其目标是让无障碍编程变得简单，并对用户实用。

- 任何不是由文本组成的元素都应该有一个替代文本选项。例如，所有图像标签都支持 `AlternateText` 属性，该属性会填充 HTML 的 `alt` 标签。网页阅读器将“读出”该标签的内容来代替图像。如果你在网页上添加图像，Visual Studio 会提示你填入替代文本。
