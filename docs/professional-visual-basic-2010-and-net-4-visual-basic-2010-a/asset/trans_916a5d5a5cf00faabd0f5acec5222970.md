

## 表6-4：相关的EventLog事件

| 事件 | 描述 |
| --- | --- |
| EntryWritten | 当事件被写入日志时生成 |

表6-5描述了EventLog组件的相关方法。

## 表6-5：相关的EventLog方法

| 方法 | 描述 |
| --- | --- |
| CreateEventSource | 在指定日志中创建事件源 |
| DeleteEventSource | 删除事件源及相关条目 |
| WriteEntry | 将字符串写入指定日志 |
| Exists | 用于确定特定事件日志是否存在 |
| SourceExists | 用于确定日志中是否存在特定源 |
| GetEventLogs | 检索特定计算机上的所有事件日志列表 |
| Delete | 删除整个事件日志。请谨慎使用此方法。 |

表6-6描述了EventLog组件的相关属性。

## 表6-6：相关的EventLog属性

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

*来自ExceptionHandlingSampleCodeForm的代码片段*

前面的代码声明了两个变量：一个用于实例化日志，一个用于保存条目类型信息。请注意，在创建源之前，需要检查源是否存在。以下两行代码实现了这一点：

```
If Not EventLog.SourceExists("Example") Then
    EventLog.CreateEventSource("Example", "System")
```

*来自ExceptionHandlingSampleCodeForm的代码片段*

在验证或创建源之后，可以设置EventLog对象的Source属性，设置Log属性以指定要写入的日志，并将EventLogEntryType设置为Information（其他选项包括Warning、Error、SuccessAudit和FailureAudit）。如果尝试写入特定日志中不存在的源，则会收到错误。设置完EventLog对象的这三个属性后，就可以写入条目了。在此示例中，将单词Error与实际异常的Message属性连接起来，形成要写入日志的字符串：

```
objLog.Source = "Example"
objLog.Log = "System"
objLogEntryType = EventLogEntryType.Information
objLog.WriteEntry("Error: " & objA.Message, objLogEntryType)
```

*来自ExceptionHandlingSampleCodeForm的代码片段*

## 写入跟踪文件

作为事件日志的替代方案，你可以将调试和错误信息写入跟踪文件。*跟踪文件*是一种基于文本的文件，你在程序中生成它来跟踪有关错误条件的详细信息。如果你想要跟踪可能填满事件日志的详细信息，或者问题的诊断需要分析特定的执行事件序列，那么跟踪文件也是补充事件日志的好方法。

本节介绍在开发跟踪文件时如何使用StreamWriter接口。在这种情况下，跟踪文件是文本文件，因此你需要了解通过设置流写入器和调试侦听器来写入文本文件所涉及的概念。StreamWriter接口通过System.IO命名空间处理。它使你能够与给定机器上文件系统中的文件进行交互。Debug类通过侦听器对象与这些输出对象交互。任何侦听器对象的工作都是收集、存储并将存储的输出发送到文本文件、日志和“输出”窗口。在示例中，你将使用TextWriterTraceListener类。

正如你将看到的，StreamWriter对象打开到文本文件的输出路径，通过将StreamWriter对象绑定到侦听器对象，可以将调试输出定向到文本文件。

跟踪侦听器是输出目标，可以是TextWriter或EventLog，也可以将输出发送到默认的“输出”窗口（即DefaultTraceListener）。TextWriterTraceListener通过提供一个输出对象来容纳Debug对象的WriteLine方法，该输出对象存储要刷新到输出流的信息，而输出流由StreamWriter接口设置。

表6-7列出了StreamWriter对象的一些常用方法。

| 方法 | 描述 |
| --- | --- |
| Close | 关闭StreamWriter |
| Flush | 将StreamWriter的所有内容刷新到创建StreamWriter时指定的输出文件 |
| Write | 将字节输出写入流。可选参数允许指定流中的位置（偏移量）。 |
| WriteLine | 将字符后跟行终止符写入当前流对象 |

表6-8列出了与Debug对象相关的一些方法，Debug对象为接下来的文本文件示例提供输出机制。

## 表6-8：常见的Debug对象方法

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

以下示例演示如何打开现有文件（名为mytext.txt）进行输出，并将其分配给Debug对象的Listeners对象，以便它可以捕获你的Debug.WriteLine语句：

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
    End Try
End Sub
```

*来自ExceptionHandlingSampleCodeForm的代码片段*

仔细查看此代码，首先创建一个StreamWriter，并将其分配给本地文件系统中的文件：

```
Dim objWriter As New _
    IO.StreamWriter("C:\mytext.txt", True)
```

然后使用Add方法将StreamWriter分配给调试侦听器：

```
Debug.Listeners.Add(New TextWriterTraceListener(objWriter))
```

此示例强制引发异常并捕获它，通过WriteLine方法将Exception对象的Message属性（即“Entry point was not found”）写入调试缓冲区：

```
Debug.WriteLine(objA.Message)
```

最后，将侦听器缓冲区刷新到输出文件并释放资源：

```
objWriter.Flush()
objWriter.Close()
objWriter = Nothing
```

运行此代码后，可以检查c:\mytext.txt文件以查看跟踪输出。

## 总结

本章回顾了Exception对象以及可用于处理异常的语法。你已经了解了异常的各种属性，并学习了如何使用公开的信息。你还看到了如何使用Throw语句将异常提升到使用代码，以及结构化异常处理如何与旧式On Error交互。如前所述，你编写的任何新代码都应使用结构化异常处理。除非是在旧代码中进行维护任务，否则应避免使用旧式On Error。

本章还介绍了写入事件日志以捕获有关生成的异常的信息。虽然你应该明智地使用事件日志以避免过载，但捕获异常信息以供事后分析是诊断中非常宝贵的工具。

本章介绍了一种为程序生成跟踪输出的简单技术。.NET中提供了更复杂的跟踪功能，可以使用Trace和TraceSwitch类，但完整的示例超出了本书的范围。通过使用Visual Basic 2010中现在可用的完整异常处理功能，你可以使应用程序更可靠，并在出现问题时更快地诊断问题。正确使用事件日志记录和跟踪还可以帮助你调整应用程序以获得更好的性能。

