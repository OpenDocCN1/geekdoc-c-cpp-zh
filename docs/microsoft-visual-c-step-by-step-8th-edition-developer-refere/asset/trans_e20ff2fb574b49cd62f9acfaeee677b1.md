

WinRT。因此，UWP 应用只能访问 .NET Framework 4.6 提供的类型和方法的一个减少子集。（在 Visual Studio 2015 中使用 C# 构建 UWP 应用时，IntelliSense 会自动显示可用功能的受限视图，省略通过 WinRT 不可用的类型和方法。）

另一方面，WinRT 提供了大量在 .NET Framework 中没有直接等价物或与 .NET Framework 中对应功能的操作方式显著不同的功能和类型，因此无法轻松翻译。WinRT 通过一个映射层使这些功能对 CLR 可用，使其看起来像 .NET Framework 类型和方法，并且您可以直接从托管代码调用它们。

因此，CLR 和 WinRT 实现的集成使 CLR 能够透明地使用 WinRT 类型，但它也支持反向互操作性：您可以使用托管代码定义类型并使其可供非托管应用程序使用，只要这些类型符合 WinRT 的期望。第 9 章强调了结构体在这方面的要求（结构体中的实例方法和静态方法在 WinRT 中不可用，且私有字段不受支持）。如果您构建的类打算通过 WinRT 被非托管应用程序使用，您的类必须遵循以下规则：

- 任何公共字段，以及任何公共方法的参数和返回值，必须是 WinRT 类型或可由 WinRT 透明翻译为 WinRT 类型的 .NET Framework 类型。受支持的 .NET Framework 类型的示例包括符合规范的值类型（如结构体和枚举）以及对应于 C# 原语的类型（int、long、float、double、string 等）。类中的私有字段受支持，并且可以是 .NET Framework 中可用的任何类型；它们不必符合 WinRT。
- 类不能重写 System.Object 的方法，除 ToString 外，并且不能声明受保护的构造函数。
- 类所在的命名空间必须与实现该类的程序集的名称相同。此外，命名空间名称（因此程序集名称）不得以“Windows”开头。
- 您不能通过 WinRT 在非托管应用程序中继承托管类型。因此，所有公共类必须是密封的。如果您需要实现多态性，可以创建一个公共接口并在必须多态的类上实现该接口。
- 您可以抛出包含在可供 UWP 应用使用的 .NET Framework 子集中的任何异常类型；您不能创建自己的自定义异常类。如果您的代码在从非托管应用程序调用时抛出未处理的异常，WinRT 会在非托管代码中引发等效异常。

WinRT 对本书记载的 C# 代码的其他功能还有其他要求。这些要求将在描述每个功能时突出显示。

## Summary

在本章中，您了解了如何定义和实现接口和抽象类。下表总结了在为接口、类和结构体定义方法时各种有效（是）和无效（否）关键字组合。

| Keyword | Interface | Abstract class | Class | Sealed class | Structure |
|---|---|---|---|---|---|
| abstract | No | Yes | No | No | No |
| new | Yes¹ | Yes | Yes | Yes | No² |
| override | No | Yes | Yes | Yes | No³ |
| private | No | Yes | Yes | Yes | Yes |
| protected | No | Yes | Yes | Yes | No⁴ |
| public | No | Yes | Yes | Yes | Yes |
| sealed | No | Yes | Yes | Yes | No |
| virtual | No | Yes | Yes | No | No |

1 接口可以扩展另一个接口并引入具有相同签名的新的方法。
2 结构体不支持继承，因此它们不能隐藏方法。
3 结构体不支持继承，因此它们不能重写方法。
4 结构体不支持继承；结构体是隐式密封的，不能被派生。

如果您想继续阅读下一章，请保持 Visual Studio 2015 运行并转到第 14 章。

- ■ 如果您现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

## Quick reference

| To | Do this |
|---|---|
| Declare an interface | Use the *interface* keyword. For example:
```
interface IDemo
{
    string GetName();
    string GetDescription();
}
``` |
| Implement an interface | Declare a class by using the same syntax as class inheritance, and then implement all the member functions of the interface. For example:
```
class Test : IDemo
{
    public string IDemo.GetName()
    {
        ...
    }

    public string IDemo.GetDescription()
    {
        ...
    }
}
``` |
| Create an abstract class that can be used only as a base class, containing abstract methods | Declare the class by using the *abstract* keyword. For each abstract method, declare the method with the *abstract* keyword and without a method body. For example:
```
abstract class GrazingMammal
{
    abstract void DigestGrass();
    ...
}
``` |
| Create a sealed class that cannot be used as a base class | Declare the class by using the *sealed* keyword. For example:
```
sealed class Horse
{
    ...
}
``` |

## Chapter 14. Using garbage collection and resource management

完成本章后，您将能够：

- 使用垃圾回收管理系统资源。
- 编写在对象被销毁时运行的代码。
- 通过编写 try/finally 语句以异常安全的方式在已知时间点释放资源。
- 通过编写 using 语句以异常安全的方式在已知时间点释放资源。
- 实现 IDisposable 接口以在类中支持异常安全的释放。

您已在前面的章节中了解如何创建变量和对象，并且应该理解创建变量和对象时内存是如何分配的。（如果您不记得，值类型是在栈上创建的，而引用类型是从堆分配内存。）计算机没有无限的内存，因此当变量或对象不再需要时，必须收回内存。值类型在超出作用域时被销毁并收回其内存。这就是容易的部分。引用类型呢？您使用 new 关键字创建对象，但对象何时以及如何被销毁？本章就是关于这个问题的。

### The life and times of an object

首先，让我们回顾一下创建对象时会发生什么。

您使用 new 操作符创建对象。以下示例创建了在第 13 章“Creating interfaces and defining abstract classes”中讨论的 Square 类的新实例

Click here to view code image

```
int sizeOfSquare = 99;
Square mySquare = new Square(sizeOfSquare); // Square is a reference type
```

从您的角度来看，new 操作是一个单一步骤，但在底层，对象创建实际上是一个两阶段过程：

1. new 操作从堆分配一块原始内存。您无法控制对象创建的这一阶段。
2. new 操作将原始内存块转换为对象；它必须初始化对象。您可以通过使用构造函数来控制这一阶段。

### Note

如果您是 C++ 程序员，您应该注意在 C# 中，您不能重载 *new* 操作来控制分配。

创建对象后，您可以使用点操作符（.）访问其成员。例如，*Square* 类包含一个名为 *Draw* 的方法，您可以调用它：

```
mySquare.Draw();
```

### Note

此代码基于继承自 *DrawingShape* 抽象类且未显式实现 *IDraw* 接口的 *Square* 类版本。有关更多信息，请参阅第 13 章。

当 *mySquare* 变量超出作用域时，*Square* 对象不再被主动引用。然后对象可以被销毁，并且它使用的内存可以被收回。（这可能不会立即发生，正如您稍后将看到的那样。）与对象创建一样，对象销毁也是一个两阶段过程。销毁的两个阶段与创建的两个阶段完全对应：

1. 公共语言运行时（CLR）必须执行一些清理工作。您可以通过编写 *destructor* 来控制这一点。
2. CLR 必须将先前属于对象的内存返回给堆；对象所在的内存必须被释放。您无法控制这一阶段。

销毁对象并将内存返回给堆的过程称为 *garbage collection*。

### Note

如果您使用 C++ 编程，请记住 C# 没有 delete 操作符。CLR 控制对象何时被销毁。

### Writing destructors

您可以使用析构函数在对象被垃圾回收时执行所需的任何清理工作。CLR 会自动清理对象使用的任何托管资源，因此在许多情况下，编写析构函数是不必要的。

