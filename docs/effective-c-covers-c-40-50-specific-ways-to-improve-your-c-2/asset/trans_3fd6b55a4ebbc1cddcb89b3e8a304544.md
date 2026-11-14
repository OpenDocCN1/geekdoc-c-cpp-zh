

```csharp
get { return theOnly; }
}

// Define the event:
public event EventHandler<LoggerEventArgs> Log;

// add a message, and log it.
public void AddMsg(int priority, string msg)
{
    // This idiom discussed below.
    EventHandler<LoggerEventArgs> l = Log;
    if (l != null)
        l(this, new LoggerEventArgs(priority, msg));
}
}
```

AddMsg 方法展示了引发事件的正确方式。用于引用日志事件处理程序的临时变量是防止多线程程序中竞态条件的重要保障。如果没有引用的副本，客户端可能会在 `if` 语句检查和事件处理程序执行之间移除事件处理程序。通过复制引用，这种情况就不会发生。

我定义了 `LoggerEventArgs` 来保存事件的优先级和消息。委托定义了事件处理程序的签名。在 Logger 类中，事件字段定义了事件处理程序。编译器看到公共事件字段定义后，会为你生成 Add 和 Remove 运算符。生成的代码与你编写以下代码完全相同：

```csharp
public class Logger
{
    private EventHandler<LoggerEventArgs> log;

    public event EventHandler<LoggerEventArgs> Log
    {
        add { log = log + value; }
        remove { log = log - value; }
    }
}
```

```csharp
public void AddMsg(int priority, string msg)
{
    EventHandler<LoggerEventArgs> l = log;
    if (l != null)
        l(null, new LoggerEventArgs(priority, msg));
}
```

C# 编译器为事件创建 add 和 remove 访问器。我认为公共事件声明语言比 add/remove 语法更简洁，也更易于阅读和维护。在你的类中创建事件时，声明公共事件，并让编译器为你创建 add 和 remove 属性。编写自己的 add 和 remove 处理程序可以让你在 add 和 remove 处理程序中完成更多工作。

事件不需要知道任何关于潜在监听器的信息。以下类会自动将所有消息路由到标准错误控制台：

```csharp
class ConsoleLogger
{
    static ConsoleLogger()
    {
        Logger.Singleton.Log += (sender, msg) =>
        {
            Console.Error.WriteLine("{0}:\t{1}",
                msg.Priority.ToString(),
                msg.Message);
        };
    }
}
```

另一个类可以将输出定向到系统事件日志：

```csharp
class EventLogger
{
    private static Logger logger = Logger.Singleton;
    private static string eventSource;
    private static EventLog logDest;

    static EventLogger()
    {
        logger.Log += (sender, msg) =>
        {
            if (logDest != null)
                logDest.WriteEntry(msg.Message,
                    EventLogEntryType.Information,
                    msg.Priority);
        };
    }

    public static string EventSource
    {
        get { return eventSource; }
        set
        {
            eventSource = value;
            if (!EventLog.SourceExists(eventSource))
                EventLog.CreateEventSource(eventSource,
                    "ApplicationEventLogger");
            if (logDest != null)
                logDest.Dispose();
            logDest = new EventLog();
            logDest.Source = eventSource;
        }
    }
}
```

事件会通知任意数量的感兴趣的客户端某事已发生。Logger 类不需要事先知道哪些对象对记录日志事件感兴趣。

Logger 类只包含一个事件。有些类（主要是 Windows 控件）拥有非常大量的事件。在这种情况下，为每个事件使用一个字段的想法可能是不可接受的。在某些情况下，定义的事件中只有少数在单个应用程序中实际被使用。如果你遇到这种情况，可以修改设计，仅在运行时需要时才创建事件对象。

核心框架中包含了如何在 Windows 控件子系统中实现此功能的示例。为了向你展示如何操作，请向 Logger 类添加子系统。

你为每个子系统创建一个事件。客户端会注册到与其子系统相关的事件上。

扩展后的 Logger 类具有一个 System.ComponentModel.EventHandlerList 容器，用于存储给定系统应引发的所有事件对象。更新后的 AddMsg() 方法现在接受一个字符串参数，用于指定生成日志消息的子系统。如果子系统有任何监听器，则会引发该事件。此外，如果某个事件监听器已注册对所有消息的兴趣，则其事件也会被引发：

```csharp
public sealed class Logger
{
    private static System.ComponentModel.EventHandlerList
    Handlers = new EventHandlerList();

    static public void AddLogger(
    string system, EventHandler<LoggerEventArgs> ev)
    {
    Handlers.AddHandler(system, ev);
    }

    static public void RemoveLogger(string system,
    EventHandler<LoggerEventArgs> ev)
    {
    Handlers.RemoveHandler(system, ev);
    }

    static public void AddMsg(string system,
    int priority, string msg)
    {
    if (!string.IsNullOrEmpty(system))
    {
    EventHandler<LoggerEventArgs> l =
    Handlers[system] as
    EventHandler<LoggerEventArgs>;

    LoggerEventArgs args = new LoggerEventArgs(
    priority, msg);
    if (l != null)
    l(null, args);
    }

    // The empty string means receive all messages:
    l = Handlers[""] as
    EventHandler<LoggerEventArgs>;
    if (l != null)
    l(null, args);
    }
}
```

此新示例将各个事件处理程序存储在 EventHandlerList 集合中。遗憾的是，EventHandlerList 没有泛型版本。因此，在这段代码中，你会看到比本书中许多示例多得多的强制转换和类型转换。客户端代码会附加到特定的子系统，并创建一个新的事件对象。对同一子系统的后续请求会检索到同一个事件对象。如果你开发的类在其接口中包含大量事件，则应考虑使用此事件处理程序集合。当客户端附加到他们选择的事件处理程序时，你会创建事件成员。在 .NET Framework 中，System.Windows.Forms.Control 类使用此实现的更复杂变体来隐藏其所有事件字段的复杂性。每个事件字段在内部访问一个对象集合，以添加和移除特定的处理程序。你可以在 C# 语言规范中找到展示此惯用法的更多信息。

EventHandlerList 类是尚未更新为新泛型版本的类之一。从 Dictionary 类构建自己的版本并不困难：

```csharp
public sealed class Logger
{
private static Dictionary<string,
EventHandler<LoggerEventArgs>>
Handlers = new Dictionary<string,
EventHandler<LoggerEventArgs>>();

static public void AddLogger(
string system, EventHandler<LoggerEventArgs> ev)
{
if (Handlers.ContainsKey(system))
Handlers[system] += ev;
else
Handlers.Add(system, ev);
}

static public void RemoveLogger(string system,
    EventHandler<LoggerEventArgs> ev)
{
    // will throw exception if system
    // does not contain a handler.
    Handlers[system] -= ev;
}

static public void AddMsg(string system,
    int priority, string msg)
{
    if (string.IsNullOrEmpty(system))
    {
        EventHandler<LoggerEventArgs> l = null;
        Handlers.TryGetValue(system, out l);

    LoggerEventArgs args = new LoggerEventArgs(
        priority, msg);
    if (l != null)
        l(null, args);

    // The empty string means receive all messages:
    l = Handlers[""] as
        EventHandler<LoggerEventArgs>;
    if (l != null)
    l(null, args);
    }
}
```

泛型版本用于处理事件映射的代码量增加，以换取减少强制转换和类型转换。我更倾向于使用泛型版本，但这只是权衡之利弊。

事件提供了一种通知监听器的标准语法。.NET 事件模式遵循事件语法来实现观察者模式。任意数量的客户端可以将处理程序附加到事件并对其进行处理。这些客户端在编译时不需要被知晓。事件不需要订阅者，系统也能正常运行。在 C# 中使用事件可以解耦

