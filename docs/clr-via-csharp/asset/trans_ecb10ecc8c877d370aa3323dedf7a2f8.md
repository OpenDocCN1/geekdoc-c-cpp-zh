
如果你的类是**密封**的，那么强烈建议你将这个特殊构造函数声明为**私有**。这将防止任何代码意外调用它，从而提高安全性。如果不是密封的，则应将这个特殊构造函数声明为**受保护**，以便只有派生类才能调用它。请注意，无论该特殊构造函数如何声明，格式化器都能够调用它。

这个构造函数接收一个对 **SerializationInfo** 对象的引用，该对象包含对象序列化时添加给它的所有值。特殊构造函数可以调用 **GetBoolean**、**GetChar**、**GetByte**、**GetSByte**、**GetInt16**、**GetUInt16**、**GetInt32**、**GetUInt32**、**GetInt64**、**GetUInt64**、**GetSingle**、**GetDouble**、**GetDecimal**、**GetDateTime**、**GetString** 和 **GetValue** 方法中的任意一个，并传入一个字符串，该字符串对应于序列化某个值时使用的名称。然后，每个方法返回的值用于初始化新对象的字段。

反序列化对象的字段时，应调用与对象序列化时传递给 **AddValue** 方法的值类型相匹配的 **Get** 方法。换句话说，如果 **GetObjectData** 方法调用了 **AddValue** 并传入了一个 **Int32** 值，那么在反序列化该对象时，应对同一个值调用 **GetInt32** 方法。如果流中值的类型与你尝试获取的类型不匹配，则格式化器会尝试使用 **IFormatterConverter** 对象将流中的值“强制转换”为所需类型。

如前所述，构造 **SerializationInfo** 对象时，会向它传递一个其类型实现 **IFormatterConverter** 接口的对象。由于格式化器负责构造 **SerializationInfo** 对象，因此它会选择自己想要的任何 **IFormatterConverter** 类型。Microsoft 的 **BinaryFormatter** 和 **SoapFormatter** 类型始终构造 **System.Runtime.Serialization.FormatterConverter** 类型的实例。Microsoft 的格式化器不提供任何让你选择其他 **IFormatterConverter** 类型的方法。

**FormatterConverter** 类型调用 **System.Convert** 类的静态方法在核心类型之间转换值，例如将 **Int32** 转换为 **Int64**。然而，要在其他任意类型之间转换值，**FormatterConverter** 会调用 **Convert** 的 **ChangeType** 方法，将序列化（或原始）类型强制转换为 **IConvertible** 接口，然后调用相应的接口方法。因此，若要允许可序列化类型的对象被反序列化为另一种类型，你可能需要考虑让你的类型实现 **IConvertible** 接口。请注意，只有在反序列化对象以及调用类型与流中值类型不匹配的 **Get** 方法时，才会使用 **FormatterConverter** 对象。

特殊构造函数可以不调用上面列出的各种 **Get** 方法，而是调用 **GetEnumerator**，它返回一个 **System.Runtime.Serialization.SerializationInfoEnumerator** 对象，可用于遍历 **SerializationInfo** 对象中包含的所有值。枚举的每个值都是一个 **System.Runtime.Serialization.SerializationEntry** 对象。

当然，欢迎你定义自己的类型，该类型派生自实现了 `ISerializable` 的 `GetObjectData` 和特殊构造函数的类型。如果你的类型也实现 `ISerializable`，那么你对 `GetObjectData` 的实现和对特殊构造函数的实现必须调用基类中的相同函数，以便对象能够正确序列化和反序列化。不要忘记这样做，否则对象将无法正确序列化或反序列化。下一节将说明如何正确定义基类型未实现此接口的 `ISerializable` 类型。

如果你的派生类型中没有任何额外字段，因此没有特殊的序列化/反序列化需求，那么你完全不必实现 `ISerializable`。与所有接口成员一样，`GetObjectData` 是虚方法，将被调用以正确序列化对象。此外，格式化器将特殊构造函数视为“虚拟化的”。也就是说，在反序列化期间，格式化器会检查它尝试实例化的类型。如果该类型未提供特殊构造函数，则格式化器会扫描基类，直到找到实现了特殊构造函数的基类。

> **重要** 特殊构造函数中的代码通常从传递给它的 `SerializationInfo` 对象中提取字段。在提取字段时，不能保证这些对象已完全反序列化，因此特殊构造函数中的代码不应尝试操作它提取出的对象。
>
> 如果你的类型必须访问提取出的对象上的成员（例如调用方法），则建议你的类型还提供一个应用了 `OnDeserialized` 特性的方法，或者让你的类型实现 `IDeserializationCallback` 接口的 `OnDeserialization` 方法（如 `Dictionary` 示例所示）。调用此方法时，所有对象的字段都已设置。但是，无法保证多个对象的 `OnDeserialized` 或 `OnDeserialization` 方法被调用的顺序。因此，虽然字段可能已初始化，但如果被引用的对象也提供了 `OnDeserialized` 方法或实现了 `IDeserializationCallback` 接口，你仍然不知道该被引用对象是否已完全反序列化。

## 如何在基类型未实现此接口时定义实现 `ISerializable` 的类型

如前所述，`ISerializable` 接口极其强大，因为它允许类型完全控制该类型的实例如何序列化和反序列化。然而，这种能力是有代价的。现在该类型还负责序列化其基类型的所有字段。如果基类型也实现 `ISerializable` 接口，那么序列化基类型的字段很容易；只需调用基类型的 `GetObjectData` 方法。

然而，有一天你可能会发现自己定义了一个需要控制其序列化的类型，但该类型的基类型未实现 `ISerializable` 接口。在这种情况下，派生类必须手动序列化基类型的字段：获取这些字段的值并将它们添加到 `SerializationInfo` 集合中。然后，在特殊构造函数中，你还必须从集合中取出这些值，并以某种方式设置基类的字段。如果基类的字段是公共或受保护的，那么完成所有这些工作很容易（尽管繁琐）；但如果基类的字段是私有的，则可能非常困难或根本无法做到。

以下代码展示了如何正确实现 ISerializable 的 GetObjectData 方法及其隐含的构造函数，以便序列化基类型的字段：

```csharp
[Serializable]
internal class Base {
    protected String m_name = "Jeff";
    public Base() { /* Make the type instantiable */ }
}

[Serializable]
internal class Derived : Base, ISerializable {
    private DateTime m_date = DateTime.Now;
    public Derived() { /* Make the type instantiable */ }

    // If this constructor didn't exist, we'd get a SerializationException
    // This constructor should be protected if this class were not sealed
    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    private Derived(SerializationInfo info, StreamingContext context) {
        // Get the set of serializable members for our class and base classes
        Type baseType = this.GetType().BaseType;
        MemberInfo[] mi = FormatterServices.GetSerializableMembers(baseType, context);

        // Deserialize the base class's fields from the info object
        for (Int32 i = 0; i < mi.Length; i++) {
            // Get the field and set it to the deserialized value
            FieldInfo fi = (FieldInfo)mi[i];
            fi.SetValue(this, info.GetValue(baseType.FullName + "+" + fi.Name, fi.FieldType));
        }

        // Deserialize the values that were serialized for this class
        m_date = info.GetDateTime("Date");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context) {
        // Serialize the desired values for this class
        info.AddValue("Date", m_date);

        // Get the set of serializable members for our class and base classes
        Type baseType = this.GetType().BaseType;
        MemberInfo[] mi = FormatterServices.GetSerializableMembers(baseType, context);

        // Serialize the base class's fields to the info object
        for (Int32 i = 0; i < mi.Length; i++) {
            // Prefix the field name with the fullname of the base type
            info.AddValue(baseType.FullName + "+" + mi[i].Name,
                ((FieldInfo)mi[i]).GetValue(this));
        }
    }
    public override String ToString() {
        return String.Format("Name={0}, Date={1}", m_name, m_date);
    }
}
```
