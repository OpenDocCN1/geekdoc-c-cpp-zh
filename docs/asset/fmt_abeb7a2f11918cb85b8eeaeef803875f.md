
## 第 24 章 运行时序列化

在本章中：
序列化/反序列化快速上手 ........................... 662
使类型可序列化 ....................................................... 667
控制序列化与反序列化 ................................ 668
格式化程序如何序列化类型实例 ................................. 672
控制序列化/反序列化的数据 ........................ 673
流上下文 ................................................................ 680
将类型序列化为不同类型并将对象反序列化为不同对象 ........................................................... 682
序列化代理 ........................................................ 684
在反序列化对象时重写程序集和或类型...... 689

序列化是将对象或连接对象的图图转换为字节流的过程。反序列化是将字节流转换为其连接对象的图图的过程。在对象与字节流之间进行转换的能力是一种极其有用的机制。以下是一些示例：

- 应用程序的状态（对象图）可以轻松保存到磁盘文件或数据库中，并在下次运行应用程序时恢复。`ASP.NET` 通过序列化和反序列化来保存和恢复会话。
- 一组对象可以轻松复制到系统剪贴板，然后粘贴到相同或另一个应用程序中。事实上，`Windows Forms` 和 `Windows Presentation Foundation (WPF)` 使用了这种技术。
- 一组对象可以被克隆并作为“备份”，而用户可以操作“主”对象组。
- 一组对象可以轻松通过网络发送到运行在另一台机器上的进程。`Microsoft .NET Framework` 的远程架构会序列化按值封装（marshaled by value）的对象。正如第 22 章“`CLR` 托管与 `AppDomains`”所讨论的，它还用于跨 `AppDomain` 边界发送对象。

除了上述之外，一旦你在内存中将对象序列化为字节流，就很容易以更有用的方式处理数据，例如对数据进行加密和压缩。

### 第四部分 核心设施

由于序列化如此有用，许多程序员花费数小时编写代码来执行此类操作也并不稀奇。从历史上看，这些代码编写起来困难，而且极其繁琐且容易出错。开发者需要处理的一些问题包括通信协议、客户端/服务器数据类型不匹配（例如小端/大端序问题）、错误处理、引用其他对象的对象，以及 `out` 参数、结构体数组等等。

不过，你会高兴地知道，`.NET Framework` 内置了对序列化和反序列化的极佳支持。这意味着上述提到的所有问题现在都由 `.NET Framework` 完全且透明地处理了。作为开发人员，你可以在序列化之前和反序列化之后处理你的对象，并让 `.NET Framework` 处理中间的部分。

在本章中，我将解释 `.NET Framework` 如何暴露其序列化和反序列化服务。对于几乎所有数据类型，这些服务的默认行为就足够了，这意味着你几乎不需要为自己编写序列化工作。然而，有极少数类型的序列化服务默认行为是不够的。幸运的是，序列化服务具有很扩展性，我还会解释如何利用这些扩展机制，允许你在序列化或反序列化对象时执行一些强大的操作。例如，我将演示如何将版本 1 对象序列化到磁盘文件，然后在一年后将其反序列化为版本 2 对象。

> 注意：本章关注公共语言运行时 (`CLR`) 中的序列化技术，它对 `CLR` 类型有深入理解，可以将对象的所有公共、受保护、内部甚至私有字段序列化为压缩的二进制流以实现高性能。如果你希望序列化为 `XML`，请使用 `System.Runtime.Serialization.DataContractSerializer`。`.NET Framework` 还提供了其他设计用于 `CLR` 类型与非 `CLR` 数据类型之间操作的序列化技术。这些其他序列化技术使用了 `System.Xml.Serialization.XmlSerializer` 类和 `System.Runtime.Serialization.DataContractSerializer` 类。

### 序列化/反序列化快速上手

让我们先来看代码：

```assembly
using System;
using System.Collections.Generic;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
internal static class QuickStart {
    public static void Main() {
        // 创建对象图并将其序列化到流中
        var objectGraph = new List<string> { "Jeff", "Kristin", "Aidan", "Grant" };
        Stream stream = SerializeToMemory(objectGraph);
        // 重置此演示的所有内容
        stream.Position = 0;
        objectGraph = null;
        // 反序列化对象并证明其有效
        objectGraph = (List<string>) DeserializeFromMemory(stream);
        foreach (var s in objectGraph) Console.WriteLine(s);
    }
    private static MemoryStream SerializeToMemory(object objectGraph) {
        // 构建一个用于序列化对象的流
        MemoryStream stream = new MemoryStream();
        // 构建一个完成所有繁重工作的格式化程序
        BinaryFormatter formatter = new BinaryFormatter();
        // 告诉格式化程序将对象序列化到流
        formatter.Serialize(stream, objectGraph);
        // 将序列化对象的流返回给调用者
        return stream;
    }
    private static Object DeserializeFromMemory(Stream stream) {
        // 构建一个完成所有工作的格式化程序
        BinaryFormatter formatter = new BinaryFormatter();
        // 告诉格式化程序从流中反序列化对象
        return formatter.Deserialize(stream);
    }
}
```

```sharp
// 构建一个执行所有复杂工作的序列化格式器
BinaryFormatter formatter = new BinaryFormatter();
// 这一行在本章的“流上下文”部分中会有解释
formatter.Context = new StreamingContext(StreamingStates.Clone);
// 将对象图序列化到内存流中
formatter.Serialize(stream, original);
// 在反序列化之前，将内存流移回开头
stream.Position = 0;
// 将图反序列化为一组新对象，并
// 由调用者返回图的根节点（深拷贝）
return formatter.Deserialize(stream);
```

在此处，我想对我们的讨论增加几点说明。首先，需要由你来确保你的代码在序列化和反序列化时使用相同的格式器。例如，不要编写先使用 `SoapFormatter` 序列化对象图，然后使用 `BinaryFormatter` 反序列化该图的代码。如果 `Deserialize` 无法解析流的内容，将抛出 `System.Runtime.Serialization.SerializationException`。

我想指出的第二点是，将多个对象图序列化到单个流中是可行的，而且非常有用。例如，假设我们有以下类定义：

```sharp
[Serializable] internal sealed class Customer { /* ... */ }
[Serializable] internal sealed class Order { /* ... */ }
```

然后，在我们的应用程序类中，我们定义了以下静态字段：

```sharp
private static List<Customer> s_customers = new List<Customer>();
private static List<Order> s_pendingOrders = new List<Order>();
private static List<Order> s_processedOrders = new List<Order>();
```

现在，我们可以使用如下所示的方法将应用程序的状态序列化到流中：

```sharp
private static void SaveApplicationState(Stream stream) {
    // 构建一个执行所有复杂工作的序列化格式器
    BinaryFormatter formatter = new BinaryFormatter();
```

```csharp
    // 序列化应用程序的整个状态
    formatter.Serialize(stream, s_customers);
    formatter.Serialize(stream, s_pendingOrders);
    formatter.Serialize(stream, s_processedOrders);
}
```

### 第四部分 核心设施

为了重建我们应用程序的状态，我们将使用如下方法反序列化状态：

```csharp
private static void RestoreApplicationState(Stream stream) {
    // 构建一个执行所有复杂工作的序列化格式器
    BinaryFormatter formatter = new BinaryFormatter();
    // 反序列化应用程序的整个状态（与序列化时的顺序一致）
    s_customers = (List<Customer>) formatter.Deserialize(stream);
    s_pendingOrders = (List<Order>) formatter.Deserialize(stream);
    s_processedOrders = (List<Order>) formatter.Deserialize(stream);
}
```

我想指出的第三点也是最后一点与程序集有关。在序列化对象时，类型的名称以及定义该类型的程序集名称会被写入流中。`BinaryFormatter` 输出程序集的完整身份，这包含了程序集的文件名（不含扩展名）、版本号、文化信息和公钥信息。在反序列化对象时，格式器首先获取程序集身份，并通过调用 `System.Reflection.Assembly.Load` 方法（在第23章“程序集加载与反射”中讨论过）确保该程序集已加载到执行 `AppDomain` 中。

程序集加载后，格式器会在程序集中查找与对象匹配的类型。如果对象不包含匹配的类型，将抛出异常且无法反序列化任何对象。如果找到匹配的类型，将创建一个该类型的实例并用流中的值初始化其字段。然后将抛出 `SerializationException` 且没有更多对象可以被反序列化。在本章后面的部分，我将展示一些允许你覆盖此行为的复杂机制。

- **重要**：某些应用程序使用 `Assembly.Load` 来加载程序集，并从加载的程序集中定义的类型构造对象。这些对象可以顺利地序列化到流中。然而，在反序列化此流时，格式器尝试尝试调用 `Assembly.Load` 方法而不是 `LoadFrom` 方法来加载程序集。在大多数情况下，`CLR` 将无法找到程序集文件，导致抛出 `SerializationException`。这让许多开发者感到意外：既然对象可以序列化，他们期望它们能够正确反序列化。

如果你的应用程序使用了通过 `Assembly.Load` 加载的程序集中定义的类型，我建议你实现一个签名与 `System.EventHandler` 委托匹配的方法，并在调用格式器的 `Deserialize` 方法之前，通过 `System.AppDomain.Resolve` 注册该方法。在事件 `Deserialize` 运行后注销该方法。现在，当格式器加载程序集失败时，`CLR` 会调用你的 `EventHandler` 方法。该方法将接收到加载失败程序集的身份。方法可以从程序集的身份中提取程序集文件名，并使用该名称构建应用程序已知可以找到程序集文件的路径。然后，方法可以使用 `Assembly.Load` 加载程序集，并将生成的 `Assembly` 引用从 `ResolveEventHandler` 方法返回。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_683_0.png)

### 第24 章 运行时序列化 667

本节介绍了如何序列化和反序列化对象图的基础知识。在剩余章节中，我们将查看为了定义自己的可序列化类型必须执行的操作，并查看允许你对序列化和反序列化进行各种机制。

#### 使类型可序列化

在设计类型时，开发者必须有意识地决定是否允许类型实例被序列化。默认情况下，类型是不可序列化的。例如，以下代码无法执行：

```csharp
internal struct Point { public Int32 x, y; };
private static void OptSerialization() {
    Point pt = new Point { x = 1, y = 2 };
    using (var stream = new MemoryStream()) {
        new BinaryFormatter().Serialize(stream, pt); // 抛出 SerializationException
    }
}
```

如果你在程序中构建并运行此代码，你会发现格式器的 `Serialize` 方法抛出了 `System.Runtime.Serialization.SerializationException`。问题在于 `Point` 开发者没有指示 `Point` 对象是可以序列化的。为了解决这个问题，开发者必须如下所示对该类型应用 `System.SerializableAttribute` 标记。（注意该标记定义在 `System` 命名空间，而不是 `System.Runtime.Serialization` 命名空间。）

```csharp
[Serializable]
internal struct Point { public Int32 x, y; };
```

现在，如果我们重新编译并运行应用程序，它按预期运行，`Point` 对象将序列化到流中。在序列化对象图时，格式器会检查每个对象是否可序列化。如果图中的任何对象不可序列化，格式器的 `Serialize` 方法将抛出 `SerializationException` 异常。

> 注意：序列化对象图时，某些对象的类型可能是可序列化的，而某些对象可能不可序列化。出于性能考虑，格式器在序列化图之前不会验证图中的所有对象都可序列化。因此，在序列化对象图时，可能在抛出 `SerializationException` 之前，某些对象已经序列化到流中。如果是这样，流包含了损坏的数据。如果你认为你可能会序列化某些对象不可序列化的对象图，你的应用程序代码应该能够从这种情况优雅地恢复。一种方案是将对象序列化到 `MemoryStream`。然后，如果所有对象都成功序列化，你就可以将字节复制到任何你真正需要的流中（例如文件、网络）。

### 第四部分 核心设施

`SerializableAttribute` 自定义属性只能应用于引用类型（`class`）、值类型（`struct`）、枚举类型（`enum`）和委托类型（`delegate`）。

（注意，枚举类型和委托类型始终是可序列化的；不需要对这些类型显式地应用 `SerializableAttribute` 属性。）此外，`SerializableAttribute` 属性不会被派生类型继承，因此，给定以下两个定义，一个 `Person` 对象可以被 `Employee` 对象序列化：

```csharp
[Serializable]
internal class Person { ... }
```

```csharp
internal class Employee : Person { ... }
```

要修复这个问题，你只需要对 `Employee` 类型也应用 `SerializableAttribute` 属性即可：

```csharp
[Serializable]
internal class Person { ... }
```

```csharp
[Serializable]
internal class Employee : Person { ... }
```
