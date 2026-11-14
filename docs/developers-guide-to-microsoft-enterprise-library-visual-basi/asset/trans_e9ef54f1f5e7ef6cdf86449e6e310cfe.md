

针对代码中需要附加信息的特定区域，例如特别敏感进程的安全上下文详细信息。

在检查日志条目不会被筛选器阻止后，ShowDetailsAndAddExtraInfo 方法（前一节所示）会向日志条目添加一系列附加内容和自定义信息。它使用四个标准 Logging 块帮助器类，这些类可以生成附加上下文信息并将其添加到 Dictionary 中。这些帮助器类如下：

- DebugInformationProvider，将当前堆栈跟踪添加到 Dictionary 中
- ManagedSecurityContextInformationProvider，将当前标识名称、授权类型和授权状态添加到 Dictionary 中
- UnmanagedSecurityContextInformationProvider，将当前用户名和进程帐户名称添加到 Dictionary 中。
- ComPlusInformationProvider，将当前活动 ID、应用程序 ID、事务 ID（如果有）、直接调用方帐户名称和原始调用方帐户名称添加到 Dictionary 中。

以下代码展示了如何使用这些帮助器类为日志条目创建附加信息。它还演示了如何向日志条目添加自定义信息——在此示例中，是将应用程序配置文件的内容读入 Dictionary 中。填充 Dictionary 后，只需在写入该日志条目之前，将其设置为日志条目的 ExtendedProperties 属性的值即可。

```vb
' Create the additional context information to add to the LogEntry.
Dim dict As New Dictionary(Of String, Object)()
' Use the information helper classes to get information about
' the environment and add it to the dictionary.
Dim debugHelper As New DebugInformationProvider()
debugHelper.PopulateDictionary(dict)
Dim infoHelper As New ManagedSecurityContextInformationProvider()
infoHelper.PopulateDictionary(dict)
Dim secHelper As New UnmanagedSecurityContextInformationProvider()
secHelper.PopulateDictionary(dict)
Dim comHelper As New ComPlusInformationProvider()
comHelper.PopulateDictionary(dict)
' Get any other information you require and add it to the dictionary.
Dim configInfo As String = File.ReadAllText("...\App.config")
dict.Add("Config information", configInfo)
' Set the dictionary in the LogEntry and write it using the default LogWriter.
entry.ExtendedProperties = dict
defaultWriter.Write(entry)
...
```

示例在屏幕上产生以下输出。

```
Added the current stack trace to the Log Entry.
Added the current identity name, authentication type, and status to the Log Entry.
Added the current user name and process account name to the Log Entry.
Added COM+ IDs and caller account information to the Log Entry.
Added information about the configuration of the application to the Log Entry.
LogEntry written to configured trace listeners.
```

要查看添加到日志条目的附加信息，请打开 Windows 事件查看器并定位新日志条目。此处未显示该日志条目的内容，因为它超过 350 行，包含了您应用程序中发生的事件所需的几乎所有信息！

## 跟踪和关联活动

本章的最后一个主题演示了 Logging 块的另一项功能，该功能使在尝试跟踪或调试应用程序中某些顽固代码时，更容易关联多个日志条目。日志记录的一个问题是，仅依赖事件 ID 来关联与特定进程或代码部分相关的多个事件既困难又容易出错。事件 ID 通常不是唯一的，而且应用程序中不同组件实例生成的许多具有相同事件 ID 的事件会在日志中交错。

Logging 块使向特定日志条目添加附加唯一标识符变得容易，您可以稍后使用该标识符筛选日志并仅定位与特定进程或任务相关的条目。Logging 块跟踪功能使用 .NET Correlation Manager 类，该类维护一个 GUID 形式的 Activity ID。默认情况下，此 ID 未设置，但 Logging 块允许您使用 TraceManager 生成 Tracer 实例。每个实例都将 Activity ID 设置为随机生成的 GUID 值，该值仅在跟踪器上下文中维护。当跟踪器被释放或超出作用域时，Activity ID 将恢复为其先前的值。

创建跟踪器时，您需要指定一个操作名称。这实际上是块配置中定义的类别名称。在跟踪器上下文中创建的所有日志条目都将分配给该类别，此外还包括您在创建日志条目时指定的任何类别。

创建并启动跟踪器时，您可以指定一个 GUID 值，该跟踪器作用域内的所有后续日志条目以及所有未指定不同 GUID 的嵌套跟踪器都将使用指定的活动 ID。如果在前一个跟踪器的作用域内启动新的嵌套跟踪器实例，除非在创建并启动嵌套跟踪器时指定不同的 GUID，否则它将与父跟踪器具有相同的活动 ID；在这种情况下，此新活动 ID 将在该跟踪器作用域内的后续日志条目中使用。

尽管 Logging 块会自动将活动 ID 添加到每个日志条目，但使用文本格式化程序和默认模板时，它不会出现在生成的消息中。要在使用文本格式化程序的日志消息中包含活动 ID，必须在配置工具中编辑模板属性以包含标记 {property(ActivityId)}。请注意，模板定义中的属性名称区分大小写。

### 跟踪活动示例

示例“跟踪活动并将活动信息发布到类别”应有助于澄清这一点。在应用程序启动时，代码以与我们迄今使用的 LogWriter 相同的方式，从 Enterprise Library 容器中解析 TraceManager 实例。

```vb
' Resolve a TraceManager object from the container.
Dim traceMgr As TraceManager _
    = EnterpriseLibrary.Current.GetInstance(Of TraceManager)()
```

接下来，代码使用 TraceManager 的 StartTrace 方法创建并启动一个新的 Tracer 实例，指定名为 General 的类别。由于未指定 Activity ID 值，TraceManager 会自动创建一个。这是首选方法，因为运行此代码实例的每个单独进程都会生成不同的 GUID 值。这意味着您可以为每个进程隔离单个事件。

然后，代码在此跟踪器上下文中创建并写入一个日志条目，指定它除了跟踪器定义的 General 类别外，还属于 DiskFiles 类别。接下来，它创建一个指定名为 Database 类别的嵌套 Tracer 实例，并写入另一个指定名为 Important 类别的日志条目。因此，该日志条目将属于 General、Database 和 Important 类别。然后，在 Database 跟踪器超出作用域后，代码创建一个新的 Tracer，再次指定 Database 类别，但这次还指定要在此新跟踪器上下文中使用的 Activity ID。最后，它在新的 Database 跟踪器作用域内写入另一个日志条目。

```vb
' Start tracing for category 'General'. All log entries within trace context
' will be included in this category and use any specified Activity ID (GUID).
' If you do not specify an Activity ID, the TraceManager will create a new one.
Using traceMgr.StartTrace("General")
```

```vb
' Write a log entry with another category, will be assigned to both.
defaultWriter.Write("LogEntry with category 'DiskFiles' created within " _
    & "context of 'General' category tracer.", "DiskFiles")
```

```vb
' Start tracing for category 'Database' within context of 'General' tracer.
' Do not specify a GUID to use so that the existing one is used.
Using traceMgr.StartTrace("Database")

