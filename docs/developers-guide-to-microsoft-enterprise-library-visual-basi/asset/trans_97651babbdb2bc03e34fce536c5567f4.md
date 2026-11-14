

## 捕获未处理的事件并记录错误

本示例使用 **General** 类别将日志条目写入 Windows 应用程序事件日志。如果查看本示例生成的事件，您将看到上面代码中设置的值（列表末尾包括我们使用 **Dictionary** 指定的扩展属性）。您可以在图 6 中看到这一点。

![](img/d7009d38323c3b86f2dfbc5155fbf141_125_0.png)

### 图 6
*写入 General 类别的日志条目*

### 关于特殊源

实际上，日志块包含三个用于处理这些情况的特殊源。每个特殊源实际上都是一个类别，您可以向每个特殊源添加对配置的跟踪侦听器的引用，以便到达该类别的事件将被写入您指定的目标。

**All Events** 特殊源接收所有事件，不受块配置中所有其他设置的影响。如果需要，您可以使用它来提供所有事件的审计跟踪。默认情况下，它未配置任何跟踪侦听器。

**Unprocessed Category** 特殊源接收任何类别与任何配置类别均不匹配的日志条目。默认情况下，此类别未配置任何跟踪侦听器。

**Logging Errors & Warnings** 特殊源接收任何在日志记录过程中导致错误的日志条目。默认情况下，此类别包含对跟踪侦听器的引用，该侦听器将错误详细信息写入 Windows 应用程序事件日志，不过您可以根据需要重新配置它。

## 使用特殊源的示例

示例“使用特殊源捕获未处理的事件或错误”演示了日志块在这两种情况下的反应。代码首先将日志条目写入名为 InvalidCategory 的类别，该类别不存在于配置中。接下来，它将另一个日志条目写入名为 CauseLoggingError 的类别，该类别配置为使用数据库跟踪侦听器。但是，此跟踪侦听器指定了一个无效的连接字符串；它指向一个不存在的数据库。

```
' Check if logging is enabled before creating log entries.
If defaultWriter.IsLoggingEnabled() Then

    ' Create a log entry to be processed by the "Unprocessed" special source.
    defaultWriter.Write("Entry with category not defined in configuration.", _
        "InvalidCategory")

    ' Create log entry to be processed by the "Errors & Warnings" special source.
    defaultWriter.Write("Entry that causes a logging error.", "CauseLoggingError")

Else
    Console.WriteLine("Logging is disabled in the configuration.")
End If
```

您可能会认为这两个日志条目都无法到达其目标。但是，示例生成了以下消息，指示在哪里查找生成的日志条目。

```
Created a Log Entry with a category name not defined in the configuration.
The Log Entry will appear in the Unprocessed.log file in the C:\Temp folder.

Created a Log Entry that causes a logging error.
The Log Entry will appear in the Windows Application Event Log.
```

这是因为我们在特殊源部分中配置了 Unprocessed Category，并引用了一个将日志条目写入名为 Unprocessed.log 文件的平面文件跟踪侦听器。如果打开此文件，您将看到发送到 InvalidCategory 类别的日志条目。

示例对 Logging Errors & Warnings 特殊源使用默认配置。这意味着导致日志记录错误的日志条目将发送到该类别中引用的格式化事件日志跟踪侦听器。如果打开应用程序事件日志，您将在该类别中看到此条目。下面的清单显示了部分内容。

```
Timestamp: 24/11/2009 15:14:30
Message: Tracing to LogSource 'CauseLoggingError' failed. Processing for other sources will continue. See summary information below for more information. Should this problem persist, stop the service and check the configuration file(s) for possible error(s) in the configuration of the categories and sinks.
```

### 企业库分发器服务摘要：

```
-->
Message:
Timestamp: 24/11/2009 15:14:30
Message: Entry that causes a logging error.
Category: CauseLoggingError
...
...
Exception Information Details:
--------------------------------
Exception Type: System.Data.SqlClient.SqlException
Errors: System.Data.SqlClient.SqlErrorCollection
Class: 11
LineNumber: 65536
Number: 4060
Procedure:
Server: (local)\SQLEXPRESS
State: 1
Source: .Net SqlClient Data Provider
ErrorCode: -2146232060
Message: Cannot open database "DoesNotExist" requested by the login.
The login failed.
Login failed for user 'xxxxxx\xxxxx'.
...
...
Stack Trace Information Details:
--------------------------------
...
...
...
```

除了日志条目本身之外，您还可以看到该事件包含大量信息，可帮助您调试错误。它包含一条指示发生日志记录错误的消息，后跟日志条目本身。但是，之后是一个包含日志记录机制引发的异常详细信息的部分（您可以看到 SqlClient 数据访问代码生成的错误消息），之后是完整的堆栈跟踪。

需要注意的是，记录数据库和安全异常时应始终以保护日志中可能包含的敏感信息的方式进行。您必须确保适当限制对日志的访问，并且仅向其他用户公开非敏感信息。您可能需要考虑应用异常屏蔽，如第 3 章“使错误管理变得异常简单”中所述。

## 记录到数据库

在 Windows 事件日志和文本文件之后，日志记录最常见的需求之一是将日志条目存储在数据库中。日志块包含数据库跟踪侦听器，使此操作变得简单。您使用随企业库提供的脚本配置数据库，该脚本位于源代码的 \Blocks\Logging\Src\DatabaseTraceListener\Scripts 文件夹中。我们还随本章示例包含了这些脚本。

这些脚本假设您将使用本地安装的 SQL Server Express 数据库，但您可以编辑 CreateLoggingDb.cmd 文件以将目标更改为其他数据库服务器。命令文件执行的 SQL 脚本创建一个名为 Logging 的数据库，并向其中添加所需的表和存储过程。

但是，如果您只想运行我们为本章提供的示例应用程序，则无需创建数据库。项目包含一个名为 Logging.mdf 的预配置数据库文件（位于 bin\Debug 文件夹），它会自动附加到您的本地 SQL Server Express 实例。您可以使用 Visual Studio 服务器资源管理器连接到此数据库以查看内容。数据库跟踪侦听器的配置包含数据库实例属性，该属性引用在数据访问应用程序块的设置部分中配置的此数据库（参见图 7）。

![](img/d7009d38323c3b86f2dfbc5155fbf141_128_0.png)

### 图 7 数据库跟踪侦听器的配置

数据库跟踪侦听器使用文本格式化程序格式化输出，因此您可以编辑用于生成日志消息的模板以满足您的要求。如果需要，还可以向日志条目添加扩展属性。此外，与所有跟踪侦听器一样，您可以根据需要按严重性筛选日志条目。

数据库中的 Log 表仅包含常用值的列，例如消息、事件 ID、优先级、严重性、标题、时间戳、计算机和进程详细信息等。它还包含名为 FormattedMessage 的列，其中包含文本格式化程序生成的消息。

### 使用数据库跟踪侦听器

示例“将日志条目发送到数据库”演示了数据库跟踪侦听器的使用。代码相对简单，遵循与前面创建扩展属性 Dictionary 的示例相同的风格，然后使用 LogWriter 的 Write 方法写入两个日志条目。第一个日志条目由 LogWriter 根据传递给 Write 方法的参数值创建。第二个日志条目在代码中作为新的 LogEntry 实例生成，方法是指定构造函数参数的值。还要注意，使用简单的 Dictionary 作为日志条目的 ExtendedProperties 向日志条目添加其他信息是多么容易。

```
' Check if logging is enabled before creating log entries.
If defaultWriter.IsLoggingEnabled() Then

    ' Create a Dictionary of extended properties
    Dim exProperties As New Dictionary(Of String, Object())
    exProperties.Add("Extra Information", "Some Special Value")

    ' Create a LogEntry using the constructor parameters.
    defaultWriter.Write("Log entry with category, priority, event ID, severity, " _
        & "title, and extended properties.", "Database", _
        5, 9008, TraceEventType.Warning, _
        "Logging Block Examples", exProperties)

    ' Create a LogEntry using the constructor parameters.
    Dim entry As New LogEntry("LogEntry with category, priority, event ID, " _
        & "severity, title, and extended properties.", _
        "Database", 8, 9009, TraceEventType.Error, _
        "Logging Block Examples", exProperties)

    defaultWriter.Write(entry)
Else
    Console.WriteLine("Logging is disabled in the configuration.")
End If
```

