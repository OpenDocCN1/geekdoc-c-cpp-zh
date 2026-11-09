
这个接口中只有一个方法，即 **GetObjectData**。但大多数实现此接口的类型还会实现一个特殊构造函数，我稍后将对此进行描述。

> **重要提示** **ISerializable** 接口的一大问题是：一旦某个类型实现了它，所有派生类型也必须实现它，并且派生类型必须确保调用基类的 **GetObjectData** 方法和特殊构造函数。此外，一旦某个类型实现了此接口，就永远不能移除它，因为这会失去与派生类型的兼容性。**密封**类型实现 **ISerializable** 接口总是可以的。使用本章前面描述的自定义特性可以避免与 **ISerializable** 接口相关的所有潜在问题。

> **重要提示** **ISerializable** 接口和特殊构造函数旨在供格式化器使用。但是，其他代码可能会调用 **GetObjectData**，此时它可能返回潜在的敏感信息，或者其他代码可能构造一个传入损坏数据的对象。因此，建议对 **GetObjectData** 方法和特殊构造函数应用以下特性：
>
> `[SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]`

当格式化器序列化对象图时，它会查看每个对象。如果对象的类型实现了 **ISerializable** 接口，那么格式化器会忽略所有自定义特性，转而构造一个新的 **System.Runtime.Serialization.SerializationInfo** 对象。此对象包含应为该对象序列化的实际值集。

构造 **SerializationInfo** 时，格式化器传递两个参数：**Type** 和 **System.Runtime.Serialization.IFormatterConverter**。**Type** 参数标识正在被序列化的对象。唯一标识一个类型需要两项信息：类型的字符串名称及其程序集标识（包括程序集名称、版本、区域性和公钥）。构造 **SerializationInfo** 对象时，它会获取类型的全名（通过在内部查询 **Type 的 FullName** 属性），并将此字符串存储在私有字段中。你可以通过查询 **SerializationInfo 的 FullTypeName** 属性来获取类型的全名。同样，构造函数会获取类型的定义程序集（通过在内部查询 **Type 的 Module** 属性，然后查询 **Module 的 Assembly** 属性，再查询 **Assembly 的 FullName** 属性），并将此字符串存储在私有字段中。你可以通过查询 **SerializationInfo 的 AssemblyName** 属性来获取程序集标识。

> **注意** 虽然可以设置 **SerializationInfo 的 FullTypeName** 和 **AssemblyName** 属性，但不建议这样做。如果要更改正在被序列化的类型，建议调用 **SerializationInfo 的 SetType** 方法，并传入对 **Type** 对象的引用。调用 **SetType** 可确保类型的全名和定义程序集被正确设置。调用 **SetType** 的示例将在本章后面的“将类型序列化为不同类型并将对象反序列化为不同对象”一节中展示。

一旦 **SerializationInfo** 对象构造并初始化完成，格式化器就会调用该类型的 **GetObjectData** 方法，并向其传递对 **SerializationInfo** 对象的引用。**GetObjectData** 方法负责确定序列化对象所需的信息，并将这些信息添加到 **SerializationInfo** 对象中。**GetObjectData** 通过调用 **SerializationInfo** 类型提供的众多重载 **AddValue** 方法之一，来指明要序列化的信息。对于要添加的每项数据，**AddValue** 都会被调用一次。

下面的代码展示了 **Dictionary<TKey, TValue>** 类型如何实现 **ISerializable** 和 **IDeserializationCallback** 接口，以控制其对象的序列化和反序列化。

```csharp
[Serializable]
public class Dictionary<TKey, TValue> : ISerializable, IDeserializationCallback {
    // Private fields go here (not shown)

    private SerializationInfo m_siInfo; // Only used for deserialization

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

    // Method called after all key/value objects have been deserialized
    public virtual void OnDeserialization(Object sender) {
        if (m_siInfo == null) return; // Never set, return

        Int32 num = m_siInfo.GetInt32("Version");
        Int32 num2 = m_siInfo.GetInt32("HashSize");
        m_comparer = (IEqualityComparer<TKey>)
            m_siInfo.GetValue("Comparer", typeof(IEqualityComparer<TKey>));
        if (num2 != 0) {
            m_buckets = new Int32[num2];
            for (Int32 i = 0; i < m_buckets.Length; i++) m_buckets[i] = -1;
            m_entries = new Entry<TKey, TValue>[num2];
            m_freeList = -1;
            KeyValuePair<TKey, TValue>[] pairArray = (KeyValuePair<TKey, TValue>[])
                m_siInfo.GetValue("KeyValuePairs", typeof(KeyValuePair<TKey, TValue>[]));
            if (pairArray == null) {
                ThrowHelper.ThrowSerializationException(
                    ExceptionResource.Serialization_MissingKeys);
            }

            for (Int32 j = 0; j < pairArray.Length; j++) {
                if (pairArray[j].Key == null) {
                    ThrowHelper.ThrowSerializationException(
                        ExceptionResource.Serialization_NullKey);
                }

                Insert(pairArray[j].Key, pairArray[j].Value, true);
            }
        }
        else {
            m_buckets = null;
        }
        m_version = num;
        m_siInfo = null;
    }
}
```

每个 **AddValue** 方法都接受一个 **String** 名称和一些数据。通常，数据是简单值类型，例如 **Boolean**、**Char**、**Byte**、**SByte**、**Int16**、**UInt16**、**Int32**、**UInt32**、**Int64**、**UInt64**、**Single**、**Double**、**Decimal** 或 **DateTime**。但是，你也可以调用 **AddValue**，向它传递对 **Object**（例如 **String**）的引用。在 **GetObjectData** 添加完所有必要的序列化信息后，它会返回格式化器。

> **注意** 你应始终调用某个重载的 **AddValue** 方法来为你的类型添加序列化信息。如果字段的类型实现了 **ISerializable** 接口，不要对该字段调用 **GetObjectData**。而应调用 **AddValue** 来添加该字段；格式化器会看到该字段的类型实现了 **ISerializable**，并会为你调用 **GetObjectData**。如果你对字段对象调用 **GetObjectData**，格式化器在反序列化流时将不知道要创建新对象。

格式化器现在会取出添加到 **SerializationInfo** 对象中的所有值，并将它们逐个序列化到流中。你会注意到，**GetObjectData** 方法还传入了另一个参数：对 **System.Runtime.Serialization.StreamingContext** 对象的引用。大多数类型的 **GetObjectData** 方法会完全忽略此参数，因此我现在不讨论它。我将在本章后面的“流上下文”一节中讨论它。

所以现在你知道了如何设置用于序列化的所有信息。此时，让我们将注意力转向反序列化。当格式化器从流中提取对象时，它会为新对象分配内存（通过调用 **System.Runtime.Serialization.FormatterServices** 类型的静态 **GetUninitializedObject** 方法）。最初，该对象的所有字段都设置为 0 或 null。然后，格式化器检查该类型是否实现 **ISerializable** 接口。如果存在此接口，格式化器会尝试调用一个特殊构造函数，其参数与 **GetObjectData** 方法的参数相同。
