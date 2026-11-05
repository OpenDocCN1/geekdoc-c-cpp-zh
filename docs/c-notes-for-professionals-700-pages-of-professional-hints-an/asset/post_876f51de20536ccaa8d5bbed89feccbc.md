
```
AddOrMult(a, b, ref add, ref mult); //AddOrMult(a, b, out add, out mult);
Console.WriteLine(add); //5
Console.WriteLine(mult); //6
}

private static void AddOrMult(int a, int b, ref int add, ref int mult) //AddOrMult(int a, int b,
out int add, out int mult)
{
    add = a + b;
    mult = a * b;
}
```

## Chapter 125: Binary Serialization

### Section 125.1: Controlling serialization behavior with attributes

If you use the [NonSerialized] attribute, then that member will always have its default value after deserialization (ex. 0 for an int, null for string, false for a bool, etc.), regardless of any initialization done in the object itself (constructors, declarations, etc.). To compensate, the attributes [OnDeserializing] (called just BEFORE deserializing) and [OnDeserialized] (called just AFTER deserializing) together with their counterparts, [OnSerializing] and [OnSerialized] are provided.

Assume we want to add a "Rating" to our Vector and we want to make sure the value always starts at 1. The way it is written below, it will be 0 after being deserialized:

```
[Serializable]
public class Vector
{
    public int X;
    public int Y;
    public int Z;

    [NonSerialized]
    public decimal Rating = 1M;

    public Vector()
    {
        Rating = 1M;
    }

    public Vector(decimal initialRating)
    {
        Rating = initialRating;
    }
}
```

To fix this problem, we can simply add the following method inside of the class to set it to 1:

```
[OnDeserializing]
void OnDeserializing(StreamContext context)
{
    Rating = 1M;
}
```

Or, if we want to set it to a calculated value, we can wait for it to be finished deserializing and then set it:

```
[OnDeserialized]
void OnDeserialized(StreamContext context)
{
    Rating = 1 + ((X+Y+Z)/3);
}
```

Similarly, we can control how things are written out by using [OnSerializing] and [OnSerialized].

### Section 125.2: Serialization Binder

The binder gives you an opportunity to inspect what types are being loaded in your application domain

Create a class inherited from SerializationBinder

```csharp
class MyBinder : SerializationBinder
{
    public override Type BindToType(string assemblyName, string typeName)
    {
        if (typeName.Equals("BinarySerializationExample.Item"))
            return typeof(Item);
        return null;
    }
}
```

Now we can check what types are loading and on this basis to decide what we really want to receive

For using a binder, you must add it to the BinaryFormatter.

```csharp
object DeserializeData(byte[] bytes)
{
    var binaryFormatter = new BinaryFormatter();
    binaryFormatter.Binder = new MyBinder();

    using (var memoryStream = new MemoryStream(bytes))
        return binaryFormatter.Deserialize(memoryStream);
}
```

The complete solution

```csharp
using System;
using System.IO;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters.Binary;

namespace BinarySerializationExample
{
    class MyBinder : SerializationBinder
    {
        public override Type BindToType(string assemblyName, string typeName)
        {
            if (typeName.Equals("BinarySerializationExample.Item"))
                return typeof(Item);
            return null;
        }
    }

    [Serializable]
    public class Item
    {
        private string _name;
        public string Name
        {
            get { return _name; }
            set { _name = value; }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var item = new Item
            {
                Name = "Orange"
            };

            var bytes = SerializeData(item);
            var deserializedData = (Item)DeserializeData(bytes);
        }

        private static byte[] SerializeData(object obj)
        {
            var binaryFormatter = new BinaryFormatter();
            using (var memoryStream = new MemoryStream())
            {
                binaryFormatter.Serialize(memoryStream, obj);
                return memoryStream.ToArray();
            }
        }

        private static object DeserializeData(byte[] bytes)
        {
            var binaryFormatter = new BinaryFormatter
            {
                Binder = new MyBinder()
            };

            using (var memoryStream = new MemoryStream(bytes))
                return binaryFormatter.Deserialize(memoryStream);
        }
    }
}
```

### Section 125.3: Some gotchas in backward compatibility

This small example shows how you can lose backward compatibility in your programs if you do not take care in advance about this. And ways to get more control of serialization process

At first, we will write an example of the first version of the program:

Version 1

```
[Serializable]
class Data
{
    [OptionalField]
    private int _version;

    public int Version
    {
        get { return _version; }
        set { _version = value; }
    }
}
```

And now, let us assume that in the second version of the program added a new class. And we need to store it in an array.

Now code will look like this:

Version 2

```csharp
[Serializable]
class NewItem
{
    [OptionalField]
    private string _name;

    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
}

[Serializable]
class Data
{
    [OptionalField]
    private int _version;

    public int Version
    {
        get { return _version; }
        set { _version = value; }
    }

    [OptionalField]
    private List<NewItem> _newItems;

    public List<NewItem> NewItems
    {
        get { return _newItems; }
        set { _newItems = value; }
    }
}
```

And code for serialize and deserialize

```csharp
private static byte[] SerializeData(object obj)
{
    var binaryFormatter = new BinaryFormatter();
    using (var memoryStream = new MemoryStream())
    {
        binaryFormatter.Serialize(memoryStream, obj);
        return memoryStream.ToArray();
    }
}

private static object DeserializeData(byte[] bytes)
{
    var binaryFormatter = new BinaryFormatter();
    using (var memoryStream = new MemoryStream(bytes))
    {
        return binaryFormatter.Deserialize(memoryStream);
    }
}
```

And so, what would happen when you serialize the data in the program of v2 and will try to deserialize them in the program of v1?

You get an exception:

System.Runtime.Serialization.SerializationException was unhandled
Message=The ObjectManager found an invalid number of fixups. This usually indicates a problem in the Formatter.Source=mscorlib
StackTrace:
at System.Runtime.Serialization.ObjectManager.DoFixups()
at System.Runtime.Serialization.Formatters.Binary.ObjectReader.Deserialize(HeaderHandler handler, __BinaryParser serParser, Boolean fCheck, Boolean isCrossAppDomain, IMethodCallMessage methodCallMessage)
at System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(Stream serializationStream, HeaderHandler handler, Boolean fCheck, Boolean isCrossAppDomain, IMethodCallMessage methodCallMessage)
at System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(Stream serializationStream)
at Microsoft.Samples.TestV1.Main(String[] args) in c:\Users\andrew\Documents\Visual Studio 2013\Projects\vs\CSV1 Application\TestV1Part2\TestV1Part2.cs:line 29
at System.AppDomain._nExecuteAssembly(Assembly assembly, String[] args)
at Microsoft.VisualStudio.HostingProcess.HostProc.RunUsersAssembly()
at System.Threading.ExecutionContext.Run(ExecutionContext executionContext, ContextCallback callback, Object state)
at System.Threading.ThreadHelper.ThreadStart()

### Why?

The ObjectManager has a different logic to resolve dependencies for arrays and for reference and value types. We added an array of new the reference type which is absent in our assembly.

When ObjectManager attempts to resolve dependencies it builds the graph. When it sees the array, it can not fix it immediately, so that it creates a dummy reference and then fixes the array later.

And since this type is not in the assembly and dependencies can't be fixed. For some reason, it does not remove the array from the list of elements for the fixes and at the end, it throws an exception "IncorrectNumberOfFixups".

It is some 'gotchas' in the process of serialization. For some reason, it does not work correctly only for arrays of new reference types.

A Note:
Similar code will work correctly if you do not use arrays with new classes

And the first way to fix it and maintain compatibility?

- Use a collection of new structures rather than classes or use a dictionary(possible classes), because a dictionary it's a collection of keyvaluepair(it's structure)
- Use ISerializable, if you can't change the old code

### Section 125.4: Making an object serializable

Add the [Serializable] attribute to mark an entire object for binary serialization:

```csharp
[Serializable]
public class Vector
{
    public int X;
    public int Y;
    public int Z;

    [NonSerialized]
    public decimal DontSerializeThis;
}
```
