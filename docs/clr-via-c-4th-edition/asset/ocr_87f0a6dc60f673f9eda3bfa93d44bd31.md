```
```csharp
// Create a DateTime that represents the local time on the machine & serialize it
DateTime localTimeBeforeSerialize = DateTime.Now;
formatter.Serialize(stream, localTimeBeforeSerialize);

// The stream displays the Universal time as a string to prove it worked
stream.Position = 0;
Console.WriteLine(new StreamReader(stream).ReadToEnd());

// Deserialize the universal time string & convert it to a local DateTime
stream.Position = 0;
DateTime localTimeAfterDeserialize = (DateTime)formatter.Deserialize(stream);

// Prove it worked correctly:
Console.WriteLine("LocalTimeBeforeSerialize={0}", localTimeBeforeSerialize);
Console.WriteLine("LocalTimeAfterDeserialize={0}", localTimeAfterDeserialize);
    }
}
```
```

After steps 1 through 4 have executed, the formatter is ready to use the registered surrogate types. When the formatter's Serialize method is called, each object's type is looked up in the set maintained by the SurrogateSelector. If a match is found, then the ISerializationSurrogate object's GetObjectData method is called to get the information that should be written out to the stream.

When the formatter's Deserialize method is called, the type of the object about to be deserialized is looked up in the formatter's SurrogateSelector and if a match is found, then the ISerializationSurrogate object's SetObjectData method is called to set the fields within the object being deserialized.

Internally, a SurrogateSelector object maintains a private hash table. When AddSurrogate is called, the Type and StreamingContext make up the key and the ISerializationSurrogate object is the key's value. If a key with the same Type/StreamingContext already exists, then AddSurrogate throws an ArgumentException. By including a StreamingContext in the key, you can register one surrogate type object that knows how to serialize/deserialize a DateTime object to a file and register a different surrogate object that knows how to serialize/deserialize a DateTime object to a different process.

> > **Note** The BinaryFormatter class has a bug that prevents a surrogate from serializing objects with references to each other. To fix this problem, you need to pass a reference to your ISerializationSurrogate object to FormatterServices's static GetSurrogateForCyclicalReference method. This method returns an ISerializationSurrogate object, which you can then pass to the SurrogateSelector's AddSurrogate method. However, when you use the GetSurrogateForCyclicalReference method, your surrogate's SetObjectData method must modify the value inside the object referred to by SetObjectData's obj parameter and ultimately return null or obj to the calling method. The downloadable code that accompanies this book shows how to modify the UniversalTimeLocalTimeSerializationSurrogate class and the SerializationSurrogateDemo method to support cyclical references.