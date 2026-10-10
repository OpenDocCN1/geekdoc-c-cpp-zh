
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

你的类型可以实现 `System.Runtime.Serialization.ISerializable` 接口，其定义如下：

```
public interface ISerializable {
    void GetObjectData(SerializationInfo info, StreamingContext context);
}
```

该接口仅包含一个方法 `GetDataObject`。大多数实现此接口的类型也会实现一个我将要描述的特殊构造函数。

> **重要** `ISerializable` 接口的一个大问题是，一旦某个类型实现了它，所有的派生类型也必须实现它，并且派生类型必须确保它们调用了基类的 `GetObjectData` 方法和特殊构造函数。此外，一旦一个类型实现了此接口，它就永远无法移除它，因为这将会导致失去与派生类型的兼容性。对于密封类（`sealed types`），实现 `ISerializable` 接口总是安全的。使用本章前面描述的自定义特性可以避免与 `ISerializable` 接口相关的潜在问题。

> **重要** `ISerializable` 接口和特殊构造函数旨在供格式化程序使用。然而，其他代码可能会调用 `GetObjectData`，这可能会返回敏感信息，或者其他代码可能会构造一个传入损坏数据的对象。因此，建议你在 `GetObjectData` 方法和特殊构造函数上应用以下特性：

`[SecurityPermissionAttribute(SecurityAction.Action, SerializationFormatter = true)]`

当格式化程序序列化对象图时，它会检查每个对象。如果对象实现了 `ISerializable` 接口，格式化程序将忽略所有自定义特性，而是构造一个新的 `System.Runtime.Serialization.SerializationInfo` 对象。该对象包含了应该为该对象序列化的实际值集。

在构造 `SerializationInfo` 时，格式化程序传递两个参数：`Type` 和 `System.Runtime.Serialization.IFormatter`。`Type` 标识被序列化的对象。唯一标识一个类型需要两个信息：类型的字符串名称和它的程序集标识（包括程序集名称、版本、文化和公共访问性）。当构造 `SerializationInfo` 对象时，它会获取该类型的全名（通过内部查询 `Type` 的 `FullName` 属性）并将此字符串存储在私有字段中。你可以通过查询 `SerializationInfo` 的 `FullName` 属性获取该类型的全名。同样，构造函数获取定义该类型的程序集（通过查询 `Type` 的 `Module` 属性，接着查询 `Assembly` 属性，最后查询 `Assembly` 的 `FullName` 属性），并将其存储在私有字段中。你可以通过查询 `SerializationInfo` 的 `AssemblyName` 属性获取程序集标识。

## 第 24 章 运行时序列化

注意：虽然你可以设置 `SerializationInfo` 的 `FullTypeName` 和 `Assembly` 属性，但不建议这样做。如果你想更改被序列化的类型，建议调用 `SerializationInfo.SetType` 方法，并传入指向所需 `Type` 对象的引用。调用 `SetType` 可确保类型名称和程序集被正确设置。调用 `SetType` 的示例可以在本章稍后的“作为不同类型序列化类型并作为不同对象反序列化对象”部分看到。

`SerializationInfo` 对象构造并初始化后，格式化程序调用该类型的 `GetDataObject` 方法，并传递 `SerializationInfo` 对象的引用。`DataObject` 方法负责确定序列化该对象所需的信息，并将这些信息添加到 `SerializationInfo` 对象中。`GetObjectData` 通过调用 `SerializationInfo` 类型提供的许多重载方法之一来指示要序列化的信息。对于你想要添加的每个数据，都会调用一次 `AddValue`。

以下代码显示了 `Dictionary<TKey, TValue>` 类型如何实现 `ISerializable` 和 `IDerializationCallback` 接口以控制其对象的序列化和反序列化。

```
[Serializable]
public class Dictionary<TKey, TValue> : ISerializable, IDerializationCallback {
 // 私有字段（未显示）

private SerializationInfo m_siInfo; // 仅用于反序列化

 // 特殊构造函数（ISerializable 要求）控制反序列化
[SecurityPermissionAttribute(SecurityAction.Demand, Serialization, SerializationFormatter = true)]
protected Dictionary(SerializationInfo info, StreamingContext context) {
 // 在反序列化期间，保存 SerializationInfo 以供 OnDeserialization 使用
 m_siInfo = info;
}

 // 控制序列化的方法
[SecurityCritical]
public void GetObjectData(SerializationInfo info, StreamingContext context) {

info.AddValue("Version", m_version);
info.AddValue("Comparer", m_comparer, typeof(IComparer<TKey>));
info.AddValue("HashSize", (m_buckets == null) ? 0 : m_buckets.Length);
 if (m_buckets != null) {
 KeyValuePair<TKey, TValue>[] array = new KeyValuePair<TKey, TValue>[Count];
 CopyTo(array, 0);
 info.AddValue("KeyPairs", array, typeof(KeyValuePair<TKey, TValue>[]));
}
}
```

```
// 在所有键值对象反序列化后调用的方法
public virtual IDerializationCallback.OnDeserialization(Object sender) {
    if (m_siInfo == null) return; // 从未设置，返回

    Int32 num = m_siInfo.GetInt32("Version");
    Int32 num2 = m_siInfo.GetInt32("HashSize");
    m_comparer = (IComparer<TKey>)m_siInfo.GetValue("Comparer", typeof(IComparer<TKey>));
    if (num != 0) {
        m_buckets = new Int32[num];
        for (Int32 i = 0; i < m_buckets.Length; i++) m_buckets[i] = -1;
        m_entries = new Entry<TKey, TValue>[num2];
        m_free_list = -1;
        KeyValuePair<TKey, TValue>[] pairArray = (KeyValuePair<TKey, TValue>[])m_siInfo.GetValue("KeyValuePairs", typeof(KeyValuePair<TKey, TValue[]>));
        if (pairArray == null)
            ThrowHelper.ThrowSerializationException("Resource.Serialization.MissingKeys");
        for (Int32 j = 0; j < pairArray.Length; j++) {
            if (pairArray[j].Key == null)
                ThrowHelper.ThrowSerializationException("Resource.Serialization.NullKey");
            Insert(pairArray[j].Key, pairArray[j].Value, true);
        }
    } else {
        m_buckets = null;
    }
    m_version = num;
    m_siInfo = null;
}
```

每个 `AddValue` 方法接收一个字符串名称和一些数据。通常，数据是简单值，如 `Boolean`, `Char`, `Byte`, `SByte`, `Int16`, `UInt16`, `Int32`, `UInt64`, `Double`, `Decimal` 或 `DateTime`。然而，你也可以调用 `AddValue` 并传入一个 `Object` 的引用作为字符串。在 `GetDataObject` 添加了所有必要的序列化信息后，它会返回给格式化程序。

> 注意：你应该始终调用重载的 `AddValue` 方法之一来为你的类型序列化信息。如果某个字段实现了 `ISerializable` 接口，不要在该字段上调用 `GetDataObject`。相反，对该字段调用 `AddValue`；格式化程序会看到该字段实现了 `ISerializable`，格式化程序会为你调用 `GetDataObject`。如果你在字段对象上调用 `GetDataObject`，格式化程序在反序列化流时就不需要创建新对象。

格式化程序现在获取所有添加到 `SerializationInfo` 对象中的值，并将它们每一个序列化到流中。你会发现 `GetDataObject` 方法传递了另一个参数：指向 `System.Runtime.Serialization.StreamingContext` 对象的引用。大多数类型的 `GetObject` 方法完全忽略此参数，因此我在这里不会讨论它。相反，我将在稍后的“`StreamingContext`”部分讨论它。

现在你了解了用于序列化的所有信息。此时，让我们转向反序列化。格式化程序从流中提取所有内容，它为新对象分配内存（通过调用 `System.Runtime.Serialization.Formatter` 类型的静态方法 `GetUninitializedObject`）。最初，该对象的所有字段都被设置为 0 或 `null`。然后，格式化程序检查类型是否实现了 `ISerializable` 接口。如果存在此接口，格式化程序将尝试调用特殊构造函数，其参数与 `Getter` 的参数相同。

如果你的类是密封的（`sealed`），强烈建议将此特殊构造函数声明为私有（`private`）。这将防止任何代码意外调用。如果不是，你应该将此特殊构造函数声明为受保护（`protected`），以便只有派生类可以调用它。注意，无论如何声明，格式化程序都能调用此特殊构造函数。

此构造函数接收一个 `SerializationInfo` 对象的引用，该对象包含了对象序列化时添加的所有值。特殊构造函数可以调用任何 `GetBoolean`, `GetChar`, `GetByte`, `GetByteString`, `GetInt16`, `GetInt32`, `GetInt32`, `GetInt64`, `GetUInt64`, `GetString`, `GetDouble`, `GetDecimal`, `DateTime`, `String` 和 `GetValue` 方法，传入与序列化值使用的名称对应的字符串。这些方法返回的值将用于初始化新对象的字段。

在反序列化对象的字段时，它将调用与序列化时传递 `AddValue` 方法的值类型匹配的 `Get` 方法。也就是说，如果 `GetDataObject` 方法调用 `AddValue` 并传入一个 `Int32` 值，那么在反序列化对象时应该调用 `GetInt32` 方法。如果流中的值与尝试获取的类型不匹配，格式化程序将尝试使用 `IFormatter-Convert` 对象将流的值“强制转换”到目标类型。

如前所述，当构造 `SerializationInfo` 对象时，它被传递一个实现 `IFormatterConverter` 接口的对象。因为格式化程序负责构造 `SerializationInfo` 对象，所以它决定了使用 `IFormatterConverter` 类型。`Microsoft.BinaryFormatter` 和 `SoapFormatter` 总是构造 `System.Runtime.Serialization.FormatterConverter` 类型的实例。微软格式化程序没有提供让你选择不同 `IFormatterConverter` 类型的值。

`FormatterConverter` 类型调用 `System.Convert` `Int32` 到 `Int64`。然而，为了在任意类型之间转换值，格式化程序调用 `Convert` 的 `ChangeType` 方法来

将序列化后的（或原始）类型转换为 `IConvertible` 接口，然后调用相应的接口方法。因此，为了允许可序列化类型的对象被反序列化为不同的类型，你可能可能考虑让你的类型实现 `IConvertible` 接口。请注意，在反序列化对象以及当你调用与流中的值类型不匹配的 `Get` 方法时，会使用 `FormatterConverter`。

与其调用之前列出的各种 `Get` 方法，特殊构造函数可以调用 `GetEnumerator`，它返回一个 `System.Runtime.Serialization.InfoEnumerator`，该枚举器可以遍历 `SerializationInfo` 对象中包含的所有值。枚举的每个值都是一个 `System.Runtime.Serialization.SerializationEntry` 对象。

当然，欢迎定义派生自 `ISerializable` 的自定义类型和特殊构造函数。如果你的类型也实现了 `ISerializable`，那么你对 `GetObjectData` 的实现以及对特殊构造函数的实现必须调用基类中的相同函数，以便对象能够被正确序列化和反序列化。不要忘记这样做，否则对象将无法正确序列化或反序列化。下一节将解释如何正确定义一个基类未实现此接口的 `ISerializable` 类型。

如果你的类型中没有任何字段，因此没有特殊的序列化/反序列化需求，则 `GetObjectData` 是虚方法，完全不需要实现 `ISerializable`。与所有接口成员一样，格式化器（`formatter`）将特殊构造函数视为“虚拟的”。也就是说，在反序列化期间，格式化器将调用它尝试实例化的类型。如果你的类型没有提供特殊构造函数，格式化器将扫描基类，直到找到一个实现了特殊构造函数的基类为止。

> **重要** 特殊构造函数中的代码通常从传递给它的 `SerializationInfo` 对象中提取字段。随着字段的提取，你无法保证它们已经完全被反序列化，因此特殊构造函数中的代码不应尝试操作这些提取出的对象。

如果你必须访问所提取对象的成员（例如调用方法），建议让你的类型提供一个应用了 `[OnDeserialized]` 特性的方法，或者让你的类型实现 `IDerializationCallback` 接口的 `OnDeserialization` 方法（如 `Dictionary` 示例所示）。当此方法被调用时，所有所有对象的字段都已设置。然而，无法保证哪些对象调用了 `OnDeserialized` 或 `OnDeserialization` 方法。因此，虽然字段可能已经初始化，但如果被引对象也提供了 `OnDeserialized` 方法或实现了 `IDerializationCallback` 接口，你仍然不知道该引用对象是否已完全反序列化。

# 如何在基类型未实现此接口时定义实现 Serializable 的类型

正如前面介绍的，`ISerializable` 接口非常强大，因为它允许类型对被序列化和反序列化的该类型实例进行完全控制。然而，这种力量是有代价的：该类型还负责序列化其基类的所有字段。如果基类也实现了 `Serializable` 接口，那么序列化基类的字段是非常简单的；你只需要调用基类的 `GetObjectData` 方法即可。
