
<asp:Button ID="Button1" runat="server" Text="Button" />

<asp:Panel ID="Panel" runat="server" 
style="display:none; background-color:White; width:200;
border-width:20px; border-color:Black; border-style:solid;
padding:20px;
你确定要点击这个按钮吗？<br />
```

```asp
<asp:Button ID="ButtonYes" runat="server" Text="Yes" />
<asp:Button ID="ButtonNo" runat="server" Text="No" />
<asp:Panel>
<div>
</form>
<body>
</html>
```

在这个示例中，`ConfirmButtonExtender` 仍然指向页面上的 `Button1` 控件，这意味着当按钮被点击时，`ConfirmButtonExtender` 将采取行动。它没有使用 `ConfirmText` 控件，而是使用了 `DisplayModalPopupControl`。在这种情况下，它指向 `ModalPopupExtender1` 控件——另一个扩展器。

`ModalPopupExtender` 反而通过 `PopupControl` 属性引用页面上的 `Panel` 控件。此 `Panel` 的内容用于点击按钮时的确认。为了这项工作，`ModalPopupExtender` 必须为 `OkControlID` 和 `CancelControlID` 属性赋值。在这种情况下，这两个属性指向包含在 `Panel` 内的两个按钮。当你运行此页面时，将得到图 19-13 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_822_0.png)

图 19-15

## DragPanelExtender

`DragPanelExtender` 允许你定义用户可以随意在页面上移动元素的区域。用户能够将元素拖放到页面的任何地方。要启用此功能，你必须做几件事。第一个建议是创建一个足够大的 `<div>` 区域以便拖动该项目。从这里开始，你需要指定用什么用作拖动手，以及哪个控件将跟随拖动手移动。在列表 19-12 的示例中，`Label` 控件被用作拖动手，而 `Panel2` 控件是跨屏幕拖动的内容。

### 列表 19-12：在页面上拖动面板控件

```asp
<%@ Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit" 
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>DragPanel 控件</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server">
</asp:ToolkitScriptManager>
<div style="height:60px">
<asp:DragPanelExtender ID="DragPanelExtender1" runat="server"
DragHandleID="Label1" TargetControlID="Panel2"
/>
</asp:DragPanelExtender>
<asp:Panel ID="Panel1" runat="server" Width="450px">
<asp:Label ID="Label1" runat="server" BackColor="Blue" />
</asp:Panel>
<asp:Panel ID="Panel2" runat="server" Width="450px">
Lorem ipsum dolor amet, consectetur adipiscing elit.
Duis accumsan lorem consectetur tempus metus
Aenean tincidunt venenatis tellus. Suspendisse molestie
```

### 列表 19-12 (续)

```text
curriculum ipsum. Curabitur ut lectus. Nulla ad nec elit
convallis vulputate. Nulla pharetra phravin nunc. Duis
or orci. Phasellus tortor at orci, mollis neque Sed.
Vestibula porta tellus orci suscipit lobortis massa.
Maecenas varius, erat non odio, ac luctus,
feugiat non, odio, mauris. Donec mauris,
metus sed, vehicula a elit, turpis nisl. Aliquam erat a neque, risus. Pellentesque 
diet, nisl, massa. Proin at massa vel nisl, 
quisque neque, neque. Sed vitae tellus. Donec 
aliquam erat, feugiat sed, nisl, dictum 
in mauris. Pellentesque massa, a elit, 
quisque neque, neque. Sed vitae tellus.
```

每个 `LinkButton` 控件都设计了一个显示在页面上的特定图像。选择其中一个选项，可以通过 `_Option_Click()` 方法更改所选图像。运行此页面将得到如图 19-17 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_825_0.png)

图 19-17

## DropShadowExtender

`DropShadowExtender` 允许你为页面上的 ASP.NET 面板或图像添加投影（DropShadow）效果。你可以设置 `TargetControlID`，并控制宽度（Width）和不透明度（Opacity），而且角应该是圆角的（Rounded）。如果面板可以移动或调整大小，还可以将 `TrackPosition` 属性设置为 `True`，以指示 JavaScript 脚本将运行以跟踪面板并更新投影。

你首先想到的使用它的地方可能是作为图像（如图 19-14 所示），但你可以将其用于任何需要的控件。

- 列表 19-14：在图像控件上使用 DropShadowExtender

```
<@ Page Language="C#" %>
<@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<server runat="server">
<title>DropShadowExtender Control</title>
</head>
<body>
<form id="form" runat="server">
<div>
<asp:ToolkitScriptManager ID="ToolkitScriptManager" runat="server">
</asp:ToolkitScriptManager>
<asp:DropShadowExtender ID="DropShadowExtender1" runat="server"
TargetControlID="Image1" />
</asp:DropShadowExtender>
<asp:Image ID="Image1" runat="server"
ImageUrl="Images/Garden.jpg" />
</div>
</form>
</body>
</html>
```

在这个示例中，实现这一操作只需像使用 `TargetControlID` 为 `Image` 的 `DropShadowExtender` 控件一样简单。在此处，图像将显示在浏览器中，如图 19-18 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_826_0.png)

图 19-18

如所述，除了图像外，你几乎可以将 DropShadowExtender 用于几乎任何地方。列表 19-15 显示了如何将其与 `Panel` 控件配合使用。

- 列表 19-15：在 Panel 控件上使用 DropShadowExtender

```
<@ Page Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit" 
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>DropShadowExtender Control</title>
</head>
<body>
<form id="form" runat="server">
<div>
<asp:ToolkitScriptManager ID="ToolkitScriptManager" runat="server" />
<asp:DropShadowExtender ID="DropShadowExtender1" runat="server" 
TargetControlID="Panel1" Rounded="True" />
<asp:Panel ID="Panel1" runat="server" BackColor="Orange" 
Width="300" HorizontalAlign="Center">
<asp:Login ID="Login1" runat="server">
</asp:Login>
</asp:Panel>
</div>
</form>
</body>
</html>
```

在这种情况下，带有 `Login` 控件的 `Panel` 控件使用 `DropShadowExtender` 控件进行了扩展。结果与图像控件的结果非常相似。然而，这里 `DropShadowExtender` 控件的一个额外之处是 `Rounded` 属性被设置为 `True`（默认设置为 `False`）。这产生了如图 19-19 所示的效果。

768 | 第 19 章 ASP.NET AJAX 控件包

![](img/7040c21013b8e6c23c612d6da3599ff8_827_0.png)

图 19-19

如从图 19-19 中所示，不仅投影的边缘是圆角的，整个 `Panel` 控件也具有圆角。你可以操作的其他属性包括控制投影不透明度的 `Opacity`（不透明度）属性，以及用于圆角边缘半径的 `Radius`（半径）属性（显然，当 `Rounded` 属性设置为 `True` 时它有效）。默认情况下，`Opacity` 设置为 1，这意味着 100% 可见。要将其设置为（例如）50% 的不透明度，你需要将 `Opacity` 值设置为 `.5`。

## DynamicPopulateExtender

`DynamicPopulateExtender` 允许你将动态 HTML 输出同步到 `Panel` 控件。为了完成这项工作，你需要一个触发向服务器回调的控件或事件，以获取 HTML，然后将其推送到 `Panel` 控件，从而在客户端进行动态更改。

与 `AutoCompleteExtender` 一样，你需要一个异步向客户端返回某些内容的服务器端事件。列表 19-6 显示了在 .aspx 页面上使用此控件的代码。

- 列表 19-6：使用 DynamicPopulateExtender 控件填充 Panel 控件

```
（注：由于原文此处代码部分存在大量混乱和重复，翻译已根据上下文逻辑进行了结构对齐）
```

Integrated Security-True;User Instance-True;
// 在代码中将此字符串放在的一行
`cmd = new SqlCommand(cmdString, conn);`
`conn.Open();`

`SqlDataReader myReader;`
`myReader = cmd.ExecuteReader(CommandBehavior.CloseConnection);`

`DataTable dt = new DataTable();`
`dt.Load(myReader);`
`myReader.Close();`

`GridView myGrid = new GridView();`
`myGrid.ID = "GridView1";`
`myGrid.DataSource = dt;`
`myGrid.DataBind();`

`StringWriter sw = new StringWriter();`
`HtmlTextWriter htw = new HtmlTextWriter(sw);`

`myGrid.Render(htp);`
`hw.Close();`

`return sw.ToString();`

文件名 `DynamicPopulateExtender.aspx.vb` 和 `DynamicPopulateExtender.aspx`

这段代码是 `DynamicPopulateExtender.aspx` 页面的后代码（code-behind），包含一个被异步调用的方法。`GetDynamicContext()` 方法接收一个参数 `contextKey`，这是一个用于确定用户点击了内容的字符串值。

根据选择，将使用特定的命令来填充 `DataTable` 对象。从这里开始，`DataTable` 对象被用作程序化 `GridView` 控件的数据源，该控件被渲染并作为字符串返回给它。客户端将获取这个长字符串并使用该文本填充其所在的 `Panel`。图 19-20 显示了点击其中一个链接的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_830_0.png)

图 19-20

## FilteredTextBoxExtender

`FilteredTextBoxExtender` 控件控制 `TextBox` 的功能，用于指定最终用户可以输入控件的字符。例如，如果你希望用户只能向文本框输入数字，则可以使用 `FilteredTextBoxExtender` 用于 `TextBox` 并控制此类行为。列表 19-18 展示了此示例。

### 列表 19-18：将文本框过滤为仅数字

```
<@ Page Language="C#" %>
<%@ Register Assembly="AjaxToolkit" TagPrefix="asp" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="server" />
    <title>FilteredTextBoxExtender Control</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server" />
            <asp:FilteredTextBoxExtender>
            <asp:FilteredTextBoxExtender Id="FilteredTextBoxExtender1" 
                runat="server"
                TargetControlID="TextBox1" FilterType="Numbers">
            </asp:FilteredTextBoxExtender>
            <asp:TextBox Id="TextBox1" runat="server"></asp:TextBox>
        </div>
    </form>
</body>
</html>
```

在这种在这种情况下，通过使用 `TargetControlID` 属性将 `FilteredTextBoxExtender` 控件附加到 `TextBox1`。`FilteredTextBoxExtender` 控件有一个 `FilterType` 属性，其值为 Custom、Lowercase、Numbers 和 Uppercase。

此示例使用了 `FilterType` 值 `Numbers`，意味着文本框中只能输入数字。如果用户尝试输入任何其他类型的信息，则什么都不会发生——框将保持为空，因为用户没有输入任何键。

`FilteredTextBoxExtender` 控件还暴露了 `FilterMode` 和 `InvalidChars` 属性。以下是使用这些属性的一个示例：

```
<asp:FilteredTextBoxExtender Id="FilteredTextBoxExtender1" runat="server"
    TargetControlID="TextBox1" InvalidChars="*" />
```
