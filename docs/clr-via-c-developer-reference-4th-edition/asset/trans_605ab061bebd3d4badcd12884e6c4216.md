

```cs
public Circle(Double radius) {
    m_radius = radius;
    m_area = Math.PI * m_radius * m_radius;
}
```

```cs
[OnDeserialized]
private void OnDeserialized(StreamingContext context) {
    m_area = Math.PI * m_radius * m_radius;
}
```

我修改了 Circle 类，使其包含一个标记有 `System.Runtime.Serialization.OnDeserializedAttribute` 自定义属性的方法。每当类型的实例被反序列化时，格式化程序会检查该类型是否定义了带有此属性的方法，如果是格式化程序就会调用该方法。当此方法被调用时，所有可序列化的字段将被正确设置，并且可以访问它们以执行完全反序列化对象所需的任何额外工作。

在上述修改后的 Circle 版本中，我让 `OnDeserialized` 方法简单地使用 `m_radius` 字段计算圆的面积并将结果放在 `m_area` 字段中。`m_area` 将获得 314.159 的预期值。

除了 `OnDeserializedAttribute` 自定义属性外，`System.Runtime.Serialization` 命名空间还定义了 `OnSerialAttribute`、`OnSerializedAttribute` 和 `OnDeserializingAttribute` 自定义属性，你可以将它们应用于类型的方法，以实现对序列化和反序列化更强的控制。这里有一个将这些属性中的每一个应用于方法的示例类。

```cs
[Serialized]
public class MyType {
    Int32 x, y; [OnDeserialized] Int32 sum;

    public MyType(Int32 x, Int32 y) {
        this.x = x; this.y = y; sum = x + y;
    }
}
```

```cs
[OnDeserializing]
private void OnDeserializing(StreamingContext context) {
    // ：为此类型新版本中的字段设置默认值
}
```

```cs
[OnDeserialized]
private void OnDeserialized(StreamingContext context) {
    // ：从字段初始化瞬态状态
    sum = x + y;
}
```

```cs
[OnSerializing]
private void OnSerializing(StreamingContext context) {
}
```

> 2 使用 `System.Runtime.Serialization.OnDeserialized` 自定义属性是对象反序列化时调用方法的首选方法，而不是让类型实现 `System.Runtime.Serialization.IDerializationCallback` 接口的 `OnDeserialization` 方法。

```cs
// 示例：序列化之前修改任何状态
}

[OnSerialized]
private void OnSerialized(StreamingContext context) {
    // ：序列化后恢复任何状态
}
```

每当你使用这四个属性中的任何一个时，定义的方法必须接受单个 `StreamingContext` 参数（在本章稍后的“流上下文”部分中讨论）并返回 `void`。该方法的名称可以是你想要的任何名称。此外，你应该将方法声明为 `private` 以防止它被普通代码调用；格式化程序具有足够的安全性，可以调用私有方法。

> 注意 当你正在序列化一组对象时，格式化程序首先调用所有标记有 `OnSerialized` 属性的对象。接着，它序列化所有对象的字段，最后调用所有对象标记有 `OnSerialized` 属性的方法。同样，当你反序列化一个对象集合时，格式化程序调用所有标记有 `OnDeserialized` 属性的对象方法，然后反序列化所有对象的字段，并调用每个对象标记有 `OnDeserialized` 属性的方法。

同样注意在反序列化期间，当格式化程序看到某个类型提供标记有 `OnDeserialized` 属性的方法时，它会将该对象的引用添加到内部列表中。在所有对象都完成反序列化后，格式化程序会反序遍历此列表并调用每个对象的 `OnDeserialized` 方法。当此方法被调用时，所有可序列化的字段将被正确设置，并且可以访问它们以执行完全反序列化对象所需的任何额外工作。反序调用这些方法是非常重要的，因为它允许内部对象在包含它们的外部对象之前完成它们反序列化。

例如，想象有一个集合对象（如 `Hashtable` 或 `Dictionary`），它内部使用哈希表来维护其项目集。集合对象类型将实现一个标记有 `OnDeserialized` 属性的方法。尽管集合对象先启动（在它的项目之前），但它的 `OnDeserialized` 方法将最后被调用（在它的任何项目的 `OnSerialized` 方法之后）。这允许项目完成反序列化，以便所有字段都能被正确初始化，从而计算出良好的哈希码。然后，集合对象创建其内部桶并使用其哈希码将项目放入桶中。我将在本章接下来的“控制序列化/反序列化数据”部分展示 `Dictionary` 类如何使用此点的示例。

![](img/0ce3b788d061e3d3095fa554b1a34adf_647_0.png)

如果你序列化了一个类型的实例，向该类型添加新字段，然后反序列化不包含该新字段的对象，格式化程序将抛出 `SerializationException`，消息显示正在反序列化的流中的数据成员数量错误。这在版本控制场景中是非常问题的，因为在新版本中添加新字段非常常见。幸运的是，你可以使用 `System.Runtime.Serialization.OptionalFieldAttribute` 来帮助你。

你对添加到类型的每个新字段应用 `OptionalFieldAttribute` 属性。现在，当格式化程序看到此属性应用于字段时，如果流中的数据不包含该字段，格式化程序将不会抛出 `SerializationException`。

# 格式化程序如何序列化实例

在本节中，我将深入介绍格式化程序如何序列化字段。这些知识可以帮助你理解本章剩余部分的高级序列化和反序列化技术。

为了方便格式化程序的操作，FCL 在 `System.Runtime.Serialization` 命名空间提供了一个 `FormatterServices` 类型。该类型只有静态方法，且无法实例化。以下步骤描述了格式化程序如何自动序列化应用了 `SerializableAttribute` 的对象。

- 1. 格式化程序调用 `FormatterServices.GetSerializableMembers` 方法。

```cs
public static MemberInfo[] GetSerializableMembers(Type type, StreamingContext context);
```

该方法使用获取类型的公共和私有实例字段（排除由 `NonSerializedAttribute` 标记的字段）。该方法返回一个 `MemberInfo` 对象数组，每个对象对应一个序列化实例字段。

- 2. 将要序列化的对象和 `System.Reflection.MemberInfo` 对象数组传递给 `FormatterServices.GetGetObject` 方法。

```cs
public static Object[] GetGetObject(Object obj, MemberInfo[] members);
```

该方法返回一个 `Object` 数组，其中每个元素标识字段的值。

- 3. 格式化程序将程序集的标识和完整类型写入流中。

- 4. 格式化程序遍历数组中的元素，将每个成员名称和值写入流中。

