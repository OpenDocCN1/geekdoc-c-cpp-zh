# Controlling Serialization and Deserialization

When you apply the `SerializableAttribute` custom attribute to a type, all instance fields (public, private, protected, and so on) are serialized.³⁴ However, a type may define some instance fields that should not be serialized. In general, there are two reasons why you would not want some of a type’s instance fields to be serialized:

+   - The field contains information that would not be valid when deserialized. For example, an object that contains a handle to a Windows kernel object (such as a file, process, thread, mutex, event, semaphore, and so on) would have no meaning when deserialized into another process or machine since Windows' kernel handles are process-relative values.
+   
+   - The field contains information that is easily calculated. In this case, you select which fields do not need to be serialized, thus improving your application’s performance by reducing the amount of data transferred.

The code below uses the `System.NonSerializedAttribute` custom attribute to indicate which fields of the type should not be serialized. (Note that this attribute is also defined in the `System` namespace, not the `System.Runtime.Serialization` namespace.)

```
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

...
```
```

In the code above, objects of `Circle` may be serialized. However, the formatter will serialize the values in the object’s `m_radius` field only. The value in the `m_area` field will not be serialized because it has the `NonSerializedAttribute` applied to it. This attribute can be applied only to a type’s fields, and it continues to apply to this field when inherited by another type. Of course, you may apply the `NonSerializedAttribute` attribute to multiple fields within a type.

So, let’s say that our code constructs a `Circle` object as follows:

³⁴ Do not use C#’s automatically implemented property feature to define properties inside types marked with the `[Serializable]` attribute, because the compiler generates the names of the fields and the generated names can be different each time that you recompile your code, preventing instances of your type from being deserializable.