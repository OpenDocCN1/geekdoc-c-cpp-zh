

# 在 Visual Studio 中工作

- 9. 将 (ID) 改为 TextToChange。
- 10. 点击设计器中的按钮。

属性面板发生变化，显示按钮的属性。

- 11. 将文本更改为 Click Me。
- 12. 将 (ID) 改为 ChangeText。

现在切换回源代码视图，并注意代码中的内容：

```xml
<@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.cs"
Inherits="Default" %>

<@ Page Title="Home Page" Language="C#" MasterFile="~Site"
Master AutoEventFirstSample="true" CodeBehind="Default.aspx"
Inherits="Default" %>

<asp:Content runat="server" Content="FeaturedContent" PlaceHolderID="FeaturedDContent">
<section class="featured">
<div class="content-wrapper">
<hgroup class="content-title">
<h1>Title &amp; Title</h1>
<h2> 2 修改此模板以启动你的 ASP.NET 应用程序。</h2>
</hgroup>
<p>了解更多关于 ASP.NET，请访问 <a href="http://asp.net/"
title="ASP.NET Website">http://asp.net/</a>。
该页面提供了 <mark>视频、教程和示例</mark>，
帮助你充分利用 ASP.NET。
如果你对 ASP.NET 有任何问题，请访问
<a href="http://forums.asp.net/18.aspx" title="ASP.NET Forum">论坛</a>
</p>
</div>
</section>
<asp:Content runat="server" ID="BodyContent" PlaceHolderID="MainContent">
<asp:Label ID="TextToChange" runat="server" Text="This is the text to change"
Font-Size="12pt" /></asp:Label>
<asp:Button ID="ChangeText" runat="server" Text="Click Me" />
</asp:Content>
```

| 第六卷 |
| :--- |
| 第 2 章 |
| 构建 Web 应用 |

所以，你代码的管理是由设计器为你完成的。现在，人们看起来并不像是在用 Visual Studio 捣乱他们的代码。有些人不喜欢记住 ASP.NET 的所有细节。这完全取决于你，可以用它还是不可用。

这并不是魔法，不是吧？这是一本 C# 书，如果你在一个大型公司里工作，ASP.NET 代码可能已经有人替你写好了。你想放置服务器端代码，我不会怪你的。

# 在 Visual Studio 中工作

## 在代码编辑器中编码

如果你回到设计视图并双击你拖入的 Button 控件，你将看到比这些疯狂的标记更熟悉的一些东西。通常是后台代码（code-behind），这是让服务器能够管理表单的 C# 代码。后台代码位于 `Default.aspx.cs` 文件中，位于解决方案资源管理器树形中 `Default.aspx` 的下方。这段代码应该像这样：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace AspNetFirstSample
{
    public partial class _Default : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void ChangeText_Click(object sender, EventArgs e)
        {
        }
    }
}
```

我将稍微拆解一下。我知道你以前见过类，这不只是一个类，但我想指出几点：

- * 这是一个部分类（partial class）。该类的其他部分是内置的 Web 功能，并且它们以前出现在这个文件中。事实上，没有人需要编辑它，所以微软将其移除了。我很高兴他们这么做了。这样看起来简单得多。
- * 该类继承自 `System.Web.UI.Page`。`Page` 类提供了你所需的所有工具来保持页面控件的整体。这对于某些 Web 应用程序非常重要，但稍微超出了本书的范围。请阅读 `Page` 类的文档。它是 ASP.NET 的重要部分。
- * 为 `Page.Load` 有一个事件处理器。还记得第 1 章中的 ASP.NET 加载顺序吗？（回想请求序列和回发？）这很重要。你可以在此处理程序中执行设置操作。
- * 为 `Button.Click` 有一个事件处理器。嘿，它是怎么到那儿的？你双击控件来获取默认处理程序，就像我在里面说的那样。根据你的背景，这让你感觉非常熟悉或非常陌生。这不像经典的活动页面（Active Pages）。

# 在 Visual Studio 中工作

现代化的方式带有内联脚本。虽然内联脚本是你使用 ASP.NET 编码的一种方式，但它并不是默认方式。如果你是一个 Windows 程序员，你可能会对以类似方式工作的 Web 表单感到舒服。然而，正如我在第 1 章中提到的，这些控件上没有真正的状态管理——所有都是通过 `ViewState` 变量模拟的。如果你过度使用 `ViewState`，你的应用程序将会变慢。

![](img/6df7bb88e9302e9844acc219bd7fc_0.png)

## 使用 C# 添加功能

从让表单执行某些操作开始。代码视图（Code View）基本上允许开发人员编写对 Web 表单执行有用操作的代码。在这里保持简单，但它可以变得复杂得多。目前已经有一个 `Button.Click` 的事件处理器了，所以我建议使用该方法来更改标签的文本。标签的 ID 是 `TextChange`，所以你需要添加此代码：

```csharp
OnChange.Text = "It has changed!";
```

这很简单。然而，你需要知道这将是你写过的最简单的事件处理器了。按 F5 运行应用程序。如果你犯了错误，它应该可以编译。然后启动 IIS Express，然后你的浏览器应该启动。点击 "Click Me" 按钮，你的屏幕应该像图 2-4 一样。

![](img/6df7bb88e9302e9844acc219bd7fc_1.png)

图 2-4：成功了！

# 在 Visual Studio 中工作

第一次在调试器中运行 Web 表单时，你会收到一条消息，告诉如果你想调试此项目，你需要更改 `web.config`。就本书而言，是的，然后继续继续吧。但是，请记住，当你进入生产环境时，你需要检查配置并更改此设置。我在本书的第 5 章中涵盖了这一点。在代码视图中你可以做更多——多得多（远超我在这里能涵盖的）。接下来的章节包含了你可以吸收的提示和技巧。

## 使用 Page.Load 添加更多功能

现在客户端希望在页面加载时发生某些事情。假定“某些事情”是动态的。在这个示例中它不会是动态的，但它可以可能是。由于 ASP.NET 和通用的 Windows 编程的性质，你不能总是可以在设计时编写属性——特别是对于事件。要编写事件处理器，请按照以下步骤操作：

- 1. 首先通过在代码视图中编写事件处理器。

```csharp
protected void ChangeColor(object sender, EventArgs e)
{
    TextChange.BackColor = System.Drawing.Color.Red;
}
```

![](img/6df7bb88e9302e9844acc219bd7fc_0.png)

不需要 C# 事件参数。如果你想让它们正常工作，请包含它们。在代码视图中操作：

- 2. 回到设计视图并选择 `TextChange` 标签。
- 3. 打开属性面板并点击顶部的闪电图标。这让属性面板变成了事件面板。
- 4. 在下拉列表中点击 `Load` 事件，如图 2-5 所示。
- 5. 选择你在步骤 1 中创建的 `ChangeColor` 方法。
- 6. 再次运行应用程序。

该标签的背景颜色应该设置为红色。

