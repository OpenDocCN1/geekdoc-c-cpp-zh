
```csharp
        // Reset everything for this demo
        stream.Position = 0;
        objectGraph = null;

        // Deserialize the objects and prove it worked
        objectGraph = (List<String>) DeserializeFromMemory(stream);
        foreach (var s in objectGraph) Console.WriteLine(s);
    }

    private static MemoryStream SerializeToMemory(Object objectGraph) {
        // Construct a stream that is to hold the serialized objects
        MemoryStream stream = new MemoryStream();

        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to serialize the objects into the stream
        formatter.Serialize(stream, objectGraph);

        // Return the stream of serialized objects back to the caller
        return stream;
    }

    private static Object DeserializeFromMemory(Stream stream) {
        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to deserialize the objects from the stream
        return formatter.Deserialize(stream);
    }
}
```

哇，看看这有多简单！**SerializeToMemory** 方法构造了一个 **System.IO.MemoryStream** 对象。该对象标识序列化字节块应放置的位置。然后，该方法构造一个 **BinaryFormatter** 对象（可在 **System.Runtime.Serialization.Formatters.Binary** 命名空间中找到）。格式化器是一种类型（实现 **System.Runtime.Serialization.IFormatter** 接口），它知道如何序列化和反序列化对象图。框架类库（FCL）附带两个格式化器：**BinaryFormatter**（本代码示例中使用）和 **SoapFormatter**（可在 **System.Runtime.Serialization.Formatters.Soap** 命名空间中找到，并在 System.Runtime.Serialization.Formatters.Soap.dll 程序集中实现）。

> **注意** 从 .NET Framework 3.5 版开始，**SoapFormatter** 类已过时，不应在生产代码中使用。不过，它对于调试序列化代码仍然有用，因为它会生成可读的 XML 文本。若要在生产代码中使用 XML 序列化和反序列化，请参见 **XmlSerializer** 和 **DataContractSerializer** 类。

要序列化对象图，只需调用格式化器的 **Serialize** 方法，并向其传递两项内容：对流对象的引用，以及对你希望序列化的对象图的引用。流对象标识序列化字节应放置的位置，并且可以是派生自 **System.IO.Stream** 抽象基类的任何类型的对象。这意味着你可以将对象图序列化到 **MemoryStream**、**FileStream**、**NetworkStream** 等。

**Serialize** 的第二个参数是对对象的引用。该对象可以是任何东西：**Int32**、**String**、**DateTime**、**Exception**、**List<String>**、**Dictionary<Int32, DateTime>** 等等。**objectGraph** 参数所引用的对象可以引用其他对象。例如，**objectGraph** 可以引用一个集合，而该集合又引用一组对象。这些对象还可以引用其他对象。当调用格式化器的 **Serialize** 方法时，图中的所有对象都会被序列化到流中。

格式化器通过引用描述每个对象类型的元数据，知道如何序列化完整的对象图。**Serialize** 方法在序列化每个对象时，使用反射查看该对象类型中的实例字段。如果这些字段中的任何一个引用了其他对象，那么格式化器的 **Serialize** 方法知道也要序列化这些对象。

格式化器具有非常智能的算法。它们知道将图中的每个对象最多一次地序列化到流中。也就是说，如果图中的两个对象相互引用，那么格式化器会检测到这一点，只将每个对象序列化一次，并避免进入无限循环。

在我的 **SerializeToMemory** 方法中，当格式化器的 **Serialize** 方法返回时，**MemoryStream** 被直接返回给调用方。应用程序可以按任意方式使用这个扁平字节数组的内容。例如，它可以将其保存到文件中、复制到剪贴板、通过网络发送，等等。

**DeserializeFromMemory** 方法将流反序列化回对象图。这个方法比序列化对象图还要简单。在这段代码中，构造一个 **BinaryFormatter**，然后调用其 **Deserialize** 方法。该方法将流作为参数，并返回对反序列化对象图中根对象的引用。

在内部，格式化器的 **Deserialize** 方法检查流的内容，构造流中所有对象的实例，并初始化所有这些对象中的字段，使它们具有与对象图序列化时相同的值。通常，你会将 **Deserialize** 方法返回的对象引用强制转换为应用程序所期望的类型。

> **注意** 下面是一个有趣且有用的方法，它使用序列化来制作对象的深拷贝（或克隆）：

```csharp
private static Object DeepClone(Object original) {
    // Construct a temporary memory stream
    using (MemoryStream stream = new MemoryStream()) {
        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // This line is explained in this chapter's "Streaming Contexts" section
        formatter.Context = new StreamingContext(StreamingContextStates.Clone);

        // Serialize the object graph into the memory stream
        formatter.Serialize(stream, original);

        // Seek back to the start of the memory stream before deserializing
        stream.Position = 0;

        // Deserialize the graph into a new set of objects and
        // return the root of the graph (deep copy) to the caller
        return formatter.Deserialize(stream);
    }
}
```

![](img/3c46ff5b170881db4209d365b1f7a808_681_0.png)

至此，我想在讨论中补充几点说明。首先，你需要确保代码在序列化和反序列化时使用相同的格式化器。例如，不要编写这样的代码：使用 **SoapFormatter** 序列化对象图，然后使用 **BinaryFormatter** 反序列化该图。如果 **Deserialize** 无法解读流的内容，则会引发 **System.Runtime.Serialization.SerializationException** 异常。

我想指出的第二点是，将多个对象图序列化到单个流中是可行的，而且也非常有用。例如，假设我们有以下两个类定义：

```csharp
[Serializable] internal sealed class Customer { /* ... */ }
[Serializable] internal sealed class Order { /* ... */ }
```

然后，在应用程序的主类中，我们定义以下静态字段：

```csharp
private static List<Customer> s_customers       = new List<Customer>();
private static List<Order>    s_pendingOrders   = new List<Order>();
private static List<Order>    s_processedOrders = new List<Order>();
```

现在，我们可以使用如下所示的方法将应用程序的状态序列化到单个流中：

```csharp
private static void SaveApplicationState(Stream stream) {
    // Construct a serialization formatter that does all the hard work
    BinaryFormatter formatter = new BinaryFormatter();

    // Serialize our application's entire state
    formatter.Serialize(stream, s_customers);
    formatter.Serialize(stream, s_pendingOrders);
    formatter.Serialize(stream, s_processedOrders);
}
```

要重建应用程序的状态，我们将使用如下所示的方法反序列化该状态：

```csharp
private static void RestoreApplicationState(Stream stream) {
    // Construct a serialization formatter that does all the hard work
    BinaryFormatter formatter = new BinaryFormatter();

    // Deserialize our application's entire state (same order as serialized)
    s_customers      = (List<Customer>) formatter.Deserialize(stream);
    s_pendingOrders  = (List<Order>)    formatter.Deserialize(stream);
    s_processedOrders = (List<Order>)   formatter.Deserialize(stream);
}
```

我想指出的第三点也是最后一点，与程序集有关。序列化对象时，类型的完整名称和该类型所在程序集的名称会被写入流中。默认情况下，**BinaryFormatter** 输出程序集的完整标识，其中包括程序集文件名（不带扩展名）、版本号、区域性和公钥信息。反序列化对象时，格式化器首先获取程序集标识，并通过调用 **System.Reflection.Assembly's Load** 方法（在第 23 章“程序集加载与反射”中讨论）确保程序集已加载到正在执行的 AppDomain 中。

程序集加载后，格式化器会在该程序集中查找与正在反序列化的对象匹配的类型。如果程序集不包含匹配的类型，则会引发异常，并且无法再反序列化更多对象。如果找到匹配的类型，则创建该类型的实例，并根据流中包含的值初始化其字段。如果该类型的字段与从流中读取的字段名称不完全匹配，则会引发 **SerializationException** 异常，并且无法再反序列化更多对象。在本章后面，我将讨论一些复杂的机制，它们允许你重写其中某些行为。

![](img/3c46ff5b170881db4209d365b1f7a808_683_0.png)

> **重要** 一些可扩展应用程序使用 **Assembly.LoadFrom** 加载程序集，然后从已加载程序集中定义的类型构造对象。这些对象可以顺利序列化到流中。但是，在反序列化此流时，格式化器会尝试通过调用 **Assembly's Load** 方法（而不是调用 **LoadFrom** 方法）来加载程序集。在大多数情况下，CLR 将无法定位程序集文件，从而导致引发 **SerializationException** 异常。这令许多开发人员感到意外：既然对象已正确序列化，他们期望它们也能正确反序列化。
>
> 如果你的应用程序序列化的对象，其类型定义在应用程序使用 **Assembly.LoadFrom** 加载的程序集中，那么我建议你实现一个签名与 **System.ResolveEventHandler** 委托匹配的方法，并在调用格式化器的 **Deserialize** 方法之前，将此方法注册到 **System.AppDomain's AssemblyResolve** 事件。（在 **Deserialize** 返回后，从该事件中注销此方法。）这样，每当格式化器无法加载程序集时，CLR 就会调用你的 **ResolveEventHandler** 方法。该方法会接收加载失败的程序集的标识。该方法可以从程序集标识中提取程序集文件名，并使用此名称构造应用程序已知可找到程序集文件的路径。然后，该方法可以调用 **Assembly.LoadFrom** 加载程序集，并从 **ResolveEventHandler** 方法返回得到的 **Assembly** 引用。

