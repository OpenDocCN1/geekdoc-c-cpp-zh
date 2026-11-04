
```
shows.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "Learning C#" });
shows.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 9, 0, 0), ShowTitle = "Learning C#" });
}
```

- 6. 在页面加载底部添加数据源和数据绑定命令。

我已将我在代码中添加的行加粗：

```
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET Databinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "ASP.NET Styling", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 9, 0, 0), ShowTitle = "Learning C#" });
    GridView1.DataSource = shows;
    Page.DataBind();
}
```

- 7. 按 <F5> 查看应用程序运行。

如图 3-6 所示，数据库中的列都已自动绑定到 HTML 网格。

这都很好，但如果您不想显示 ID，或者想将列放置在更喜欢的位置怎么办？您也可以这样做；只是需要多花一点功夫。

GridView 自动显示表中所有列的功能由一个属性处理：AutoGenerateColumns。我们需要做的第一件事就是将其设置为 False。这告诉 ASP.NET 我们将手动设置所有列。

接下来，我们必须告诉 C# 我们使用的是哪些列。这可以在 ASP.NET 代码中完成，但这是一本 C# 书。让我们在 C# 代码中完成。

我们需要在网格中添加两列——比如 Channel 和 Episode。为了做到这一点，我们需要定义并设置两个 BoundField 对象。然后我们需要将它们添加到网格中。这就是在标记中添加 datacolumn 标签时在幕后发生的事情。

**Figure 3-6:** 电视节目表！这里的列已绑定到网格。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_701_0.png)

以下是生成的标记。我将添加到页面加载事件处理程序中的代码行加粗了：

```
List<Show> shows = new List<Show>();
protected void Page_Load(object sender, EventArgs e)
{
    shows.Add(new Show { ID = 1, Channel = 5, EpisodeTitle = "ASP.NET DataBinding", ScheduledTime = new DateTime(2009, 4, 12, 12, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 2, Channel = 5, EpisodeTitle = "ASP.NET Styling", ScheduledTime = new DateTime(2009, 4, 12, 13, 0, 0), ShowTitle = "The C# Show" });
    shows.Add(new Show { ID = 3, Channel = 8, EpisodeTitle = "Inheritance", ScheduledTime = new DateTime(2009, 4, 16, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 4, Channel = 8, EpisodeTitle = "Partial Classes", ScheduledTime = new DateTime(2009, 4, 17, 9, 0, 0), ShowTitle = "Learning C#" });
    shows.Add(new Show { ID = 5, Channel = 8, EpisodeTitle = "Operator Overloading", ScheduledTime = new DateTime(2009, 4, 18, 9, 0, 0), ShowTitle = "Learning C#" });

    GridView1.DataSource = shows;
    GridView1.AutoGenerateColumns = false;

    BoundField channelColumn = new BoundField();
    channelColumn.DataField = "Channel";
    channelColumn.HeaderText = "Channel";
    GridView1.Columns.Add(channelColumn);

    BoundField episodeColumn = new BoundField();
    episodeColumn.DataField = "EpisodeTitle";
    episodeColumn.HeaderText = "Episode";
    GridView1.Columns.Add(episodeColumn);

    Page.DataBind();
}
```

## 自定义控件样式

当您的数据已在控件中时，您需要让控件看起来是某种样式。这里有很多选项。所有控件都带有可在设计时和运行时设置的属性，或绑定到级联样式表（CSS）。

能够设置样式是必要的；能够使用 C# 在运行时管理样式几乎是魔法。使用这三种方法的组合可以创建动态应用程序，为用户提供最佳体验。

### 设置控件属性

迄今为止，设置控件样式最简单的方法是使用内置属性。它很直接，您确切地知道要将外观应用到哪里，并且 IntelliSense 会帮助您完成。

请注意，我没有说这是做样式的“最佳”方式。我说的是它是最简单的方式。

设置控件属性存在诸多问题。如果您有多个控件需要设置，您必须在每个控件上设置属性——即使它们相同。运行时必须处理大量额外内容。此外，它会使您的代码变得混乱。

然而，有时您确实需要以这种方式设置样式。查看它们全部的最佳方法是查看属性面板。将其设置为分类，并在底部查看，如图 3-7 所示。如果您在此处实际设置属性，它们将像下面的示例一样出现在标记中，而不是代码隐藏中，但您至少可以在这里找到名称。

```
<asp:GridView ID="GridView1" runat="server"
onselectedindexchanged="GridView1_SelectedIndexChanged">
 <RowStyle BackColor="#FF6666" />
</asp:GridView>
```

在您获得要设置的内容的名称后，您就可以像设置其他任何属性一样设置它：

```
GridView1.RowStyle.BackColor = System.Drawing.Color.Red;
```

最困难的部分是发现样式将需要什么框架元素作为值。确定此值的最简单方法是键入等号左侧的部分，然后将鼠标悬停在属性上以查看其声明方式。例如，BackColor 需要一个 System.Drawing.Color 元素。当我发现这一点时，我就知道去哪里获取值了。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_703_0.png)

**Figure 3-7:** 属性面板中的样式。

### 使用 CSS 绑定样式

由于我们处于 Web 应用程序中，使用级联样式表（CSS）似乎是处理样式的一个不错的方法。ASP.NET 中的几乎每个控件都有一个属性——CssClass——可以利用作为项目一部分加载的样式。

开始时，您需要一些 CSS 类，它们与 .NET 类不同。CSS 中的类是一组样式，可以连接到一组标记，以便匹配它们之间可以匹配的属性。要使用 CSS 绑定样式，请按照以下步骤操作：

- 1. 右键单击项目并选择添加新项。
- 2. 从对话框中选择样式表。我将其命名为 Chapter3.css。
- 3. 当样式表出现时，右键单击 CSS 大纲并选择添加样式规则。
- 4. 在元素对话框中，选择类名并在文本框中输入 GridView。
- 5. 单击如图 3-8 所示的右箭头按钮。
- 6. 按确定，并注意样式表中出现的新条目。

**Figure 3-8:** 添加样式表类

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_704_0.png)

仅用于演示，我在样式表中添加了一些内容。

```
body
{
}
.GridView
{
    font-family:French Script MT;
    background-color: Fuchsia;
}
```

要将其绑定到控件，我们使用 CssClass 属性，它接受 CSS 文件中的类。首先在页面标记中使用 ASP.NET 标记中的“link”片段将 CSS 文件链接到相关页面（请记住将其放在 `<head>` 标签部分）。

在代码隐藏中，只需像设置其他任何属性一样设置 CssClass 属性，如下所示：

```
GridView1.CssClass = "GridView";
```

### 确保网站可访问

当我说可访问时，我并不是指服务器是否正常运行。我说的是确保您使用的控件可供有残疾的人使用，例如视力、听力或触觉减弱的人。这些人的浏览体验与您或我不同。

微软在可访问的 Web 浏览方面投入了大量资金，您会很高兴地发现大多数控件开箱即用时就会做出良好的可访问性决策。然而，了解如何将它们用于此目的需要花费一些精力。

如果您为大型企业或政府构建网站，Section 508（《康复法》修正案）使这一点非常重要。请访问 www.section508.gov 了解更多信息。
