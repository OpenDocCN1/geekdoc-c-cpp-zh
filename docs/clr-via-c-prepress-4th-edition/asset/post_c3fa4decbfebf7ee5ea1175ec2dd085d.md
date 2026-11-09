
```text
Heap size=      85,000 - Before doing anything
# of methods=48,467
Heap size=    7,065,632 - After building cache of MethodInfo objects
Heap size=    7,453,496 - Holding MethodInfo and RuntimeMethodHandle cache
Heap size=    6,732,704 - After freeing MethodInfo objects
Heap size=    7,372,704 - Size of heap after re-creating MethodInfo objects
Heap size=      192,232 - After freeing MethodInfos and RuntimeMethodHandles
```

## Chapter 24: Runtime Serialization

In this chapter:

- Serialization/Deserialization Quick Start 662
- Making a Type Serializable 667
- Controlling Serialization and Deserialization 668
- How Formatters Serialize Type Instances 672
- Controlling the Serialized/Deserialized Data 673
- Streaming Contexts 680
- Serializing a Type as a Different Type and Deserializing an Object as a Different Object 682
- Serialization Surrogates 684
- Overriding the Assembly and/or Type When Deserializing an Object 689

Serialization is the process of converting an object or a graph of connected objects into a stream of bytes. Deserialization is the process of converting a stream of bytes back into its graph of connected objects. The ability to convert objects to and from a byte stream is an incredibly useful mechanism. Here are some examples:

- An application's state (object graph) can easily be saved in a disk file or database and then restored the next time the application is run. ASP.NET saves and restores session state by way of serialization and deserialization.
- A set of objects can easily be copied to the system's clipboard and then pasted into the same or another application. In fact, Windows Forms and Windows Presentation Foundation (WPF) use this.
- A set of objects can be cloned and set aside as a “backup” while a user manipulates the “main” set of objects.
- A set of objects can easily be sent over the network to a process running on another machine. The Microsoft .NET Framework’s remoting architecture serializes and deserializes objects that are marshaled by value. It is also used to send objects across AppDomain boundaries, as discussed in Chapter 22, “CLR Hosting and AppDomains.”

In addition to the above, once you have serialized objects in a byte stream in memory, it is quite easy to process the data in more useful ways, such as encrypting and compressing the data.

With serialization being so useful, it is no wonder that many programmers have spent countless hours developing code to perform these types of actions. Historically, this code is difficult to write and is extremely tedious and error-prone. Some of the difficult issues that developers need to grapple with are communication protocols, client/server data type mismatches (such as little-endian/big-endian issues), error handling, objects that refer to other objects, in and out parameters, arrays of structures, and the list goes on.

Well, you’ll be happy to know that the .NET Framework has fantastic support for serialization and deserialization built right into it. This means that all of the difficult issues mentioned above are now handled completely and transparently by the .NET Framework. As a developer, you can work with your objects before serialization and after deserialization and have the .NET Framework handle the stuff in the middle.

In this chapter, I explain how the .NET Framework exposes its serialization and deserialization services. For almost all data types, the default behavior of these services will be sufficient, meaning that it is almost no work for you to make your own types serializable. However, there is a small minority of types where the serialization service’s default behavior will not be sufficient. Fortunately, the serialization services are very extensible, and I will also explain how to tap into these extensibility mechanisms, allowing you to do some pretty powerful things when serializing or deserializing objects. For example, I’ll demonstrate how to serialize Version 1 of an object out to a disk file and then deserialize it a year later into an object of Version 2.

**Note** This chapter focuses on the runtime serialization technology in the common language runtime (CLR), which has a deep understanding of CLR data types and can serialize all the public, protected, internal, and even private fields of an object to a compressed binary stream for high performance. See the `System.Runtime.Serialization.NetDataContractSerializer` class if you wish to serialize CLR data types to an XML stream. The .NET Framework also offers other serialization technologies that are designed more for interoperating between CLR data types and non-CLR data types. These other serialization technologies use the `System.Xml.Serialization.XmlSerializer` class and the `System.Runtime.Serialization.DataContractSerializer` class.

### Serialization/Deserialization Quick Start

Let's start off by looking at some code:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;

internal static class QuickStart {
    public static void Main() {
        // Create a graph of objects to serialize them to the stream
        var objectGraph = new List<String> { "Jeff", "Kristin", "Aidan", "Grant" };
        Stream stream = SerializeToMemory(objectGraph);

        // Reset everything for this demo
        stream.Position = 0;
        objectGraph = null;

        // Deserialize the objects and prove it worked
        objectGraph = (List<String>) DeserializeFromMemory(stream);
        foreach (var s in objectGraph) Console.WriteLine(s);
    }

    private static MemoryStream SerializeToMemory(object objectGraph) {
        // Construct a stream that is to hold the serialized objects
        MemoryStream stream = new MemoryStream();

        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to serialize the objects into the stream
        formatter.Serialize(stream, objectGraph);

        // Return the stream of serialized objects back to the caller
        return stream;
    }

    private static object DeserializeFromMemory(Stream stream) {
        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to deserialize the objects from the stream
        return formatter.Deserialize(stream);
    }
}
```

Wow, look how simple this is! The `SerializeToMemory` method constructs a `System.IO.MemoryStream` object. This object identifies where the serialized block of bytes is to be placed. Then the method constructs a `BinaryFormatter` object (which can be found in the `System.Runtime.Serialization.Formatters.Binary` namespace). A formatter is a type (implementing the `System.Runtime.Serialization.IFormatter` interface) that knows how to serialize and deserialize an object graph. The Framework Class Library (FCL) ships with two formatters: the `BinaryFormatter` (used in this code example) and a `SoapFormatter` (which can be found in the `System.Runtime.Serialization.Formatters.Soap` namespace and is implemented in the `System.Runtime.Serialization.Formatters.Soap.dll` assembly).

**Note** As of version 3.5 of the .NET Framework, the `SoapFormatter` class is obsolete and should not be used in production code. However, it can still be useful for debugging serialization code as it produces XML text which you can read. To use XML serialization and deserialization in production code, use the `XmlSerializer` and `DataContractSerializer` classes.

To serialize a graph of objects, just call the formatter’s `Serialize` method and pass it two things: a reference to a stream object and a reference to the object graph that you wish to serialize. The stream object identifies where the serialized bytes should be placed and can be an object of any type derived from the `System.IO.Stream` abstract base class. This means that you can serialize an object graph to a `MemoryStream`, a `FileStream`, a `NetworkStream`, and so on.

The second parameter to `Serialize` is a reference to an object. This object could be anything: an `Int32`, a `String`, a `DateTime`, an `Exception`, a `List<String>`, a `Dictionary<Int32, DateTime>`, and so on. The object referred to by the `objectGraph` parameter may refer to other objects. For example, `objectGraph` may refer to a collection that refers to a set of objects. These objects may also refer to other objects. When the formatter’s `Serialize` method is called, all objects in the graph are serialized to the stream.

Formatters know how to serialize the complete object graph by referring to the metadata that describes each object’s type. The `Serialize` method uses reflection to see what instance fields are in each object’s type as it is serialized. If any of these fields refer to other objects, then the formatter’s `Serialize` method knows to serialize these objects, too.

Formatters have very intelligent algorithms. They know to serialize each object in the graph no more than once out to the stream. That is, if two objects in the graph refer to each other, then the formatter detects this, serializes each object just once, and avoids entering into an infinite loop.

In my `SerializeToMemory` method, when the formatter’s `Serialize` method returns, the `MemoryStream` is simply returned to the caller. The application uses the contents of this flat byte array any way it desires. For example, it could save it in a file, copy it to the clipboard, send it over a wire, or whatever.

The `DeserializeFromMemory` method deserializes a stream back into an object graph. This method is even simpler than serializing an object graph. In this code, a `BinaryFormatter` is
