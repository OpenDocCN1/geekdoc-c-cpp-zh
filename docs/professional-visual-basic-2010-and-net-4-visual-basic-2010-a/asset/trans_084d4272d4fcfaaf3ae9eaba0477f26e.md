

完成之后，继续编写均值计算的代码。你在名为 MeanCalc 的类中完成此操作：

```
Option Explicit
Dim mintValue As Integer
Dim mdblValues() As Double
Dim mdblMean As Double
Private Sub Class_Initialize()
Reset
End Sub
Private Sub IMegaCalc_AddInput(InputValue As Double)
mintValue = mintValue + 1
ReDim Preserve mdblValues(mintValue)
mdblValues(mintValue) = InputValue
End Sub
Private Sub IMegaCalc_DoCalculation()
Dim iValue As Integer
mdblMean = 0#
If (mintValue = 0) Then Exit Sub
For iValue = 1 To mintValue
mdblMean = mdblMean + mdblValues(iValue)
Next iValue
mdblMean = mdblMean / mintValue
End Sub
Private Function IMegaCalc_GetOutput() As Double
IMegaCalc_GetOutput = mdblMean
End Function
Private Sub IMegaCalc_Reset()
mintValue = 0
End Sub
```

来自 MeanCalc 的代码片段

## 第 2 步：注册旧版组件

如果你已经进行到这一步，那么你现在应该拥有了你的旧版组件。在同一台机器上开发新的 .NET 应用程序时，你无需做任何额外操作，因为构建过程已经注册了你的组件。但是，如果你正在全新机器上工作，则必须在那里注册它。为此，打开一个命令窗口（在 Windows Vista 和 Windows 7 上，确保使用管理员权限启动命令窗口）并使用位于 C:\Windows\system32 的 regsvr32.exe 用以下命令注册它：

![](img/d99870e80390742f93963da7be0b2e61_933_0.png)

图 28-1

```
regsvr32 MeanCalculator2.dll
```

然后你应该会看到图 28-1 中显示的结果。

## .NET 应用程序

本章使用的 .NET 应用程序，你只需要实例化一个 MeanCalc 对象的实例，并让它为你计算均值。为此，创建一个名为 CalcApp 的 Visual Basic .NET Windows 窗体应用程序项目。布局后，窗体看起来与图 28-2 所示相同。

两个文本框分别称为 txtInput 和 txtOutput；第二个文本框不允许用户输入。三个命令按钮分别是 btnAdd、btnCalculate 和 btnReset。

![](img/d99870e80390742f93963da7be0b2e61_934_0.png)

# 图 28-2

## 从 .NET 引用旧版 COM 组件

在深入编写窗体按钮背后的代码之前，你首先需要让新的应用程序感知 MeanCalculator2 组件。通过 Project Properties 将组件引用添加到项目中。从 References 选项卡选择“Add…”按钮以打开 Add Reference 对话框。此对话框包含五个选项卡：.NET、COM、Projects、Browse 和 Recent。从 COM 选项卡中，选择 Interop .MeanCalculator2（见图 28-3）。

![](img/d99870e80390742f93963da7be0b2e61_934_1.png)

# 图 28-3

请注意，在 References 选项卡中显示的引用列表中，你现在可以看到 MeanCalculator 组件。此视图在图 28-4 中呈现。

![](img/d99870e80390742f93963da7be0b2e61_935_0.png)

图 28-4

## .NET 应用程序内部

现在你已成功在 .NET 应用程序中引用了组件，可以使用 COM 组件提供的功能完成应用程序的编码。为了开始使用 COM 组件提供的新功能，将一个全局变量（mobjMean）添加到代码中，该变量将保存对均值计算组件实例的引用，如下所示：

```
Public Class Form1
    Dim mobjMean As MeanCalculator2.MeanCalc = New MeanCalculator2.MeanCalc()
```

来自 Form1 的代码片段

接下来，添加窗体按钮背后的代码。首先，处理 Add 按钮，添加以下调用 COM 组件的代码：

```
Private Sub btnAdd_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles btnAdd.Click
    mobjMean.AddInput(CDbl(txtInput.Text))
    txtInput.Text = ""
End Sub
```

来自 Form1 的代码片段

这会将输入文本框中的内容添加到用于计算的数字列表中。接下来，这里是 Calculate 按钮的代码：

```
Private Sub btnCalculate_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles btnCalculate.Click
    mobjMean.DoCalculation()
```

作为 COM 对象的包装器的 .NET 程序集（DLL）。如果你经常这样做，那么最好一次性完成包装，然后让你的应用程序开发人员导入 resulting .NET 程序集即可。让我们看看如何完成此任务。

Visual Studio 代表你创建默认互操作程序集的过程称为 tlbImp.exe。名称代表 Type Library Import，这正是该过程所做的。它包含在 .NET Framework SDK 中，你可能希望将机器上的 PATH 环境变量扩展到包含 .NET Framework SDK 的 \bin 目录。

TlbImp 以 COM DLL 作为输入，并生成 .NET 程序集 DLL 作为输出。默认情况下，.NET 程序集具有与类型库相同的名称，而在 VB6 组件的情况下，这将始终与 COM DLL 相同。这意味着你必须显式指定不同的输出文件。你可以通过使用 /out: 开关来实现这一点。如果你想在每个步骤中看到正在发生的事情，那么你还应该指定 /verbose 标志：

```
tlbimp MeanCalculator2.dll /out:MeanCalculatorNet2.dll
```

将 COM DLL 转换为 .NET 程序集后，你现在可以像引用任何其他 .NET DLL 一样在应用程序中引用它们。

## 晚期绑定

你已经看到可以在 .NET 应用程序中对 COM 组件成功进行早期绑定，但如果想改用晚期绑定怎么办？假设你在应用程序开发时无法访问类型库。你仍然可以使用 COM 组件吗？.NET 等效的晚期绑定是否存在？

答案是肯定的，确实存在，但它不如 VB6 中那样透明。让我们看看 VB6 中发生了什么。如果你想进行早期绑定，你会这样做：

```
Dim myObj As MyObj
Set myObj = New MyObj
MyObj.MyMethod (...)
```

对于晚期绑定，它看起来会像这样：

```
Dim myObj As Object
Set myObj = CreateObject ("MyLibrary.MyObject")
MyObj.MyMethod (...)
```

这里幕后实际上发生了大量活动，但其中大部分超出了 .NET 开发人员的关注范围。

## 晚期绑定的示例

对于本章构建的示例，让我们将计算器扩展为更通用的框架，可以将输入馈送到多个不同的计算模块，而不仅仅是当前实现的那一个。对于此示例，你将在内存中保留一个计算 ProgID 的表，并向用户提供一个组合框来选择正确的计算。

## 示例 COM 对象

关于晚期绑定要首先注意的第一件事是，你只能对默认接口进行晚期绑定，在本例中为 MeanCalculator2.MeanCalc。幸运的是，此组件是作为独立库开发的，没有对其他接口的引用。

## 计算框架

对于你的通用计算框架，你将在 Visual Basic 2010 中创建一个名为 CalcFrame 的新应用程序。你基本上会使用与之前相同的对话框，但在窗体顶部多了一个组合框。此新布局如图 28-7 所示。

![](img/d99870e80390742f93963da7be0b2e61_938_0.png)

# 图 28-7

新的组合框称为 cmbCalculation。为此正常工作，你还需要禁用控件 txtInput、btnAdd、btnCalculate 和 btnReset，直到你知道所选计算是否有效。你需要访问新下拉列表的属性并添加两个。开始你的应用程序时，导入 Reflection 命名空间，你需要它来处理应用程序的晚期绑定：

```
Imports System.Reflection
```

窗体就位后，向应用程序的代码添加几个成员变量：

```
Public Class Form1
    Inherits System.Windows.Forms.Form
    Private mstrObjects() As String
    Private mnObject As Integer
    Private mtypCalc As Type
    Private mobjcalc As Object
```

来自 Form1 的代码片段

从那里，向 Form1_Load 添加几行新代码：

```
Private Sub Form1_Load(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles MyBase.Load
    mnObject = 0
    AddObject("Mean", "MeanCalculator2.MeanCalc")
    AddObject("StdDev", "StddevCalculator.StddevCalc")
    If (mnObject > 0) Then
        cmbCalculation.SelectedIndex = 0
    End If
End Sub
```

来自 Form1 的代码片段

