serialize. The stream object identifies where the serialized bytes should be placed and can be an object of any type derived from the **System.IO.Stream** abstract base class. This means that you can serialize an object graph to a **MemoryStream**, a **FileStream**, a **NetworkStream**, and so on.

The second parameter to **Serialize** is a reference to an object. This object could be anything: an **Int32**, a **String**, a **DateTime**, an **Exception**, a **List<String>**, a **Dictionary<Int32, DateTime>**, and so on. The object referred to by the **objectGraph** parameter may refer to other objects. For example, **objectGraph** may refer to a collection that refers to a set of objects. These objects may also refer to other objects. When the formatter’s **Serialize** method is called, all objects in the graph are serialized to the stream.

Formatters know how to serialize the complete object graph by referring to the metadata that describes each object’s type. The **Serialize** method uses reflection to see what instance fields in each object’s type as it is serialized. If any of those fields refer to other objects, then the formatter’s **Serialize** method knows to serialize these objects, too.

Formatters have very intelligent algorithms. They know to serialize each object in the graph no more than once out to the stream. That is, if two objects in the graph refer to each other, then the formatter detects this, serializes each object just once, and avoids entering into an infinite loop.

In my **SerializeToMemory** method, when the formatter’s **Serialize** method returns, the **MemoryStream** is simply returned to the caller. The application uses the contents of this flat byte array any way it desires. For example, it could save it in a file, copy it to the clipboard, send it over a wire, or whatever.

The **DeserializeFromStream** method deserializes a stream back into an object graph. This method is even simpler than serializing an object graph. In this code, a **BinaryFormatter** is constructed and then its **Deserialize** method is called. This method takes the stream as a parameter and returns a reference to the root object within the deserialized object graph.

Internally, the formatter’s **Deserialize** method examines the contents of the stream, constructs instances of all the objects that are in the stream, and initializes the fields in all these objects so that they have the same values they had when the object graph was serialized. Typically, you will cast the object reference returned from the **Deserialize** method into the type that your application is expecting.

> **Note** Here’s a fun, useful method that uses serialization to make a deep copy, or clone, of an object:

```
```csharp
private static Object DeepClone(Object original) {
    // Construct a temporary memory stream
    using (MemoryStream stream = new MemoryStream()) {
```
```

![](bbox=[0.091, 0.808, 0.13, 0.844])