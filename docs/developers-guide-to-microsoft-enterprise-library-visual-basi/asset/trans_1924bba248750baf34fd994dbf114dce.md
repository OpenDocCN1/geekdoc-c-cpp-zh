

要查看此示例创建的两条日志消息，可以使用 Visual Studio 服务器资源管理器打开 bin\Debug 文件夹中的 Logging.mdf 数据库。你会发现第二条消息的 FormattedMessage 列包含以下内容。你可以看到我们在消息末尾使用 Dictionary 添加的扩展属性信息。

```
Timestamp: 03/12/2009 17:14:02
Message: LogEntry with category, priority, event ID, severity, title, and extended properties.
Category: Database
Priority: 8
EventId: 9009
Severity: Error
Title: Logging Block Examples
Activity ID: 00000000-0000-0000-0000-000000000000
Machine: BIGFOOT
App Domain: LoggingExample.vshost.exe
ProcessID: 5860
Process Name: E:\Logging\Logging\bin\Debug\LoggingExample.vshost.exe
Thread Name:
Win32 ThreadId:3208
Extended Properties: Extra Information - Some Special Value
```

请注意，由于 Log 和 CategoryLog 表之间存在引用，你不能简单地删除已记录的信息。但是，数据库包含一个名为 ClearLogs 的存储过程，你可以执行它来删除所有日志条目。

本示例提供的数据库的连接字符串为：
Data Source=.\SQLEXPRESS;AttachDbFilename=|DataDirectory|\Logging.mdf;Integrated Security=True;User Instance=True

如果你使用企业库随附的脚本配置了其他数据库，运行此示例时可能会出现错误。这很可能是因为你的 App.config 文件中数据库的连接字符串无效。此外，使用“管理工具”文件夹中的“服务”小程序检查 SQL Server (SQLEXPRESS) 数据库服务（名为 MSSQL$SQLEXPRESS 的服务）是否正在运行。

## 测试日志筛选器状态

如前示例所示，日志块允许你在创建和写入日志条目之前检查日志是否已启用。如果日志未启用，你可以避免这对应用程序造成的额外负载。但是，即使启用了日志，也不能保证特定的日志条目会写入目标日志存储。例如，如果消息优先级低于指定级别，它可能会被优先级筛选器阻止；或者它可能仅属于一个或多个类别，而这些类别的相关类别筛选器已禁用日志（这在仅为调试用途设计的日志代码中是常见场景）。

示例“检查筛选器状态并向日志条目添加上下文信息”演示了如何在实际调用 **写入** 方法之前检查特定日志条目是否会写入其目标。在检查日志未被全局禁用后，示例会创建具有不同类别和优先级的两个 **日志条目** 实例。它将每个实例依次传递给另一个名为 **显示详细信息并添加额外信息** 的方法。以下是创建 **日志条目** 实例的代码。

```
' Check if logging is enabled before creating log entries.
If defaultWriter.IsLoggingEnabled() Then
    ' Create a new LogEntry with two categories and priority 3.
    Dim logCategories As String() = New String() {"General", "DiskFiles"}
    Dim entry1 As New LogEntry("Logging with categories 'General' and _
        & " 'DiskFiles' and Priority 3.", logCategories, _
        3, 9009, TraceEventType.Error, _
        "Logging Block Examples", Nothing)
    ShowDetailsAndAddExtraInfo(entry1)
    ' Create a new LogEntry with one category and priority 1.
    logCategories = New String() {"BlockedByFilter"}
    Dim entry2 As New LogEntry("Logging with category 'BlockedByFilter' and _
        & " Priority 1.", logCategories, 1, 9010, _
        TraceEventType.Information, _
        "Logging Block Examples", Nothing)
    ShowDetailsAndAddExtraInfo(entry2)
Else
    Console.WriteLine("Logging is disabled in the configuration.")
End If
```

**显示详细信息并添加额外信息** 方法接受一个 **日志条目** 实例并执行两项不同的操作。首先，它展示了如何获取日志块将如何处理日志条目的信息。在需要以编程方式确定特定日志条目是否被特定跟踪源检测到，或是否会写入特定目标的高级场景中，这可能很有用。其次，它演示了如何检查特定筛选器或所有筛选器是否会阻止日志条目写入其目标。

## 获取有关跟踪源和跟踪侦听器的信息

**显示详细信息并添加额外信息** 方法的第一部分遍历由 LogWriter 类的 **获取匹配的跟踪源** 方法公开的跟踪源（**日志源** 实例）集合。每个 **日志源** 实例都公开一个 **侦听器** 集合，该集合包含有关侦听器的信息（侦听器指定将发送日志条目的目标）。

```
Sub ShowDetailsAndAddExtraInfo(ByVal entry As LogEntry)

    ' Display information about the Trace Sources and Listeners for this LogEntry.
    Dim sources As IEnumerable(Of LogSource) _
        = defaultWriter.GetMatchingTraceSources(entry)

    For Each source As LogSource In sources
        Console.WriteLine("Log Source name: '{0}'", source.Name)
        For Each listener As TraceListener In source.Listeners
            Console.WriteLine(" - Listener name: '{0}'", listener.Name)
        Next
    Next
    ...
```

## 检查筛选器是否会阻止日志条目

接下来，ShowDetailsAndAddExtraInfo 方法检查是否有任何筛选器会阻止当前日志条目。你可以采用两种方式来执行此操作。你可以依次查询每个筛选器类型，或者仅查询特定筛选器类型，方法是使用 LogWriter 类的 GetFilter 方法获取该类型筛选器的引用。然后，你可以检查此筛选器是否已启用，并使用 ShouldLog 方法（向其传递日志条目的类别列表）来查看日志记录是否会成功。

以下代码演示了这种方法。它还展示了如果你不关心特定筛选器类型的结果时可以使用的更简单方法。LogWriter 类还公开了 ShouldLog 方法，该方法指示是否有任何筛选器会阻止此条目。

```
...
    ' Check if any filters will block this LogEntry.
    ' This approach allows you to check for specific types of filter.
    ' If there are no filters of the specified type configured, the GetFilter
    ' method returns null, so check this before calling the ShouldLog method.
    Dim catfilter As CategoryFilter = defaultWriter.GetFilter(Of CategoryFilter)()
    If catfilter Is Nothing OrElse catfilter.ShouldLog(entry.Categories) Then
        Console.WriteLine("Category Filter(s) will not block this LogEntry.")
    Else
        Console.WriteLine("A Category Filter will block this LogEntry.")
    End If

    Dim prifilter As PriorityFilter = defaultWriter.GetFilter(Of PriorityFilter)()
    If prifilter Is Nothing OrElse prifilter.ShouldLog(entry.Priority) Then
        Console.WriteLine("Priority Filter(s) will not block this LogEntry.")
    Else
        Console.WriteLine("A Priority Filter will block this LogEntry.")
    End If

    ' Alternatively, a simple approach can be used to check for any type of filter
    If defaultWriter.ShouldLog(entry) Then
        Console.WriteLine("This LogEntry will not be blocked by config settings.")
    ...
    ' Add context information to log entries after checking that the log entry
    ' will not be blocked due to configuration settings. See the following
    ' section 'Adding Additional Context Information' for details.
    ...
    Else
    Console.WriteLine("This LogEntry will be blocked by configuration settings.")
    End If
End Sub
```

在确定日志记录将成功后，你可以添加额外的上下文信息并写入日志条目。稍后你将看到实现此目的的代码。与此同时，以下是示例生成的输出。你可以看到，它包含之前代码创建的两个日志条目各自的日志（跟踪）源和侦听器详细信息，以及检查是否有任何类别筛选器会阻止每个日志条目的结果。

```
Created a LogEntry with categories 'General' and 'DiskFiles'.
Log Source name: 'General'
- Listener name: 'Formatted Eventlog TraceListener'
Log Source name: 'DiskFiles'
- Listener name: 'FlatFile TraceListener'
- Listener name: 'XML TraceListener'
Category Filter(s) will not block this LogEntry.
Priority Filter(s) will not block this LogEntry.
...
This LogEntry will not be blocked due to configuration settings.
Created a LogEntry with category 'BlockedByFilter', and Priority 1.
Log Source name: 'BlockedByFilter'
- Listener name: 'Formatted Eventlog TraceListener'
A Category Filter will block this LogEntry.
A Priority Filter will block this LogEntry.
This LogEntry will be blocked due to configuration settings.
```

## 添加其他上下文信息

虽然在日志消息中包含每种可想象的信息很有用，但这并不总是最佳方法。从环境中收集信息会占用处理周期，并增加日志记录对应用程序造成的负载。日志块经过高度优化，以尽量减少日志记录带来的负载。例如，一些不太有用的信息默认不会包含在日志消息中——特别是那些收集需要额外资源的信息。

但是，如果你愿意，可以收集此信息。你可以决定仅在调查问题时才启用的特殊调试检测中执行此操作，或者

