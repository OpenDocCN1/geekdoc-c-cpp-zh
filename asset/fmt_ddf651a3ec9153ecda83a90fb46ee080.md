
在这里，惰性求避免了在 `a` 为 0 时尝试除法。

除了位逻辑运算符外，C# 还有左移和右移运算符。例如，`a = a >> n;` 将位向右移动，而 `a = a << n;` 将位向左移动。你可以将左移视为整数乘以 2，将右移视为除以 2。如果被移动的数据类型是有符号的 32 位或 64 位类型，则会执行算术右移，即新的高位被设置为符号位。如果数据类型是无符号 32 位或 64 位类型，则执行逻辑右移，即一个零被移入高位。

如果你想对符号类型执行逻辑移动，可以简单地使用强制类型转换。例如：

```csharp
int a = -1;
int b = a >> 8;
```

执行的是算术右移，但：

```csharp
int c = (int) ((uint) a >> 8);
```

执行的是逻辑右移，即从右侧移入零。

所有的逻辑运算符以及针对 32 位或 64 位数据类型的移位。在简单逻辑操作的情况下，16 位和 8 位数据会自动转换为 32 位类型，你需要使用显式强制转换来恢复原始数据类型，例如：

```csharp
byte a = 0xFF, b = 0xF0;
byte c = (byte) (a & b);
```

移位的操作也同样简单，例如以下操作的结果是：

```csharp
Int16 a = 0xFF;
Int16 c = (Int16)((int)a << 8);
```

你将发现有符号类型上存在一个问题。如果你尝试分配一个表示负数的十六进制值，例如：

```csharp
Int16 a = (Int16)0xFFFF;
```

你会发现它不起作用。

如果你想强制让它工作，请使用：

```csharp
Int16 a;
unchecked { a = (Int16)0xFFFF; }
```

此时变量声明现在必须分开，否则它将只在 `unchecked` 作用范围内定义。为了避免这种情况，请使用无符号类型，如：

```csharp
UInt16 a = 0xFFFF;
UInt16 c = (UInt16)(a << 16);
```

你可以认为使用无符号类型是表示模式的最佳方法，但在其他数据类型上进行位操作是必要的，仅仅是因为这是本练习的目的。

你可以使用移位和逻辑运算符的组合来创建其他类型的移位，包括位旋转。例如，创建一个左旋转非常容易：

```csharp
UInt16 RotateLeft(UInt16 data, int n) {
    Int16 mask;
    unchecked(mask=(Int16)0x8000);
    mask = (Int16)(mask >> (n-1));
    String s = mask.ToString("X");
    UInt16 top = (UInt16)(data & mask);
    top = (UInt16)(top >> (16 - n));
    data = (UInt16)(data << n);
    data = (UInt16)(data | top);
    return data;
}
```

这种方法通过使用算术移位创建一个高 n 位被设置为 1 的掩码来实现。我们必须使用掩码来提取高 n 位，这些位通过右移变成低位。最后执行左移 `n` 位，原本的高 n 位通过组合表达式以更紧凑的形式存储，但关于这种方法效率如何的问题，只能通过与替代方法进行基准测试来回答，例如执行重复移位和高低位传输。

### BitConverter

不得不诉诸位操作的最常见原因之一是你有一个原始字节流，并需要将其转换为结构化数据。逻辑操作对非整数类型不起作用，如果你想将字节转换为浮点数，就会产生一些问题。将字节转换为整数类型甚至也不容易。也就是说，最经常需要解决的问题是你有一组字节流，字节组代表浮点值或整数值，而你需要将流转换为这些值。

这就是 `BitConverter` 类变得重要的地方。它旨在帮助你将对象序列化为字节并反转，但这并没有阻止我们将其用于其他用途。`BitConverter` 拥有一个 `GetBytes` 方法，可以将任何标准数据类型转换为字节数组，并有一个特定的 `ToType` 方法，可以将相同的字节数组转换回相应的数据类型。例如：

```csharp
double a=1.34;
byte[] data;
data=BitConverter.GetBytes(a);
```

返回一个包含存储在 `a` 中的位的 8 字节数组。还有两种形式的 `ToType` 让你指定位置。在处理原始数据时，`BitConverter` 是非常有用的。

## 第27 章

### 结构体

结构体是 C# 和大多数编程语言中的基础数据类型。在 C# 中，结构体是类的值类型等效物，而不是引用类型。通常情况下，结构体也可以拥有方法和属性，除了继承的情况外，它们可以像类一样使用。结构体不能继承另一个结构体或另一个类。

数据结构本质上是简单的，但你可能会对事情变得复杂感到惊讶。问题大多出现在你必须处理在其他语言中创建的结构时，无论是保存和重新加载、通过网络传输，还是调用不是 C# 或 .NET 的原生函数。

你需要大致了解如何使用 PInvoke 调用 API 函数，以及什么是封送（marshaling），这在第25 章中涵盖过。本章描述的许多技术可以扩展到任何数据类型。

### Layout

在许多情况下，你可以简单地声明并使用结构体，而无需担心它是如何实现的，特别是在内存中是如何布局的。然而，如果你必须为其他程序提供结构体，或者使用“外部”结构体，那么内存布局就变得很重要。你认为以下结构体的大小是多少？

```csharp
public struct struct {
    public byte a;      // 1 字节
    public int b;       // 4 字节
    public short c;     // 2 字节
    public byte d;      // 1 字节
}
```

一个合理的答案是 8 字节，这是字段大小的总和。

# 结语

位操作是我们尝试避免的，但在某些应用程序中，由于需要与原始数据甚至硬件交互，它是不可避免的。在大多数情况下，你可以使用安全代码完成工作，但仍然需要诉诸不安全代码，但只要加小心这就可以是安全的。

如果你实际上使用以下代码来调查结构体的大小：

```csharp
int size = Marshal.SizeOf(test);
```

你会发现，在大多数情况下，该结构体占了 12 字节。这是因为大多数 CPU 在处理大小大于单个字节且在特定地址边界上对齐的数据时工作得最好。源自 Pentium 的 CPU 喜欢以 16 字节为块的形式处理数据，并将数据对齐在与数据大小相同的地址边界上。例如，一个 4 字节的整数应该对齐在 4 字节的地址边界上，即地址的形式应为 `4n-i` 形式。具体细节并不重要，你只需要意识到这些考虑因素会修改你可能预期的布局。

重要的是，编译器将使用“填充（padding）”字节来对齐结构体内部的数据。你可以显式地控制填充，但请注意，如果你使用未对齐的数据，某些处理器会抛出异常。要控制结构体的布局，你需要使用 `InteropServices` 命名空间；因此添加：

```csharp
using System.Runtime.InteropServices;
```

结构体由 `[StructLayout]` 属性进行控制。例如：

```csharp
[StructLayout(LayoutKind.Sequential)]
public struct struct1
{
    public byte a;      // 1 byte
    public int b;       // 4 bytes
    public short c;     // 2 bytes
    public byte d;      // 1 byte
}
```

这会强制编译器按照定义中列出的顺序顺序分配结构体，这也是它的默认行为。

`LayoutKind` 的其他值还包括 `Auto`（允许编译器确定布局）和 `Explicit`（允许程序员指定每个字段的大小）。`Explicit` 通常用于创建没有紧凑（no packing）的顺序布局，但在大多数情况下，使用 `Pack` 字段更为简单。它告诉编译器如何对组成字段的数据进行大小设置和对齐。例如，如果你指定 `Pack = 1`，则结构体的组织方式将使得每个字段都位于字节边界上，并且可以一次读取一个字节，即不需要紧凑填充。如果你将结构体的定义改为：

```csharp
[StructLayout(LayoutKind.Sequential, Pack = 1)]
public struct struct1
```

你会发现它现在的大小是 8 字节，这对应于字段在内存中按顺序排列且没有填充字节。这正是你在处理 Windows API 和 C/C++ 中定义的大多数结构体时需要的。

在大多数情况下，你不需要使用 `Pack` 的其他值，但如果你设置 `Pack = 2`，你会发现结构体的大小现在变为 10 字节，因为每个字节字段上都增加了一个字节，使得整个结构体能够以 2 字节为块进行读取。如果你设置 `Pack = 4`，大小会增加到 12 字节，允许整个结构体以 4 字节为块进行读取。之后就不会有变化了，因为一旦填充大小等于或大于 CPU 使用的对齐方式（对于 Intel 架构是 8 字节），它就会被忽略。

不同 `pack` 大小下的结构体布局如下：

| byte | byte | byte |
|---|---|---|
| int | | |
| | int | |
| short | short | |
| byte | byte | int |
| Pack=1 | | short |
| 8 bytes | Pack=2 | byte |
| | 10 bytes | Pack=4 |
| | | 12 bytes |

同样值得提到的是，你可以仅通过重新排列字段来修改结构体的紧凑方式。例如，通过将字段顺序更改为：

```csharp
public struct struct1
{
    public byte b; // 1 byte
    public byte d; // 1 byte
    public short c; // 2 bytes
    public int b; // 4 bytes
}
```

该结构体不需要填充，在不需要任何干预的情况下仅占用 8 字节。

# 显式（Being Explicit）

如果你确实想指定为任何特定字段分配空间，可以使用 `Explicit`。例如：

```csharp
[StructLayout(LayoutKind.Explicit)]
public struct struct1
{
    [FieldOffset(0)]
    public byte a; // 1 byte
    [FieldOffset(1)]
    public int b; // 4 bytes
    [FieldOffset(5)]
    public short c; // 2 bytes
    [FieldOffset(7)]
    public byte d; // 1 byte
}
```

产生一个没有任何填充的 8 字节结构体。从这个意义上，它等同于 `Pack = 1`，而后者的使用要简单得多。然而，`Explicit` 给了你完全的控制。例如：

```csharp
[StructLayout(LayoutKind.Explicit)]
public struct struct1
{
    [FieldOffset(0)]
    public byte a; // 1 byte
    [FieldOffset(1)]
    public int b; // 4 bytes
    [FieldOffset(10)]
    public short c; // 2 bytes
    [FieldOffset(14)]
    public byte d; // 1 byte
}
```

产生一个 16 字节的结构体。这是因为结构体内部不允许使用固定数组。如果你需要固定大小的缓冲区，可以使用：

```csharp
public struct struct1
{
    public byte a;
    public int b;
    public short c;
    public byte[] buffer;
}
```

会生成错误。要访问固定大小字段，你必须对 `buffer` 使用指针运算，参见下一章，该章节当然是“不安全的（unsafe）”。
