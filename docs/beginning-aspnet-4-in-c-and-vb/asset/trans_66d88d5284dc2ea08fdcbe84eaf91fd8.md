

消息格式化程序实现 `IMessageFormatter` 接口。在 `System.Messaging` 命名空间中提供了三种消息格式化程序：

- `XmlMessageFormatter` 是默认格式化程序。它使用 XML 序列化对象。有关 XML 格式化的更多信息，请参阅第 33 章“操作 XML”。
- 使用 `BinaryMessageFormatter`，消息以二进制格式序列化。这些消息比使用 XML 格式化的消息更短。
- `ActiveXMessageFormatter` 是一种二进制格式化程序，因此消息可以通过 COM 对象读取或写入。使用此格式化程序，可以用 .NET 类将消息写入队列，并用 COM 对象从队列中读取消息，反之亦然。

图 46-8 中显示的 XML 示例消息在图 46-9 中使用 `BinaryMessageFormatter` 进行格式化。

![](img/d7d2ffa0a76feaab821930e95daace93_1429_0.png)

图 46-9

## 发送复杂消息

除了传递字符串之外，还可以将对象传递给 `MessageQueue` 类的 `Send()` 方法。类的类型必须满足一些特定要求，但这些要求取决于格式化程序。

对于二进制格式化程序，类必须使用 `[Serializable]` 特性实现可序列化。使用 .NET 运行时序列化，所有字段都会被序列化（包括私有字段）。可以通过实现 `ISerializable` 接口来定义自定义序列化。你可以在第 29 章“操作文件和注册表”中了解有关 .NET 运行时序列化的更多信息。

XML 序列化由 XML 格式化程序执行。使用 XML 序列化时，所有公共字段和属性都会被序列化。可以使用 `System.Xml.Serialization` 命名空间中的特性来影响 XML 序列化。你可以在第 33 章中了解有关 XML 序列化的更多信息。

## 接收消息

要读取消息，仍然可以使用 `MessageQueue` 类。通过 `Receive()` 方法，可以读取单条消息并将其从队列中移除。如果消息以不同的优先级发送，则读取优先级最高的消息。读取相同优先级的消息可能意味着最先发送的消息并不是最先读取的消息，因为网络中的消息顺序无法保证。要确保顺序，应使用事务性消息队列。

在下面的示例中，从私有队列 `MyPrivateQueue` 读取一条消息。之前，一个简单字符串被传递给了消息。使用 `XmlMessageFormatter` 读取消息时，必须将所读取对象的类型传递给格式化程序的构造函数。在示例中，`System.String` 类型被传递给 `XmlMessageFormatter` 构造函数的参数数组。此构造函数允许传入一个包含类型字符串的字符串数组，或一个类型数组。

使用 `Receive()` 方法读取消息，然后将消息正文写入控制台：

```
using System;
using System.Messaging;

namespace Wrox.ProCSharp.Messaging
{
    class Program
    {
        static void Main()
        {
            var queue = new MessageQueue(@".\Private$\MyPrivateQueue");
            queue.Formatter = new XmlMessageFormatter(
                new string[] {"System.String"});

            Message message = queue.Receive();
            Console.WriteLine(message.Body);
        }
    }
}
```

代码片段 SendMessage/Program.cs

`Receive()` 方法是同步的，如果队列中没有消息，它会一直等待直到队列中有消息。

## 枚举消息

除了使用 `Receive()` 方法逐条读取消息外，还可以使用枚举器遍历所有消息。`MessageQueue` 类实现了 `IEnumerable` 接口，因此可以用于 `foreach` 语句。这里，消息不会从队列中移除，而只是查看消息以获取其内容：

```
var queue = new MessageQueue(@".\Private$\MyPrivateQueue");
queue.Formatter = new XmlMessageFormatter(
    new string[] {"System.String"});

foreach (Message message in queue)
{
    Console.WriteLine(message.Body);
}
```

除了使用 `IEnumerable` 接口外，还可以使用 `MessageEnumerator` 类。`MessageEnumerator` 实现了 `IEnumerator` 接口，但具有更多功能。使用 `IEnumerable` 接口时，消息不会从队列中移除。`MessageEnumerator` 的 `RemoveCurrent()` 方法会将消息从枚举器当前游标位置移除。

在示例中，使用 `MessageQueue.GetMessageEnumerator` 方法访问 `MessageEnumerator`。`MoveNext()` 方法通过 `MessageEnumerator` 逐条查看消息。`MoveNext()` 方法被重载，允许将时间跨度作为参数。这是使用此枚举器的一大优势。这里，线程可以等待消息到达队列，但只能等待指定的时间跨度。`Current` 属性由 `IEnumerator` 接口定义，返回对消息的引用：

```
var queue = new MessageQueue(@".\Private$\MyPrivateQueue");
queue.Formatter = new XmlMessageFormatter(
    new string[] {"System.String"});

using (MessageEnumerator messages = queue.GetMessageEnumerator())
{
    while (messages.MoveNext(TimeSpan.FromMinutes(30)))
    {
        Message message = messages.Current;
        Console.WriteLine(message.Body);
    }
}
```

## 异步读取

`MessageQueue` 类的 `Receive` 方法会一直等待，直到队列中有消息可以读取。为了避免阻塞线程，可以在 `Receive` 方法的重载版本中指定超时时间。超时后，必须再次调用 `Receive()` 才能从队列中读取消息。除了轮询消息之外，还可以调用异步方法 `BeginReceive()`。在调用 `BeginReceive()` 开始异步读取之前，应设置 `ReceiveCompleted` 事件。`ReceiveCompleted` 事件需要一个 `ReceiveCompletedEventHandler` 委托，该委托引用的方法会在消息到达队列并可读取时被调用。在示例中，`MessageArrived` 方法被传递给 `ReceiveCompletedEventHandler` 委托：

```
var queue = new MessageQueue(@"\\.\Private$\MyPrivateQueue");
queue.Formatter = new XmlMessageFormatter(
    new string[] { "System.String" });

queue.ReceiveCompleted += MessageArrived;
queue.BeginReceive();
// thread does not wait
```

处理程序方法 `MessageArrived` 需要两个参数。第一个参数是事件源，即 `MessageQueue`。第二个参数的类型为 `ReceiveCompletedEventArgs`，包含消息和异步结果。在示例中，调用队列的 `EndReceive()` 方法获取异步方法的结果，即消息：

```csharp
public static void MessageArrived(object source, ReceiveCompletedEventArgs e)
{
    MessageQueue queue = (MessageQueue)source;
    Message message = queue.EndReceive(e.AsyncResult);
    Console.WriteLine(message.Body);
}
```

如果消息不应从队列中移除，可以将 `BeginPeek()` 和 `EndPeek()` 方法与异步 I/O 一起使用。

## 课程订购应用程序

为了演示消息队列的使用，在本节中，你将创建一个订购课程的示例解决方案。该示例解决方案由三个程序集组成：

- 一个组件库（CourseOrder），包含队列中发送和接收的消息的实体类
- 一个 WPF 应用程序（CourseOrderSender），向消息队列发送消息
- 一个 WPF 应用程序（CourseOrderReceiver），从消息队列接收消息

## 课程订购类库

发送和接收应用程序都需要订单信息。因此，实体类被放入单独的程序集中。`CourseOrder` 程序集包含三个实体类：`CourseOrder`、`Course` 和 `Customer`。在此示例应用程序中，并非所有属性都如同在实际应用程序中那样实现，而仅实现了足以说明概念的部分属性。

在 Course.cs 文件中，定义了 `Course` 类。该类只有一个属性，用于表示课程标题：

```csharp
namespace Wrox.ProCSharp.Messaging
{
    public class Course
    {
        public string Title { get; set; }
    }
}
```

