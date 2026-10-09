
```asp
<@ Page Language="VB" %>
<% Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit" TagPrefix="cc1" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>UpdatePanelExtender Control</title>
</head>
<body>
  <script runat="server">
    Protected Sub Calendar1_SelectionChanged(ByVal As Object, ByVal As EventArgs)
        Label.Text = "The date is selected is & & Calendar1.SelectedDate.ToLongDateString()
    End Sub
  </script>
  <form id="form1" runat="server">
    <div>
      <asp:ScriptManager ID="ScriptManager1" runat="server"></asp:ScriptManager>
      <cc1:UpdatePanelAnimationExtender ID="UpdatePanelAnimationExt1" runat="server" TargetID="UpdatePanel">
        <Animations>
          <OnUpdated>
            <Sequence>
              <Color PropertyKey="background" StartValue="#FFFFFF" EndValue="#FFFFFF" Duration="5.0" />
            </Sequence>
          </OnUpdated>
        </Animations>
      </cc1:UpdatePanelAnimationExtender>
      <asp:UpdatePanel ID="UpdatePanel" runat="server">
        <ContentTemplate>
          <asp:Label ID="Label" runat="server"/>
          <asp:Calendar ID="Calendar1" runat="server" OnSelectionChanged="Calendar1_SelectionChanged"/>
        </ContentTemplate>
      </asp:UpdatePanel>
    </div>
  </form>
</body>
</html>
```

## 第 20 章：ASP.NET AJAX Control Toolkit

```html
<asp:Calendar ID="Calendar1" runat="server"
    onselectionchanged="Calendar1_SelectionChanged">
</asp:Calendar>
</ContentTemplate>
</asp:UpdatePanel>
</div>
</form>
<body
<html>
```

```csharp
<%@ Page Language="C#" %>

<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit"
TagPrefix="ccl" %>

<script runat="server">
    protected void Calendar1_SelectionChanged(object sender,
    EventArgs args)
{
    Label.Text = "The date selected is " +
    Calendar1.SelectedDate.ToShortDateString();
}
</script>
```

通过这段代码，当你点击日历中的某个日期时，`UpdatePanel`的整个背景将根据动画指定的，从一种颜色变为另一种颜色，持续五秒钟。你定义的动画可以变得复杂，而豪华动画将局限于本章的范围。

## ValidatorCalloutExtender

最后一个扩展器控件是`ValidatorCalloutExtender`控件。该控件允许你为操作表单的用户添加一个更显目的验证消息。你不是将其与被验证的控件关联，而是将其与验证控件本身关联。列表 20-35 展示了将`ValidatorCalloutExtender`控件与`RegularExpressionValidator`控件关联的示例。

### 列表 20-35：使用 ValidatorCalloutExtender 创建验证控件

```csharp
<%@ Page Language="C#" %>

<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="ccl" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>ValidatorCalloutExtender Control</title>
</head>
<body>
    <form id="form" runat="server">
<div>
```

```html
<asp:ScriptManager ID="ScriptManager1" run="server">
</asp:ScriptManager>
<cc:ValidatorCalloutExtender ID="ValidatorCalloutExtender1"
run="server" ControlID="RegularExpressionValidator1">
</cc:ValidatorCalloutExtender>
Email Address:&nbsp;
<asp:TextBox ID="TextBox" run="server"></asp:TextBox>
<asp:RegularExpressionValidator ID="RegularExpressionValidator1"
run="server"
ErrorMessage="You must enter an email address" Display="None"
ControlToValidate="TextBox"
ValidationExpression="^[\w-\.]+([.[\w-]*)@([\w-]+\.)+[a-zA-Z]{2,4}$"
</asp:RegularExpressionValidator><br />
<asp:Button ID="Button" run="server" Text="Submit" />
</div>
</form>
</body>
</html>
```

该页面包含一个用于表单的文本框、一个提交按钮，并按照惯常的方式构建了一个`RegularExpressionValidator`控件，只不过你可能使用了`Display`属性将其设置为`None`。你不希望普通的 ASP.NET 验证控件显示其消息，因为这将会与`ValidatorCalloutExtender`显示的消息冲突。尽管`Display`属性被设置为`None`，但你仍然使用`ErrorMessage`属性提供错误信息。运行此页面将产生图 20-41 所示的结果。

![](img/eb54f286ad47e89bbf83e32d279e6dd_1029_0.png)

## ASP.NET AJAX Control Toolkit 服务器控件

接下来的 ASP.NET AJAX 控件并不总是扩展其他 ASP.NET 控件，而是本身就是控件。后续章节将详细介绍这些控件。

### Accordion 控件（手风琴控件）

`Accordion`控件用于指定一组面板，类似于 Microsoft Outlook 中著名的导航菜单。每个面板由一个头部模板和一个内容模板组成。所有面板的头部模板始终可见，而用户可以通过点击头部来选择查看哪个面板。之前活动面板的内容将隐藏起来，取而代之的是显示新选面板的内容。

`Accordion`控件可以在不同活动面板之间切换时提供渐变过渡效果。将`FadeProperties`设置为`True`，你就可以设置`TransitionDuration`和`FramesPerSecond`值。默认值分别为 250 毫秒和每秒 40 帧。

`SelectedIndex`属性允许你通过声明式和程序化方式控制显示哪个面板。其他重要属性是`AutoSize`和`Height`属性。`AutoSize`属性默认为`None`，这意味着`Accordion`控件的大小根据活动面板而变化。屏幕上的其他内容可能会移动以适应变化的大小。然而，当`AutoSize`属性被设置为`Limit`时，大小将被限制在`Height`值上。如果内容大于可用尺寸，活动面板将滚动。另一个可能的值是`All`，如果内容不足以满足提供的`Height`值，则会展开面板。这是一个`Accordion`控件的运行示例。`Accordion`控件使用了两个面板。

### 列表 20-36：带有两个 AccordionPanes 的 Accordion 控件

```csharp
<%@ Page Language="C#" %>
<% Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="cc" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>AccordionControl</title>
<style type="text/css">
.titlebar {
    background-color:Blue;
    font-size:large;
    font-family:Verdana;
    border:3px Black;
}
</style>
</head>
<body>
<form id="form1" runat="server">
    <div>
    <asp:ScriptManager ID="ScriptManager1" runat="server">
    </asp:ScriptManager>
    <cc:Accordion ID="Accordion" runat="server" HeaderCssClass="titlebar"
HeaderSelectedCss="titlebar"
FadeTransitions="true"
TransitionDuration="333"
FramesPerSecond="30">
<Panes>
<cc:AccordionPane runat="server">
<Header>
    This is the first pane
</Header>
```

```html
<Content>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Donec accumsan lorem. Ut consectetuer metus. A Aenean tincidunt metus. Suspendisse molestie cursus. Curabitur lectus. Nulla dolor nec elit convallis vulputate. Nullam pharetra pulinar nunc orci. Phasellus a pretulum porta eu orci. Suspendisse massa. Maecenas erat, non ullamcorper non, mauris eleifend, ut gravida nisl neque a. Vivamus facilisis. Cras vivera. Curabitur augue et dolor posuere. Aenean at magna eros tempora pharetra. Aenean mauris.
</Content>
</cc:AccordionPane>
<cc:AccordionPane runat="server">
<Header>
This is the second pane
</Header>
<Content>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Donec accumsan lorem. Ut consectetuer metus. A Aenean tincidunt metus. Suspendisse molestie cursus. Curabitur lectus. Nulla dolor nec elit convallis vulputate. Nullam pharetra pulinar nunc orci. Phasellus a pretulum porta eu orci. Suspendisse massa. Maecenas erat, non ullamcorper non, mauris eleifend, ut gravida nisl neque a. Vivamus facilisis. Cras vivera. Curabitur augue et dolor posuere. Aenean at magna eros tempora pharetra. Aenean mauris.
</Content>
</cc:AccordionPane>
</Panes>
</Accordion>
</div>
</form>
</body>
</html>
```

该页面包含一个用于表单的文本框、一个提交按钮，并按照惯常的方式构建了一个`RegularExpressionValidator`控件，只不过你可能使用了`Display`属性将其设置为`None`。你不希望普通的 ASP.NET 验证控件显示其消息，因为这将会与`ValidatorCalloutExtender`显示的消息冲突。尽管`Display`属性被设置为`None`，但你仍然使用`ErrorMessage`属性提供错误信息。运行此页面将产生图 20-41 所示的结果。

![](img/eb54f286ad47e89bbf83e32d279e6dd_1029.png)

## ASP.NET AJAX Control Toolkit 服务器控件

接下来的 ASP.NET AJAX 控件并不总是扩展其他 ASP.NET 控件，而是本身就是控件。后续章节将详细介绍这些控件。

## Accordion 控件

`Accordion`控件用于指定一组面板，类似于 Microsoft Outlook 中著名的导航菜单。每个面板由一个头部模板和一个内容模板组成。所有面板的头部模板始终可见，而用户可以通过点击头部来选择查看哪个面板。之前活动面板的内容将隐藏起来，取而代之的是显示新选面板的内容。

`Accordion`控件可以在不同活动面板之间切换时提供渐变过渡效果。将`FadeProperties`设置为`True`，你就可以设置`TransitionDuration`和`FramesPerSecond`值。默认值分别为 250 毫秒和每秒 40 帧。

`SelectedIndex`属性允许你通过声明式和程序化方式控制显示哪个面板。其他重要属性是`AutoSize`和`Height`属性。`AutoSize`属性默认为`None`，这意味着`Accordion`控件的大小根据活动面板而变化。屏幕上的其他内容可能会移动以适应变化的大小。然而，当`AutoSize`属性被设置为`Limit`时，大小将被限制在`Height`值上。如果内容大于可用尺寸，活动面板将滚动。另一个可能的值是`All`，如果内容不足以满足提供的`Height`值，则会展开面板。这是一个`Accordion`控件的运行示例。`Accordion`控件使用了两个面板。

### 列表 20-36：带有两个 AccordionPanes 的 Accordion 控件
