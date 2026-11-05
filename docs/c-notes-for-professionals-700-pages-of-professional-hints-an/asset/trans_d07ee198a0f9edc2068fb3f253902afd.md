
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

## 第125章：二进制序列化

### 第125.1节：使用属性控制序列化行为

如果使用 [NonSerialized] 属性，则该成员在反序列化后将始终具有其默认值（例如 int 为 0，string 为 null，bool 为 false 等），无论对象本身进行的任何初始化（构造函数、声明等）。为弥补这一点，提供了属性 [OnDeserializing]（在反序列化前调用）和 [OnDeserialized]（在反序列化后调用）以及其对应属性 [OnSerializing] 和 [OnSerialized]。

假设我们想为 Vector 添加一个 "Rating"，并且希望该值始终从 1 开始。如下所示编写，反序列化后它将为 0：

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

为修复此问题，我们只需在类内部添加以下方法将其设为 1：

```
[OnDeserializing]
void OnDeserializing(StreamContext context)
{
    Rating = 1M;
}
```

或者，如果我们想将其设为计算值，可以等待其完成反序列化后再设置：

```
[OnDeserialized]
void OnDeserialized(StreamContext context)
{
    Rating = 1 + ((X+Y+Z)/3);
}
```

同样，我们可以使用 [OnSerializing] 和 [OnSerialized] 来控制如何写入内容。

### 第125.2节：序列化绑定器

绑定器使你有机会检查在应用程序域中加载的类型

创建一个继承自 SerializationBinder 的类

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

现在我们可以检查正在加载的类型，并据此决定我们真正想要接收的内容

使用绑定器时，必须将其添加到 BinaryFormatter。

```csharp
object DeserializeData(byte[] bytes)
{
    var binaryFormatter = new BinaryFormatter();
    binaryFormatter.Binder = new MyBinder();

    using (var memoryStream = new MemoryStream(bytes))
        return binaryFormatter.Deserialize(memoryStream);
}
```

完整的解决方案

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

### 第125.3节：向后兼容性中的一些陷阱

这个小示例展示了如果不提前注意这个问题，你的程序如何会失去向后兼容性。以及获得更多序列化过程控制的方法

首先，我们将编写程序第一个版本的示例：

版本 1

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

现在，假设在程序的第二个版本中添加了一个新类。我们需要在数组中存储它。

现在代码将如下所示：

版本 2

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

用于序列化和反序列化的代码

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

那么，当你在 v2 程序中序列化数据并尝试在 v1 程序中反序列化它们时会发生什么？

你会得到一个异常：

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

### 为什么？

ObjectManager 对于数组和引用类型与值类型的依赖解析有不同的逻辑。我们添加了一个新引用类型的数组，而该类型在我们的程序集中不存在。

当 ObjectManager 尝试解析依赖关系时，它会构建图。当它看到数组时，无法立即修复它，因此它会创建一个虚拟引用，然后稍后修复数组。

由于该类型不在程序集中，依赖关系无法修复。出于某种原因，它没有从修复元素列表中删除数组，最后抛出异常 "IncorrectNumberOfFixups"。

这是序列化过程中的一些 'gotchas'。出于某种原因，它仅对新引用类型的数组不起作用。

注意：
如果不使用包含新类的数组，类似的代码将能正常工作

那么第一种修复并保持兼容的方法是什么？

- 使用新的结构集合而不是类，或使用字典（可能包含类），因为字典是 KeyValuePair 的集合（它是结构）
- 如果无法更改旧代码，使用 ISerializable

### 第125.4节：使对象可序列化

添加 [Serializable] 属性以标记整个对象进行二进制序列化：

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
