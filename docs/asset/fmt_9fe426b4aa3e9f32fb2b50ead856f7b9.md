
## 清单 20.16：在不安全代码中使用指针修改不可变字符串

```
string text = "S5280ft";
Console.Write("{0} = ", text);
unsafe // Requires /unsafe switch.
{
    fixed (char* pText = text)
    {
        char* p = pText;
        *++p = 'm';
        *++p = '1';
        *++p = '1';
        *++p = 'e';
        *++p = ' ';
        *++p = ' ';
    }
}
Console.WriteLine(text);
```

清单 20.16 的结果出现在输出 20.2 中。

### 输出 20.2

```
S5280ft = Smile
```

在这种情况下，你获取原始地址，并使用前置递增运算符按引用类型的大小（`sizeof(char)`）递增它。接下来，你使用间接运算符解引用该地址，然后为该位置赋予一个不同的字符。类似地，对指针使用 `+` 和 `-` 运算符会按 `* sizeof(T)` 操作数改变地址，其中 `T` 是引用类型。

类似地，比较运算符（`==`、`!=`、`<`、`>`、`<=` 和 `>=`）可用于比较指针，实际上转换为地址位置值的比较。

解引用运算符的一个限制是无法解引用 `void*`。`void*` 数据类型表示指向未知类型的指针。由于数据类型未知，它不能被解引用以产生变量。相反，要访问 `void*` 引用的数据，你必须将其转换为任何其他指针类型，然后解引用后者。

你可以使用索引运算符而不是间接运算符来实现与清单 20.16 相同的行为（参见清单 20.17）。

## 清单 20.17：在不安全代码中使用索引运算符修改不可变字符串

```
string text;
text = "S5280ft";
Console.Write("{0} = ", text);

unsafe // Requires /unsafe switch.
{
    fixed (char* pText = text)
    {
        pText[1] = 'm';
        pText[2] = 'i';
        pText[3] = 'l';
        pText[4] = 'e';
        pText[5] = ' ';
        pText[6] = ' ';
    }
}
Console.WriteLine(text);
```

清单 20.17 的结果出现在输出 20.3 中。

## 通过委托执行不安全代码

正如本章开头所承诺的，我们以一个完整的工作示例结束，这可能是你在 C# 中所能做的最“不安全”的事情：获取一个指向内存块的指针，用它填充机器代码的字节，创建一个引用新代码的委托，然后执行它。这段特定的汇编代码确定执行代码的机器是虚拟机还是真实机器。如果机器是虚拟的，它会输出“Inside Matrix！”清单 20.19 展示了如何做到这一点。

### 初学者专题

#### 什么是虚拟计算机？

虚拟计算机（或虚拟机），也称为客户机，是通过运行在宿主操作系统上并与宿主计算机硬件交互的软件进行虚拟化或模拟的。例如，可以在运行最新版本 Windows 的计算机上安装虚拟计算机软件（如 VMware Workstation 和 Microsoft Hyper-V）。软件安装后，用户可以在软件中配置客户机，启动它，并安装操作系统，就像它是一台真正的计算机，而不仅仅是用软件虚拟化出来的。

### 清单 20.19：为不安全代码指定块

```
using System.Runtime.InteropServices;

class Program
{
    unsafe static int Main(string[] args)
    {
        // Assign redpill
        byte[] redpill = {
            0x0f, 0x01, 0x0d,        // asm SIDT instruction
            0x00, 0x00, 0x00, 0x00,  // placeholder for an address
            0xc3};                   // asm return instruction

        unsafe
        {
            fixed (byte* matrix = new byte[6],
                redpillPtr = redpill)
            {
                // Move the address of matrix immediately
                // following the SIDT instruction of memory.
                *(uint*)&redpillPtr[3] = (uint)&matrix[0];

                using (VirtualMemoryPtr codeBytesPtr =
                    new VirtualMemoryPtr(redpill.Length))
                {
                    Marshal.Copy(
                        redpill, 0,
                        codeBytesPtr, redpill.Length);

                    MethodInvoker method =
                        (MethodInvoker)Marshal.GetDelegateForFunctionPointer(
                        codeBytesPtr, typeof(MethodInvoker));

                    method();
                }
                if (matrix[5] > 0xd0)
                {
                    Console.WriteLine("Inside Matrix!\n");
                    return 1;
                }
                else
                {
                    Console.WriteLine("Not in Matrix.\n");
                    return 0;
                }
            } // fixed
        } // unsafe
    }
}
```

清单 20.19 的结果出现在输出 20.5 中。

#### 输出 20.5

```
Inside Matrix!
```

## 在 C# 中使用 Windows Runtime 库

Windows RT 是 Windows 8 操作系统的版本，只支持沉浸式“Metro 风格”应用程序，而不支持传统的“桌面”应用程序。支持沉浸式应用程序的操作系统 API 库称为 Windows Runtime，简称 WinRT。

尽管 WinRT API 本质上是非托管 COM API，但它们使用与 .NET 运行时相同的元数据格式来描述；因此 WinRT 不仅支持使用非托管语言编写的沉浸式 Windows 应用程序的开发，也支持使用托管语言（如 C#）编写的此类应用程序，而无需使用本章其余部分描述的 `P/Invoke` 技巧。

WinRT API 经过精心设计，对 C# 用户而言显得很自然。然而，在编写面向 WinRT 的 C# 程序时，你应该注意一些小的“阻抗不匹配”问题。

### 具有自定义添加和移除处理程序的 WinRT 事件

实现“观察者”模式有许多不同的方式。在 C# 中，正如我们已经讨论过的，事件通常作为多播委托类型的字段来实现。也就是说，声明一个委托类型的字段，该委托可以引用许多不同的方法。当事件触发时，这些委托方法被调用。要向事件添加事件处理程序或从事件中移除事件处理程序，你本质上需要创建一个新的多播委托，并用新委托替换该字段的值。

当你在事件上使用 `+=` 和 `-=` 运算符时，所有这些机制都会自动为你实现。C# 还允许你通过 `add` 和 `remove` 事件访问器方法，在你的类的用户添加或移除事件处理程序时运行自定义代码。

从使用者的角度来看，WinRT 事件没有区别。在 C# 程序中添加或移除 WinRT 对象的事件处理程序时，你可以像平时一样使用 `+=` 和 `-=`；C# 编译器会确保在生成代码时使用适当的 WinRT 机制。然而，对于自定义事件访问器，WinRT 使用的机制与传统的 C# 程序略有不同，这反过来又影响了你在 C# 中为 WinRT 类型编写自定义事件访问器的方式。

在常规 C# 事件中，当你从事件中移除委托时，该委托会作为 `remove` 访问器的隐藏值参数传递。`add` 和 `remove` 访问器都不返回值。具有自定义访问器的 WinRT 事件使用一种略有不同的机制：当你向事件添加委托时，`add` 访问器返回一个“令牌”。要从事件中移除该委托，你将令牌——而不是委托——传递给 `remove` 访问器。如果你希望为 WinRT 事件编写自定义访问器，则必须遵循 WinRT 事件模式。

幸运的是，WinRT 库提供了一个特殊的辅助类，为你跟踪令牌及其对应的委托。该模式类似于清单 20.20 中所示的代码。

#### LISTING 20.20: The WinRT Event Pattern

```
using System;
class WinRTEvent
{
    EventRegistrationTokenTable<EventHandler> table = null;
    public event EventHandler MyEvent
    {
        add
        {
            return EventRegistrationTokenTable<EventHandler>
                .GetOrCreateEventRegistrationTokenTable(ref table)
                .AddEventHandler(value);
        }
        remove
        {
            return EventRegistrationTokenTable<EventHandler>
                .GetOrCreateEventRegistrationTokenTable(ref table)
                .RemoveEventHandler(value);
        }
    }
    void OnMyEvent()
    {
        EventHandler handler =
            EventRegistrationTokenTable<EventHandler>
                .GetOrCreateEventRegistrationTokenTable(ref table)
                .InvocationList;
        if (handler != null)
            handler(this, new EventArgs());
    }
}
```

As you can see, every time a handler is added to the event, removed from the event, or invoked, a table is created if one does not exist already. (There should be one table variable per event.) The table manages the relationship between the token returned from the adder and the multicast delegate in the table. Just replace the `EventHandler` type with the appropriate delegate type for your event, and add whatever code you want to the `add` and `remove` accessors.

### Automatically Shimmed Interfaces

Another difference between WinRT invocation and regular .NET invocation code is that certain frequently used interfaces have slightly different names and members in WinRT. The C# compiler and .NET runtime know about these differences, and automatically generate code behind the scenes that “shims” one interface to another so as to minimize the impact on the developer. The two most notable examples are `IEnumerable<T>`, which is called `IIterable<T>` in WinRT, and `IDisposable`, which is called `IClosable` in WinRT.

Because these interfaces are automatically shimmed, you can use a method that returns `IClosable` in any context that requires an `IDisposable`, such as a `using` statement. Similarly, sequences and collections behave the same regardless of whether they use the C# standard interface or the WinRT version.

### Task-Based Asynchrony

The WinRT APIs do not use `Task<T>` to represent asynchronous work. (See Chapter 18 for a detailed explanation of how to use `Task<T>` and the C# 5 `await` operator.) Rather, they use the `IAsyncAction<T>` interface. This type has many of the same features as `Task<T>`; for example, it supports a cancellation mechanism, a progress-reporting mechanism, and so on.

The C# 5 `await` operator works just as well with an operand of type `IAsyncAction<T>` as it does with `Task<T>`. However, a C# 5 method decorated with the `async` keyword that contains an `await` operator still must return `Task` or `Task<T>`, or be `void`-returning; it is not legal for an `async` method to return `IAsyncAction<T>`. To convert an `IAsyncAction<T>` to an equivalent `Task<T>`, just call the `AsTask()` method on it.

The vast majority of other issues related to WinRT are essentially API changes, and a detailed discussion of them is beyond the scope of this book. It is important to note, however, that in WinRT all high-latency synchronous methods previously available in .NET 4.5 and earlier have been dropped, leaving only the `*Async` asynchronous equivalents.

## SUMMARY

As demonstrated throughout this book, C# offers great power, flexibility, consistency, and a fantastic structure. This chapter highlighted the ability of C# programs to perform very low-level machine-code operations.

Before we end the book, Chapter 21 briefly describes the underlying execution platform and shifts the focus from the C# language to the broader platform in which C# programs execute.

# 21 The Common Language Infrastructure
