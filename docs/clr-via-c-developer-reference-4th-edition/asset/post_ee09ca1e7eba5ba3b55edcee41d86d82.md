
## TABLE 24-1 StreamingContext's Public Read-Only Properties

| Member Name | Member Type | Description |
|---|---|---|
| State | StreamingContextStates | A set of bit flags indicating the source or destination of the objects serialized/deserialized |
| Context | Object | A reference to object that contains any user-desired context information |

A method that receives a StreamingContext structure can examine the State property's bit flags to determine the source or destination of the objects serialized/deserialized. Table 24-2 shows the possible bit flag values.

## TABLE 24-2 StreamingContext's Flags

| Flag Name | Flag Value | Description |
|---|---|---|
| CrossProcess | 0x0001 | The source or destination is a different process on the same machine |
| CrossMachines | 0x0002 | The source or destination is on a different machine. |
| File | 0x0004 | The source or destination is a file. Don't assume that process will deserialize the data, and |
| Persistence | 0x0008 | The source or destination is a store as a database or file. Don't assume the same process will deserialize the data, and |
| Remoting | 0x0010 | The source or destination is remoting to an unknown location. The location may be on the same machine but also may be on another machine. |
| Other | 0x0020 | The source or destination is unknown. |
| Clone | 0x0040 | The object graph is cloned. The serialization code may assume the same process will deserialize the data, and it is safe to access handles or unmanaged resources. |
| CrossAppDomain | 0x0080 | The source or destination is a different AppDomain. |
| All | 0x00FF | The source or destination may be any of the above contexts. This is the default context. |

Now that you know how to get this information, let's discuss how you would set this information. The IFormatter interface (which is implemented by both the BinaryFormatter and the SoapFormatter types) defines a read/write StreamingContext property called Context. When you construct a formatter, it initializes its Context property so that StreamingContext-States is set to All and the reference to the additional state object is set to null.

After a formatter is constructed, you can construct a StreamingContext using any of the StreamingContext flags, and you can optionally pass a reference to an object containing any additional context information you need. Now, all you need to do is set the formatter's Context property with this new StreamingContext object before calling the formatter's Serialize or Deserialize methods. Code demonstrating how to tell a formatter that you are serializing/deserializing an object graph for the sole purpose of cloning all the objects in the graph is shown in the DeepClone method presented earlier in this chapter.

## Serializing a Type As a Different Type and Deserializing Object As a Different Object

.NET Framework's serialization infrastructure is quite rich, and in this section, we discuss how a developer can design a type that can serialize or deserialize itself into a different type or object. Below are some examples where this is interesting:

- Some types (as System.DBNull System.Reflection.Missing) are designed to have only one instance per AppDomain. These types are frequently called singletons. If you have a reference to a DBNull object, serializing and deserializing it should not cause a new DBNull object to be created in the AppDomain. After deserializing, the returned reference should refer to the AppDomain's already-existing DBNull object.

- Some types (as System.Type, System.Reflection.Assembly, and other reflection types like MemberInfo have one instance per type, assembly, member, and so on. Imagine you have an array where each element references a MemberInfo object. It's possible that five array elements reference a single MemberInfo object. After serializing and deserializing the array, the five elements referred to a single MemberInfo object should all refer to a single MemberInfo object. What's more, these elements should refer to the one MemberInfo object that exists for the specific member in the AppDomain. You could also imagine how this could be useful for polling database connection objects or any other type of object.

- For remotely controlled objects, the CLR serializes information about the server object, when deserialized by the client, causes the CLR to create a proxy object. This type of the proxy object is a different type than the server object, but this is transparent to the client. When the client calls instance methods on the proxy object, the proxy internally makes the call to the server that actually performs the request.

Let's look at some code that shows how to properly serialize and deserialize a singleton type.

```cs
// There should be only one instance of this type per AppDomain
[Serializable]
public sealed class Singleton : ISerializable {
    // This is the one instance of this type
    private static readonly Singleton s_theoneObject = new Singleton();

    // Here are the instance fields
    public String Name = "Jeff"
    public DateTime Date = DateTime.Now;

        // Private constructor allowing this type to construct the singleton
    private Singleton() { }

    // Method returning a reference to the singleton
    public static Singleton GetSingleton() { return s_theoneObject; }
```

```cs
// Method called when serializing an Explicit Interface Impl. Here
// I recommend using
[SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
void ISerializable.GetObjectData(SerializationInfo info, StreamingContext context) {
    info.SetType(SingletonSerializationHelper());
    // No other values needed to be added
}

[Serializable]
private sealed class SingletonSerializationHelper : IObjectReference {
// Method called after this object (which has no fields) is deserialized
public Object GetRealObject(StreamingContext context) {
    return Singleton.GetSingleton();
}
}
```

// NOTE: The special constructor is NOT necessary because it's never called

The Singleton class represents a type that allows only one instance of it to exist per App-Domain. The following code tests the Singleton's serialization and deserialization code to ensure that only one instance of the Singleton ever exists in the AppDomain.

```cs
private static void singletonTest() {
// Create an array with multiple elements referring to the one Singleton object
Singleton[] a = { Singleton.GetSingleton(), Singleton.GetSingleton() };
Console.WriteLine("Do both elements refer to the same object? " + (a[0] == a[1])); // "True"

using (var stream = new MemoryStream()) {
    BinaryFormatter formatter = new BinaryFormatter();

    // Serialize and deserialize the array elements
    formatter.Serialize(stream, a);
    stream.Position = 0;
    Singleton[] a2 = (Singleton[])formatter.Deserialize(stream);

    // Prove that it worked
    Console.WriteLine("Do both elements refer to the same object? " + (a2[0] == a2[1])); // "True"
    Console.WriteLine("Do all elements refer to the same object? " + (a[0] == a2[0])); // "True"
}
```

Now, let's walk through the code to understand what's happening. When the Singleton type is loaded into the AppDomain, the CLR calls its static constructor, which constructs a Singleton object and saves a reference to it in a static field, s_theoneObject. The Singleton class doesn't offer any public constructors, which prevents any other code from constructing other instances of this class.

Now, SingletonTest calls the formatter's Serialize method to serialize the array and its elements. When serializing the first Singleton, the formatter detects that the Singleton type implements the ISerializable interface and calls the GetDataObject method. This method calls SetType, passing in the SerializationHelper type, which tells the formatter to serialize the Singleton object as a SerializationHelper instead. Because AddValue is not called, no additional field information is written to the stream. The formatter automatically detected that array elements refer to a single object, the formatter serializes one object.

After serializing the array, SingletonTest calls the formatter's Deserializer method. When deserializing, the formatter tries to deserialize a SerializationHelper object because this is how the formatter was "triggered" into serializing. (In fact, this is why the Singleton class does not provide the special constructor that is usually required when implementing the ISerializable interface.) After constructing the SerializationHelper object, the formatter sees that this type implements the System.Runtime.IObjectReference interface. This interface is defined in the FCL as:

```cs
public interface IObjectReference {
    Object GetRealObject(StreamingContext context);
}
```

When types implement this interface, the formatter calls the GetRealObject method. This method returns a reference to the object that you really want a reference now deserialization of the object has completed. In my example, the SerializationHelper type GetRealObject returns a reference to the Singleton object that already exists in the AppDomain. So, when the formatter's Deserialize method returns, a2 array contains two elements, both of which refer to the AppDomain's Singleton object. The SerializationHelper object used to help with the deserialization is immediately unreachable and will be garbage collected in the future.

The second call to WriteLine displays "True," verifying that a2's array elements refer to the same object. The third and last call to WriteLine also displays "True," proving that the elements in both arrays refer to the exact same object.
