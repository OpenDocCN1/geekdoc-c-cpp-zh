

# 序列化/反序列化快速上手

让我们先看一些代码。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;

internal static class QuickStart {
    public static void Main() {
        // 创建对象图并序列化到流中
        var objectGraph = new List<String> { "Jeff", "Kristin", "Aidan", "Grant" };
        Stream stream = SerializeToMemory(objectGraph);

        // 为此演示重置所有内容
        stream.Position = 0;
        objectGraph = null;

        // 反序列化对象并证明其有效
        objectGraph = (List<String>)DeserializeFromMemory(stream);
        foreach (var s in objectGraph) Console.WriteLine(s);
    }

    private static MemoryStream SerializeToMemory(Object objectGraph) {
        // 构建一个用于存放序列化对象的流
        MemoryStream stream = new MemoryStream();

        // 构建一个执行所有核心工作的序列化格式器
        BinaryFormatter formatter = new BinaryFormatter();

        // 通知格式器将对象序列化到流中
        formatter.Serialize(stream, objectGraph);

        // 将序列化对象的流返回给调用者
        return stream;
    }

    private static Object DeserialFromMemory(Stream stream) {
        // 构建一个执行所有核心工作的序列化格式器
        BinaryFormatter formatter = new BinaryFormatter();

        // 通知格式器从流中反序列化对象
        return formatter.Deserialize(stream);
    }
}
```

哇，看这有多简单！`SerializeToMemory` 方法构建了一个 `System.MemoryStream` 对象来标识要存放的序列化字节块。然后该方法构建了一个 `BinaryFormatter` 对象（可以在 `System.Runtime.Serialization.Binary` 命名空间中找到）。格式器是一种知道如何序列化和反序列化对象的类型。框架类库（FCL）提供了 `System.Runtime.Serialization.Formatter` 接口，并包含两个格式器：`BinaryFormatter`（在此代码示例中使用）和 `SoapFormatter`（可以在 `System.Runtime.Serialization.Formatters.Soap` 命名空间中找到，并实现在 `System.Runtime.Serialization.Formatters.Soap.dll` 程序集中）。

> 自 .NET Framework 3.5 版本起，`SoapFormatter` 类已过时，不应在生产代码中使用。然而，它对于调试序列化代码可能很有用，因为它产生的是你可以读取的 XML 文本。若要在生产代码中使用 XML 序列化和反序列化，请参阅 `XmlSerializer` 和 `DataContractSerializer` 类。

要序列化对象图，只需调用格式器的 `Serialize` 方法并传递两个内容：指向流对象的引用以及指向想要序列化的对象图的引用。流标识了序列化字节应该放置的位置，它可以是任何派自 `System.IO.Stream` 抽象类的类型对象。这意味着你可以将对象图序列化到 `MemoryStream`、`FileStream`、`NetworkStream` 等。

`Serialize` 的第二个参数是对一个对象的引用。该对象可以是任何类型：`Int32`、`String`、`DateTime`、`Exception`、`List<String>`、`Dictionary<Int32, DateTime>` 等。`objectGraph` 参数引用的对象可能会引用其他对象。例如，`objectGraph` 可能引用一个包含一组对象的集合。这些对象可能再次引用其他对象。当调用格式器的 `Serialize` 方法时，图中的所有对象都会被序列化到流中。

格式器通过引用描述每个对象类型的元数据，知道如何序列化整个图表。`Serialize` 方法使用反射来查看每个对象类型中的哪些实例字段被序列化。如果这些字段中的任何一个引用其他对象，那么格式器的 `Serialize` 方法也知道如何序列化这些对象。

格式器拥有非常智能的算法。它们知道图中的每个对象到流的序列化次数不会超过一次。也就是说，如果图中的两个对象相互引用，格式器会检测到这一点，对每个对象序列化一次，并避免进入无限循环。

在我的 `SerializeToMemory` 方法中，当格式器的 `Serialize` 方法返回时，`MemoryStream` 直接被返回给调用者。应用程序使用它需要的扁平化字节数组。例如，它可以将其保存到文件、复制到剪贴板、通过网络发送或进行任何其他操作。

![](img/0ce3b788d061e3d3095fa554b1a34adf_639_0.png)

`DeserializeFromStream` 方法将流反序列化回对象图。在此代码中，构建了 `BinaryFormatter` 然后调用了它的 `Deserialize` 方法。该方法接受流作为参数，并返回反序列化对象图内根对象的引用。

在内部，格式器的 `Deserialize` 方法检查流的内容，构建流中所有对象的实例，并初始化这些对象中的字段，以便它们的值与对象图序列化时的值相同。通常，你将从 `Deserialize` 方法返回的对象引用转换为你的应用程序所预期的类型。

![](img/0ce3b788d061e3d3095fa554b1a34adf_640_0.png)

> **注意**：这里有一个使用序列化对对象进行深拷贝或克隆的有用方法。

```csharp
private static object DeepClone(Object original) {
    // 构建一个临时内存流
    using (MemoryStream stream = new MemoryStream()) {
        // 构建一个执行所有核心工作的序列化格式器
        BinaryFormatter formatter = new BinaryFormatter();

        // 这一行将在本章中解释
        // 将对象图序列化到流中
        formatter.Serialize(stream, original);

        // 回到内存流的开头
        stream.Position = 0;

        // 将图（深拷贝）返回给调用者
        return formatter.Deserialize(stream);
    }
}
```

到这里，我想为我们的讨论增加几点注释。首先，确保你的代码在序列化和反序列化时使用相同的格式器取决于你。例如，假设我们有以下类定义。

```csharp
[Serializable] internal class Customer { /* ... }
[Serializable] internal class Order { /* ... }
```

第 24 章 运行时序列化 615

然后，在应用程序的主类中，我们定义了静态字段。

```csharp
private static List<Customer> s_customers = new List<Customer>();
private static List<Order> s_pendingOrders = new List<Order>();
private static List<Order> s_processedOrders = new List<Order>();
```

现在，可以使用如下所示的方法将应用程序状态序列化到单个流。

```csharp
private static void SaveApplicationState(Stream stream) {
    // 构建一个执行所有核心工作的序列化格式器
    BinaryFormatter formatter = new BinaryFormatter();

    // 序列化整个应用程序状态
    formatter.Serialize(stream, s_customers);
    formatter.Serialize(stream, s_pendingOrders);
    formatter.Serialize(stream, s_processedOrders);
}
```

为了重建应用程序状态，我们将使用如下所示的方法反序列化状态：

```csharp
private static void RestoreApplicationState(Stream stream) {
    // 构建一个执行所有核心工作的序列化格式器
    BinaryFormatter formatter = new BinaryFormatter();

    // 反序列化整个应用程序状态（与反序列化顺序一致）
    s_customers = (List<Customer>)formatter.Deserialize(stream);
    s_pendingOrders = (List<Order>)formatter.Deserialize(stream);
    s_processedOrders = (List<Order>)formatter.Deserialize(stream);
}
```

最后，我想指出如何处理程序集。在序列化对象时，类型的全名和定义该类型的程序集名称会被写入流。`BinaryFormatter` 输出程序集的完整身份，包括程序集的文件（不带扩展名）、版本号、文化和公密钥信息。在反序列化对象时，格式器首先获取程序集身份并确保将其加载到执行应用程序的 `Assembly.Load` 方法中（在第 23 章“程序集加载与反射”中讨论）。

在加载程序集后，格式器在程序集中查找匹配的类型，如果程序集不包含匹配类型，则抛出异常，且无法继续反序列化。如果找到了匹配类型，则会创建该类型的实例并根据流中包含的值对其字段进行初始化。如果类型字段与从流中读取的字段名称完全匹配，将抛出 `SerializationException` 且无法继续反序列化。在本章的后半部分，我将讨论一些允许你覆盖部分行为的高级机制。

