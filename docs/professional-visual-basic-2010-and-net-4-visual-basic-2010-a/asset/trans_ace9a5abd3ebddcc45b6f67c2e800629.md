

```
Messagebox.Show("Caught any other errors")
Finally
Messagebox.Show(Str(intZ))
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

如前所述，你在第一个 Catch 块中捕获除零错误，并且异常存储在 objA 中，以便你稍后可以引用其属性。

你抛出一个带有更通用消息的新异常（“0 as divisor”），该消息更容易解释，并且你通过使用 Exception 对象的重载构造函数将 objA 附加为 InnerException 对象来构建你的堆栈：

```
Throw (New Exception("0 as divisor", objA))
```

你在一个新的 Catch 语句中捕获新抛出的异常。注意它没有捕获特定类型的错误：

```
Catch objB As Exception
```

然后你为新异常构造一个错误消息并在消息框中显示它：

```
Dim sError As String
sError = "My Message: " & objB.Message & vbCrLf & vbCrLf
sError &= "Inner Exception Message: " & _
objB.InnerException.Message & vbCrLf & vbCrLf
sError &= "Method Error Occurred: " & objB.TargetSite.Name
MessageBox.Show(sError)
```

Code snippet from ExceptionHandlingSampleCodeForm

产生的消息框如 图 6-3 所示。

首先包含你自己的消息，该消息基于你自己的代码抛出的新异常。然后 InnerException 获取堆栈中的下一个异常，即除零异常，并包含其消息。最后，TargetSite 属性为你提供抛出异常的方法名称。TargetSite 在用于开发人员跟踪意外问题的用户日志或错误报告中特别有帮助。

![](img/d99870e80390742f93963da7be0b2e61_295_0.png)

FIGURE 6-3

在此消息框之后，Finally 子句显示另一个消息框，只显示 intZ 的当前值，该值为零，因为除法失败。此第二个框也在后面的其他示例中出现。

## Source and StackTrace

Source 和 StackTrace 属性为用户提供有关错误发生位置的信息。此补充信息可能非常宝贵，因为用户可以将它传递给故障排除人员，以便更快地解决错误。以下示例使用这两个属性并在错误发生时显示反馈：

```
Sub HandlerExample2()
Dim intX As Integer
Dim intY As Integer
Dim intZ As Integer
intY = 0
intX = 5
' First Required Error Statement.
Try
' Cause a "Divide by Zero"
intZ = CType((intX \ intY), Integer)
' Catch the error.
Catch objA As System.DivideByZeroException
    objA.Source = "HandlerExample2"
    Messagebox.Show("Error Occurred at: " & _
        objA.Source & objA.StackTrace)
Finally
    Messagebox.Show(Str(intZ))
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

Messagebox 语句的输出非常详细，提供错误发生的整个路径和行号，如 图 6-4 所示。
请注意，此信息也包含在前面检查过的 ToString 方法中（参见 图 6-1）。

![](img/d99870e80390742f93963da7be0b2e61_296_0.png)

FIGURE 6-4

## GetBaseException

当你深入到一组抛出的异常中时，GetBaseException 方法非常有用。此方法通过递归检查 InnerException 直到到达 InnerException 属性为空的异常对象为止，从而返回原始异常。该异常通常是引发一系列意外事件的异常。

在下面的代码中，异常链以除零开始，导致异常对象 objA。链随后继续使用异常对象 objB 和 objC，两者都在代码中创建。这最后两个异常都是通过使用 Exception 类的构造函数创建的，该构造函数接受该新异常的 InnerException 的参数。最后，在 objC 上访问 GetBaseException 方法：

```
Sub HandlerExample3()
    Dim intX As Integer
    Dim intY As Integer
    Dim intZ As Integer
    intY = 0
    intX = 5
    ' First Required Error Statement.
    Try
        ' Cause a "Divide by Zero"
        intZ = CType((intX \ intY), Integer)
        ' Catch the error.
    Catch objA As System.DivideByZeroException
        Try
            Throw (New Exception("0 as divisor", objA))
        Catch objB As Exception
            Try
                Throw (New Exception("New error", objB))
            Catch objC As Exception
                Messagebox.Show(objC.GetBaseException.Message)
            End Try
        End Try
    Finally
        Messagebox.Show(Str(intZ))
    End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

调用 objC.GetBaseException 将通过 InnerException 回溯，ObjC 的 InnerException 为 objB，然后通过 objB 的 InnerException，即原始异常 objA。然而，objA 的 InnerException 为空，因为它是除零引起的原始异常。因此，objC.GetBaseException.Message 返回原始 OverflowException 消息的 Message 属性，即使你在原始错误发生后抛出了多个错误：

```
MessageBox.Show(objC.GetBaseException.Message)
```

换句话说，代码回溯到作为 objA 捕获的异常并显示与 objA.Message 属性相同的消息，如 图 6-5 所示。

![](img/d99870e80390742f93963da7be0b2e61_297_0.png)

## HelpLink

HelpLink 属性获取或设置特定 Exception 对象的帮助链接。它可以设置为任何字符串值，但通常设置为 URL。如果你在代码中创建自己的异常，你可能希望将 HelpLink 设置为更详细描述错误的 URL（或 URN）。然后捕获异常的代码可以转到该链接。你可以使用以下代码创建并抛出自己的自定义应用程序异常：

```
Dim exc As New ApplicationException("A short description of the problem")
exc.HelpLink = "http://mysite.com/somehtmlfile.htm"
Throw exc
```

Code snippet from ExceptionHandlingSampleCodeForm

在捕获异常时，可以使用 HelpLink 启动查看器，以便用户查看有关问题的详细信息。以下示例展示了这一点，使用 Windows 内置的 Explorer：

```
Sub HandlerExample4()
Try
    Dim exc As New ApplicationException("A short description of the problem")
    exc.HelpLink = "http://mysite.com/somehtmlfile.htm"
    Throw exc
    ' Catch the error.
Catch objA As System.Exception
    Shell("explorer.exe " & objA.HelpLink)
End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

这将导致启动 Internet Explorer 以显示 URL 指定的页面。CLR 或 .NET Framework 类抛出的大多数异常的 HelpLink 属性为空。你应该只在你自己之前将其设置为 URL（或其他类型的链接信息）时才依赖使用 HelpLink。

## INTEROPERABILITY WITH VB6-STYLE ERROR HANDLING

由于 Visual Basic 2010 仍然支持来自 .NET 版本之前的 VB 的旧 On Error 语句，你可能会遇到使用 On Error 而不是结构化异常处理来处理错误的代码。你可以在单个程序中使用这两种技术，但不能在单个例程中同时使用两者。如果你在单个例程中同时尝试使用 On Error 和 Try...Catch，你将收到语法错误。

Visual Basic 编译器确实允许这两种错误处理技术相互通信。例如，假设你有一个使用 Err.Raise 将错误提升到调用代码的例程。还假设调用代码在 Try...Catch 块中进行调用。在这种情况下，Err.Raise 创建的错误在调用代码中成为异常，并被 Catch 块捕获，就像正常的异常一样。以下代码示例说明了这一点。首先，创建一个使用 Err.Raise 创建错误的子程序，如下所示：

```
Private Sub RaiseErrorWithErrRaise()
    Err.Raise(53)  ' indicates File Not Found
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

然后从按钮的 Click 事件中调用此例程，并将调用放在 Try...Catch 块中：

```
Private Sub Button2_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Button2.Click
    Try
        RaiseErrorWithErrRaise()
    Catch ex As Exception
        MessageBox.Show(ex.Message)
    End Try
End Sub
```

Code snippet from ExceptionHandlingSampleCodeForm

当单击按钮时，它将显示一个消息框，显示“File Not Found”。即使 File Not Found 错误是由 Err.Raise 引发的，它也会自动转换为 .NET 异常。

同样，由被调用例程中的 Throw 语句生成的异常也可以由调用例程中的 On Error 捕获。异常随后被转换为类似于 VB6 Err 对象的 Err 对象。

## ERROR LOGGING

错误日志记录在许多应用程序中对于彻底的故障排除非常重要。应用程序的最终用户通常会忘记错误的确切内容。记录特定错误到日志中可以让你在不重现错误的情况下获取特定的错误消息。

虽然错误日志记录非常重要，但你只希望将其用于捕获特定级别的错误，因为它会带来开销并可能降低应用程序的性能。具体来说，只记录对应用程序完整性至关重要的错误——例如，会导致应用程序正在处理的数据变得无效的错误。

错误日志记录主要有三种方法：

- 在战略位置的文本文件或平面文件中写入错误信息。
- 将错误信息写入中央数据库。
- 将错误信息写入系统的事件日志，这些日志在 .NET Framework 4 支持的所有 Windows 版本上均可用。.NET Framework 包含一个组件，可用于在任何给定机器上写入和读取系统、应用程序和安全日志。

你选择的日志类型取决于你希望捕获的错误类别以及你将运行应用程序的机器类型。如果你选择写入事件日志，则需要对错误进行分类并将其写入适当的日志文件。资源、硬件和系统级错误最适合系统事件日志。数据访问错误最适合应用程序事件日志。权限错误最适合安全事件日志。

### The Event Log

有三个 Windows 事件日志可用：系统、应用程序和安全日志。这些日志中的事件可以使用事件查看器查看，该查看器可从控制面板访问。访问管理工具，然后选择事件查看器子部分以查看事件。通常，你的应用程序将使用应用程序事件日志。

