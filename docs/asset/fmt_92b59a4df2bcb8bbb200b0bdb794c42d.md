
`Code snippet from ExceptionHandlingSampleCodeForm`

`Messagebox`语句的输出非常详细，提供错误发生的整个路径和行号，如图6-4所示。
请注意，此信息也包含在前面检查过的`ToString`方法中（参见图6-1）。

![](img/d99870e80390742f93963da7be0b2e61_296_0.png)

FIGURE 6-4

### GetBaseException

当你深入到一组抛出的异常中时，`GetBaseException`方法非常有用。此方法通过递归检查`InnerException`直到到达`InnerException`属性为空的异常对象为止，从而返回原始异常。该异常通常是引发一系列意外事件的异常。

在下面的代码中，异常链以除零开始，导致异常对象`objA`。链随后继续使用异常对象`objB`和`objC`，两者都在代码中创建。这最后两个异常都是通过使用`Exception`类的构造函数创建的，该构造函数接受该新异常的`InnerException`的参数。最后，在`objC`上访问`GetBaseException`方法：

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

`Code snippet from ExceptionHandlingSampleCodeForm`

调用`objC.GetBaseException`将通过`InnerException`回溯，`ObjC`的`InnerException`为`objB`，然后通过`objB`的`InnerException`，即原始异常`objA`。然而，`objA`的`InnerException`为空，因为它是除零引起的原始异常。因此，`objC.GetBaseException.Message`返回原始`OverflowException`消息的`Message`属性，即使你在原始错误发生后抛出了多个错误：

```
MessageBox.Show(objC.GetBaseException.Message)
```

换句话说，代码回溯到作为`objA`捕获的异常并显示与`objA.Message`属性相同的消息，如图6-5所示。

![](img/d99870e80390742f93963da7be0b2e61_297_0.png)

### HelpLink

`HelpLink`属性获取或设置特定`Exception`对象的帮助链接。它可以设置为任何字符串值，但通常设置为URL。如果你在代码中创建自己的异常，你可能希望将`HelpLink`设置为更详细描述错误的URL（或URN）。然后捕获异常的代码可以转到该链接。你可以使用以下代码创建并抛出自己的自定义应用程序异常：

```
Dim exc As New ApplicationException("A short description of the problem")
exc.HelpLink = "http://mysite.com/somehtmlfile.htm"
Throw exc
```

`Code snippet from ExceptionHandlingSampleCodeForm`

在捕获异常时，可以使用`HelpLink`启动查看器，以便用户查看有关问题的详细信息。以下示例展示了这一点，使用Windows内置的Explorer：

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

`Code snippet from ExceptionHandlingSampleCodeForm`

这将导致启动Internet Explorer以显示URL指定的页面。CLR或.NET Framework类抛出的大多数异常的`HelpLink`属性为空。你应该只在你自己之前将其设置为URL（或其他类型的链接信息）时才依赖使用`HelpLink`。

### INTEROPERABILITY WITH VB6-STYLE ERROR HANDLING

由于Visual Basic 2010仍然支持来自.NET版本之前的VB的旧`On Error`语句，你可能会遇到使用`On Error`而不是结构化异常处理来处理错误的代码。你可以在单个程序中使用这两种技术，但不能在单个例程中同时使用两者。如果你在单个例程中同时尝试使用`On Error`和`Try...Catch`，你将收到语法错误。

Visual Basic编译器确实允许这两种错误处理技术相互通信。例如，假设你有一个使用`Err.Raise`将错误提升到调用代码的例程。还假设调用代码在`Try...Catch`块中进行调用。在这种情况下，`Err.Raise`创建的错误在调用代码中成为异常，并被`Catch`块捕获，就像正常的异常一样。以下代码示例说明了这一点。首先，创建一个使用`Err.Raise`创建错误的子程序，如下所示：

```
Private Sub RaiseErrorWithErrRaise()
    Err.Raise(53)  ' indicates File Not Found
End Sub
```

`Code snippet from ExceptionHandlingSampleCodeForm`

然后从按钮的Click事件中调用此例程，并将调用放在`Try...Catch`块中：

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

`Code snippet from ExceptionHandlingSampleCodeForm`

当单击按钮时，它将显示一个消息框，显示“File Not Found”。即使File Not Found错误是由`Err.Raise`引发的，它也会自动转换为.NET异常。

同样，由被调用例程中的`Throw`语句生成的异常也可以由调用例程中的`On Error`捕获。异常随后被转换为类似于VB6 `Err`对象的`Err`对象。

### ERROR LOGGING

错误日志记录在许多应用程序中对于彻底的故障排除非常重要。应用程序的最终用户通常会忘记错误的确切内容。记录特定错误到日志中可以让你在不重现错误的情况下获取特定的错误消息。

虽然错误日志记录非常重要，但你只希望将其用于捕获特定级别的错误，因为它会带来开销并可能降低应用程序的性能。具体来说，只记录对应用程序完整性至关重要的错误——例如，会导致应用程序正在处理的数据变得无效的错误。

错误日志记录主要有三种方法：

- 在战略位置的文本文件或平面文件中写入错误信息。
- 将错误信息写入中央数据库。
- 将错误信息写入系统的事件日志，这些日志在.NET Framework 4支持的所有Windows版本上均可用。.NET Framework包含一个组件，可用于在任何给定机器上写入和读取系统、应用程序和安全日志。

你选择的日志类型取决于你希望捕获的错误类别以及你将运行应用程序的机器类型。如果你选择写入事件日志，则需要对错误进行分类并将其写入适当的日志文件。资源、硬件和系统级错误最适合系统事件日志。数据访问错误最适合应用程序事件日志。权限错误最适合安全事件日志。

#### The Event Log

有三个Windows事件日志可用：系统、应用程序和安全日志。这些日志中的事件可以使用事件查看器查看，该查看器可从控制面板访问。访问管理工具，然后选择事件查看器子部分以查看事件。通常，你的应用程序将使用应用程序事件日志。

### 表6-4：相关的EventLog事件

| 事件 | 描述 |
| --- | --- |
| EntryWritten | 当事件被写入日志时生成 |

表6-5描述了`EventLog`组件的相关方法。

### 表6-5：相关的EventLog方法

| 方法 | 描述 |
| --- | --- |
| CreateEventSource | 在指定日志中创建事件源 |
| DeleteEventSource | 删除事件源及相关条目 |
| WriteEntry | 将字符串写入指定日志 |
| Exists | 用于确定特定事件日志是否存在 |
| SourceExists | 用于确定日志中是否存在特定源 |
| GetEventLogs | 检索特定计算机上的所有事件日志列表 |
| Delete | 删除整个事件日志。请谨慎使用此方法。 |

表6-6描述了`EventLog`组件的相关属性。

### 表6-6：相关的EventLog属性

| 属性 | 描述 |
| --- | --- |
| Source | 指定要写入条目的源 |
| Log | 用于指定要写入的日志。三个日志分别是系统、应用程序和安全。如果未指定，默认是应用程序日志。 |

以下示例演示了其中一些方法和属性：

```
Sub LoggingExample1()
    Dim objLog As New EventLog()
    Dim objLogEntryType As EventLogEntryType
    Try
        Throw New EntryPointNotFoundException()
    Catch objA As System.EntryPointNotFoundException
        If Not EventLog.SourceExists("Example") Then
            EventLog.CreateEventSource("Example", "System")
        End If
        objLog.Source = "Example"
        objLog.Log = "System"
        objLogEntryType = EventLogEntryType.Information
        objLog.WriteEntry("Error: " & objA.Message, objLogEntryType)
    End Try
End Sub
```

*来自`ExceptionHandlingSampleCodeForm`的代码片段*

前面的代码声明了两个变量：一个用于实例化日志，一个用于保存条目类型信息。请注意，在创建源之前，需要检查源是否存在。以下两行代码实现了这一点：

```
If Not EventLog.SourceExists("Example") Then
    EventLog.CreateEventSource("Example", "System")
```

*来自`ExceptionHandlingSampleCodeForm`的代码片段*

在验证或创建源之后，可以设置`EventLog`对象的`Source`属性，设置`Log`属性以指定要写入的日志，并将`EventLogEntryType`设置为`Information`（其他选项包括`Warning`、`Error`、`SuccessAudit`和`FailureAudit`）。如果尝试写入特定日志中不存在的源，则会收到错误。设置完`EventLog`对象的这三个属性后，就可以写入条目了。在此示例中，将单词`Error`与实际异常的`Message`属性连接起来，形成要写入日志的字符串：

```
objLog.Source = "Example"
objLog.Log = "System"
objLogEntryType = EventLogEntryType.Information
objLog.WriteEntry("Error: " & objA.Message, objLogEntryType)
```

*来自`ExceptionHandlingSampleCodeForm`的代码片段*

### 写入跟踪文件

作为事件日志的替代方案，你可以将调试和错误信息写入跟踪文件。*跟踪文件*是一种基于文本的文件，你在程序中生成它来跟踪有关错误条件的详细信息。如果你想要跟踪可能填满事件日志的详细信息，或者问题的诊断需要分析特定的执行事件序列，那么跟踪文件也是补充事件日志的好方法。

本节介绍在开发跟踪文件时如何使用`StreamWriter`接口。在这种情况下，跟踪文件是文本文件，因此你需要了解通过设置流写入器和调试侦听器来写入文本文件所涉及的概念。`StreamWriter`接口通过`System.IO`命名空间处理。它使你能够与给定机器上文件系统中的文件进行交互。`Debug`类通过侦听器对象与这些输出对象交互。任何侦听器对象的工作都是收集、存储并将存储的输出发送到文本文件、日志和“输出”窗口。在示例中，你将使用`TextWriterTraceListener`类。

正如你将看到的，`StreamWriter`对象打开到文本文件的输出路径，通过将`StreamWriter`对象绑定到侦听器对象，可以将调试输出定向到文本文件。

跟踪侦听器是输出目标，可以是`TextWriter`或`EventLog`，也可以将输出发送到默认的“输出”窗口（即`DefaultTraceListener`）。`TextWriterTraceListener`通过提供一个输出对象来容纳`Debug`对象的`WriteLine`方法，该输出对象存储要刷新到输出流的信息，而输出流由`StreamWriter`接口设置。

表6-7列出了`StreamWriter`对象的一些常用方法。

| 方法 | 描述 |
| --- | --- |
| Close | 关闭`StreamWriter` |
| Flush | 将`StreamWriter`的所有内容刷新到创建`StreamWriter`时指定的输出文件 |
| Write | 将字节输出写入流。可选参数允许指定流中的位置（偏移量）。 |
| WriteLine | 将字符后跟行终止符写入当前流对象 |

表6-8列出了与`Debug`对象相关的一些方法，`Debug`对象为接下来的文本文件示例提供输出机制。

### 表6-8：常见的Debug对象方法

| 方法 | 描述 |
| --- | --- |
| Assert | 检查条件，如果为False则显示消息 |
| Close | 对输出缓冲区执行刷新并关闭所有侦听器 |
| Fail | 以“中止/重试/忽略”消息框的形式发出错误消息 |
| Flush | 刷新输出缓冲区并将其写入侦听器 |
| Write | 将字节写入输出缓冲区 |
| WriteLine | 将字符后跟行终止符写入输出缓冲区 |
| WriteIf | 如果特定条件为True，则将字节写入输出缓冲区 |
| WriteLineIf | 如果特定条件为True，则将字符后跟行终止符写入输出缓冲区 |

以下示例演示如何打开现有文件（名为`mytext.txt`）进行输出，并将其分配给`Debug`对象的`Listeners`对象，以便它可以捕获你的`Debug.WriteLine`语句：

```
Sub LoggingExample2()
    Dim objWriter As New _
        IO.StreamWriter("C:\mytext.txt", True)
    Debug.Listeners.Add(New TextWriterTraceListener(objWriter))
    Try
        Throw (New EntryPointNotFoundException())
    Catch objA As System.EntryPointNotFoundException
        Debug.WriteLine(objA.Message)
        objWriter.Flush()
        objWriter.Close()
        objWriter = Nothing
```
