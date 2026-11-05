
```
class Class3
{
    public static void H() {
        Class1.F();        // F is not called
    }
}
```

类 Class2 和 Class3 各自包含对条件方法 Class1.F 的调用，该方法根据 DEBUG 是否定义而为条件。由于该符号在 Class2 的上下文中定义，而在 Class3 中未定义，因此 Class2 中的对 F 的调用被包含，而 Class3 中的对 F 的调用被省略。

在继承链中使用条件方法可能会令人困惑。通过 base 以 base.M 的形式对条件方法进行的调用受正常条件方法调用规则的约束。示例中

文件 class1.cs:

```
using System;
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

文件 class2.cs:

```
using System;
class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();                // base.M is not called!
    }
}
```

文件 class3.cs:

```
#define DEBUG
using System;
class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();                   // M is called
    }
}
```

Class2 包含对其基类中定义的 M 的调用。由于基方法根据符号 DEBUG 的存在而为条件，且该符号未定义，因此此调用被省略。因此，该方法仅向控制台写入“Class2.M executed”。谨慎使用预处理指令可以消除此类问题。

## 17.4.2.2 条件属性类

用一个或多个 Conditional 属性装饰的属性类（§17.1）是条件属性类。

因此，条件属性类与在其 Conditional 属性中声明的条件编译符号相关联。以下示例：

```
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

将 TestAttribute 声明为与条件编译符号 ALPHA 和 BETA 相关联的条件属性类。

条件属性的属性规范（§17.2）如果在其关联的条件编译符号中的一个或多个在规范点被定义则包含，否则属性规范被省略。

需要注意的是，条件属性类的属性规范的包含或排除由规范点处的条件编译符号控制。示例中

```
File test.cs:
    using System;
    using System.Diagnostics;
    [Conditional("DEBUG")]
    public class TestAttribute : Attribute {}

File class1.cs:
    #define DEBUG
    [Test]        // TestAttribute is specified
    class Class1 {}

File class2.cs:
    #undef DEBUG
    [Test]        // TestAttribute is not specified
    class Class2 {}
```

类 Class1 和 Class2 各自用属性 Test 装饰，该属性根据 DEBUG 是否定义而为条件。由于该符号在 Class1 的上下文中定义而在 Class2 中未定义，因此 Class1 上的 Test 属性的规范被包含，而 Class2 上的 Test 属性的规范被省略。

## 17.4.3 Obsolete 属性

Obsolete 属性用于标记不应再使用的类型和类型的成员。

```csharp
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class |
        AttributeTargets.Struct |
        AttributeTargets.Enum |
        AttributeTargets.Interface |
        AttributeTargets.Delegate |
        AttributeTargets.Method |
        AttributeTargets.Constructor |
        AttributeTargets.Property |
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute: Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

如果程序使用用 Obsolete 属性装饰的类型或成员，编译器会发出警告或错误。具体而言，如果未提供 error 参数，或提供了 error 参数且其值为 false，则编译器发出警告。如果指定了 error 参数且其值为 true，则编译器发出错误。

示例中

```csharp
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() {}
}
class B
{
    public void F() {}
}
class Test
{
    static void Main() {
        A a = new A();      // warning
        a.F();
    }
}
```

类 A 用 Obsolete 属性装饰。Main 中对 A 的每次使用都会产生警告，其中包含指定的消息，“This class is obsolete; use class B instead.”

## 17.5 用于互操作的特性

*注意：本节仅适用于 Microsoft .NET 对 C# 的实现。*

## 17.5.1 与 COM 和 Win32 组件的互操作

.NET 运行库提供了大量属性，使 C# 程序能够与使用 COM 和 Win32 DLL 编写的组件互操作。例如，DllImport 属性可用于

static extern 方法以指示该方法的实现位于 Win32 DLL 中。这些属性位于 System.Runtime.InteropServices 命名空间中，这些属性的详细文档可在 .NET 运行时文档中找到。

## 17.5.2 与其他 .NET 语言的互操作

## 17.5.2.1 IndexerName 属性

在 .NET 中，索引器使用索引属性实现，并在 .NET 元数据中具有名称。如果索引器没有 IndexerName 属性，则默认使用名称 Item。IndexerName 属性使开发人员能够覆盖此默认值并指定不同的名称。

```csharp
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute : Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} }
    }
}
```

## 18. 不安全代码

如前几章所述的核心 C# 语言，与 C 和 C++ 相比，其显著区别在于省略了指针作为数据类型。相反，C# 提供了引用以及创建由垃圾回收器管理的对象的能力。这种设计结合其他特性，使 C# 比 C 和 C++ 更安全得多。在核心 C# 语言中，根本不可能出现未初始化的变量、“dangling” 指针或索引超出数组边界的表达式。 routinely 困扰 C 和 C++ 程序的整类错误因此被消除。

尽管 C 或 C++ 中几乎每种指针类型构造在 C# 中都有引用类型对应物，但仍存在需要访问指针类型的情况。例如，在没有指针访问的情况下，可能无法或不切实际地与底层操作系统接口、访问内存映射设备或实现时间关键算法。为解决此需求，C# 提供了编写不安全代码的能力。

在不安全代码中，可以声明和操作指针、执行指针与整数类型之间的转换、获取变量的地址，等等。从某种意义上说，在 C# 程序中编写不安全代码就像在 C# 程序中编写 C 代码一样。

从开发人员和用户的角度来看，不安全代码实际上是一种“安全”特性。不安全代码必须用 unsafe 修饰符明确标记，因此开发人员不可能意外使用不安全特性，并且执行引擎会确保不安全代码无法在不受信任的环境中执行。

## 18.1 不安全上下文

C# 的不安全特性仅在不安全上下文中可用。不安全上下文是通过在类型或成员的声明中包含 unsafe 修饰符，或使用 unsafe-statement 来引入的：

- 类、结构、接口或委托的声明可以包含 unsafe 修饰符，在这种情况下，该类型声明的整个文本范围（包括类、结构或接口的主体）被视为不安全上下文。
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数或静态构造函数的声明可以包含 unsafe 修饰符，在这种情况下，该成员声明的整个文本范围被视为不安全上下文。
- unsafe-statement 使能够在块内使用不安全上下文。与之关联的块的整个文本范围被视为不安全上下文。

相关的语法扩展如下所示。为简洁起见，省略号 (...) 用于表示在前几章中出现的产生式。

```
class-modifier:
    ...
    unsafe

struct-modifier:
    ...
    unsafe

interface-modifier:
    ...
    unsafe
```
