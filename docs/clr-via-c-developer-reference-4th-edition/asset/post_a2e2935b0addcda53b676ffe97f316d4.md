
run-time handle instance and vice versa. Fortunately, this is easy using the following conversion methods and properties:

- To convert a Type to a RuntimeHandle, call Type's static GetTypeHandle method passing in the reference to the Type object.
- To convert a RuntimeHandle to a Type object, call Type's static GetTypeFromHandle method passing in the RuntimeHandle.
- To convert a FieldInfo object to a RuntimeFieldHandle, query FieldInfo's instance read-only FieldHandle property.
- To convert a RuntimeHandle to a FieldInfo object, call FieldInfo's static GetFieldFromHandle method.
- To convert a MethodInfo object to a RuntimeMethodHandle, query MethodInfo's instance read-only MethodHandle property.
- To convert a RuntimeHandle to a MethodInfo object, call MethodInfo's static GetMethodFromHandle method.

The following program sample acquires a lot of MethodInfo objects, converts them to RuntimeMethodHandle instances, and shows the working set difference.

```c
using System;
using System.Reflection;
using System.Collections.Generic;

public sealed class Program {
    private const BindingFlags c_bf = BindingFlags.FlattenHierarchy | BindingFlags.Instance |
    BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic;

    public static void Main() {
        // Show size of heap before doing any reflection stuff
        Show("Before doing anything");

        // Build cache of MethodInfo objects for all methods in MSCorlib.dll
        List<MethodBase> methodInfos = new List<MethodBase>();
        foreach (Type t in typeof(object).Assembly.GetExportedTypes()) {
            if (t.IsGenericTypeDefinition) continue;
            MethodBase[] mb = t.GetMethods(c_bf);
            methodInfos.AddRange(mb);
        }

        // Show number of methods and size of heap after binding to all methods
        Console.WriteLine("# of methods={0:N}", methodInfos.Count);
        Show("After building cache of MethodInfo objects");
    }
```

```csharp
// Build cache for RuntimeMethodHandles for all MethodInfo objects
List<RuntimeMethodHandle> methodHandles =
methodInfos.ConvertAll<RuntimeMethodHandle>(mb => mb.RuntimeMethodHandle);
```

```csharp
Show("Holding MethodInfo and RuntimeMethodHandle cache");
GC.KeepAlive(methodInfos); // Prevent cache from being GC early

methodInfos = null; // Allow cache to be GC now
Show("After freeing MethodInfo objects");

methodInfos = methodHandles.ConvertAll<MethodBase>(
mh => MethodBase.GetHandle(rmh));
Show("Size of heap after re-creating MethodInfo objects");
GC.KeepAlive(methodHandles); // Prevent cache from being GC early
GC.KeepAlive(methodInfos); // Prevent cache from being GC early

methodHandles = null; // Allow cache to be GC now
methodInfos = null; // Allow cache to be GC now
Show("After freeing MethodInfos and RuntimeMethodHandles");
```

When I compiled and executed this program, I got the following output:

```
Heap size=85,000 - Before doing anything
# of methods=48,407
Heap size=7,065,632 - After building cache of MethodInfo objects
Heap size=7,453,496 - Holding MethodInfo and RuntimeMethodHandle cache
Heap size=6,732,704 - After freeing MethodInfo objects
Heap size=7,372,704 - Size of heap after re-creating MethodInfo objects
Heap size=192,232 - After freeing MethodInfos and RuntimeMethodHandles
```

# CHAPTER 24

# Runtime Serialization

In this chapter:

- Serialization/Deserialization Quick Start ........................................ 613
Making a Type Serializable ..................................................................................... 617
Controlling Serialization and Deserialization ................................................... 619
How Formatters Serialize Type Instances ................................................................ 623
Controlling the Serialized/Deserialized Data ............................................................... 624
Streaming Contexts .............................................................................................. 631
Serializing a Type As a Different Type and
Deserializing an Object As a Different Object ................................................ 633
Serialization Surrogates ....................................................................................... 636
Overriding the Assembly/or Type .................................................................
When Deserializing an Object ................................................................................ 641

Serialization is the process of converting an object or a graph of connected objects into a stream of bytes. Deserialization is the process of converting a stream of bytes back into its graph of connected objects. The ability to convert objects to and from a byte stream is an incredibly useful mechanism. Here are some examples:

- An application's state (object graph) can be easily saved in a disk file or database and then restored the next time the application is run. ASP.NET saves and restores session state by way of serialization and deserialization.
- A set of objects can easily be copied to the system-clipboard and pasted into the same or another application. In fact, Windows Forms and Windows Presentation Foundation (WPF) use this.
- A set of objects can be cloned and set aside as a "backup" while a user manipulates the "main" set of objects.
- A set of objects can easily be sent over the network to a process running on another machine. The Microsoft .NET Framework's removing architecture serializes and deserializes objects that are marshaled by value. It is also used to send objects across AppDomain boundaries, as discussed in Chapter 22, "CLR Hosting and AppDomains."

In addition to the preceding examples, after you have serialized objects in a byte stream in memory, it is quite easy to process the data in more useful ways, such as encrypting and compressing the data.

With serialization being so useful, it is no wonder that many programmers have spent countless hours developing code to perform these types of actions. Historically, this code is difficult to write and is extremely tedious and error-prone. Some of the difficult issues developers need to grapple with communication protocols, client/server data type mismatches (such as little-endian/big-endian issues), error handling, objects that refer to other objects, and in out parameters, arrays of structures, and this goes on.

Well, you'll be happy to know that the .NET Framework has fantastic support for serialization and deserialization built right into it. This means that all of the difficult issues mentioned above are handled completely and transparently by the .NET Framework. As a developer, you can work with your objects before serialization and after deserialization and the .NET Framework handle the stuff in the middle.

In this chapter, I explain how the .NET Framework exposes its serialization and deserialization services. For almost all data types, the default behavior of these services will be sufficient, meaning it is almost no work for you to make your own serialization services. However, there is a small minority of types where the serialization service's default behavior will not be sufficient. Fortunately, the serialization services are very extensible, and I will also explain how to tap into this extensibility mechanisms to do some pretty powerful things when serializing or deserializing objects. For example, I'll demonstrate how to serialize Version 1 of an object out to a disk file and deserialize it later into an object of Version 2.

> Note This chapter focuses on the runtime serialization technology in the common language runtime (CLR), which has a deep understanding of CLR data types and can serialize all public, protected, internal, and even private fields of an object to a compressed binary stream for high performance. See the System.Runtime.Serialization.DataContractSerializer class if you want to serialize CLR data types to an XML stream. The .NET Framework also offers other serialization technologies that are designed for interoperating between CLR data types and non-CLR data types. These other serialization technologies use the System.Xml.Serialization.XmlSerializer class and the System.Runtime.Serialization.DataContractSerializer class.
