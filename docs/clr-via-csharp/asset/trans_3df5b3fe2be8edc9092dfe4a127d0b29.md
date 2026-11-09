

System.Int32 类型。正因如此，下面四行代码都能正确编译，并生成完全相同的 IL：

```csharp
int              a = 0;                       // Most convenient syntax
System.Int32     a = 0;                       // Convenient syntax
int              a = new int();               // Inconvenient syntax
System.Int32     a = new System.Int32();      // Most inconvenient syntax
```

表 5-1 显示了在 C# 中具有对应基元类型的 FCL 类型。对于符合通用语言规范（CLS）的类型，其他语言也会提供类似的基元类型。不过，语言并不要求为不符合 CLS 的类型提供任何支持。

**表 5-1** 具有对应 FCL 类型的 C# 基元类型

| 基元类型 | FCL 类型 | 符合 CLS | 描述 |
|---|---|---|---|
| sbyte | System.SByte | 否 | 有符号 8 位值 |
| byte | System.Byte | 是 | 无符号 8 位值 |
| short | System.Int16 | 是 | 有符号 16 位值 |
| ushort | System.UInt16 | 否 | 无符号 16 位值 |
| int | System.Int32 | 是 | 有符号 32 位值 |
| uint | System.UInt32 | 否 | 无符号 32 位值 |
| long | System.Int64 | 是 | 有符号 64 位值 |
| ulong | System.UInt64 | 否 | 无符号 64 位值 |
| char | System.Char | 是 | 16 位 Unicode 字符（`char` 永远不会表示 8 位值，而在非托管 C++ 中可能会表示 8 位值） |
| float | System.Single | 是 | IEEE 32 位浮点值 |
| double | System.Double | 是 | IEEE 64 位浮点值 |
| bool | System.Boolean | 是 | `true`/`false` 值 |
| decimal | System.Decimal | 是 | 一种 128 位高精度浮点值，通常用于不能容忍舍入误差的财务计算。在这 128 位中，1 位表示值的符号，96 位表示值本身，8 位表示要用来除以 96 位值的 10 的幂（范围可以是 0 到 28）。其余位未使用。 |
| string | System.String | 是 | 字符数组 |
| object | System.Object | 是 | 所有类型的基类型 |
| **dynamic** | **System.Object** | 是 | 对于公共语言运行时（CLR）而言，**dynamic** 与 **object** 完全相同。不过，C# 编译器允许 **dynamic** 变量使用简化语法参与动态调度。有关更多信息，请参阅本章末尾的“**dynamic** 基元类型”部分。 |

换一种方式来说，C# 编译器会自动假定你在所有源代码文件中都使用了以下 **using** 指令（如第 4 章“类型基础”中所述）：

```csharp
using sbyte  = System.SByte;
using byte   = System.Byte;
using short  = System.Int16;
using ushort = System.UInt16;
using int    = System.Int32;
using uint   = System.UInt32;
...
```

C# 语言规范指出：“作为一种编码风格，相比使用完整的系统类型名称，更推荐使用关键字。”我不同意语言规范的这一观点；我更喜欢使用 FCL 类型名称，并完全避免使用基元类型名称。事实上，我希望编译器甚至不要提供基元类型名称，而是强制开发人员使用 FCL 类型名称。理由如下：

- 我见过许多开发人员感到困惑，不知道应在代码中使用 **string** 还是 **String**。因为在 C# 中，**string**（关键字）与 **System.String**（FCL 类型）完全对应，所以二者没有区别，可以使用其中任意一个。同样，我听过一些开发人员说，当应用程序运行在 32 位操作系统上时，**int** 表示 32 位整数；而当应用程序运行在 64 位操作系统上时，它表示 64 位整数。这种说法完全错误：在 C# 中，**int** 始终对应 **System.Int32**，因此无论代码运行在哪种操作系统上，它都表示 32 位整数。如果程序员在代码中使用 **Int32**，也可以消除这种潜在的困惑。

- 在 C# 中，**long** 对应 **System.Int64**，但在另一种编程语言中，**long** 可能对应 **Int16** 或 **Int32**。实际上，C++/CLI 会将 **long** 视为 **Int32**。如果某人习惯使用另一种编程语言，那么他或她在阅读使用某种语言编写的源代码时，很容易误解代码的意图。事实上，大多数语言甚至不会将 **Long** 视为关键字，也不会编译使用它的代码。

- FCL 中有许多方法会将类型名称作为其方法名称的一部分。例如，**BinaryReader** 类型提供了 **ReadBoolean**、**ReadInt32**、**ReadSingle** 等方法，而 **System.Convert** 类型提供了 **ToBoolean**、**ToInt32**、**ToSingle** 等方法。虽然编写下面的代码是合法的，但对我来说，包含 **float** 的那一行感觉非常不自然，而且不容易看出这一行是正确的：

```csharp
BinaryReader br = new BinaryReader(...);
float val = br.ReadSingle();  // OK, but feels unnatural
Single val = br.ReadSingle();  // OK and feels good
```

- 许多只使用 C# 的程序员往往会忘记，还可以使用其他编程语言来针对 CLR 进行开发。因此，C# 特有的习惯会渗入类库代码中。例如，Microsoft 的 FCL 几乎完全使用 C# 编写，FCL 团队的开发人员现在已经在类库中引入了诸如 **Array's GetLongLength** 这样的方法。该方法返回一个 **Int64** 值，在 C# 中它是 **long**，但在其他语言（如 C++/CLI）中却不是。另一个例子是 **System.Linq.Enumerable's LongCount** 方法。

基于以上所有原因，本书将始终使用 FCL 类型名称。

在许多编程语言中，你可能会认为下面的代码可以正确编译和执行：

```csharp
Int32  i = 5;   // A 32-bit value
Int64  l = i;   // Implicit cast to a 64-bit value
```

不过，根据第 4 章中介绍的类型转换讨论，你可能不会认为这段代码能够编译。毕竟，**System.Int32** 和 **System.Int64** 是不同的类型，并且二者都不是从另一个类型派生而来。好消息是，C# 编译器确实能够正确编译这段代码，而且代码也会按预期运行。为什么呢？原因在于，C# 编译器深入了解基元类型，并在编译代码时应用了自己的特殊规则。换句话说，编译器能够识别常见的编程模式，并生成必要的 IL，使编写的代码按预期工作。具体来说，C# 编译器支持与类型转换、字面量和运算符相关的模式，如下面的示例所示。

首先，编译器能够执行基元类型之间的隐式或显式类型转换，例如：

```csharp
Int32  i = 5;        // Implicit cast from Int32 to Int32
Int64  l = i;        // Implicit cast from Int32 to Int64
Single s = i;        // Implicit cast from Int32 to Single
Byte   b = (Byte) i; // Explicit cast from Int32 to Byte
Int16  v = (Int16) s; // Explicit cast from Single to Int16
```

如果转换是“安全的”，C# 就允许隐式类型转换，也就是说，转换不会造成数据丢失，例如将 **Int32** 转换为 **Int64**。但是，如果转换存在潜在风险，C# 就要求使用显式类型转换。对于数值类型而言，“不安全”意味着转换结果可能会损失精度或数值范围。例如，从 Int32 转换为 Byte 需要显式类型转换，因为较大的 Int32 数字可能会损失精度；从 Single 转换为 Int16 也需要类型转换，因为 Single 能表示的数值范围可能大于 Int16。

请注意，不同的编译器可能会生成不同的代码来处理这些类型转换操作。例如，将值为 6.8 的 Single 转换为 Int32 时，有些编译器可能生成将 6 放入 Int32 的代码，而另一些编译器可能通过向上舍入将结果转换为 7。顺便说一下，C# 始终会截断结果。有关 C# 对基元类型执行类型转换时所遵循的确切规则，请参阅 C# 语言规范中的“转换”部分。

除了类型转换之外，基元类型还可以表示为字面量。字面量被视为其自身类型的实例，因此可以像下面这样使用该实例调用实例方法：

```csharp
Console.WriteLine(123.ToString() + 456.ToString());   // "123456"
```

此外，如果表达式由字面量组成，编译器能够在编译时计算该表达式，从而提高应用程序的性能。

```csharp
Boolean found = false;       // Generated code sets found to 0
Int32 x = 100 + 20 + 3;      // Generated code sets x to 123
String s = "a" + "bc";       // Generated code sets s to "a bc"
```

最后，编译器会自动了解如何解释代码中使用的运算符，以及解释这些运算符的顺序（例如 `+`、`-`、`*`、`/`、`%`、`&`、`|`、`^`、`!`、`~`、`==`、`!=`、`>`、`<`、`>=`、`<=`、`<<`、`>>`、`++`、`--` 等）：

```csharp
Int32 x = 100;                  // Assignment operator
Int32 y = x + 23;               // Addition and assignment operators
Boolean lessThanFifty = (y < 50); // Less-than and assignment operators
```

## 经过检查和未经检查的基元类型操作

程序员都清楚，许多针对基元类型的算术运算都可能导致溢出：

```csharp
Byte b = 100;
b = (Byte) (b + 200);            // b now contains 44 (or 2C in Hex).
```

> **重要提示** 执行上述算术运算时，第一步要求将所有操作数值扩展为 32 位值（如果任何操作数需要超过 32 位，则扩展为 64 位值）。因此，b 和 200（都只需要少于 32 位的值）会先转换为 32 位值，然后再相加。结果是一个 32 位值（十进制为 300，十六进制为 12C），必须将其转换为 Byte，才能将结果存回变量 b。C# 不会隐式地为你执行此类型转换，这就是前面代码第二行中必须使用 Byte 类型转换的原因。

