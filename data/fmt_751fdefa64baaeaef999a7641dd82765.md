
- `UsedDynamicToInvokeMember` 演示了如何使用 C# 动态原始类型（在第 5 章末尾“原始类型、引用类型和值类型”中讨论）来简化访问成员的语法。此外，如果你打算在所有相同类型的不同对象上调用同一个成员，这种技术可以提供相当不错的性能，因为绑定将在每个类型发生一次并被缓存，以便可以多次快速调用。你也可以使用这种技术来调用不同类型对象上的成员。

# 第 23 章 程序集加载与反射

```csharp
using System;
using System.Reflection;
using Microsoft.CSharp.RuntimeBinder;
```

```csharp
// 此类用于用于演示反射
// 它有一个字段、构造函数、方法、属性和一个事件
internal sealed class SomeType {
    private Int32 m_someField;
    public SomeType(ref Int32 x) { x *= 2; }
    public override String ToString() { return m_someField.ToString(); }
    public Int32 SomeProp {
        get { return m_someField; }
        set {
            if (value < 1)
                throw new ArgumentOutOfRangeException("value");
            m_someField = value;
        }
    }
    public event EventHandler SomeEvent;
    private void NoCompilerWarnings() { }
}
```

```csharp
public static class Program {
    private const BindingFlags c_bf = BindingFlags.DeclaredOnly | BindingFlags.Public |
        BindingFlags.NonPublic | BindingFlags.Instance;

    public static void Main() {
        Type t = typeof(SomeType);
        UseInvokeMemberToBindAndInvokeMember(t);
        Console.WriteLine();

        BindToMemberThenInvokeMember(t);
        Console.WriteLine();

        BindToMemberCreateDelegateToThenInvokeMember(t);
        Console.WriteLine();

        UseDynamicToBindAndInvokeMember(t);
        Console.WriteLine();
    }

    private static void UseInvokeMemberToBindAndInvokeMember(Type t) {
        Console.WriteLine("UseInvokeMemberToBindAndInvokeMember");

        // 构造 Type 的实例
        Object[] args = new Object[] { 12 }; // 构造函数参数
        Console.WriteLine("x before constructor called: " + args[0]);
        Object obj = t.InvokeMember(null, c_bf | BindingFlags.CreateInstance,
            null, null, args);
        Console.WriteLine("Type: " + obj.GetType().ToString());
        Console.WriteLine("x after constructor returns: " + args[0]);

        // 读取和写入字段
        t.InvokeMember("m_someField", c_bf | BindingFlags.SetField,
            null, obj, new Object[] { 5 });
        Int32 v = (Int32)t.InvokeMember("m_someField", c_bf | BindingFlags.GetField,
            null, obj, null);
        Console.WriteLine("someField: " + v);

        // 调用方法
        String s = (String)t.InvokeMember("ToString", c_bf | BindingFlags.InvokeMethod,
            null, obj, null);
        Console.WriteLine("ToString: " + s);

        // 写入属性
        try {
            t.InvokeMember("SomeProp", c_bf | BindingFlags.SetMethod,
                null, obj, new Object[] { -1 });
        } catch (TargetInvocationException e) {
            Console.WriteLine("Property set catch: " + e.InnerException.Message);
        }
    }
    
    // 其他方法将根据示例在此处继续
}
```

# 656 第四部分 设施

```csharp
catch (ArgumentOutOfRangeException) {
    Console.WriteLine("Property set catch.");
}
setSomeProp(2);
var getSomeProp = (Func<Int32>)Delegate.Create(typeof(Func<Int32>), obj, obj.GetMethod());
Console.WriteLine("Prop: " + getSomeProp());
```

```csharp
// 从事件中添加和删除委托
EventInfo = obj.GetType().GetEvent("SomeEvent", c_bf);
var addSomeEvent = (Action<EventHandler>)Delegate.CreateDelegate(typeof(EventHandler), obj, obj.AddMethod());
addSomeEvent(CallBack);
var removeSomeEvent = (Action<EventHandler>)Delegate.CreateDelegate(typeof(EventHandler), obj, obj.GetRemoveMethod());
removeSomeEvent(CallBack);
```

```csharp
private static void UseDynamicToBindAndInvokeMember(Type t) {
    Console.WriteLine("DynamicToBindAndInvokeMember");
}
```

```csharp
// 构造一个实例（你无法创建指向构造函数的委托）
Object[] args = new Object[] { 12 }; // 构造函数参数
Console.WriteLine("before constructor called: " + args[0]);
dynamic obj = Activator.CreateInstance(t, args);
Console.WriteLine("Type: " + obj.GetType().ToString());
Console.WriteLine("after constructor returns: " + args[0]);
```

```csharp
// 读取一个字段的值
try {
    obj.m_someField = 5;
    Int32 v = (Int32)obj.m_someField;
    Console.WriteLine("someField: " + v);
}
```

```csharp
catch (RuntimeException e) {
// 我们到达这里是因为字段是私有的
    Console.WriteLine("Failed to access field: " + e.Message);
}
```

```csharp
// 调用一个方法
String s = (String)obj.ToString();
Console.WriteLine("ToString: " + s);
```

```csharp
// 写属性
try {
    obj.SomeProp = 0;
}
```

```csharp
catch (ArgumentOutOfRangeException) {
    Console.WriteLine("Property set catch.");
}
```

```csharp
obj.SomeProp = 2;
Int32 val = (Int32)obj.SomeProp;
Console.WriteLine("SomeProp: " + val);
```

# 第 23 章 程序集加载与反射

```csharp
// 从事件中添加和删除委托
obj.SomeEvent += new EventHandler(EventCallback);
obj.SomeEvent -= new EventHandler(EventCallback);
```

如果你编译并运行这段代码，你将看到以下输出：

```
InvokeMemberToBindAndInvokeMember
x before constructor called: 12
Type: SomeType
x after constructor returns: 24
someField: 5
ToString: 5
Property set catch.
SomeProp: 2
```

```
BindMemberThenInvokeMember
x before constructor called: 12
Type: SomeType
x after constructor returns: 24
someField: 33
ToString: 33
Property set catch.
SomeProp: 2
```

```
BindMemberCreateDelegateToMemberThenInvokeMember
x before constructor called: 12
Type: SomeType
x after constructor returns: 24
ToString: 0
Property set catch.
SomeProp: 2
```

```
UseDynamicToBindAndInvokeMember
x before constructor called: 12
Type: SomeType
x after constructor returns: 24
Failed to access field: 'SomeType.m_someField' is inaccessible due to its protection level
ToString: 0
Property set catch.
SomeProp: 2
```

注意 `SomeType` 的构造函数接收一个引用的 `Int32` 作为其唯一参数。之前的代码展示了如何调用此构造函数，以及如何在返回后检查修改后的 `Int32` 值。此外，`BindMemberThenInvokeMember` 方法顶部是一个对 `Type` 的 `GetType` 方法的调用，传递了字符串 "System.Int32"。字符串中的符号 (&) 允许我识别通过引用传递的参数。该引用是类型名称 Backus-Naur 范法的一部分，你可以在 FCL 文档中查找到它。代码也可以写成这样：

```csharp
ConstructorInfo ctor = t.GetConstructor(new Type[] { typeof(Int32).MakeByRefType() });
```

# 使用绑定句柄减少进程的内存消耗

许多应用程序绑定到一组类型（`Type` 对象）或类型成员（派自 `MemberInfo` 的对象），并将这些对象保存在某种集合中。稍后，应用程序会在集合中搜索特定对象并调用该对象。这是一种很好的方法，但存在一个小问题：`Type` 和派自 `MemberInfo` 的对象需要大量内存。如果应用程序持有过多的此类对象并偶尔调用它们，内存消耗将剧增。

在内部，CLR 有一种更紧凑的方式来表示这些信息。使用句柄代替对象，开发者可以减少工作集。CLR 为了运行定义了三种句柄（在 System 命名空间中）：`RuntimeHandle`, `FieldHandle`, 和 `MethodHandle`。

```csharp
using System;
using System.Reflection;
using System.Collections.Generic;

public sealed class Program {
    private const BindingFlags c_bf = BindingFlags.FlattenHierarchy | BindingFlags.Instance |
        BindingFlags.Static | BindingFlags.Public | BindingFlags.NonPublic;

    public static void Main() {
        // 操作前的堆大小
        Show("Before doing anything");

        // 为所有方法构建 MethodInfo 对象缓存
        List<MethodBase> methodInfos = new List<MethodBase>();
        foreach (Type t in typeof(object).Assembly.GetExportedTypes()) {
            // 跳过泛型
            if (t.IsGenericDefinition) continue;
            MethodBase mb = t.GetMethods(c_bf);
            methodInfos.Add(mb);
        }

        // 显示绑定所有方法后的数量和大小
        Console.WriteLine("# of methods={0}", methodInfos.Count);
        Show("After building cache of MethodInfo objects");

        // 为 MethodInfo 对象构建 RuntimeHandle 缓存
        List<RuntimeMethodHandle> runtimeMethodHandles = methodInfos.ConvertAll(mb => mb.MethodHandle);

        Show("Holding MethodInfo and RuntimeHandle cache");
        GC.KeepAlive(methodInfos); // 防止被 GC 回收

        methodInfos = null; // 允许现在回收缓存
        Show("After freeing MethodInfo objects");

        // 使用句柄重建 MethodInfo 对象
        methodInfos = runtimeMethodHandles.ConvertAll<MethodBase>(rhm => MethodBase.GetFromHandle(rhm));
        Show("Size of heap after re-creating MethodInfo objects");
        GC.KeepAlive(runtimeMethodHandles); // 防止被 GC 回收
        GC.KeepAlive(methodInfos); // 防止被 GC 回收
    }

    private static void Show(string message) {
        // 实现未显示
    }
}
```

当我编译并运行此程序时，我得到了以下输出：

Heap size= 85,000 - Before doing anything

# methods=48,467

Heap size= 7,065,632 - After building cache of MethodInfo objects

Heap size= 7,453,496 - Holding MethodInfo and RuntimeHandle cache

Heap size= 6,732,704 - After freeing MethodInfo objects
