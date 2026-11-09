```
~~~csharp
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
~~~
```

Wow, look how simple this is! The **SerializeToMemory** method constructs a **System.IO.MemoryStream** object. This object identifies where the serialized block of bytes is to be placed. Then the method constructs a **BinaryFormatter** object (which can be found in the **System.Runtime.Serialization.Formatters.Binary** namespace). A formatter is a type (implementing the **System.Runtime.Serialization.IFormatter** interface) that knows how to serialize and deserialize an object graph. The Framework Class Library (FCL) ships with two formatters: the **BinaryFormatter** (used in this code example) and a **SoapFormatter** (which can be found in the **System.Runtime.Serialization.Formatters.Soap** namespace and is implemented in the System.Runtime.Serialization.Formatters.Soap.dll assembly).

> > **Note** As of version 3.5 of the .NET Framework, the **SoapFormatter** class is obsolete and should not be used in production code. However, it can still be useful for debugging serialization code as it produces XML text which you can read. To use XML serialization and deserialization in production code, see the **XmlSerializer** and **DataContractSerializer** classes.

To serialize a graph of objects, just call the formatter's **Serialize** method and pass it two things: a reference to a stream object and a reference to the object graph that you wish to