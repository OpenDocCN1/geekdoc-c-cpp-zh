
DropShadowExtender is also attached to the control. The second rectangular panel is decorated with a DragPanelExtender. In Figure 20-25, it is moved from its original position to a new location partially overlapping with the collapsible panel.

Listing 20-23 shows the code of the page.

# LISTING 20-23: PanelExtendersSample.aspx

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
  For a long time, C# could not compete with the flexibility of these languages and tools. But, that is no longer the case.
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
The version of COM provides dynamic binding as a unified
approach to selecting and carrying out operations.
Operations can be uniformly applied on various objects
independently of whether a specific object comes from
(through interoperability), IronRuby, IronPython, the HTML
DOM, or from any other context.
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

You can set controls to expand and collapse the panel through the ExpandControlID and CollapsePanel properties respectively. You can also specify the style and images for the panel with the ExpandedText, CollapsedText, ExpandedImage, and CollapsedImage properties. When you set SuppressBack to True, no postbacks are initiated when you expand or collapse the panel. The DropShadowExtender has a few properties to specify how shadow should be applied to the panel. Width lets you set the size of the shadow, which can be Rounded with the specified Radius. Opacity also be set. When your panel is movable or resizable, setting TrackPosition to True will follow the shadow to the panel. DragPanelExtender requires only specifying the DragHandleID property points to the control that serves as handle.

Two controls help you display pop-up panels (or other pop-up controls) on the page:

- PopupControlExtender can be attached to any control to open a pop-up window that displays additional content. This pop-up window will be interactive and work within an UpdatePanel, so it will be capable of performing server-side processing (including postbacks) without affecting the rest of the page.
- ModalPopupExtender allows you to display content in an element that mimics a dialog box, which prevents the user from interacting with the page.

When you use the AjaxControls project, PopupExtendersSample.aspx page shows how you can use these controls. Use PopupControlExtender to display a ListBox filled with names. This is bound to a TextBox that, when it receives focus, the ListBox is immediately popped up. Figure 20-26 shows this situation. Selecting an item from the ListBox will close the pop-up panel and use the selected name to create the TextBox's content. When you click the Send button, a modal pop-up panel is displayed, allowing you to confirm message sending, as shown in Figure 20-27.

![](img/b597c74e848b27b0d30153ae1606_993_0.png)
![](img/b597c74e848b27b0d30153ae1606_993_1.png)

# LISTING 20-24: PopupExtendersSample.aspx

![](img/b597c74e848b27b0d30153ae1606_994_0.png)

```asp
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="PopupExtenderSample.aspx.cs"
Inherits="ControlSamples.PopupExtenderSample" %>
<% Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit"
TagPrefix="asp" %>
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/xhtml-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta runat="server">
<title>Ajax PopupExtender sample</title>
<style type="text/css">
modalBackground {
background-color:Gray;
filter:alpha(opacity=70);
opacity:0.7;
}
</style>
</head>
<body style="font-family: verdana; font-size: 12px">
<form id="form" runat="server">
<div>
<asp:ScriptManager ID="ToolkitScriptManager1" runat="server" />
<asp:UpdatePanel runat="server" ID="up2">
<ContentTemplate>
Message Title:
<asp:TextBox ID="MessageTextBox" AutoComplete="off" />
<br /><br />
<asp:Panel ID="ExpertPanel" runat="server" CssClass="popupControl">
<div style="border:1px outset white; width:140px">
<asp:ListBox ID="ExpertList" runat="server" Width="140px"
DataSourceID="ExpertDataSource"
DataField="Name"
DataValue="Name"
AutoPostBack="true"
Rows="8"
OnChanged="ExpertList_SelectedIndexChanged" />
<asp:AccessDataSource ID="ExpertDataSource" runat="server"
DataFile="~/App_Data/ExpertData.mdb"
SelectCommand="SELECT [Name] FROM [Expert]" />
```

[995]

# LISTING 20-24 (continued)

```asp
Position="Bottom"
CommitScript="e.value = 'Your expert is: ' + e.value;" />
</div>
<asp:Panel>
<p>Are you sure you want to send the message?</p>
<div>
<asp:Button ID="OkButton" runat="server" Text="OK"
OnClick="OnClickClick"
UseSubmitBehavior="False" />
<asp:Button ID="CancelButton" runat="server" Text="Cancel"
OnClick="CancelButtonClick"
UseSubmitBehavior="False" />
</p>
</div>
</asp:Panel>
<asp:ModalPopupExtender ID="ModalPopupExtender" runat="server"
TargetControlID="SendButton"
PopupControlID="PopupPanel"
BackgroundCssClass="modalBackground"
OkControlID="OkButton"
CancelControlID="CancelButton"
DropShadow="true" />
</ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
</body>
</html>
```
