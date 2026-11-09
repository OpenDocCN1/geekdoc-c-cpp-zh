
```csharp
Circle c = new Circle(10);
```

在内部，m_area 字段会被设置为大约等于 314.159 的值。当此对象被序列化时，只有 m_radius 字段的值（10）会被写入流。这正是我们想要的，但现在当流被反序列化回 Circle 对象时，我们遇到了一个问题。反序列化时，Circle 对象的 m_radius 字段会被设置为 10，但其 m_area 字段会被初始化为 0——而不是 314.159！

下面显示的代码演示如何修改 Circle 类型以解决此问题：

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

我修改了 Circle，使其现在包含一个用 System.Runtime.Serialization.OnDeserializedAttribute 自定义特性标记的方法。[^35] 每当某个类型的实例被反序列化时，格式化器会检查该类型是否定义了带有此特性的方法，然后格式化器会调用此方法。调用此方法时，所有可序列化字段都已正确设置，并且可以访问这些字段来执行完全反序列化该对象所需的任何附加工作。

在上面的 Circle 修改版本中，我让 OnDeserialized 方法仅使用 m_radius 字段计算圆的面积，并将结果放入 m_area 字段。现在，m_area 将具有所需的值 314.159。

除了 OnDeserializedAttribute 自定义特性之外，System.Runtime.Serialization 命名空间还定义了 OnSerializingAttribute、OnSerializedAttribute 和 OnDeserializingAttribute 自定义特性，你可以将它们应用于类型的方法，以便对序列化和反序列化进行更多控制。下面是一个

> [^35]: 使用 System.Runtime.Serialization.OnDeserialized 自定义特性是在对象被反序列化时调用方法的首选方式，而不是让类型实现 System.Runtime.Serialization.IDeserializationCallback 接口的 OnDeserialization 方法。

此方法返回一个 Object 数组，其中每个元素标识被序列化对象中某个字段的值。这个 Object 数组与 MemberInfo 数组是并行的。也就是说，Object 数组中的元素 0 是由 MemberInfo 数组中元素 0 所标识的成员的值。

- 3. 格式化器将程序集的标识和类型的完整名称写入流。
- 4. 格式化器随后枚举这两个数组中的元素，将每个成员的名称和值写入流。

以下步骤描述格式化器如何自动反序列化一个其类型应用了 SerializableAttribute 特性的对象：

- 5. 格式化器从流中读取程序集的标识和完整类型名称。如果程序集当前未加载到 AppDomain 中，则会加载它（如前所述）。如果无法加载程序集，则会引发 SerializationException 异常，并且无法反序列化该对象。如果程序集已加载，格式化器会将程序集标识信息和类型的完整名称传递给 FormatterServices 的静态 GetTypeFromAssembly 方法：
  
    ```csharp
public static Type GetTypeFromAssembly(Assembly assem, String name);
    ```
  
  此方法返回一个 System.Type 对象，指示正在被反序列化的对象的类型。
- 6. 格式化器调用 FormatterServices 的静态 GetUninitializedObject 方法：
  
    ```csharp
public static Object GetUninitializedObject(Type type);
    ```
  
  此方法为新对象分配内存，但不调用该对象的构造函数。但是，对象的所有字节都会初始化为 null 或 0。
- 7. 格式化器现在像之前一样，通过调用 FormatterServices 的 GetSerializableMembers 方法来构造并初始化一个 MemberInfo 数组。此方法返回已序列化且需要反序列化的字段集合。
- 8. 格式化器根据流中包含的数据创建并初始化一个 Object 数组。
- 9. 对新分配对象的引用、MemberInfo 数组以及并行的字段值 Object 数组会被传递给 FormatterServices 的静态 PopulateObjectMembers 方法：
  
    ```csharp
public static Object PopulateObjectMembers(
    object obj, MemberInfo[] members, Object[] data);
    ```
  
  此方法枚举这些数组，将每个字段初始化为其对应的值。此时，对象已完全反序列化。

## 控制序列化/反序列化的数据

正如本章前面所讨论的，控制序列化和反序列化过程的最佳方式是使用 OnSerializing、OnSerialized、OnDeserializing、OnDeserialized、NonSerialized 和 OptionalField 特性。然而，在一些非常罕见的场景中，这些特性并不能提供你所需的全部控制。此外，格式化器在内部使用反射，而反射很慢，这会增加序列化和反序列化对象所需的时间。要完全控制哪些数据被序列化/反序列化，或消除反射的使用，你的类型可以实现 System.Runtime.Serialization.ISerializable 接口，其定义如下：

```csharp
public interface ISerializable {
    void GetObjectData(SerializationInfo info, StreamingContext context);
}
```

此接口中只有一个方法 GetObjectData。但大多数实现此接口的类型还会实现一个特殊构造函数，我将在稍后描述。

**重要** ISerializable 接口的大问题在于，一旦某个类型实现了它，所有派生类型也必须实现它，并且派生类型必须确保调用基类的 GetObjectData 方法和特殊构造函数。此外，一旦某个类型实现了此接口，就永远不能移除它，因为这会失去与派生类型的兼容性。密封类型实现 ISerializable 接口总是可以的。使用本章前面描述的自定义特性可以避免与 ISerializable 接口相关的所有潜在问题。

**重要** ISerializable 接口和特殊构造函数旨在供格式化器使用。然而，其他代码可能会调用 GetObjectData，从而可能返回潜在敏感信息，或者其他代码可能会构造一个传入损坏数据的对象。因此，建议将以下特性应用于 GetObjectData 方法和特殊构造函数：

```csharp
[SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
```

当格式化器序列化对象图时，它会查看每个对象。如果其类型实现了 ISerializable 接口，那么格式化器会忽略所有自定义特性，转而构造一个新的 System.Runtime.Serialization.SerializationInfo 对象。此对象包含应为此对象序列化的实际值集合。

构造 SerializationInfo 时，格式化器传递两个参数：Type 和 System.Runtime.Serialization.IFormatterConverter。Type 参数标识正在被序列化的对象。唯一标识一个类型需要两条信息：类型的字符串名称及其程序集标识（包括程序集名称、版本、区域性和公钥）。构造 SerializationInfo 对象时，它会获取类型的完整名称（通过在内部查询 Type 的 FullName 属性），并将此字符串存储在私有字段中。你可以通过查询 SerializationInfo 的 FullTypeName 属性来获取类型的完整名称。同样，构造函数会获取类型的定义程序集（通过在内部查询 Type 的 Module 属性，然后查询 Module 的 Assembly 属性，再查询 Assembly 的 FullName 属性），并将此字符串存储在私有字段中。你可以通过查询 SerializationInfo 的 AssemblyName 属性来获取程序集的标识。

> **注意** 虽然可以设置 SerializationInfo 的 FullTypeName 和 AssemblyName 属性，但不建议这样做。如果要更改正在被序列化的类型，建议调用 SerializationInfo 的 SetType 方法，并传入所需 Type 对象的引用。调用 SetType 可确保类型的完整名称和定义程序集被正确设置。本章后面的“将类型序列化为不同类型并将对象反序列化为不同对象”一节中给出了调用 SetType 的示例。

一旦 SerializationInfo 对象构造并初始化完成，格式化器就会调用该类型的 GetObjectData 方法，并向其传递对 SerializationInfo 对象的引用。GetObjectData 方法负责确定序列化该对象所需的信息，并将这些信息添加到 SerializationInfo 对象中。GetObjectData 通过调用 SerializationInfo 类型提供的众多重载 AddValue 方法之一来指示要序列化哪些信息。对于希望添加的每项数据，都会调用一次 AddValue。

下面的代码大致展示了 Dictionary<TKey, TValue> 类型如何实现 ISerializable 和 IDeserializationCallback 接口，以控制其对象的序列化和反序列化。

```csharp
[Serializable]
public class Dictionary<TKey, TValue> : ISerializable, IDeserializationCallback {
    // Private fields go here (not shown)

    private SerializationInfo m_siInfo;  // Only used for deserialization

    // Special constructor (required by ISerializable) to control deserialization
    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    protected Dictionary(SerializationInfo info, StreamingContext context) {
        // During deserialization, save the SerializationInfo for OnDeserialization
        m_siInfo = info;
    }

    // Method to control serialization
    [SecurityCritical]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context) {

        info.AddValue("Version", m_version);
        info.AddValue("Comparer", m_comparer, typeof(IEqualityComparer<TKey>));
        info.AddValue("HashSize", (m_buckets == null) ? 0 : m_buckets.Length);
        if (m_buckets != null) {
            KeyValuePair<TKey, TValue>[] array = new KeyValuePair<TKey, TValue>[Count];
            CopyTo(array, 0);
            info.AddValue("KeyValuePairs", array, typeof(KeyValuePair<TKey, TValue>[]));
        }
    }
}
```
