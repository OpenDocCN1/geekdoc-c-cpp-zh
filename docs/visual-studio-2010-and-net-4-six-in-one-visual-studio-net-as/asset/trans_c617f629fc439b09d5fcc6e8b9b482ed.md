
DropShadowExtender 也挂载到了控件上。第二个矩形面板由 DragPanelExtender 装饰。在图 20-25 中，它从原始位置移动到了新位置，与可折叠面板部分重叠。

列表 20-23 显示了页面的代码。

# 列表 20-23: PanelExtendersSample.aspx

```asp
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="PanelExtenders.aspx.cs"
Inherits="CSharpPanelManager.PanelExtenders" %>

<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/html/html-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
runat="server">
<title>Ajax Panel examples sample</title>
</head>
<body style="font-family: verdana; font-size:12px">
<form id="form" runat="server">
<asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server" />
<div>
<asp:Panel ID="Panel2" runat="server" Height="30px">
<div style="padding: 5px; vertical-align:middle;">
<div style="float: left;">Dynamics in C#</div>
<div style="float: left; margin-left: 20px;">
<asp:Label ID="Label1" runat="server" Text="Show Details..."></asp:Label>
</div>
<div style="float: right; vertical-align:middle;">
<asp:ImageButton ID="Image1" runat="server"
ImageUrl="/Images/ShowDetails.png"
AlternateText="Show Details..." />
</</div>
</div>
</asp:Panel>
<asp:Panel ID="CSharpPanel" runat="server"
Style="padding: 12px; background-color: Yellow"
Height="0">
<p>
长期以来，C# 无法与这些语言和工具的灵活性相竞争。但现在情况已不再如此。
</p>
</asp:Panel>
<asp:CollapsiblePanelExtender ID="cDemo" runat="Server"
TargetControlID="Panel2"
ExpandControlID="Panel2"
CollapseControlID="Panel2"
Collapsed="True"
TextLabel="Label1"
ImageControlID="Image1 />
</div>
</form>
```

```asp
ExpandedText='Hide Details...'
CollapsedText='(Show Details...)'
ExpandedImage='/Images/HideDetails.png'
CollapsedImage='/Images/ShowDetails.png'
SuppressPostBack='true' />
<asp:DropShadowExtender ID="DropShadowExtender1" runat="server"
TargetControlID="CSharpPanel"
Width="80"
Rounded="true"
Radius="6"
Opacity=".25"
TrackPosition="true" />
<hr />
<hr />
<div style="height:300px; width:250px; float: left; padding: 5px;">
<asp:Panel ID="HandlePanel" runat="server" Width="100%" Height="20px"
Style="z-index:20px;"BorderStyle="Solid" BorderWidth="1px" BorderColor="black">
<div style="cursor:move">Drag me</div>
<asp:Panel ID="InfoPanel" runat="server" Width="100%" Height="20px"
Style="overflow:auto; padding: 8px; Background=#F4BCC"
BorderWidth="2px" BorderColor="black"
BorderStyle="Solid">
<div>
<p>
COM 的版本提供了动态绑定，作为选择和执行操作的统一方法。
操作可以一致地应用于各种对象，而不论特定对象是来自
（通过互操作性）、IronRuby、IronPython、HTML
DOM，还是来自任何其他语境。
</p>
</div>
</asp:Panel>
</div>
<div style="clear: both;"></div>
<asp:DraggableExtender ID="DraggableExtender1" runat="server"
TargetControlID="DraggablePanel"
DragHandleID="HandlePanel" />
</div>
</form>
</body>
</html>
```

## PopupExtenders.aspx

你可以分别通过 `ExpandControlID` 和 `CollapsePanel` 属性设置控件来展开和折叠面板。你还可以通过 `ExpandedText`、`CollapsedText`、`ExpandedImage` 和 `CollapsedImage` 属性指定面板的样式和图像。当你设置 `SuppressBack` 为 `True` 时，展开或折叠面板时不会触发回回。`DropShadowExtender` 有几个属性可以指定阴影如何应用于面板。`Width` 允许你设置阴影的大小，并且可以通过指定的 `Radius` 进行圆角处理。`Opacity` 也可以设置。当你的面板可移动或可调整大一时，将 `TrackPosition` 设置为 `True` 将使阴影跟随面板。`DragPanelExtender` 只需要指定 `DragHandleID` 属性，指向作为手柄的控件。

有两个控件可以帮助你在页面上显示弹出面板（或其他弹出控件）：

- `PopupControlExtender` 可以挂载到任何控件上，以打开一个显示额外内容的弹出窗口。该弹出窗口将具有交互性，并在 `UpdatePanel` 内部工作，因此它能够执行服务器端处理（包括回回），而不影响页面的其他部分。
- `ModalPopupExtender` 允许你在模拟对话框的元素中显示内容，从而防止用户与页面进行交互。

当你使用 AjaxControls 项目时，`PopupExtendersSample.aspx` 页面显示了你如何使用这些控件。使用 `PopupControlExtender` 显示一个填充了名称的 `ListBox`。它绑定到 `TextBox` 上，当它获得焦点时，`ListBox` 会立即弹出。图 20-26 显示了这种情况。从 `ListBox` 中选择一个项将关闭弹出面板，并使用所选名称创建 `TextBox` 的内容。当你点击 Send 按钮时，将显示一个模态弹出面板，允许你确认消息发送，如图 20-27 所示。

![](img/b597c74e848b27b0d30153ae1606_993_0.png)
