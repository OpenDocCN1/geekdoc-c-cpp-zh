
此示例定义了 `CONDITION_A`，因此 `MethodA()` 正常执行。`CONDITION_B` 则既未通过 `#define` 定义，也未使用 `csc.exe /Define` 选项定义。因此，来自此程序集内部对 `Program.MethodB()` 的所有调用都将不执行任何操作。

在功能上，`ConditionalAttribute` 与在方法调用周围放置 `#if`/`#endif` 相似。然而语法更简洁，因为开发人员只需将 `ConditionalAttribute` 属性添加到目标方法即可产生该效果，而无需对调用方本身进行任何更改。

`C#` 编译器在编译期间注意到对被调用方法上的属性，并且假设预处理器标识符存在，它会消除对该方法的任何调用。`ConditionalAttribute` 不会影响目标方法本身的编译后 CIL 代码（除了添加属性元数据之外）。相反，它通过删除调用来影响编译期间的调用站点。这进一步将 `ConditionalAttribute` 与跨程序集调用时的 `#if`/`#endif` 区分开来。因为被装饰的方法仍然被编译并包含在目标程序集中，所以是否调用方法的决定不是基于被调用方程序集中的预处理器标识符，而是基于调用方程序集。换句话说，如果你创建一个定义了 `CONDITION_B` 的第二个程序集，则来自第二个程序集对 `Program.MethodB()` 的任何调用都将执行。这在许多跟踪和测试场景中是一个有用的特性。事实上，对 `System.Diagnostics.Trace` 和 `System.Diagnostics.Debug` 的调用使用此特性，并带有 `TRACE` 和 `DEBUG` 预处理器标识符上的 `ConditionalAttributes`。

因为方法在预处理器标识符未定义时不会执行，所以 `ConditionalAttribute` 不能用于包含 `out` 参数或指定除 `void` 以外的返回类型的方法。否则会引起编译时错误。这是有意义的，因为被装饰方法内的代码可能根本不会执行，因此不知道向调用方返回什么。同样，属性不能被 `ConditionalAttribute` 装饰。`ConditionalAttribute` 的 `AttributeUsage`（参见本章前面标题为“`System.AttributeUsageAttribute`”的部分）为 `AttributeTargets.Class`（从 `.NET Framework 2.0` 开始）和 `AttributeTargets.Method`，这允许属性用于方法或类上。然而，类用法是特殊的，因为 `ConditionalAttribute` 仅允许在派生自 `System.Attribute` 的类上使用。

当 `ConditionalAttribute` 装饰自定义属性时，这一特性始于 `.NET Framework 2.0`，后者只能在调用程序集中定义了条件字符串时通过反射检索。如果没有此类条件字符串，查找自定义属性的反射将无法找到它。

# System.ObsoleteAttribute

如前所述，预定义属性会影响编译器和/或运行时行为。`ObsoleteAttribute` 提供了另一个影响编译器行为的属性的例子。其目的是帮助代码版本控制，提供一种向调用方指示特定成员或类型不再是最新的手段。列表 17.24 是 `ObsoleteAttribute` 用法的示例。如输出 17.8 所示，任何编译调用了标记有 `ObsoleteAttribute` 的成员的代码的调用方都会导致编译时警告，可选地为错误。

## LISTING 17.24: Using ObsoleteAttribute

```
class Program
{
    public static void Main()
    {
        ObsoleteMethod();
    }
    [Obsolete]
    public static void ObsoleteMethod()
    {
    }
}
```

## OUTPUT 17.8

```
c:\Sample\Code\obsoleteAttributeTest.cs(24,1): warning CS0612:
Program.ObsoleteMethod()' is obsolete
```

在这种情况下，`ObsoleteAttribute` 只是显示警告。然而，属性上还有两个额外的构造函数。其中一个 `ObsoleteAttribute(string message)` 将附加的消息参数附加到编译器的过时消息上。此消息的最佳实践是提供替换过时代码的指导。第二个构造函数是一个 `bool error` 参数，它强制将警告记录为错误。

`ObsoleteAttribute` 允许第三方通知开发人员已弃用的 API。警告（不是错误）允许原始 API 在开发人员能够更新调用代码之前继续工作。

# 智能系统性能评估报告

本文档对多种人工智能系统进行了综合性能评估，涵盖了图像生成、文本理解和推理能力等多个维度，旨在为后续系统优化提供参考依据。

![](img/25683ccec0773ba5b8794b11f2b12877_751_0.png)

从上图可以看出，不同系统在不同任务上的表现存在显著差异，其中新一代模型在多数指标上均优于前代版本。

- 图像生成质量提升约 35%
- 推理速度提高 2.3 倍
- 显存占用降低 40%

综合评估结果表明，当前先进的人工智能系统已具备较强的实用能力，但在复杂场景与多模态理解方面仍需进一步优化.

```
Console.WriteLine(documentAfter.Title);
}
}
```

```
// Serializable classes use SerializableAttribute.
[Serializable]
class Document
{
    public string Title = null;
    public string Data = null;
    [NonSerialized]
    public long _WindowHandle = 0;
    class Image
    {
    }
    [NonSerialized]
    private Image Picture = new Image();
}
```

## Output 17.9 shows the results of Listing 17.25.

# OUTPUT 17.9

```
A cacophony of ramblings from my potpourri of notes
```

`Listing 17.25` serializes and deserializes a `Document` object. Serialization involves instantiating a formatter (`System.Runtime.Serialization.Formatters.Binary.BinaryFormatter`, in this example) and calling `Serialization()` with the appropriate stream object. Deserializing the object simply involves calling the formatter’s `Deserialize()` method, specifying the stream that contains the serialized object as an argument. However, given that the return from `Deserialize()` is of type `object`, you also need to cast it specifically to the type that was serialized.

Notice that serialization occurs for the entire object graph (all items associated with the serialized object [`Document`] via a field). Therefore, all fields in the object graph also must be serializable.

# System.NonSerializable

Fields that are not serializable should be decorated with the `System.NonSerializable` attribute, which tells the serialization framework to ignore them. The same attribute should appear on fields that should not be persisted for use-case reasons. Passwords and Windows handles are

good examples of fields that should not be serialized: Windows handles because they change each time a window is re-created, and passwords because data serialized into a stream is not encrypted and can be readily accessed. Consider the Notepad view of the serialized document in Figure 17.2.

![](img/25683ccec0773ba5b8794b11f2b12877_753_0.png)

FIGURE 17.2: BinaryFormatter Does Not Encrypt Data

Listing 17.25 set the Title field, and the resultant `*.BIN` file includes the text in plain view.

# Providing Custom Serialization

One way to add encryption is to provide custom serialization. Ignoring the complexities of encrypting and decrypting, this requires implementing the `ISerializable` interface in addition to using `SerializableAttribute`. The interface requires only the `GetObjectData()` method to be implemented. However, this is sufficient only for serialization. To support deserialization as well, it is necessary to provide a constructor that takes parameters of type `System.Runtime.Serialization.SerializationInfo` and `System.Runtime.Serialization.StreamingContext` (see Listing 17.26).

## LISTING 17.26: Implementing System.Runtime.Serialization.ISerializable

```
using System;
using System.Runtime.Serialization;
[Serializable]
class EncryptableDocument :
    ISerializable
{
    public EncryptableDocument() { }
    enum Field
    {
        Title,
        Data
    }
}
public string Title;
public string Data;
public static string Encrypt(string data)
{
    string encryptedData = data;
    // Key-based encryption ...
    return encryptedData;
}
public static string Decrypt(string encryptedData)
{
    string data = encryptedData;
    // Key-based decryption...
    return data;
}
#region ISerializable Members
public void GetObjectData(
    SerializationInfo info, StreamingContext context)
{
    info.AddValue(
        Field.Title.ToString(), Title);
    info.AddValue(
        Field.Data.ToString(), Encrypt(Data));
}
public EncryptableDocument(
    SerializationInfo info, StreamingContext context)
{
    Title = info.GetString(
        Field.Title.ToString());
    Data = Decrypt(info.GetString(
        Field.Data.ToString()));
}
#endregion
}
```
