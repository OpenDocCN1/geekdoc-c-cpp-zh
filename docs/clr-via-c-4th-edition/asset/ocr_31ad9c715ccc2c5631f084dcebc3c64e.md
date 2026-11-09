```
```csharp
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
```

In this code, there is a base class, Base, which is marked only with the SerializableAttribute custom attribute. Derived from Base is Derived, which is also marked with the SerializableAttribute attribute and also implements the ISerializable interface. To make the situation more interesting, you'll notice that both classes define a String field called m_name. When calling SerializationInfo's AddValue method, you can't add multiple values with the same name. The preceding code handles this situation by identifying each field by its class name prepended to the field's name. For example, when the GetObjectData method calls AddValue to serialize Base's m_name field, the name of the value is written as "Base+m_name."

# ## Streaming Contexts

As mentioned earlier, there are many destinations for a serialized set of objects: same process, different process on the same machine, different process on a different machine, and so on. In some rare situations, an object might want to know where it is going to be deserialized so that it can emit its state differently. For example, an object that wraps a Windows semaphore object might decide to serialize its kernel handle if the object knows that it will be deserialized into the same process, because kernel handles are valid within a process. However, the object might decide to serialize the semaphore's string name if it knows that the object will be deserialized on the same machine but into a different process. Finally, the object might decide to throw an exception if it knows that it will be deserialized in a process running on a different machine because a semaphore is valid only within a single machine.

A number of the methods mentioned earlier in this chapter accept a StreamingContext. A StreamingContext structure is a very simple value type offering just two public read-only properties, as shown in Table 24-1.