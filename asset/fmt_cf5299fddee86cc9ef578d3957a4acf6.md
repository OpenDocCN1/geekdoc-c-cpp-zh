
# C#

```csharp
public partial class SlideShowExtender : System.Web.UI.Page
{
    [System.Web.Services.WebMethodAttribute(),
     System.Web.Services.ScriptMethodAttribute()]
    public static Slide[] GetSlides(string contextKey)
    {
        return new AjaxControlToolkit.Slide[] {
            new AjaxControlToolkit.Slide("Images/ToolkitLogo.jpg"),
            "The Logo", "This is the Ajax Control Toolkit Logo.",
            new AjaxControlToolkit.Slide("Images/ToolkitLogo1.jpg"),
            "The 2nd Logo", "This is the modified Ajax Control Toolkit Logo.",
            new AjaxControlToolkit.Slide("Images/ToolkitLogo2.jpg"),
            "The 3rd Logo", "This is another modified Ajax Control Toolkit Logo."
        };
    }
}
```

带有后台代码（code-behind），`SlideShowExtender` 有一个调用图片的方法。该方法 `GetSlides()` 返回 `Slide` 对象数组，需要位置、标题和描述。运行此页面，你将得到如图 24-36 所示的结果。

![](img/67a6707ff505c052edb96c0128fb3096_988_0.png)

图 24-36

点击页面上的播放按钮将循环播放图片直到完成，除非你设置了 `SlideShowExtender` 的 `Loop` 属性为 True（默认设置为 False）。

另一个需要注意的属性是 `PlayInterval`。该属性的值是浏览器切换到下一张图片所需的毫秒数。默认将其设置为 3000 毫秒。

## TextBoxWatermarkExtender

`TextBoxWatermarkExtender` 允许你在控件中放置说明，让用户更好地了解如何使用控件。这可以是文本，也可以是图片（使用 CSS）。列表 24-32 展示了与 `TextBox` 使用此控件的示例。

## 列表 24-32：使用 TextBoxWatermarkExtender

```xml
<%@ Language="C#" %>
<%@ Assembly="AjaxControlToolkit" %>
<%@ Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<!DOCTYPE html>
<html>
<head runat="server">
  <title>TextBoxWatermarkExtender</title>
  <style type="text/css">
    .watermark{
      width:150px;
      font:Verdana;
      font-style:italic;
      color:Gray;
    }
  </style>
</head>
<body>
  <form id="form1" runat="server">
    <div>
      <asp:ToolkitScriptManager ID="ScriptManager1" runat="server">
      </asp:ToolkitScriptManager>
      <asp:TextBoxWatermarkExtender ID="WatermarkExtender"
        runat="server"
        Watermark="Enter something here"
        TargetControlID="TextBox1"
        WatermarkCssClass="watermark">
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
      </asp:TextBoxWatermarkExtender>
    </div>
  </form>
</body>
</html>
```

`TextBoxWatermarkExtender` 与简单的 `TextBox` 关联，并使用 `Watermark` 属性提供显示在 `TextBox` 内部的文本。图 24-37 显示了控件的结果。

要为文本应用任何样式，可以使用 `WatermarkCssClass`，如列表 24-33 所示。

## 列表 24-33：为水印应用样式

## 第 24 章 | AJAX 控制工具包 (AJAX CONTROL TOOLKIT)

## 代码列表 24-34（续上）

```asp
<asp:ToggleButtonExtender>
<asp:CheckBox ID="Checkbox1" runat="server"
Text="&nbsp;Option One /"
<asp:ToggleButtonExtender ID="ToggleButtonExtender2"
runat="server" TargetControlID="Checkbox2"
UncheckedImageUrl="Images/Checked.gif"
CheckedImageAlternateText="Checked"
UncheckedImageAlternateText="Not Checked" ImageWidth="25"
ImageHeight="25">
</asp:ToggleButtonExtender>
<asp:CheckBox ID="Checkbox2" runat="server"
Text="&nbsp;Option Two /"
</div>
</form>
</</body>
</html>
```

此页面包含两个 `CheckBox` 控件。每个复选框都有一个关联的 `ToggleButtonExtender` 控件，并配合 `MutuallyExclusiveCheckBoxExtender` 控件将这两个框框绑定在一起。`ToggleButtonExtender` 控件使用 `CheckedImageUrl` 和 `UncheckedImageUrl` 属性来指定要使用的适当图像。然后，如果用户的浏览器禁用了图像，则将使用在 `CheckedImageAlternateText` 和 `UncheckedImageAlternateText` 属性中提供的文本。你还需要为范围指定 `ImageWidth` 和 `ImageHeight` 属性的值。

运行此页面得到的结果与图 24-39 所示类似。

## UpdatePanelAnimationExtender

在 `UpdatePanel` 内容刷新时对其进行动画处理是一个常见场景。`UpdatePanelAnimationExtender` 允许你使用工具包中提供的系列动画，并在指定的 `UpdatePanel` 更新或更新完成后自动协调这些动画。

`UpdatePanelAnimationExtender` 允许你针对两个特定事件为 `Panel` 控件应用动画。第一个是 `OnUpdating` 事件，第二个是 `OnUpdated` 事件。你可以使用 Ajax Control Toolkit 提供的动画框架根据这两个事件来更改页面样式。代码列表 24-35 显示了当用户点击页面上位于 `UpdatePanel` 控件的日历（`Calendar`）控件中的某个特定日期时，`OnUpdated` 事件的示例。

## 代码列表 24-35：在 OnUpdated 事件上使用动画

### VB

```vb
<@ Page Language="VB" %>
<%@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<script runat="server">
Protected Sub SubCalendar1_CheckedChanged(sender As Object, ByVal e As EventArgs)
Label1.Text = "The date selected is " & 
Calendar1.SelectedDate.ToLongDateString()
End Sub
</script>
```

![](img/67a6707ff505c052edb96c0128fb3096_991_0.png)

图 24-39

### ASP.NET AJAX 控件

```html
<!DOCTYPE html>
<html runat="server">
  <title>UpdatePanelAnimationExtender Control</title>
</head>
<body>
  <form id="form1" runat="server">
<div>
    <asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server">
    </asp:ToolkitScriptManager>
    <asp:UpdatePanelAnimationExtender
      ID="UpdatePanelAnimationExtender1"
      runat="server" TargetControlID="UpdatePanel">
      <Animations>
        <Color PropertyKey="background"
          StartValue="#999996"
          EndValue="#FFFFFFFF" Duration="5.0" />
      </Animations>
    </asp:UpdatePanelAnimationExtender>
    <asp:UpdatePanel ID="UpdatePanel" runat="server">
      <ContentTemplate>
        <asp:Label ID="Label" runat="server"></asp:Label>
        <br />
        <asp:Calendar ID="Calendar1" runat="server"
          onselectionchanged="Calendar1_SelectionChanged(object sender, EventArgs e)" />
      </ContentTemplate>
    </asp:UpdatePanel>
</div>
  </form>
</body>
</html>
```

### C#

```csharp
<@ Page Language="C#" %>
<@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit"
TagPrefix="asp" %>
<script runat="server">
protected void Calendar1_SelectionChanged(object sender, EventArgs e)
{
  Label.Text = "The date selected is " + Calendar1.SelectedDate.ToLongDateString();
}
</script>
```

通过这段代码，当你点击日历控件内的一个日期时，包含日历的 `UpdatePanel` 的整个背景将从一种颜色变为另一种颜色，持续时间为你构建的动画中指定的 5 秒。你定义的动画可以变得复杂，而构建豪华的动画超出了本章的范围。

## ValidatorCalloutExtender

最后一个扩展器控件是 `ValidatorCalloutExtender` 控件。该控件允许你为表单的终端用户添加更明显的验证消息。你将此控件不是与被验证的控件关联，而是与验证控件本身关联。代码列表 24-36 展示了将 `ValidatorCalloutExtender` 控件与 `RegularExpressionValidator` 控件关联的示例。

## 代码列表 24-36：使用 ValidatorCalloutExtender 创建验证提示

```csharp
<@ Language="C# %>
<@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<!DOCTYPE html>
<html runat="server">
<title>ValidatorCalloutExtender Control</title>
</head>
<body>
  <form id="form1" runat="server">
<div>
    <asp:ToolkitScriptManager ID="ToolkitScriptManager1" runat="server"></asp:ToolkitScriptManager>
    <asp:ValidatorCalloutExtender ID="ValidatorCalloutExtender1"
        runat="server" TargetControlID="RegularExpressionValidator1"></asp:ValidatorCalloutExtender>
    <asp:Label Text="Email:">
    <asp:TextBox ID="TextBox1" runat="server" />
    <asp:RegularExpressionValidator ID="RegularExpressionValidator1"
        runat="server" ErrorMessage="You must enter an email address" Display="None"
        ControlToValidate="TextBox1"
        ValidationExpression="[\w-]+\[\w-]+\.[\w-]{2,4}" />
    <br />
    <asp:Button ID="Button" runat="server" Text="Submit" />
  </div>
  </form>
</body>
</html>
```

此页面包含一个文本框、一个提交按钮和一个正则表达式控件。`ValidatorCalloutExtender` 允许你在验证失败时显示错误消息。虽然 `Display` 属性设置为 `None`，但 `ValidatorCalloutExtender` 会提供提示信息。运行此页面产生的结果如图 24-40 所示。

![](img/67a6707ff505c052edb96c0128fb3096_993_0.png)

图 24-40

# 列表 24-37（续）

```asp
<asp:AccordionPane runat="server" ID="AccordionPanel">
  <Header>
    这是第一个面板
  </Header>
  <Content>
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Dunc accumsan lorem. Ut consectetur metus.
    Aenean tincidunt venenatis tellus. Suspendisse molestie
    curs ipsum. Curabitur ut lectus. Nulla acc nulla nec
    convallis putate. Nullam pharetra pulinar nunc. Duis
    norci. Phasellus tortor at neque.
    Vestibum porta tellus eu. Suspendisse quis massa.
    Maecenas varius, erat non ullamcorper, mauris erat
    if odio, ut gravida nisque a ipsum. Vivamus
    facilisis. Cras viverra. Curabitur.
    ut augue dolor semper posuere. Aenean at magna eu eros
    temporheta. Aenean mauris.
  </Content>
  <asp:AccordionPane runat="server" ID="AccordionPane2">
    <Header>
    这是第二个面板
  </Header>
    <Content>
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
```
