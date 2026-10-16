
```csharp
true)]
    public static void CreateHardLink(string oldFileName,
            string newFileName)
    {
        NativeMethods.CreateHardLink(oldFileName, newFileName);
    }
}
}
```

现在你可以使用这个类轻松创建硬链接。如果程序第一个参数传入的文件不存在，你会得到一个异常，消息为：系统找不到指定的文件。如果文件存在，你会得到一个新文件名，它引用原始文件。你可以通过在一个文件中更改文本轻松验证这一点；它也会出现在另一个文件中（代码文件 PInvokeSample/Program.cs）：

```csharp
using PInvokeSampleLib;
using System.IO;
using static System.Console;

namespace PInvokeSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            if (args.Length != 2)
            {
                WriteLine("usage: PInvokeSample" +
                    "existingfilename newfilename");
                return;
            }
            try
            {
                FileUtility.CreateHardLink(args[0], args[1]);
            }
            catch (IOException ex)
            {
                WriteLine(ex.Message);
            }
        }
    }
}
```

对于原生方法调用，你经常需要使用Windows句柄。Windows句柄是一个32位或64位的值，根据句柄类型的不同，某些值是不允许的。对于.NET 1.0中的句柄，通常使用 IntPtr 结构，因为你可以通过该结构设置任何可能的32位值。然而，对于某些句柄类型，这导致了安全问题、潜在的线程竞态条件以及终结阶段句柄泄漏。这就是为什么.NET 2.0引入了 SafeHandle 类。SafeHandle 类是所有Windows句柄的抽象基类。Microsoft.Win32.SafeHandles 命名空间内的派生类有 SafeHandleZeroOrMinusOneIsInvalid 和 SafeHandleMinusOneIsInvalid。顾名思义，这些类不接受无效的0或-1值。进一步派生的句柄类型包括 SafeFileHandle、SafeWaitHandle、SafeNCryptHandle 和 SafePipeHandle，它们可以被特定的Windows API调用使用。

例如，要映射Windows API CreateFile，你可以使用以下声明来返回一个 SafeFileHandle。当然，通常你可以改用.NET类 File 和 FileInfo。

```csharp
[DllImport("Kernel32.dll", SetLastError = true,
    Charset = Charset.Unicode)]
internal static extern SafeFileHandle CreateFile(
string fileName,
[MarshalAs(UnmanagedType.U4)] FileAccess fileAccess,
[MarshalAs(UnmanagedType.U4)] FileShare fileShare,
IntPtr securityAttributes,
[MarshalAs(UnmanagedType.U4)] FileMode creationDisposition,
int flags,
SafeFileHandle template);
```

## 总结

请记住，要成为一名真正熟练的C#程序员，你必须对内存分配和垃圾回收的工作原理有扎实的理解。本章描述了CLR如何在堆和栈上管理和分配内存。还说明了如何编写正确释放非托管资源的类，以及如何在C#中使用指针。这些都是高级主题，新手程序员往往理解不足且经常错误实现。至少，本章应该帮助你理解如何使用 IDisposable 接口和 using 语句释放资源。

下一章继续介绍一个重要的C#语言构造，它也会影响IL代码的生成：泛型。

## 6 泛型

### 本章内容

- 泛型概述
- 创建泛型类
- 泛型类的特性
- 泛型接口
- 泛型结构
- 泛型方法

### 本章代码下载

本章的wrox.com代码下载可在 www.wrox.com/go/professionalcsharp6 的“下载代码”选项卡中找到。本章代码分为以下主要示例：

- 链表对象
- 链表示例
- 文档管理器
- 变体
- 泛型方法
- 特化

## 泛型概述

泛型不仅对于C#，对于.NET而言也是一个重要概念。泛型不仅仅是C#编程语言的一部分；它们与程序集中的IL（中间语言）代码深度集成。通过泛型，你可以创建独立于所包含类型的类和方法。不需要为不同类型编写大量功能相同的类或方法，只需创建一个方法或类。

减少代码量的另一种选择是使用 Object 类。然而，使用从 Object 类派生的类型进行传递并不安全。泛型类使用泛型类型，这些类型会根据需要替换为特定类型。这实现了类型安全：如果泛型类不支持某个特定类型，编译器就会发出警告。

泛型不仅限于类；在本章中，你还会看到泛型接口和泛型方法。你可以在第9章“委托、Lambda表达式和事件”中了解泛型委托。

泛型并非C#独有；其他语言也存在类似的概念。例如，C++模板与泛型有一些相似之处。然而，C++模板和.NET泛型之间有一个很大的区别。对于C++模板，当模板以特定类型实例化时，需要模板的源代码。C++编译器为每个特定模板实例的类型生成独立的二进制代码。与C++模板不同，泛型不仅是C#语言的一种构造，还与公共语言运行时（CLR）一起定义。这使得即使泛型类是用C#定义的，也可以在Visual Basic中以特定类型实例化泛型。

以下各节探讨泛型的优点和缺点，特别是以下方面：

- 性能
- 类型安全
- 二进制代码复用
- 代码膨胀
- 命名指南

## 性能

泛型的一大优点是性能。在第11章“集合”中，你会看到来自命名空间 `System.Collections` 和 `System.Collections.Generic` 的非泛型和泛型集合类。将值类型与非泛型集合类一起使用时，当值类型转换为引用类型以及反向转换时，会发生装箱和拆箱。

> **注意** 装箱和拆箱在第8章“运算符和强制转换”中讨论。这里仅对这些术语作简短回顾。

值类型存储在栈上，而引用类型存储在堆上。C#类是引用类型，结构是值类型。.NET使得将值类型转换为引用类型变得容易，因此你可以在任何需要对象（即引用类型）的地方使用值类型。例如，可以将 `int` 赋值给对象。从值类型到引用类型的转换称为*装箱*。如果方法要求对象作为参数，并且传递了值类型，则会自动发生装箱。相反方向，可以使用拆箱将装箱的值类型转换为值类型。使用拆箱时，需要强制转换运算符。

下面的示例展示了来自命名空间 `System.Collections` 的 `ArrayList` 类存储对象；`Add` 方法被定义为需要对象作为参数，因此整数类型会被装箱。当从 `ArrayList` 中读取值时，将对象转换为整数类型时会发生拆箱。这可能从用于将ArrayList集合的第一个元素赋给变量i1的强制转换运算符中显而易见，但在foreach语句中，当访问int类型的变量i2时，同样会发生拆箱：

```csharp
var list = new ArrayList();
list.Add(44);    // boxing - convert a value type to a reference type

int i1 = (int)list[0];    // unboxing - convert a reference type to
                        // a value type

foreach (int i2 in list)
{
    WriteLine(i2);    // unboxing
}
```

装箱和拆箱易于使用，但会对性能产生很大影响，尤其是在迭代许多项时。

与使用对象不同，来自命名空间 `System.Collections.Generic` 的 `List<T>` 类允许你在使用时定义类型。在此示例中，`List<T>` 类的泛型类型被定义为int，因此int类型用于即时（JIT）编译器动态生成的类中。装箱和拆箱不再发生：

```csharp
var list = new List<int>();
list.Add(44);    // no boxing - value types are stored in the List<int>

int i1 = list[0];    // no unboxing, no cast needed

foreach (int i2 in list)
{
    WriteLine(i2);
}
```

## 类型安全

泛型的另一个特性是类型安全。与 `ArrayList` 类一样，如果使用对象，则可以向该集合添加任何类型。下面的示例展示了将整数、字符串和MyClass类型的对象添加到类型为ArrayList的集合中：

```csharp
var list = new ArrayList();
list.Add(44);
list.Add("mystring");
list.Add(new MyClass());
```

如果使用下面的foreach语句迭代该集合（该语句使用整数元素迭代），编译器会接受此代码。但是，由于集合中并非所有元素都可以转换为int，因此会发生运行时异常：

```csharp
foreach (int i in list)
{
    WriteLine(i);
}
```

