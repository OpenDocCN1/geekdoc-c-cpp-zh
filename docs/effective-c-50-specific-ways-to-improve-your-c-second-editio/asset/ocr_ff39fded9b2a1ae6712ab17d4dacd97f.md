```
private OtherClass otherThing;

private const int DEFAULT_VALUE = 5;
private int value2;

// public constructors elided.

// Private constructor used only
// by the Serialization framework.
private MyType(SerializationInfo info,
    StreamingContext cnxt)
{
    label = info.GetString("label");
    otherThing = (OtherClass)info.GetValue("otherThing",
        typeof(OtherClass));
    try
    {
        value2 = info.GetInt32("value2");
    }
    catch (SerializationException)
    {
        // Found version 1.
        value2 = DEFAULT_VALUE;
    }
}

[SecurityPermissionAttribute(SecurityAction.Demand,
    SerializationFormatter = true)]
void ISerializable.GetObjectData(SerializationInfo inf,
    StreamingContext cxt)
{
    inf.AddValue("label", label);
    inf.AddValue("otherThing", otherThing);
    inf.AddValue("value2", value2);
}
}
```

The serialization stream stores each item as a key/value pair. The code generated from the attributes uses the variable name as the key for each value. When you add the ISerializable interface, you must match the key name