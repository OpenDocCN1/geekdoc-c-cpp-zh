# How to Define a Type That Implements Serializable When the Base Type Doesn't Implement This Interface

As mentioned earlier, the ISerializable interface is extremely powerful, because it allows a type to take complete control over instances of the type serialized and deserialized. However, this power comes at cost: The type is responsible for serializing all of its base type's fields as well. Serializing the base type's fields is easy if the base type also implements the Serializable interface; you just call the base type's GetObjectData method.

However, someday, you may find yourself defining a type that needs to control of its serialization, but whose base type does not implement the Serializable interface. In this case, your derived class must manually serialize the base type's fields by grabbing their values and adding them to the SerializationInfo collection. Then, in your constructor, you will also have to get the values out of the constructor and set the base class's fields. Doing all of this is easy (albeit tedious) if the base class's fields are public or protected, but it can be very difficult or impossible to the base class's fields are private.

This following code shows how properly implement Serializable's GetObject method and its implied constructor so that the base type's fields are serialized.

```
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
```