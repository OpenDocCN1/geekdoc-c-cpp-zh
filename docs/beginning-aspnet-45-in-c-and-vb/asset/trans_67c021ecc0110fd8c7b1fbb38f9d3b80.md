
## 试一试：使用 TreeView 控件构建导航系统

在本练习中，你将向 `<nav>` 元素添加一个 TreeView 控件，位置紧挨着你之前创建的 Menu 下方，然后将 TreeView 绑定到与 Menu 相同的数据源。接下来，你将编写一些代码，根据当前活动的主题显示 Menu 或 TreeView。

- 1. 在标记视图中打开母版页，并在 Menu 控件正下方，从工具箱中拖出一个 TreeView 控件来添加它。
- 2. 在该控件的开始和结束标签之间，添加以下 `<LevelStyles>` 元素：

```
<LevelStyles>
<asp:TreeNodeStyle CssClass="FirstLevelMenuItems" />
</LevelStyles>
```

`FirstLevelMenuItems` 类选择器定义在你上一章添加的 DarkGrey.css 文件中，用于在第一级的每个树项上方留出一些空间。

- 3. 切换到设计视图，单击一次 TreeView，再单击小箭头打开智能任务面板。从 Choose Data Source 下拉菜单中选择 SiteMapDataSource1，即你为 Menu 控件创建的数据源控件（参见图 7-9）。

![](img/eadab2ccd79b253c01a3fdff2321202d_316_0.png)

图 7-9

一旦选择数据源，TreeView 就会在设计视图中更新，并显示站点地图文件中的正确菜单项。

- 4. 打开 TreeView 控件的属性网格，将 ShowExpandCollapse 属性设置为 False。
- 5. 在文档中单击任意位置以使其获得焦点，然后按 F7 打开母版页文件的代码隐藏文件，找到之前用于在主题列表中预选主题的 Page_Load 事件。在该代码下方、方法结束之前，添加以下加粗代码，根据当前活动的主题显示或隐藏 TreeView 和 Menu 控件：

**VB.NET**

```vbnet
    item.Selected = True
    End If
End If
End If
Select Case Page.Theme.ToLower()
    Case "darkgrey"
        Menu1.Visible = False
        TreeView1.Visible = True
    Case Else
        Menu1.Visible = True
        TreeView1.Visible = False
End Select
End Sub
```

**C#**

```csharp
    item.Selected = true;
    }
    }
switch (Page.Theme.ToLower())
{
    case "darkgrey":
        Menu1.Visible = false;
        TreeView1.Visible = true;
        break;
    default:
        Menu1.Visible = true;
        TreeView1.Visible = false;
        break;
}
}
```

- 6. 保存所有更改，并在浏览器中打开 Default.aspx。根据当前活动的主题，你应该看到 Menu 或 TreeView 控件。从列表中选择不同的主题，页面将重新加载，现在显示另一个控件作为网站的导航系统（参见图 7-10）。

> **常见错误** 如果你从 BasePage 类中检查标题的代码收到错误，请确保在 Web.config 文件的 `<pages>` 元素中设置了有效的主题。如果在从一个页面移动到另一个页面时主题似乎发生切换，请确保你的页面继承自 BasePage，如果你基于自定义模板创建新页面，就应该是这种情况。

![](img/eadab2ccd79b253c01a3fdff2321202d_318_0.png)

图 7-10

## 工作原理

与 Menu 控件一样，TreeView 控件可以从 SiteMapDataSource 控件获取数据，而 SiteMapDataSource 又从 Web.sitemap 文件获取信息。默认情况下，TreeView 显示加号和减号，表示可以折叠和展开项。对于站点菜单，这可能没有太大意义，因此通过将 ShowExpandCollapse 设置为 False，可以有效地隐藏这些图像。TreeView 允许你设置许多样式属性，包括 NodeStyle、RootNodeStyle 和 LevelStyles，这些属性会影响树中各个项的外观。在本练习中，你使用 LevelStyles 应用了一个名为 FirstLevelMenuItems 的类，该类在顶层每个项（如 Home 和 Reviews）上方添加了一些空间。

母版页的代码隐藏文件中的代码通过检查 Page 的 Theme 属性来确定当前主题。当 DarkGrey 是当前主题时，代码隐藏 Menu，然后显示 TreeView。在 Case Else / default 块中，情况正好相反。这意味着对于 Monochrome 主题以及你将来可能添加的所有主题，TreeView 将被隐藏，而使用 Menu 作为导航系统。

TreeView 仍然存在与以前版本的 ASP.NET 中 Menu 控件相同的问题，即它会生成大量臃肿的 HTML。不幸的是，该控件没有 RenderingMode 属性，因此如果你使用 TreeView，就只能使用基于 table 的 HTML。

- 1. 在标记视图中打开母版页，找到 `MainContent <section>` 元素。在其开始标签之后、`<asp:ContentPlaceHolder>` 标签之前，按 Enter 键创建一些空间，然后从工具箱中拖出一个 `SiteMapPath`。在 `SiteMapPath` 后面紧接着添加两个换行符（`<br />`）。最终代码应与以下类似：

```
<section id="MainContent">
<asp:SiteMapPath ID="SiteMapPath1" runat="server"></asp:SiteMapPath><br /> </br />
<asp:ContentPlaceHolder ID="cpMainContent" runat="server">
```

- 2. 保存更改，然后在浏览器中请求 `Default.aspx`。注意，页面现在显示从站点根目录（由 Home 文本标识）到当前页面的路径。单击 Menu 或 TreeView 控件中的几个项来浏览站点，你会看到每个页面的面包屑都会变化。图 7-11 显示了 Firefox 中 All Reviews 页面的面包屑。All Reviews 页面是 Reviews 的子元素，而 Reviews 又位于 Home 根元素之下。

![](img/eadab2ccd79b253c01a3fdff2321202d_320_0.png)

图 7-11

导航到其中一个子页面时，你可以单击路径中的元素向上移动一级或多级。单击图 7-11 所示页面中的 Reviews 会返回主 Reviews 页面，单击 Home 会返回站点根目录。

- 3. 使用主题选择器切换到另一个主题。注意，`SiteMapPath` 看起来几乎相同，只是链接的颜色不同，链接颜色由每个主题的 CSS 文件定义。

## 工作原理

`SiteMapPath` 渲染为一系列 `<span>` 元素，其中包含链接或纯文本。以下是在图 7-11 中 `SiteMapPath` 的部分 HTML 代码：

```
<span><a title="Home" href="/">Home</a></span>
<span> &gt; </span>
<span><a title="Reviews published on this site" href="/Reviews/Default.aspx">Reviews</a></span>
<span> &gt; </span>
<span>All Reviews</span>
```

前两个菜单项（Home 和 Reviews）由链接（`<a>`）表示，使你可以导航到其 `href` 属性中定义的页面。最后一个菜单项——All Reviews——只是纯文本。

在元素之间，你会看到一个 `<span>`，其中包含你在 PathSeparator 属性中设置的字符。由于该分隔符字符 (>) 在 HTML 中具有特殊含义，因此其值被编码为 &gt;（大于号），以确保它在浏览器中最终显示为纯文本字符。

如果你在浏览器中查看页面的 HTML，还会看到一个 `<a>` 元素，用于跳过链接。`<a>` 包含一个小图像，其 `left` 属性设置为一个较大的负值，因此它位于可见浏览器窗口之外，你不会看到它。这对于使用屏幕阅读器的视力障碍用户非常有用，因为它使他们能够跳过导航，直接进入页面内容。TreeView 和 Menu 控件使用相同的方法，防止屏幕阅读器在每次页面加载时朗读整个站点结构。

这三个导航控件为你的网站提供了很好的客户端导航系统功能集。Menu 和 TreeView 控件都可以快速显示站点的整个结构，使用户能够轻松找到方向。SiteMapPath 帮助用户了解他们在站点中的位置，并为他们提供一种简单的方法来导航到站点层次结构中更高级别的页面。

除了从客户端浏览器进行导航之外，通过代码从服务器端将用户导航到另一个页面也非常常见。下一节将讨论其工作原理。

## 编程重定向

编程重定向在 ASP.NET 页面中非常有用和常见。例如，假设有一个页面允许用户向数据库输入评论。用户单击 Save 按钮后，评论被保存，用户会被带到另一个页面，在那里她可以看到完整评论。

ASP.NET 支持三种主要方式以编程方式将用户重定向到新页面。前两种方式，Response.Redirect 和 Response.RedirectPermanent（在 ASP.NET 4 中引入），会向浏览器发送指令以获取新页面。第三种方式，Server.Transfer，在服务器端执行。由于客户端和服务器端重定向之间存在很大差异，以下部分将更详细地介绍它们。

### 以编程方式将客户端重定向到另一个页面

在每个 ASPX 页面中，你都可以访问一个名为 Response 的属性，你在之前为所选主题保存 cookie 时已经见过它。Response 对象使你能够访问有用的属性和方法，这些属性和方法都与服务器向用户浏览器发出的响应相关。其中两个方法是 Redirect 和 RedirectPermanent。这些方法向浏览器发送请求新页面的指令。如果你想将用户重定向到站内的另一个页面或完全不同的网站，这会很有用。

Redirect 和 RedirectPermanent 之间的区别主要与搜索引擎优化有关。使用 Redirect 会告诉客户端页面已临时移动。你经常使用它根据某个操作将用户重定向到新页面。例如，在填写联系表单后，你可能希望将用户发送到显示消息的 ThankYou.aspx。

