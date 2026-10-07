
```
<div>
<asp:ScriptManager ID='ScriptManager1' runat='server' />
<asp:UpdatePanel ID='UpdatePanel1' runat='server'>
  <ContentTemplate>
    <asp:Label ID='Label1' runat='server' Text=""></asp:Label>
    <asp:Timer ID='Timer1' runat='server' />
  </ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
</body>
</html>
@@ Language="C#" %>
<script runat="server">
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
        Label1.Text = DateTime.Now.ToString();
}

protected void Timer1_Tick(object sender, EventArgs e)
{
    Label1.Text = DateTime.Now.ToString();
}
</script>
```

在这种情况下，`ScriptManager` 控制位于页面上。`UpdatePanel` 控制是一个容器，允许你只更新页面的部分。

## UpdatePanel 控制（更新面板控件）

`UpdatePanel` 控制是一个允许你只更新页面部分的容器。你有几种方法来处理异步回传。最简单的方法是第一种并在列表 18-13 中显示。

### `<ContentTemplate>` 元素

### 728 | 第 18 章 | ASP.NET AJAX

#### 列表 18-13：将触发器放在 UpdatePanel 内部

```asp
@ Page Language="VB" %>
<script runat="server">
Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    Label1.Text = "This button was clicked on " & _
    DateTime.Now.ToString()
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>UpdatePanel Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager Id="ScriptManager1" runat="server"></asp:ScriptManager>
<asp:UpdatePanel Id="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:Label Id="Label1" runat="server"></asp:Label>
<br />
<br />
<asp:Button Id="Button1" runat="server" Text="Click to initiate async request" OnClick="Button1_Click" />
</ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
</body>
</html>
```

```csharp
@ Page Language="C#" %>
<script runat="server">
protected void Button1_Click(object sender, EventArgs e)
{
    Label1.Text = "This button was clicked on " + 
    DateTime.Now.ToString();
}
</script>
```

列表 18-13 展示了这种模型中的一个大问题：当异步回传发生时，你不仅发送了 `Label` 控制的日期时间值，还发送了页面上按钮的完整代码，如下所示：

265 [UpdatePanel][UpdatePanel]此按钮于 11/23/2009 11:45:21 AM 被点击</</span>

```html
<br />
<input type="submit" name="Button" value="Click to initiate async request"
Id="Button" />
```

```
164|hidden|__VIEWSTATE|/W4WEwHIE23nQIwMw9fKCACAIwYCAIwFqFMjMDQAgIDwW8AbHA4EVV4DA0Y9GCBcYID8QZDIbWMw9fKCAAbYAbAnO7MTY5HBBTRK2
KGIGBw2MCV6By3FPTC|48|hidden|EVENTVALIDIFICATION|weXAGL43YdXwBMw54RBI
I5Z2VY1|MCV6By3J+RD0|0|asyncPostBackControlIDs||11|
updatePanelIDs||10|childUpdateIDs||12|panelToRefreshIDs||11|
updatePanel|2|asyncPostBackTimeout|90|22|form|SimpleUpdatePanel.aspx|11|
/>
```

这段通过客户端异步回回（Postback）点击的代码显示了 `UpdatePanel` 中包含的内容被刷新了。你可以通过仅包含页面控件中实际更新的部分来精简页面。如果你将按钮从 `UpdatePanel` 控件的 `<ContentTemplate>` 部分中取出，那么你必须在控件内部包含一个 `<Triggers>` 部分。

之所以这样做是，尽管你想更改的内容是通过异步回回进行的，但你仍然需要绑定一个页面来触发回回的发生。这就是 `UpdatePanel` 控件 `<Triggers>` 部分的作用。你可以使用该控件的这一部分指定启动异步页面回回的变量。通过使用 `UpdatePanel` 控件内的 `<Triggers>` 元素，你可以重写列表 18-13，如列表 18-14 所示。

# 列表 18-14：使用触发器引起异步回回

```aspnet
<%@ Page Language="server" %>
```

```aspnet
<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
Label1.Text = "This button was clicked on &" &
DateTime.Now.ToString()
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>UpdatePanel</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ScriptManager ID="ScriptManager1" runat="server">
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:Label ID="Label1" runat="server"/></asp:Label>
</ContentTemplate>
<Triggers>
<asp:AsyncBackTrigger ControlID="Button1" EventName="Click" />
</Triggers>
</asp:UpdatePanel>
<br />
<br />
<asp:Button ID="Button1" runat="server"
Text="Click to initiate async request"
OnClick="Button1_Click" />
```

```aspnet
</div>
</form>
</body>
</html>
<%@ Page Language="C#" %>
<script runat="server">
  protected void Button1_Click(object sender, EventArgs e)
  {
    Label1.Text = "This button was clicked on " +
    DateTime.Now.ToString();
  }
</script>
```

在这种情况下，按钮和 HTML 元素位于 `UpdatePanel` 控件的 `ContentTemplate` 部分之外，因此每次异步回回都不会被发送回客户端。`ContentTemplate` 中的唯一需要更改的项是 `Label` 控件。将这一切连接在一起的是 `<Triggers>` 部分。

`Triggers` 部分可以包含两个控件：`AsyncBackTrigger` 和 `PostBackTrigger`。在这种情况下，使用了 `AsyncBackTrigger`。`PostBackTrigger` 会导致全页回回，而 `AsyncBackTrigger` 只引起异步回回（显然，通过控件的名称）。

从列表 18-14 的示例可以看出，哪些属性用于将控件绑定到异步回回的触发器：`Control` 和 `EventName` 属性。在这里你想作为异步回回的启动器。`EventName` 属性的值（由控件 `ID` 属性指定）是你想从客户端异步请求中调用的事件。在这种情况下，控件的 `Click` 被调用，它更改了位于 `UpdatePanel` 控件 `<ContentTemplate>` 部分的控件的值。

运行此页面并点击按钮会给你一个较小的异步响应：

```
108|UpdatePanel UpdatePanel
<span id="Label1">Click this</span> |11:58:56 AM
```

虽然与之前的示例显著不同，但稍微大了一点——相似性在于该示例使用的页面尺寸（显示了更显著的改进）。如何使用 `UpdatePanel` 控件构建你的页面。

# 使用 Visual Studio 构建触发器

如果你喜欢在构建 ASP.NET 页面时在 Visual Studio 设计界面上工作，那么你会发现构建 ASP.NET 页面支持在 `UpdatePanel` 控件内创建触发器。要查看此操作，请在页面上放置单个 `UpdatePanel` 控件，并在属性框中查看控件。`Triggers` 列表允许你修改与其关联的项目，如图 18-11 所示。

# ASP.NET AJAX 服务器控件

在属性框中点击此按钮会启动 `UpdatePanel` 编辑器，如图 18-12 所示。此编辑器允许你添加任意数量的触发器并将它们关联。点击将触发器添加到你的 `UpdatePanel` 控件的 `<Triggers>` 部分。

# UpdateProcess 控件

Visual Studio AJAX 扩展中的最后一个服务器控件是 `UpdateProcess` 控件。某些异步回回的执行需要一些时间，是因为响应的大小或返回结果所需的时间。`UpdateProcess` 控件允许向客户端提供视觉信号，显示工作正在进行且浏览器不会锁定。

#### 列表 18-15：使用 UpdateProcess 控件向客户端显示文本消息

```vbnet
<%@ Language="VB" %>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        System.Thread.Sleep(10000)
        Label1.Text = "This button was clicked on " &
        DateTime.Now.ToString()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>UpdatePanel</title>
    </head>
    <body>
        <form id="form1" runat="server">
            <div>
                <asp:ScriptManager ID="ScriptManager1" runat="server">
```

# 列表 18-15（续）

```aspnet
<asp:UpdateProgress ID="UpdateProgress" runat="server">
  <ProgressTemplate>
    An update is occurring...
  </ProgressTemplate>
</asp:UpdateProgress>
<asp:UpdatePanel ID="UpdatePanel" runat="server"
  UpdateMode="Conditional">
  <ContentTemplate>
    <asp:Label ID="Label" runat="server"></asp:Label>
  </ContentTemplate>
  <Triggers>
    <asp:AsyncPostBackTrigger ID="Button1"
      Event="Click" />
  </Triggers>
</asp:UpdatePanel>
<br />
<br />
<asp:Button ID="Button1" runat="server"
  Text="Click to initiate async request"
  OnClick="Button1_Click" />
</form>
</body>
</html>
```

```csharp
# Page Language="C#" %>
<script runat="server">
protected void Button1_Click(object sender, EventArgs e)
{
  Label.Text = "This button was clicked on " +
  DateTime.Now.ToString();
}
</script>
```

为了给响应添加延迟（模拟长时间运行计算机进程），调用了 `Thread.Sleep()` 方法。从这里开始，在页面显示更新消息的部分添加 `UpdateProgress` 控件。在这种情况下，`UpdateProgress` 控件被添加到 `UpdatePanel` 服务器控件上方。该控件没有进入 `UpdatePanel` 内部，而是位于控件外部。然而，像 `UpdatePanel` 控件一样，`UpdateProgress` 控件也是一个模板控件。

`UpdatePlace` 控件只有一个子元素：`<ProgressTemplate>` 元素。控件中此部分的任何内容在 `UpdateProgress` 控件被触发时都会出现。在所示内容中，图 18-13 中显示的唯一项将会出现。

![](img/7040c21013b8e6c23c612d6da3599ff8_791_0.png)

FIGURE 18-13

在这种情况下，文本会立即出现，并且在异步回传（Postback）完成之前不会消失。你放在 `<ProgressTemplate>` 区域中的代码实际上包含在页面中，但通过 CSS 禁用了它的显示。

```
<div id="UpdateProgress1" style="display:none">
  An update is occurring...
</div>
```

# 控制消息出现的时间

现在，`UpdateProgress` 在点击按钮后就会出现。然而，你的某些过程可能不会花费那么长时间，而且你可能并不总是需要等待进度通知发送到客户端。`UpdateProgress` 控件包含一个 `DisplayAfter` 属性，它允许你控制进度更新消息何时出现。列表 18-16 显示了 `DisplayAfter` 属性的使用。

#### 列表 18-16：使用 `DisplayAfter` 属性

```
<UpdateProgress ID="UpdateProgress1" runat="server" DisplayAfter="5000">
  <ProgressTemplate>
    An update is occurring...
  </ProgressTemplate>
</UpdateProgress>
```

`DisplayAfter` 属性的值是一个数字，代表 `UpdateProgress` 控件在显示 `<ProgressTemplate>` 部分的内容之前等待的毫秒数。列表 18-16 中的代码指定 `<ProgressTemplate>` 部分将显示 5,000 毫秒（5 秒）。

# 在 `<ProgressTemplate>` 中添加图像

之前使用 `UpdateProgress` 控件的示例使用了此文本控件，但你可以在此模板控件中放置任何想要的内容。例如，你可以放置一个旋转图像，向用户显示请求正在处理。列表 18-17 显示了图像的使用。

#### 列表 18-17：在 `<ProgressTemplate>` 部分使用图像
