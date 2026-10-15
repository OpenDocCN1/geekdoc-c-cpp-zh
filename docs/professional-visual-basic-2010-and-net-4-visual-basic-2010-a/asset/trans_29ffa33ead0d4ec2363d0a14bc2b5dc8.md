
你在这里所做的是构建一个计算列表。完成后，你选择列表中的第一项。让我们来看看那个 AddObject 子程序：

```
Private Sub AddObject(ByVal strName As String, ByVal strObject As String)
    cmbCalculation.Items.Add(strName)
    mnObject = mnObject + 1
    ReDim Preserve mstrObjects(mnObject)
    mstrObjects(mnObject - 1) = strObject
End Sub
```

前面的代码段将计算名称添加到组合框中，并将其 ProgID 添加到一个字符串数组。这两者都没有排序，因此你会得到它们之间的一一映射。看看当你通过组合框选择计算时会发生什么：

```
Private Sub cmbCalculation_SelectedIndexChanged(ByVal sender As System.Object,
    ByVal e As System.EventArgs) _
    Handles cmbCalculation.SelectedIndexChanged

    Dim intIndex As Integer
    Dim bEnabled As Boolean
    intIndex = cmbCalculation.SelectedIndex
    mtypCalc = Type.GetTypeFromProgID(mstrObjects(intIndex))
    If (mtypCalc Is Nothing) Then
        mobjcalc = Nothing
        bEnabled = False
    Else
        mobjcalc = Activator.CreateInstance(mtypCalc)
        bEnabled = True
    End If
    txtInput.Enabled = bEnabled
    btnAdd.Enabled = bEnabled
    btnCalculate.Enabled = bEnabled
    btnReset.Enabled = bEnabled
End Sub
```

这个示例中有两个关键调用。第一个是 `Type.GetTypeFromProgID`。它接收传入的 ProgID 字符串并将其转换为 Type 对象。这个过程要么成功要么失败；如果失败，则禁用所有控件并让用户重试。如果成功，则创建该类型所描述对象的一个实例。你在调用静态方法 `Activator.CreateInstance()` 时完成此操作。

对于这个示例，假设用户已经选择了你可以成功实例化的计算。接下来呢？用户输入一个数字并点击表单上的 Add 按钮：

```
Private Sub btnAdd_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnAdd.Click
    Dim objArgs() As Object
    objArgs = New Object(0) {CDbl(txtInput.Text)}
    mtypCalc.InvokeMember("AddInput", BindingFlags.InvokeMethod, _
    Nothing, mobjCalc, objArgs)
    txtInput.Text = ""
End Sub
```

这里重要的调用是 `InvokeMember()` 方法。让我们仔细看看发生了什么。向 `InvokeMember()` 方法传递了五个参数：

- 第一个参数是你要调用的方法名称：在本例中是 `AddInput`。因此，你不是直接进入例程在内存中的位置，而是让 .NET 运行时为你查找它。
- `BindingFlags` 枚举中的值告诉它调用一个方法。
- 下一个参数提供特定于语言的绑定信息，本例中不需要。
- 第四个参数是对 COM 对象本身的引用（你使用 `Activator.CreateInstance` 实例化的那个对象）。
- 最后，第五个参数是一个对象数组，表示该方法的参数。在本例中，只有一个参数，即输入值。

在 VB6 后期绑定的底层，正在发生与此非常类似的事情，只不过在这里它被赤裸裸地暴露出来了。在某些方面，这并非坏事，因为它应该强调一个观点：应尽可能避免后期绑定。无论如何，让我们继续并完成程序。以下是其他按钮的其余事件处理程序：

```
Private Sub btnCalculate_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnCalculate.Click
    Dim objResult As Object
    mtypCalc.InvokeMember("DoCalculation", BindingFlags.InvokeMethod, _
        Nothing, mobjCalc, Nothing)
    objResult = mtypCalc.InvokeMember("GetOutput", _
        BindingFlags.InvokeMethod, Nothing, mobjCalc, Nothing)
    txtOutput.Text = CStr(objResult)
End Sub
Private Sub btnReset_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnReset.Click
    mtypCalc.InvokeMember("Reset", BindingFlags.InvokeMethod, _
        Nothing, mobjCalc, Nothing)
    txtInput.Text = ""
    txtOutput.Text = ""
End Sub
```

*来自 Form1 的代码片段*

## 运行计算框架

让我们通过运行应用程序来快速完成这项工作。图 28-8 显示了当你选择不存在的计算 StdDev 时会发生什么。

如屏幕截图所示，输入字段已按预期被禁用。图 28-9 显示了当你选择 Mean 时会发生什么。然后你可以输入几个数值并重新测试 Mean 计算。这一次，输入字段已启用，计算可以像之前一样执行。

![](img/d99870e80390742f93963da7be0b2e61_940_0.png)

![](img/d99870e80390742f93963da7be0b2e61_940_1.png)

关于后期绑定最后再说一句：本示例特意确保你检查了对象是否成功实例化。在真实应用程序中，你还需要确保方法调用成功并且捕获所有异常——你没有编译器为你找出所有错误的奢侈。

## ACTIVEX 控件

让我们从基本的 COM 对象转向 ActiveX 控件。你将做与基本 COM 组件大致相同的事情（除了与 ActiveX 控件无关的后期绑定）：使用 VB6 构建一个旧版控件，然后将其导入到你的 .NET Visual Basic 项目中。

## 旧版 ActiveX 控件

对于你的旧版 ActiveX 控件，你将构建一个类似按钮的简单对象，它能够解释鼠标单击，并根据其状态显示两种颜色之一。为了完成此任务，你将再次进入 VB6，所以如果你手头没有 VB6，可以随意跳过下一节，下载 OCX 文件（样本代码中 VB6\Magic\ 目录下的 Magic.ocx），并在开始开发 .NET 应用程序时再继续。

## 步骤 1：创建控件

这一次，在 VB6 IDE 中，你需要创建一个 ActiveX 控件项目。对于此示例，将项目命名为 Magic，将控件类命名为 MagicButton，以体现其非凡的能力。从工具箱中选择一个 Shape 控件，并将其放置在 VB6 为你提供的 UserControl 窗体上。将窗体上提供的形状重命名为 shpButton，并按如下更改其属性：

| 属性 | 值 |
|---|---|
| `FillStyle` | 0 ‘实心 |
| `Shape` | 4 ‘圆角矩形 |
| `FillColor` | &H008F8F8F& |

填充颜色的十六进制值表示灰色。接下来，在 Shape 控件顶部添加一个标签，并将其重命名为 lblText。将该控件的属性更改如下：

| 属性 | 值 |
|---|---|
| `BackStyle` | 0 ‘透明 |
| `Alignment` | 2 ‘居中 |

切换到 MagicButton 组件的代码视图。在提供的代码中，添加两个名为 Caption 和 State 的属性，以及一个名为 Click() 的事件，同时添加处理属性初始化和持久化的代码，以确保形状正确调整大小并且标签居中。你还需要在代码中处理鼠标单击。MagicButton 类的最终代码如下所示：

```
Option Explicit
Public Event Click()
Dim mintState As Integer
Public Property Get Caption() As String
    Caption = lblText.Caption
End Property
Public Property Let Caption(ByVal vNewValue As String)
    lblText.Caption = vNewValue
    PropertyChanged ("Caption")
End Property
Public Property Get State() As Integer
    State = mintState
End Property
Public Property Let State(ByVal vNewValue As Integer)
    mintState = vNewValue
    PropertyChanged ("State")
    If (State = 0) Then
        shpButton.FillColor = &HFFFFFF&
    Else
        shpButton.FillColor = &H8F8F8F&
    End If
End Property
Private Sub UserControl_InitProperties()
    Caption = Extender.Name
    State = 1
End Sub
Private Sub UserControl_ReadProperties(PropBag As PropertyBag)
    Caption = PropBag.ReadProperty("Caption", Extender.Name)
    State = PropBag.ReadProperty("State", 1)
End Sub
Private Sub UserControl_WriteProperties(PropBag As PropertyBag)
    PropBag.WriteProperty "Caption", lblText.Caption
    PropBag.WriteProperty "State", mintState
End Sub
Private Sub UserControl_Resize()
    shpButton.Move 0, 0, ScaleWidth, ScaleHeight
    lblText.Move 0, (ScaleHeight - lblText.Height) / 2, ScaleWidth
End Sub
Private Sub lblText_Click()
    RaiseEvent Click
End Sub
Private Sub UserControl_MouseUp(Button As Integer, Shift As Integer, _
    X As Single, Y As Single)
    RaiseEvent Click
End Sub
```

来自 MagicButton 的代码片段

如果你构建此项目，你将得到一个名为 Magic.ocx 的 ActiveX 控件。

## 步骤 2：注册你的旧版控件

现在你拥有了旧版控件。和之前一样，如果你在同一台机器上开发新的 .NET 应用程序，那么你无需再做任何其他事情，因为你的控件已由构建过程注册。但是，如果你在一台全新的机器上工作，或者你没有在 Visual Basic 6 中构建该控件，那么你需要在其中注册它。和之前一样，打开命令窗口并按如下方式注册：

```
regsvr32 Magic.ocx
```

你应该再次看到图 28-1 中所示的对话框，这次它表明你的 Magic.ocx 组件已成功注册。完成后，你就可以构建 .NET 应用程序了。

## 又一个 .NET 应用程序

这个 .NET 应用程序比上一个更简单。这次你只需要显示一个按钮，用户单击它时颜色会发生变化。首先，在 Visual Basic 中创建一个名为 ButtonApp 的 .NET Windows 应用程序项目。然而，在开始开发之前，通过在工具箱的“常规”部分中右键单击并选择“选择项”来扩展工具箱以纳入你的新控件。图 28-10 显示了上下文菜单。选择“选择项”后，你将看到图 28-11 中所示的窗口。
