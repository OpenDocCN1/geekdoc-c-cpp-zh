
cast the serialized (or original) type to an IConvertible interface and then calls the appropriate interface method. Therefore, to allow objects of a serializable type to be deserialized as a different type, you may want to consider having your type implement the IConvertible interface. Note that the FormatterConverter is used when deserializing objects and when you're calling a Get method type that doesn't match the type of value in the stream.

Instead of calling the various Get methods previously listed, the special constructor could call GetEnumerator, which returns a System.Runtime.Serialization.InfoEnumerator that can be used to iterate through all the values contained within the SerializationInfo object. Each value enumerated is a System.Runtime.Serialization.SerializationEntry object.

Of course, you are welcome to define a type of your own that derives from a ISerializable and special constructor. If your type also implements ISerializable, your implementation of GetObjectData and your implementation of the special constructor must call the same functions in the base class in order for the object to be serialized and deserialized properly. Do not forget to do this or the objects will not serialize or deserialize correctly. The next section explains how to properly define an ISerializable type whose base doesn't implement this interface.

If your type doesn't have any fields in it and therefore has no special serialization/deserialization needs, GetObjectData is virtual and do not have to implement ISerializable at all. Like all interface members, the formatter treats the special constructor as "virtualized". That is, during deserialization, the formatter will call the type that it is trying to instantiate. If your type doesn't offer the special constructor, then the formatter will scan base classes until it finds one that implements the special constructor.

> **Important** The code in the special constructor typically extracts its fields from the SerializationInfo object that is passed to it. As the fields are extracted, you are not guaranteed that they are fully deserialized, so the code in the special constructor should not attempt to manipulate the objects that extracts.

If you must access members (such as call methods) on an extracted object, it is recommended that your type provide a method that has the OnDeserialized attribute applied to it or have your type implement the IDerializationCallback-interface's OnDeserialization method (as shown in the Dictionary example). When this method is called, all objects have had their fields set. However, there is no guarantee to which objects have their OnDeserialized or OnDeserialization method called. So, although the fields may be initialized, you still don't know if a referenced object is completely deserialized if that referenced object also provides an OnDeserialized method or implements the IDerializationCallback interface.

# How to Define a Type That Implements Serializable When the Base Type Doesn't Implement This Interface

As mentioned earlier, the ISerializable interface is extremely powerful, because it allows a type to take complete control over instances of the type serialized and deserialized. However, this power comes at cost: The type is responsible for serializing all of its base type's fields as well. Serializing the base type's fields is easy if the base type also implements the Serializable interface; you just call the base type's GetObjectData method.

However, someday, you may find yourself defining a type that needs to control of its serialization, but whose base type does't implement the Serializable interface. In this case, your derived class must manually serialize the base type's fields by grabbing their values and adding them to the SerializationInfo collection. Then, in your constructor, you will also have to get the values out of the constructor and set the base class's fields. Doing all of this is easy (albeit tedious) if the base class's fields are public or protected, but it can be very difficult or impossible to the base class's fields are private.

This following code shows how properly implement Serializable's GetObject method and its implied constructor so that the base type's fields are serialized.

```sharp
[Serializable]
internal class Base {
    protected String m_name = "Jeff";
    public Base() { /* Make the type instantiable */ }
}

[Serializable]
internal sealed class Derived : Base, ISerializable {
    private DateTime m_date = DateTime.Now;
    public Derived() { /* Make the type instantiable */ }

    // If this constructor didn't exist, we'd get a SerializationException
    // This constructor should be protected if it was not sealed
    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    private Derived(SerializationInfo info, StreamingContext context) {
        // Get the set of members for our class and base classes
        Type baseType = this.GetType();
        MemberInfo[] mi = FormatterServices.GetSerializableMembers(baseType, context);
        // Deserialize the base class's fields from the info object
        for (Int32 i = 0; i < mi.Length; i++) {
            // Get the field and set it to the deserialized value
            FieldInfo fi = (FieldInfo)info[i];
            fi.SetValue(this, info.GetValue(baseType.FullName + "+" + fi.Name, fi.FieldType));
        }

        // Deserialize the values that were serialized for this class
        m_date = (DateTime)info.GetValue("Date");
    }
}
```

```sharp
[SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
public virtual void GetObjectData(SerializationInfo info, StreamingContext context) {
    // Serialize the default values for this class
    info.AddValue("Date", m_date);

    // Get the set of serializable members for our class and base classes
    Type baseType = this.GetType().BaseType;
    MemberInfo[] mi = FormatterServices.GetSerializableMembers(baseType, context);

    // Serialize the base class's fields to the info object
    for (Int i = 0; i < mi.Length; i++) {
        // Prefix the field name with the fullname of the base type
        info.AddValue(baseType.FullName + "-" + mi[i].Name,
            (FieldInfo)mi[i].GetValue(this));
    }
}
public override string ToString() {
    return String.Format("Name={0}, Date={1}", m_name, m_date);
}
```

In this code, there is a base class, which is marked only with the SerializableAttribute custom attribute. Derived from Base is Derived, which is also marked with the Serializable-Attribute attribute and implements the ISerializable interface. To make the situation more interesting, you'll notice that both classes define a String called m_name. When calling SerializationInfo's AddValue, you can't add multiple values with the same name. The preceding code handles this by identifying each by class name prepended to the field's name. For example, when the GetObjectData method calls AddValue to serialize Base's m_name field, the name of the value is written as "Base+m_name."

# Streaming Contexts

As mentioned earlier, there are many destinations for a serialized set of objects: same process, different process on the same machine, different process on a different machine, and so on. In some cases, an object might want to know where it is going to be serialized so it can emit its state differently. For example, an object that wraps a Windows semaphore object might decide to serialize its kernel handle if the object knows that it is serialized into the same process, because kernel handles are valid within a process. However, the object might decide to serialize the semaphore's name if it knows that the object will be serialized on the same machine but into a different process. Finally, the object might decide to throw an exception if it knows that it is serialized in a process running on a different machine because a semaphore is valid only within a single machine.

A number of methods mentioned earlier in this chapter accept a StreamingContext. A StreamingContext structure is a very simple value type offering two public read-only-properties, as shown in Table 24-1.
