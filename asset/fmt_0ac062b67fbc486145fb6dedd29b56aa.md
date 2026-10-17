
注意，这很容易修复。然而，反过来——定义一个派自没有应用 `SerializableAttribute` 属性的基类的类型——就很难修复。但这是设计如此；如果基类类型允许其类型的实例被序列化，那么字段无法被序列化，因为基对象本质上是派生对象的一部分。这就是为什么 `System.Object` 被应用了 `SerializableAttribute`。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_685_0.png)

> 注意：通常情况下，建议你定义的大多数类型都是可序列化的。毕竟，这为你这些类型的用户提供了很大的灵活性。然而，你必须意识到字段是被声明为 public、protected、internal 还是 private。如果一个类型包含敏感或安全数据（如密码），或者如果数据在传输后没有意义或价值，你可能不想让该类型可序列化。

如果你发现自己正在使用一个并非为序列化设计的类型，并且没有该类型的源码来添加序列化支持，一切还没有结束。在本章的“反序列化对象时重写程序集和或类型”部分，我将解释如何让任何不可序列化的类型变为序列化。

## 控制序列化与反序列化

当你对一个类型应用 `SerializableAttribute` 自定义属性时，所有的实例字段（public、private、protected 等）都是可序列化的。然而，一个类型可能会定义某些不应序列化的实例字段。通常情况下，你不希望某个类型的某些字段被序列化的原因有两个：

- 不要在标记有 `[Serializable]` 属性的类型内部使用 C# 的自动属性功能定义属性，因为编译器会生成字段名称，且生成的名称在每次重新编译代码时都可能不同，导致你的类型实例无法被反序列化。
- 字段包含在反序列化时将无效的信息。例如，一个包含 Windows 内核对象句柄（如文件、进程、线程、互斥锁、事件、信号量等）的对象在反序列化到另一个进程或机器时将没有任何意义。Windows 内核句柄是进程相关的值。
- 字段包含容易计算的信息。在这种情况下，你选择哪些字段不需要序列化，通过减少传输的数据量来提高应用程序的性能。

下面的代码使用了 `System.SerializedAttribute` 自定义属性来指示类型中的哪些字段不应被序列化。（注意该属性也定义在 `System.Runtime.Serialization` 命名空间中。）

```csharp
[Serializable]
internal class Circle {
    private Double m_radius;
    [NonSerialized]
    private Double m_area;
    public Circle(Double radius) {
        m_radius = radius;
        m_area = Math.PI * m_radius * m_radius;
    }
}
```

在上面的代码中，`Circle` 的对象可以被序列化。然而，格式器只会序列化对象中 `m_radius` 字段的值。`m_area` 字段中的值不会被序列化，因为它被应用了 `NonSerializedAttribute`。该属性只能应用于类型的字段，并且当它被另一个类型继承时依然继续有效。当然，你可以在一个类型中的多个字段上应用 `NonSerializedAttribute`。

所以，假设我们的代码如下构造了一个新对象：

```csharp
Circle c = new Circle(10);
```

在内部，`m_area` 字段被设置为一个接近 314.159 的值。当此对象被序列化时，只有 `m_radius` 字段的值（10）被写入流中。这正是我们想要的，但现在当流被反序列化回 `Circle` 对象时，我们就遇到了问题。在反序列化时，`Circle` 对象的 `m_radius` 字段将被设置为 10，但其 `m_area` 字段将被初始化为 0——而不是 314.159！

## 第四部分 核心设施

下面的代码演示了如何修改 `Circle` 类型来修复这个问题：

```csharp
[Serializable]
internal class Circle {
    private Double m_radius;
    [NonSerialized]
    private Double m_area;
    public Circle(Double radius) {
        m_radius = radius;
        m_area = Math.PI * m_radius * m_radius;
    }
    [OnDeserialized]
    private void OnDeserialized(StreamingContext context) {
        m_area = Math.PI * m_radius * m_radius;
    }
}
```

# 第四部分 核心设施

如果你对类型的实例进行序列化，为该类型添加一个新字段，然后尝试反序列化不包含该新字段的对象，格式化器会抛出一个 `SerializationException`，消息指示正在序列化的流中的成员数量错误。这在版本控制场景中非常不利，因为在较新版本中类型添加字段是非常常见的。幸运的是，你可以使用 `System.Runtime.Serialization.OptionalFieldAttribute` 来帮助你。

你将 `OptionalFieldAttribute` 应用到类型的每个新字段上，当格式化器使用应用到字段上的属性时，如果流中的数据不包含该字段，格式化器将不会抛出 `SerializationException`。

## 格式化器序列类型实例

在本节中，我将介绍格式化器如何序列化对象的字段。这些知识可以帮助你理解本章其余部分解释的更高级的序列化反序列化技术。

为了方便格式化器，FCL（框架类库）在 `System.Runtime.Serialization` 命名空间中提供了 `FormatterServices` 类型。该类型仅包含静态方法，不能实例化。以下步骤描述了格式化器如何自动序列化应用了 `SerializableAttribute` 的对象：

格式化器调用 `FormatterServices` 的 `GetSerializableMembers` 方法：

```
public static MemberInfo[] GetSerializableMembers(Type type, StreamingContext context);
```

该方法使用反射获取类型的公共和私有实例字段（排除任何标记有 `NonSerializedAttribute` 属性的字段）。该方法返回一个 `MemberInfo` 对象数组，每个对象对应一个可序列化的实例字段。

- 2. 然后将正在序列化的对象和 `System.Reflection.MemberInfo` 对象数组传递给 `FormatterServices` 的静态方法 `GetObjectData`：

```go
public static Object[] GetObjectData(Object obj, MemberInfo[] members);
```

该方法返回一个 `Object` 数组，其中每个元素标识一个被序列化字段的值。此 `Object` 数组和 `MemberInfo` 数组是并行的。也就是说，`Object` 数组中的元素 O 是 `MemberInfo` 数组中元素 O 所标识的成员的值。

- 3. 格式化器将程序集的标识和类型的全名写入流中。
- 4. 随后，格式化器枚举两个数组中的元素，将每个成员名称和值写入流中。

以下步骤描述了格式化器如何自动反序列化应用了 `SerializableAttribute` 的对象：

- 1. 格式化器从流中读取程序的标识和全名。如果程序集尚未加载到 `AppDomain` 中，则会加载它（如前所述）。如果无法加载，将抛出 `SerializationException` 且无法反序列化对象。如果已加载，格式化器将程序集标识信息和类型的全名传递给 `FormatterServices` 的静态方法 `GetTypeFromAssembly`：

```
public static Type GetTypeFromAssembly(Assembly assembly, String name);
```

该方法返回一个 `System.Type` 对象，指示正在被反序列化的对象类型。

- 2. 格式化器调用 `FormatterServices` 的 `GetUninitializedObject` 方法：

```
public static Object GetUninitializedObject(Type type);
```

该方法为新对象分配内存，但不会调用对象的构造函数。然而，对象的所有字节都将初始化为 `null` 或 0。

- 3. 格式化器在调用 `FormatterServices` 的 `GetSerializableMembers` 方法的同时，构造并初始化 `MemberInfo` 数组。该方法返回已序列化并需要反序列化的字段集。
- 4. 格式化器从流中包含的数据创建并初始化一个 `Object` 数组。

```
public static void PopulateObjectMembers(Object obj, MemberInfo[] members, Object[] data);
```

该方法枚举数组，将每个字段初始化为其对应的值。此时，对象已完全完成反序列化。

## 控制序列化/反序列化数据

正如本章讨论的，控制序列化反序列化过程的最佳方法是使用 `OnSerializing`、`OnSerialized`、`OnDeserializing`、`OnDeserialized`、`NonSerialized` 和 `OptionalField` 属性。然而，在少数情况下，这些属性无法为你提供所需的全部控制。此外，格式化器内部使用反射且速度慢，这增加了序列化和反序列化对象的时间。为了完全控制被序列化/反序列化的数据或消除对反射的使用，你的类型可以实现 `System.Runtime.ISerializable` 接口，其定义如下：

```
public interface ISerializable {
    void GetObjectData(SerializationInfo info, StreamingContext context);
}
```

# 第四部分 核心设施

该接口仅有一个方法 `GetObjectData`。但大多数实现此接口的类型还会实现一个特殊的构造函数，我稍后会描述。

> **重要** `ISerializable` 接口的主要问题是，一旦类型实现了它，所有派生类型都必须实现它，且派生类型必须确保调用了基类的 `GetObjectData` 方法和特殊构造函数。此外，一旦类型实现了它，就永远无法移除它，因为这将会失去与派生类的兼容性。对于密封类（sealed types），实现 `ISerializable` 接口始终是安全的。使用本章之前描述的自定义属性可以避免所有与 `ISerializable` 接口相关的所有潜在问题。

> **重要** `ISerializable` 接口和特殊构造函数供格式化器使用。然而，其他代码可能会调用 `GetObjectData`，这可能会返回潜在敏感信息，或者其他代码构造一个传入损坏数据的对象。因此，建议将以下属性应用到 `GetObjectDataPermissionAttribute`：

`[SecurityAction.Demand, SerializationFormatter = true)]`

当格式化器序列化对象图时，它会检查每个对象。如果其类型实现了 `ISerializable` 接口，格式化器将忽略所有自定义属性，而是构造一个新的 `System.Runtime.Serialization.SerializationInfo` 对象。该对象包含了应被序列化的实际值集合。

在构造 `SerializationInfo` 时，格式化器传递两个参数：`Type` 和 `System.Runtime.Serialization.IFormatterConverter`。`Type` 参数标识正在序列化的对象。唯一标识一个类型需要两个信息：类型的字符串名称和它的标识（包括程序集名称、版本、颜色和公密钥）。构造 `SerializationInfo` 时获取类型名称（`FullName` 属性）并将其存储在私有字段中。你可以通过查询 `SerializationInfo.FullName` 获取类型名称。同样，构造函数获取定义的程序集（内部查询 `Type` 的 `Module` 属性，随后查询 `Assembly.Assembly` 然后查询 `Assembly.FullName`）并将其存储在私有字段中。你可以通过查询 `SerializationInfo.AssemblyName` 属性获取标识。

> **注意** 虽然可以设置 `SerializationInfo.FullName` 和 `AssemblyName` 属性，但不鼓励。如果你想更改正在序列化的类型，建议调用 `SerializationInfo.SetType` 方法，并传入所需的 `Type` 对象的引用。调用 `SetType` 可以确保类型的全名和程序集被正确设置。调用 `SetType` 的示例将在本章稍后的“作为不同类型序列化并作为不同类型反序列化对象”章节中显示。

一旦 `SerializationInfo` 对象被构造并初始化，格式化程序就会调用类型的 `GetObjectData` 方法，并传入 `SerializationInfo` 对象的引用。`GetObjectData` 方法负责确定序列化该对象所需的必要信息，并将这些信息添加到 `SerializationInfo` 对象中。`GetObjectData` 通过调用 `SerializationInfo` 类型提供的许多重载 `AddValue` 方法来指示要序列化的信息。对于你想要序列化的每部分数据，都会调用一次 `AddValue`。

以下代码展示了 `Dictionary<Key, Value>` 类型如何实现 `ISerializable` 和 `IDerializationCallback` 接口，以控制对象的序列化和反序列化。

```csharp
[Serializable]
public class Dictionary<Key, Value> : ISerializable, IDerializationCallback {
    // 此处的私有字段未显示
    private SerializationInfo m_sInfo; // 用于反序列化
    // 特殊构造函数（ISerializable 要求），用于控制化
    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    protected Dictionary(SerializationInfo info, StreamingContext context) {
        // 在反序列化期间，为 OnDeserialization 设置 SerializationInfo
        m_sInfo = info;
    }
    // 控制序列化的方法
    [Critical]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context) {
        info.AddValue("Version", m_version);
        info.AddValue("Comparer", m_comparer, typeof(IComparer<TKey>));
        info.AddValue("HashSize", m_buckets == null ? 0 : m_buckets.Length);
        if (m_buckets != null) {
            KeyValuePair<Key, Value>[] array = new KeyValuePair<Key, Value>[m_buckets.Count];
            Copy.CopyTo(array, 0);
            info.AddValue("KeyValuePairs", array, typeof(KeyValuePair<Key, Value>));
        }
    }
    // 在所有键/值对象反序列化后调用的方法
    public virtual void OnDeserialization(Object sender) {
        if (m_sInfo == null) return; // 从未设置，返回
        Int32 num = m_sInfo.GetInt32("Version");
        Int32 num2 = m_sInfo.GetInt32("HashSize");
        m_comparer = (IComparer<TKey>)m_sInfo.GetValue("Comparer", typeof(IComparer<TKey>));
        m_version = num;
        if (num2 != 0) {
            m_buckets = new Int32[num2];
            for (Int32 i = 0; i < m_buckets.Length; i++) m_buckets[i] = -1;
```
