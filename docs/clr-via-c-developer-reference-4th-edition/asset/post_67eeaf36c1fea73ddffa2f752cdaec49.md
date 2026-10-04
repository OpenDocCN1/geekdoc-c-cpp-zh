
Important Some extensible applications use Assembly.LoadFrom to load an assembly and then construct objects from types defined in the loaded assembly. These objects can be serialized without any trouble. However, when deserializing this stream, the formatter attempts to load the assembly by calling Assembly's Load method instead of calling LoadFrom. In most cases, the CLR will not be able to locate the assembly file, causing a SerializationException to be thrown. This catches many developers by surprise—because the objects serialized, the developers expect that the objects will deserialize correctly as well.

If your application serializes objects whose types are defined in an assembly that uses Assembly.LoadFrom, I recommend that you implement a method whose signature matches the System.ResolveEventHandler delegate and register this method with System.AppDomain.AssemblyResolve event just before calling a Deserialize method. Now, whenever the formatter fails to load an assembly, the CLR calls your ResolveEventHandler method. This method is passed the identity of the assembly that failed to load. The method can extract the file name from the assembly's identity and use it to construct the path where the application knows the assembly file can be found. Then, the method can call Assembly.LoadFrom to load the assembly and returning the Assembly reference back from the ResolveEventHandler method.

This section covers the basics of how to serialize and deserialize object graphs. In the remaining sections, we'll look at what you must do in order to define your serializable types, we'll also look at various mechanisms that allow you to have greater control over serialization and deserialization.

# Making a Type Serializable

When a type is designed, the developer must make the conscious decision as to whether or not allow instances of the type to be serializable. By default, types are not serializable. For example, the following code does not perform as expected.

```
internal struct Point { public Int32 x, y; }

private static void OptInSerialization() {
    Point pt = new Point { x = 1, y = 2 };
    using (var stream = new MemoryStream()) {
        new BinaryFormatter().Serialize(stream, pt); // throws SerializationException
    }
}
```

If you were to build and run this code in your program, you'd see that the formatter's Serialize method throws System.Runtime.Serialization.SerializationException. The problem is that the developer of the Point type has not explicitly indicated that Point objects may be serialized. To solve this problem, the developer must use the System.SerializableAttribute (Note that this attribute is defined in the System namespace, not the System.Runtime.Serialization namespace).

```c
[Serializable]
internal struct Point { Int32 x, y; }
```

Now, if we rebuild the application and run it, it does perform as expected and the Point objects will be serialized to the stream. When serializing an object graph, the formatter checks that every object's type is serializable. If any object in the graph is not serializable, the formatter's Serialize method throws SerializationException.

> When serializing a graph of objects, some of the objects' types may be serializable and some of the objects may not be serializable. For performance reasons, formatters not verify that all of the objects in the graph are serializable before serializing the graph. So, when serializing an object graph, it is entirely possible that some objects may be serialized to the stream before the SerializationException is thrown. If this happens, the stream contains corrupt data. If you think you may serializing an object graph where some objects may not be serializable, your application code could be able to recover gracefully from this situation. One option is to serialize the objects into a MemoryStream first. Then, if all objects are successfully serialized, you can copy the bytes in the MemoryStream to whatever stream (for example, file, network) you really want to write.

The SerializableAttribute custom attribute may be applied to reference types (class), value types (struct), enumerated types (enum), and delegate types (delegate) all serializable, (Note enumerated and delegate types there is no need to explicitly apply the SerializableAttribute to these types.) In addition, the SerializableAttribute is not inherited by derived types. So, given the following two type definitions, a Person object can be serialized, but an Employee object cannot.

```csharp
[Serializable]
internal class Person { ... }
```

```csharp
internal class Employee : Person { ... }
```

To fix this, you would just apply the SerializableAttribute attribute to the Employee type as well.

```csharp
[Serializable]
internal class Person { ... }
```

```csharp
[Serializable]
internal class Employee : Person { ... }
```

Note that this problem was easy to fix. However, the reverse—defining a type derived from a base type that doesn't have the SerializableAttribute applied to it—is not easy to fix. This is by design; if the base type doesn't allow instances of its type to be serialized, its fields cannot be serialized, because a base object is effectively part of the derived object. This is why System.Object has the SerializableAttribute attribute applied to it.

In general, it is recommended that all instance fields (public, private, protected, and so on) are serialized.

> Note: In general, it is recommended that most types define be serializable. After all, this grants a lot of flexibility to your types. However, you must be aware that serialization reads of an object's fields regardless of whether they are declared public, protected, internal, or private. You might not want to make a type serializable if it contains sensitive or secure data (like passwords) or if the data would have no meaning or value transferred.

If you find yourself using a type that was not designed for serialization, and you do not have the source code of the type to add serialization support, all is not lost. In "Overriding the Assembly and/or Type When Deserializing an Object" section later in this chapter, I will explain how you can make any non-serializable type serializable.

# Controlling Serialization and Deserialization

When you apply the Serializable attribute to a type, all instance fields (public, private, protected, and so on) are serialized. However, you may define some instance fields that should not be serialized. In general, there are two reasons why you would not want some of a type's instance fields to be serialized:

- The field contains information that would not be valid when deserialized. For example, an object that contains a handle to a Windows kernel object (such as a file, process, mutex, event, semaphore, and so on) would have no meaning when deserialized into another process or because Windows' kernel handles are process-relative values.

- The field contains information that is easily calculated. In this case, you select which fields are serialized, not to be serialized, improving your application's performance by reducing the amount of data transferred.

The following code uses the System.NonSerializedAttribute custom attribute to indicate which fields of the type should not be serialized. (Note that this attribute is also defined in the System namespace, not System.Runtime.Serialization namespace.)

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
```
