
```csharp
public interface ISerializationSurrogate
    void GetObjectData(Object obj, SerializationInfo info, StreamingContext context);

    void SetObjectData(Object obj, SerializationInfo info, StreamingContext context, ISurrogateSelector selector);
```

现在，让我们来看一个使用此接口的示例。假设你的程序包含本地于用户计算机的 `DateTime` 对象。如果你想将 `DateTime` 对象序列化到流中，但希望值以通用时间（universal time）进行序列化呢？这将允许你将数据通过网络发送到世界另一部分的机器上，并确保 `DateTime` 值是正确的。虽然你无法修改 FCL 中的 `DateTime` 类型，但你可以定义自己的代理类，来控制 `DateTime` 对象的序列化和反序列化。以下是定义该代理类的方法。

```csharp
internal sealed class UniversalLocalSerializationSurrogate : ISerializationSurrogate
{
    public void GetObjectData(Object obj, SerializationInfo info, StreamingContext context)
    {
        // 将“日期”转换为 UTC
        info.AddValue("Date", ((DateTime)obj).ToUniversalTime().ToString());
    }

    public void SetObjectData(Object obj, SerializationInfo info, StreamingContext context, ISurrogateSelector selector)
    {
        // 将 DateTime 从 UTC 转换为本地
        return DateTime.ParseExact(info.GetString("Date"), "u", null).ToLocalTime();
    }
}
```

`GetObjectData` 方法的工作方式与 `ISerializable` 接口的 `GetObjectData` 方法相同。唯一的区别是 `ISerializationSurrogate` 的 `GetDataObject` 方法多了一个额外参数：指向要序列化的“真实”对象的引用。在上面的 `GetObjectData` 方法中，该对象被强制转换为 `DateTime`，值从本地时间转换为通用时间，并将一个字符串（使用通用日期/时间格式格式化）添加到 `SerializationInfo` 集合中。

`SetDataObject` 方法在反序列化 `DateTime` 对象时被调用。当调用此方法时，会传递一个 `SerializationInfo` 对象的引用。`SetObjectData` 从集合中提取出字符串，将其解析为完整的日期/时间格式字符串，然后将生成的 `DateTime` 对象从通用时间转换为机器的本地时间。

传递给 `SetDataObject` 第一个参数的对象是一个位字符串。在调用 `SetDataObject` 之前，格式化器（通过格式化器的静态方法 `GetUninitializedObject`）会找到代理所代表的实例。该实例的字段全为空/null，且没有对该对象调用构造函数。`SetDataObject` 内部的代码可以简单地使用传入的 `SerializationInfo` 对象的值初始化此实例的字段，然后返回 `null`。或者，`SetDataObject` 也可以创建一个完全不同的对象甚至不同类型的对象，并返回该对象的引用，在这种情况下，格式化器将忽略传递给 `SetDataObject` 的对象可能发生或未发生的任何更改。

在我的示例中，`myUniversalLocalSerializationSurrogate` 类作为 `DateTime` 类型的代理，`DateTime` 是一个值类型。因此，`obj` 参数指向 `DateTime` 的装箱实例。在大多数值类型中，无法更改字段（因为它们应该是不可变的），因此我的 `SetDataObject` 方法忽略了该对象，并返回一个包含所需值的新 `DateTime` 对象。

此时，我确定你正在想格式化器是如何在尝试序列化/反序列化 `DateTime` 对象时使用此 `ISerializationSurrogate` 类型的下面的代码演示了如何使用 `UniversalLocalSerializationSurrogate` 类。

```csharp
private static void SerializationSurrogateDemo() {
    using (var stream = new MemoryStream()) {
        // 1. 构建所需的格式化器
        IFormatter formatter = new SoapFormatter();

        // 2. 构建一个 SurrogateSelector 对象
        SurrogateSelector ss = new SurrogateSelector();

        // 3. 告诉代理选择器对 DateTime 对象使用我们的代理
        ss.AddSurrogate(typeof(DateTime), formatter.Context, new UniversalLocalSerializationSurrogate());

        // 注意：AddSurrogate 可以被多次调用以注册多个代理

        // 4. 告诉格式化器使用我们的代理选择器
        formatter.SurrogateSelector = ss;
    }
}
```

```csharp
// 创建一个表示机器本地时间的 DateTime 并序列化它
TimeToBeforeSerialize = DateTime.Now;
formatter.Serialize(stream, localTimeBeforeSerialize);

// 流以字符串形式显示通用时间以证明工作正常
stream.Position = 0;
Console.WriteLine(new StreamReader(stream).ReadToEnd());

// 反序列化通用时间字符串并转换为本地 DateTime
localTimeAfterDeserialize = (DateTime)formatter.Deserialize(stream);
```

```csharp
// 证明工作正常：
Console.WriteLine("LocalTimeBeforeSerialize={0}", localTimeBeforeSerialize);
Console.WriteLine("LocalTimeAfterDeserialize={0}", localTimeAfterDeserialize);
```

执行完步骤 1 到 4 后，格式化器已准备好使用已注册的代理类型。当调用格式化器的 `Serialize` 方法时，会在 `SurrogateSelector` 维护的集合中查找每个对象。如果找到匹配，将调用 `ISerializationSurrogate` 对象的 `GetDataObject` 以获取应写入流的信息。

当调用格式化器的 `Deserialize` 方法时，会在格式化器的 `SurrogateSelector` 中查找要反序列化的对象类型，如果找到匹配，将调用 `ISerializationSurrogate` 对象的 `SetDataObject` 来设置反序列化对象内部的字段。

内部，`SurrogateSelector` 维护了一个私有哈希表。当调用 `AddSurrogate` 时，`Type` 和 `StreamingContext` 组成键，`ISerializationSurrogate` 对象是值。如果已存在相同 `Type/StreamingContext` 的键，`AddSurrogate` 将抛出 `ArgumentException`。通过将 `StreamingContext` 包含在键中，你可以注册一个知道将 `DateTime` 对象序列化/反序列化到文件的代理类型，并注册另一个知道如何将 `DateTime` 对象序列化/反序列化到不同进程的代理对象。

> `BinaryFormatter` 类有一个 bug，会导致代理无法序列化相互引用的对象。要修复这个问题，你需要将你的 `ISerializationSurrogate` 对象引用传递给 `FormServices` 的静态方法 `GetSurrogateForCyclicalReference`。该方法返回一个 `ISerializationSurrogate` 对象，你可以将其传递给 `SurrogateSelector` 的 `AddSurrogateReference` 方法，但是你的代理的 `SetDataObject` 必须修改调用方法 `SetDataObject obj` 所引用对象内部的值。随书提供的下载代码展示了如何修改 `UniversalTimeToSerialization` 类和 `SerializationSurrogateDemo` 方法以支持循环引用。

## 代理选择器链 SurrogateSelector

多个 `SurrogateSelector` 对象可以链在一起。例如，你可以有一个 `SurrogateSelector`，它维护一组序列化代理，这些代理用于将类型序列化为代理，这些代理可以在跨网络或跨应用程序域（AppDomains）之间进行装载。你还可以拥有一个 `SurrogateSelector` 对象，它包含一组序列化代理，用于将 Version 1 类型转换为 Version 2 类型。

如果你有多个希望让格式化程序使用的 `SurrogateSelector` 对象，你必须将它们链成一个链链表。`SurrogateSelector` 类型实现了 `ISurrogateSelector` 接口，该接口定义了三个方法。这三个方法都与链式操作有关。以下是 `ISurrogateSelector` 的定义。

```java
public interface ISurrogateSelector {
    void Chain(ISurrogateSelector selector);
    ISurrogateSelector GetNextSelector();
    ISerializationSurrogate GetSurrogate(Type type, StreamingContext context,
        out ISurrogateSelector selector);
}
```

`Chain` 方法在当前操作的 `SurrogateSelector` 对象（即此对象）之后插入一个 `ISurrogateSelector` 对象。`GetNextSelector` 方法返回链中下一个 `ISurrogateSelector` 的引用，如果操作的是链的末尾，则返回 null。

`GetSurrogate` 方法在由当前标识的 `SurrogateSelector` 对象中查找 `Type/StreamingContext` 对。如果找不到该对，则访问链中的下一个 `SurrogateSelector` 对象，依此类推。如果找到匹配项，`GetSurrogate` 将返回处理所查找类型序列化/反序列化的 `ISerializationSurrogate` 对象。此外，`GetSurrogate` 还会返回包含匹配项的 `SurrogateSelector` 对象；这通常是需要的但会被忽略。如果链中没有任何 `SurrogateSelector` 对象与该 `Type/StreamingContext` 对有匹配项，则 `GetSurrogate` 返回 null。

> 注意：FCL 定义了一个 `ISurrogateSelector` 接口，以及一个实现该接口的 `SurrogateSelector` 类型。然而，极少有人需要定义自己的实现该接口的类型。定义实现该接口的自定义类型的唯一理由是因为你需要在将一个类型映射到另一个类型时具有更高的灵活性。例如，你可能想以特殊方式序列化所有继承自特定基类的的类型。`System.Remoting.Messaging.RemotingSurrogateSelector` 类就是一个完美的例子。在为了移除目的而序列化对象时，CLR 使用 `RemotingSurrogateSelector` 格式化对象。该代理选择器以特殊方式序列化所有派自 `System.MarshalByRefObject` 的对象，以便反序列化在客户端侧创建代理对象。

![](img/0ce3b788d061e3d3095fa554b1a34adf_664_0.png)

第24章 运行时序列化 639

# 在反序列化对象时覆盖程序集和类型类型

在序列化对象时，格式化程序输出类型的全名以及定义该类型的程序集的全名。在反序列化对象时，格式化程序使用这些信息来确切知道构造和初始化什么类型的对象。之前关于 Deserialization-Surrogate 接口的讨论了一种允许你接管特定类型序列化和反序列化职责的机制。实现 `ISerializationSurrogate` 接口的类型绑定到特定程序集的特定类型。

然而，有时 `ISerializationSurrogate` 机制没有提供足够的灵活性。在以下场景下，将对象反序列化为与序列化时不同的类型可能是很有用的：

- 开发者可能决定将类型的实现从一个程序集移动到另一个程序集。例如，程序集的版本发生了导致新程序集与原始程序集有所不同。

- 服务器上的对象被序列化为流并发送到客户端。当客户端非常容易地处理该流时，它可以将对象反序列化为完全不同的类型，该类型的代码知道如何远程调用服务器对象的方法。

- 开发者为某个类型创建了新版本。我们将任何已序列化的对象反序列化为该类型的新版本。

`System.Runtime.Serialization.SerializationBinder` 类使得将对象反序列化为不同类型变得非常简单。要做到这一点，首先定义派自抽象 `SerializationBinder` 类型的自定义类型。在下面的代码中，假设你的程序集版本1.0.0.0 定义了一个名为 `Ver1` 的类，而你的程序集的新版本定义了 `Ver1ToVer2SerializationBinder` 类并定义了 `Ver2` 类。

```csharp
internal sealed class Ver1ToVer2SerializationBinder : SerializationBinder {
    public override Type BindTo(string assemblyName, string typeName) {
        // 将版本 1.0.0.0 的任何 Ver1 对象反序列化为 Ver2 对象

        // 计算定义 Ver1 类型的程序集
        assemVer1 = Assembly.ExecutingAssembly().GetName();
        assemVer1.Version = new Version(1, 0, 0, 0);

        // 如果从 v1.0.0.0 反序列化 Ver1 对象，将其转换为 Ver2 对象
        if (assemblyName == assemVer1.ToString() && typeName == "Ver1") return typeof(Ver2);

        // 否则，直接返回请求的相同类型
        return Type.GetType(String.Format("{0}, {1}", typeName, assemblyName));
    }
}
```

现在，在构造了格式化程序后，构造 `Ver1ToVer2SerializationBinder` 的实例，并将格式化程序的 `Binder` 读写属性指向该绑定对象。在设置 `Binder` 属性后，你现在可以调用格式化程序的 `Deserialize` 方法。在反序列化期间，格式化程序看到已设置了绑定。当每个对象即将被反序列化时，格式化程序调用绑器的 `BindTo` 方法，传递格式化程序想要反序列化的程序集名称和类型。此时，`BindToType` 决定了实际上应该构造什么类型并返回该类型。

> 注意：`SerializationBinder` 类还允许通过覆盖其 `BindToName` 方法在序列化对象时更改程序集/类型信息，该方法如下。

```csharp
public virtual void BindToName(Type serializedType,
    out string assemblyName, out string typeName)
```

在序列化期间，格式化程序调用此方法并传递它想要序列化的类型。然后你就可以（通过两个 out 参数）返回你想要序列化的程序集和类型。如果你返回 null 和 null（这是默认实现的操作），则不执行任何更改。

## 第25章

## 与 WinRT 组件的互操作

本章内容：

- CLR 投影与 WinRT 组件类型系统规则 .. 645

- 框架投影 ............................................................ 649

- 在 C# 中定义 WinRT 组件 ................................................... 658
