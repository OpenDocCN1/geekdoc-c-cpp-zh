
```csharp
        // Build cache of RuntimeMethodHandles for all MethodInfo objects
        List<RuntimeMethodHandle> methodHandles =
            methodInfos.ConvertAll<RuntimeMethodHandle>(mb => mb.MethodHandle);

        Show("Holding MethodInfo and RuntimeMethodHandle cache");
        GC.KeepAlive(methodInfos);  // Prevent cache from being GC'd early

        methodInfos = null;         // Allow cache to be GC'd now
        Show("After freeing MethodInfo objects");

        methodInfos = methodHandles.ConvertAll<MethodBase>(
            ram => MethodBase.GetMethodFromHandle(ram));
        Show("Size of heap after re-creating MethodInfo objects");
        GC.KeepAlive(methodHandles); // Prevent cache from being GC'd early
        GC.KeepAlive(methodInfos);   // Prevent cache from being GC'd early

        methodHandles = null;       // Allow cache to be GC'd now
        methodInfos = null;         // Allow cache to be GC'd now
        Show("After freeing MethodInfos and RuntimeMethodHandles");
    }
```

When I compiled and executed this program, I got the following output.

```text
Heap size=      85,000 - Before doing anything
# of methods=48,467
Heap size=   7,065,632 - After building cache of MethodInfo objects
Heap size=   7,453,496 - Holding MethodInfo and RuntimeMethodHandle cache
Heap size=   6,732,704 - After freeing MethodInfo objects
Heap size=   7,372,704 - Size of heap after re-creating MethodInfo objects
Heap size=     192,232 - After freeing MethodInfos and RuntimeMethodHandles
```

## Runtime Serialization

In this chapter:

- Serialization/Deserialization Quick Start . . . . . . . . . . . . . . . . . . . . 613
- Making a Type Serializable. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 617
- Controlling Serialization and Deserialization. . . . . . . . . . . . . . . . . . . . . 619
- How Formatters Serialize Type Instances . . . . . . . . . . . . . . . . . . . . . . . 623
- Controlling the Serialized/Deserialized Data. . . . . . . . . . . . . . . . . . . . . 624
- Streaming Contexts . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 631
- Serializing a Type As a Different Type and Deserializing an Object As a Different Object. . . . . . . . . . . . . 633
- Serialization Surrogates . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 636
- Overriding the Assembly and/or Type When Deserializing an Object. . . . . . . . . . . . . . . . . 640

*Serialization* is the process of converting an object or a graph of connected objects into a stream of bytes. *Deserialization* is the process of converting a stream of bytes back into its graph of connected objects. The ability to convert objects to and from a byte stream is an incredibly useful mechanism. Here are some examples:

- An application's state (object graph) can easily be saved in a disk file or database and then restored the next time the application is run. ASP.NET saves and restores session state by way of serialization and deserialization.
- A set of objects can easily be copied to the system's clipboard and then pasted into the same or another application. In fact, Windows Forms and Windows Presentation Foundation (WPF) use this.
- A set of objects can be cloned and set aside as a "backup" while a user manipulates the "main" set of objects.
- A set of objects can easily be sent over the network to a process running on another machine. The Microsoft .NET Framework's remoting architecture serializes and deserializes objects that are marshaled by value. It is also used to send objects across AppDomain boundaries, as discussed in Chapter 22, "CLR Hosting and AppDomains."

In addition to the preceding examples, after you have serialized objects in a byte stream in memory, it is quite easy to process the data in more useful ways, such as encrypting and compressing the data.

With serialization being so useful, it is no wonder that many programmers have spent countless hours developing code to perform these types of actions. Historically, this code is difficult to write and is extremely tedious and error-prone. Some of the difficult issues that developers need to grapple with are communication protocols, client/server data type mismatches (such as little-endian/big-endian issues), error handling, objects that refer to other objects, in and out parameters, arrays of structures, and the list goes on.

Well, you'll be happy to know that the .NET Framework has fantastic support for serialization and deserialization built right into it. This means that all of the difficult issues just mentioned are now handled completely and transparently by the .NET Framework. As a developer, you can work with your objects before serialization and after deserialization and have the .NET Framework handle the stuff in the middle.

In this chapter, I explain how the .NET Framework exposes its serialization and deserialization services. For almost all data types, the default behavior of these services will be sufficient, meaning that it is almost no work for you to make your own types serializable. However, there is a small minority of types where the serialization service's default behavior will not be sufficient. Fortunately, the serialization services are very extensible, and I will also explain how to tap into these extensibility mechanisms, allowing you to do some pretty powerful things when serializing or deserializing objects. For example, I'll demonstrate how to serialize Version 1 of an object out to a disk file and then deserialize it a year later into an object of Version 2.

> **Note** This chapter focuses on the runtime serialization technology in the common language runtime (CLR), which has a deep understanding of CLR data types and can serialize all the public, protected, internal, and even private fields of an object to a compressed binary stream for high performance. See the `System.Runtime.Serialization.NetDataContractSerializer` class if you want to serialize CLR data types to an XML stream. The .NET Framework also offers other serialization technologies that are designed more for interoperating between CLR data types and non-CLR data types. These other serialization technologies use the `System.Xml.Serialization.XmlSerializer` class and the `System.Runtime.Serialization.DataContractSerializer` class.

### Serialization/Deserialization Quick Start

Let’s start off by looking at some code.

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

    private static MemoryStream SerializeToMemory(Object objectGraph) {
        // Construct a stream that is to hold the serialized objects
        MemoryStream stream = new MemoryStream();

        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to serialize the objects into the stream
        formatter.Serialize(stream, objectGraph);

        // Return the stream of serialized objects back to the caller
        return stream;
    }

    private static Object DeserializeFromMemory(Stream stream) {
        // Construct a serialization formatter that does all the hard work
        BinaryFormatter formatter = new BinaryFormatter();

        // Tell the formatter to deserialize the objects from the stream
        return formatter.Deserialize(stream);
    }
}
```
