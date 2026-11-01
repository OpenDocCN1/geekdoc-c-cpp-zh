
来自 `DelimitedListTraceListener` 的分隔文件输出（包括进程 ID 和日期/时间）如下所示：

```
```text
"Wrox.ProCSharp.Instrumentation": Information:0:"Info message":
    5288:"":"":2009-10-11T10:35:55.8479950Z":
"Wrox.ProCSharp.Instrumentation": Error:3:"Error message":5288:"":"
    ":2009-10-11T10:35:55.8509257Z":
"Wrox.ProCSharp.Instrumentation": Information:2:
    "data":4,"":5:5288:"":"":2009-10-11T10:35:55.8519026Z":
```
```

来自 `XmlWriterTraceListener` 的 XML 输出始终包含计算机名称、进程 ID、线程 ID、消息、创建时间、源和活动 ID。其他字段（如调用堆栈、逻辑操作堆栈和时间戳）取决于跟踪输出选项。

> 你可以使用 `XmlDocument` 和 `XPathNavigator` 类来分析 XML 文件中的内容。这些类将在第 33 章“操作 XML”中介绍。

如果某个监听器需要被多个跟踪源使用，可以将监听器配置添加到 `<sharedListeners>` 元素中，该元素在跟踪源处实现。配置为共享监听器的监听器名称必须从跟踪源的监听器列表中引用：

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="Wrox.ProCSharp.Tracing" switchName="MySourceSwitch"
              switchType="System.Diagnostics.SourceSwitch">
        <listeners>
          <add name="xmlListener"
               type="System.Diagnostics.XmlWriterTraceListener"
               traceOutputOptions="None"
               initializeData="c:/logs/mytrace.xml" />
          <add name="delimitedListener" />
        </listeners>
      </source>
    </sources>
    <sharedListeners>
      <add name="delimitedListener" delimiter="," 
           type="System.Diagnostics.DelimitedListTraceListener"
           traceOutputOptions="DateTime, ProcessId"
           initializeData="c:/logs/mytrace.txt" />
    </sharedListeners>
    <switches>
      <add name="MySourceSwitch" value="Verbose"/>
    </switches>
  </system.diagnostics>
</configuration>
```
```

*代码片段 TracingDemo\app.config*

## 筛选器

每个监听器都有一个 Filter 属性，用于定义监听器是否应写入跟踪消息。例如，多个监听器可以用于同一跟踪源。其中一个监听器将详细消息写入日志文件，另一个监听器将错误消息写入事件日志。在监听器写入跟踪消息之前，它会调用关联筛选器对象的 `ShouldTrace()` 方法，以决定是否应写入该跟踪消息。

筛选器是从抽象基类 TraceFilter 派生的类。.NET 4 提供了两种筛选器实现：SourceFilter 和 EventTypeFilter。使用源筛选器，可以指定仅从特定源写入跟踪消息。事件类型筛选器是开关功能的扩展。使用开关，可以根据跟踪严重级别定义事件源是否应将跟踪消息转发给监听器。如果跟踪消息被转发，监听器现在可以使用筛选器来决定是否应写入该消息。

更改后的配置现在定义了分隔监听器仅应在严重级别为警告或更高时写入跟踪消息，因为定义了 EventTypeFilter。XML 监听器指定了 SourceFilter，并且仅接受来自源 Wrox.ProCSharp.Tracing 的跟踪消息。如果定义了大量源将跟踪消息写入同一个监听器，则可以更改监听器的配置，使其专注于来自特定源的跟踪消息。

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="Wrox.ProCSharp.Tracing" switchName="MySourceSwitch">
        <switchType="System.Diagnostics.SourceSwitch">
        <listeners>
          <add name="xmlListener" />
          <add name="delimitedListener" />
        </listeners>
      </source>
    </sources>
    <sharedListeners>
      <add name="delimitedListener" delimiter="," 
           type="System.Diagnostics.DelimitedListTraceListener"
           traceOutputOptions="DateTime, ProcessId"
           initializeData="c:\logs\mytrace.txt">
      <filter type="System.Diagnostics.EventTypeFilter"
              initializeData="Warning" />
      <add name="xmlListener"
           type="System.Diagnostics.XmlWriterTraceListener"
           traceOutputOptions="None"
           initializeData="c:\logs\mytrace.xml">
      <filter type="System.Diagnostics.SourceFilter"
              initializeData="Wrox.ProCSharp.Instrumentation" />
    </sharedListeners>
    <switches>
      <add name="MySourceSwitch" value="Verbose" />
    </switches>
  </system.diagnostics>
</configuration>
```

*代码片段 TracingDemo\App.config*

跟踪架构是可以扩展的。正如你可以编写从基类 TraceListener 派生的自定义监听器一样，你也可以创建从 TraceFilter 派生的自定义筛选器。有了这种能力，你可以创建一个筛选器，指定写入跟踪消息的条件，例如根据时间、根据最近发生的异常或根据天气。

## 相关性

借助跟踪日志，你可以通过多种方式查看不同方法之间的关系。要查看跟踪事件的调用堆栈，只需一个配置即可使用 XML 监听器跟踪调用堆栈。你还可以定义可在日志消息中显示的逻辑调用堆栈。并且你可以定义活动来映射跟踪消息。

```
```
"starting a new task");
Task.Factory.StartNew(WorkForATask);
Trace.CorrelationManager.StopLogicalOperation();
Trace.CorrelationManager.ActivityId = oldGuid;
}
```
```

从 StartActivityA() 方法内部启动的 Foo() 方法启动了一个新的逻辑操作。逻辑操作 Foo 在 StartActivityA 逻辑操作内部启动。

```
private static void Foo()
{
    Trace.CorrelationManager.StartLogicalOperation("Foo operation");

    trace.TraceEvent(TraceEventType.Verbose, 0, "running Foo");

    Trace.CorrelationManager.StopLogicalOperation();
}
```

从 StartActivityA() 方法内部创建的任务会运行 WorkForATask() 方法。这里，仅将带有开始和停止信息以及详细信息的简单跟踪事件写入跟踪。

```
private static void WorkForATask()
{
    trace.TraceEvent(TraceEventType.Start, 0, "WorkForATask started");

    trace.TraceEvent(TraceEventType.Verbose, 0, "running WorkForATask");

    trace.TraceEvent(TraceEventType.Stop, 0, "WorkForATask completed");
}
```

若要分析跟踪信息，可以启动工具 Service Trace Viewer（svctraceviewer.exe）。该工具主要用于分析 WCF 跟踪，但也可用于分析任何使用 XmlWriterTraceListener 编写的跟踪。图 19-3 在 Activity 屏幕中显示了活动，每个活动在右侧屏幕中显示事件。当选择一个事件时，你可以将显示设置为以 XML 或格式化视图显示完整消息。在格式化视图中，基本信息、应用程序数据、逻辑操作堆栈和调用堆栈都经过良好格式化。

![](img/d7d2ffa0a76feaab821930e95daace93_535_0.png)

图 19-3

图 19-4 显示了图形视图，在此视图中，可以选择不同的进程或线程以显示在单独的泳道中。当使用 TaskFactory 类创建新线程时，若选择线程视图，则会出现第二个泳道。

![](img/d7d2ffa0a76feaab821930e95daace93_536_0.png)

图 19-4

## 事件日志记录

系统管理员使用事件查看器来获取关于系统和应用程序运行状况的关键消息以及信息消息。你应该将应用程序中的错误消息写入事件日志，以便可以通过事件查看器读取这些信息。

如果配置了 EventLogTraceListener 类，则可以将跟踪消息写入事件日志。EventLogTraceListener 有一个与之关联的 EventLog 对象，用于写入事件日志条目。你也可以直接使用 EventLog 类来写入和读取事件日志。

在本节中，你将了解以下内容：

- 事件日志记录架构
- System.Diagnostics 命名空间中用于事件日志记录的类
- 向服务和其他应用程序类型添加事件日志记录
- 使用 EventLog 类的 EnableRaisingEvents 属性创建事件日志监听器
- 使用资源文件定义消息

图 19-5 显示了使用分布式 COM 访问失败时的日志条目示例。
