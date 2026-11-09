```
```csharp
public Circle(Double radius) {
    m_radius = radius;
    m_area = Math.PI * m_radius * m_radius;
}

[OnDeserialized]
private void OnDeserialized(StreamingContext context) {
    m_area = Math.PI * m_radius * m_radius;
}
```
```

I've changed Circle so that it now contains a method marked with the System.Runtime.Serialization.OnDeserializedAttribute custom attribute.² Whenever an instance of a type is deserialized, the formatter checks whether the type defines a method with this attribute on it and then the formatter invokes this method. When this method is called, all the serializable fields will be set correctly, and they may be accessed to perform any additional work that would be necessary to fully deserialize the object.

In the preceding modified version of Circle, I made the OnDeserialized method simply calculate the area of the circle by using the m_radius field and place the result in the m_area field. Now, m_area will have the desired value of 314.159.

In addition to the OnDeserializedAttribute custom attribute, the System.Runtime.Serialization namespace also defines OnSerializingAttribute, OnSerializedAttribute, and OnDeserializingAttribute custom attributes, which you can apply to your type's methods to have even more control over serialization and deserialization. Here is a sample class that applies each of these attributes to a method.

```
```csharp
[Serializable]
public class MyType {
    Int32 x, y; [NonSerialized] Int32 sum;

    public MyType(Int32 x, Int32 y) {
        this.x = x; this.y = y; sum = x + y;
    }

    [OnDeserializing]
    private void OnDeserializing(StreamingContext context) {
        // Example: Set default values for fields in a new version of this type
    }

    [OnDeserialized]
    private void OnDeserialized(StreamingContext context) {
        // Example: Initialize transient state from fields
        sum = x + y;
    }

    [OnSerializing]
    private void OnSerializing(StreamingContext context) {
```
```

² Use of the System.Runtime.Serialization.OnDeserialized custom attribute is the preferred way of invoking a method when an object is deserialized, as opposed to having a type implement the System.Runtime.Serialization.IDeserializationCallback interface's OnDeserialization method.