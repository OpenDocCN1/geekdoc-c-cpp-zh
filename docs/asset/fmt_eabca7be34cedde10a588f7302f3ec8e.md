
```vb
' Draw the circle for the signal light

grfGraphics.FillEllipse(bshBrush, nCirclePositionX,

    nCirclePositionY, nCircleDiameter, nCircleDiameter)

End Sub
```

来自 TrafficLight 的代码片段

通过从“生成”菜单中选择“生成”来生成控件库。这将在保存 Control Library 解决方案的`/bin`目录中创建一个 DLL。

接下来，启动一个新的 Windows 应用程序项目。从工具箱顶部将一个`TrafficLight`控件拖到 Windows 应用程序项目的窗体上。注意，其属性窗口包含一个`Status`属性。将它设置为`statusYellow`。窗体设计图面上控件的渲染将更改以反映这个新状态。将`TrafficLight`控件的背景色改为深灰色，以提高其对比度。（`TrafficLight`的`BackColor`属性继承自`Control`类。）

在窗体代码的顶部放置以下代码行，以使交通灯状态的枚举值可用：

```vb
Imports TrafficLight.TrafficLight
```

在窗体上添加三个按钮（分别命名为`btnRed`、`btnYellow`和`btnGreen`），以使`TrafficLight`控件显示为红色、黄色和绿色。按钮的逻辑大致如下：

```vb
Private Sub btnRed_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles btnRed.Click
    TrafficLight1.Status = TrafficLightStatus.statusRed
End Sub

Private Sub btnYellow_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles btnYellow.Click
    TrafficLight1.Status = TrafficLightStatus.statusYellow
End Sub

Private Sub btnGreen_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles btnGreen.Click
    TrafficLight1.Status = TrafficLightStatus.statusGreen
End Sub
```

在解决方案资源管理器中，右键单击你的测试 Windows 应用程序项目，然后选择“设为启动项目”。接着按 F5 运行。当测试窗体出现后，你可以通过按下按钮来更改交通灯上的“信号”。图 15-8 显示了一个示例屏幕。

当然，你在黑白屏幕截图中看不到颜色；但从位置可以判断，圆是红色的。“黄灯”显示在控件中间，“绿灯”显示在底部。这些位置都是在`Paint`事件逻辑中根据`Status`属性的值计算得出的。

对于完整的示例，最好让用户能够通过单击“交通灯”的不同部分来更改`Status`。这意味着需要包含用于检查鼠标单击、计算单击是否位于给定区域内，并在适当情况下更改`Status`属性的逻辑。在本书的可下载代码中，`TrafficLight`示例包含了此类功能。

### 为工具箱附加图标

默认情况下，出现在工具箱中控件名称旁边的图标是齿轮形状的图标。不过，你可以为控件附加一个图标供工具箱显示。有两种方法可以做到这一点。

Windows 窗体包含一个`ToolboxBitmap`属性，可以为类指定图标。它有多种用法，你可以在`ToolboxBitmap`属性的帮助文件中查看示例。

为控件附加图标的一种简便方法是让 Visual Studio 为你完成。只需找到或绘制你想要使用的图标，并将其添加到包含控件的项目中。然后重命名该图标，使其与控件同名，但扩展名为`.ico`而不是`.vb`。

例如，要为前面示例中的`TrafficLight`控件附加图标，请找到一个你喜欢的图标，将其放入项目中，并将其命名为`TrafficLight.ico`。然后，Visual Studio 会在编译过程中将该图标附加到你的控件；当控件被添加到工具箱时，将使用你的图标而不是齿轮形状的图标。

> 只有当控件通过工具箱的“选择项”选项添加时，控件在工具箱中才会显示自定义图标。因其项目当前已加载而出现在工具箱顶部的控件不会显示自定义图标。它们始终具有蓝色的齿轮状图标。

### 在其他控件中嵌入控件

创建自定义控件的另一个有价值的技术是嵌入其他控件。从某种意义上说，`UserControl`就是这样做的；但当`UserControl`用作基类时，默认情况下它只公开`UserControl`类的属性。相反，你可能希望使用`TextBox`或`Grid`等控件作为起点，但在`TextBox`或`Grid`中嵌入一个`Button`以获得某些新功能。

嵌入技术依赖于这样一个事实：在 Windows 窗体中，所有控件都可以作为其他控件的容器。Visual Basic 开发人员熟悉`Panel`和`GroupBox`可以作为容器的概念，但事实上，`TextBox`或`Grid`也可以作为其他控件的容器。

来自 TrafficLight 的代码片段

![](img/d99870e80390742f93963da7be0b2e61_605_0.png)
图 15-8

这个技术最好通过一个示例来呈现。标准的`ComboBox`控件没有让用户重置为“无选择”状态的方法。一旦选择了项目，将其设置为该状态需要代码将`SelectedIndex`设置为 -1。

本练习创建一个`ComboBox`，该`ComboBox`具有一个按钮，可将选择状态重置回“无选择”。这使用户可以直接访问该功能。现在你已经在示例中处理了多个控件，而不是逐步进行，我们将直接展示此类`ComboBox`的代码并讨论代码的工作原理：

```vb
Public Class SpecialComboBox
    Inherits ComboBox
    Dim WithEvents btnEmbeddedButton As Button
    Public Sub New()
        Me.DropDownStyle = ComboBoxStyle.DropDownList
        ' Fix up the embedded button.
        btnEmbeddedButton = New Button
        btnEmbeddedButton.Width = SystemInformation.VerticalScrollBarWidth
        btnEmbeddedButton.Top = 0
        btnEmbeddedButton.Height = Me.Height - 4
        btnEmbeddedButton.BackColor = SystemColors.Control
        btnEmbeddedButton.FlatStyle = FlatStyle.Popup
        btnEmbeddedButton.Text = "*"
        Dim fSpecial As New Font("Wingdings 3", Me.Font.Size - 1)
        btnEmbeddedButton.Font = fSpecial
        btnEmbeddedButton.Left = Me.Width - btnEmbeddedButton.Width - SystemInformation.VerticalScrollBarWidth
        Me.Controls.Add(btnEmbeddedButton)
        btnEmbeddedButton.Anchor = CType(AnchorStyles.Right Or AnchorStyles.Top Or AnchorStyles.Bottom, AnchorStyles)
        btnEmbeddedButton.BringToFront()
    End Sub
    Private Sub btnEmbeddedButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnEmbeddedButton.Click
        Me.SelectedIndex = -1
        Me.Focus
    End Sub
    Private Sub BilllysComboBox_DropDownStyleChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.DropDownStyleChanged
        If Me.DropDownStyle <> ComboBoxStyle.DropDownList Then
            Me.DropDownStyle = ComboBoxStyle.DropDownList
            Throw New InvalidOperationException("DropDownStyle must be DropDownList")
        End If
    End Sub
End Class
```
