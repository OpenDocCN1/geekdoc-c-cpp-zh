
框架类库（FCL）。例如，在C#中，`int`直接映射到`System.Int32`类型。因此，下面四行代码都能正确编译并生成完全相同的IL。

```csharp
int       a = 0;                    // Most convenient syntax
System.Int32 a = 0;                 // Convenient syntax
int       a = new int();            // Inconvenient syntax
System.Int32 a = new System.Int32(); // Most inconvenient syntax
```

表5-1列出了在C#中具有对应原始类型的FCL类型。对于符合公共语言规范（CLS）的类型，其他语言也会提供类似的原始类型。但是，语言并不需要为非CLS兼容类型提供任何支持。

### 表5-1 C#原始类型与对应的FCL类型

| 原始类型 | FCL类型 | CLS兼容 | 描述 |
|---|---|---|---|
| `sbyte` | `System.SByte` | 否 | 有符号8位值 |
| `byte` | `System.Byte` | 是 | 无符号8位值 |
| `short` | `System.Int16` | 是 | 有符号16位值 |
| `ushort` | `System.UInt16` | 否 | 无符号16位值 |
| `int` | `System.Int32` | 是 | 有符号32位值 |
| `uint` | `System.UInt32` | 否 | 无符号32位值 |
| `long` | `System.Int64` | 是 | 有符号64位值 |
| `ulong` | `System.UInt64` | 否 | 无符号64位值 |
| `char` | `System.Char` | 是 | 16位Unicode字符（`char` 永远不像非托管C++中那样表示8位值） |
| `float` | `System.Single` | 是 | IEEE 32位浮点数值 |
| `double` | `System.Double` | 是 | IEEE 64位浮点数值 |
| `bool` | `System.Boolean` | 是 | 真/假值 |
| `decimal` | `System.Decimal` | 是 | 一个128位高精度浮点值，常用于不能容忍舍入误差的金融计算。在这128位中，1位表示值的符号；96位表示值本身；8位表示将96位值除以10的幂次（该幂次可以是0到28之间的任意值）。其余位未使用。 |
| `string` | `System.String` | 是 | 一个字符数组 |
| `object` | `System.Object` | 是 | 所有类型的基类型 |
| `dynamic` | `System.Object` | 是 | 对于公共语言运行时（CLR），`dynamic` 与 `object` 相同。但是，C#编译器允许`dynamic`变量通过一种简化的语法参与动态调度。更多信息，请参阅本章末尾的“dynamic原始类型”一节。 |

另一种理解方式是，C#编译器会自动假定你的所有源代码文件中都包含以下 using 指令（如第4章“类型基础”中讨论的那样）。

```csharp
using byte   = System.Byte;
using sbyte  = System.SByte;
using short  = System.Int16;
using ushort = System.UInt16;
using int    = System.Int32;
using uint   = System.UInt32;
...
```

C#语言规范指出：“作为一种风格问题，使用关键字比使用完整的系统类型名称更受青睐。”我不同意语言规范；我更喜欢使用FCL类型名称，并完全避免使用原始类型名称。事实上，我希望编译器甚至不提供原始类型名称，而是强制开发者使用FCL类型名称。以下是我的理由：

- 我见过许多开发者感到困惑，不知道在代码中应该使用 string 还是 String。因为在C#中，string（关键字）精确映射到 System.String（FCL类型），二者没有任何区别，使用哪个都可以。同样，我听过一些开发者说，当应用程序在32位操作系统上运行时，int 表示32位整数，而在64位操作系统上运行时，它表示64位整数。这种说法绝对是错误的：在C#中，int 总是映射到 System.Int32，因此无论代码运行在什么操作系统上，它都表示32位整数。如果程序员在代码中使用 Int32，那么这个潜在的混淆也就消除了。
- 在C#中，long 映射到 System.Int64，但在另一种编程语言中，long 可能映射到 Int16 或 Int32。事实上，C++/CLI确实将 long 视为 Int32。如果一个人习惯于使用不同的编程语言，那么在阅读某种语言的源代码时，很容易误解代码的意图。实际上，大多数语言甚至不把 long 当作关键字，也不会编译使用它的代码。
- FCL有许多方法，其方法名称中包含类型名称。例如，BinaryReader 类型提供了诸如 ReadBoolean、ReadInt32、ReadSingle 等方法，而 System.Convert 类型提供了诸如 ToBoolean、ToInt32、ToSingle 等方法。虽然编写以下代码是合法的，但含有 float 的那一行对我来说非常不自然，而且这行代码是否正确并不明显。

  ```csharp
  BinaryReader br = new BinaryReader(...);
  float val = br.ReadSingle();   // OK, but feels unnatural
  Single val = br.ReadSingle();  // OK and feels good
  ```

- 许多只使用C#的程序员往往会忘记其他编程语言也可以用于CLR，因此，C#特有的风格会渗透到类库代码中。例如，微软的FCL几乎完全是用C#编写的，FCL团队的开发人员现在已经在库中引入了一些方法，比如 Array 的 GetLongLength，它返回一个 Int64 值，在C#中是 long，但在其他语言（如C++/CLI）中不是。另一个例子是 System.Linq.Enumerable 的 LongCount 方法。

基于以上所有原因，我将在本书中始终使用FCL类型名称。

在许多编程语言中，你会期望以下代码能够正确编译和执行。

```csharp
Int32 i = 5;      // A 32-bit value
Int64 l = i;      // Implicit cast to a 64-bit value
```

然而，基于第4章中关于强制转换的讨论，你不会期望这段代码能编译。毕竟，System.Int32 和 System.Int64 是不同的类型，而且两者之间不存在派生关系。不过，你会很高兴地知道，C#编译器确实能正确编译这段代码，并且按预期运行。为什么？原因是C#编译器对原始类型有深入的了解，并在编译代码时应用自己特殊的规则。换句话说，编译器能够识别常见的编程模式，并生成必要的IL，使所编写的代码按预期工作。具体来说，C#编译器支持与强制转换、字面量和运算符相关的模式，如下面的示例所示。

首先，编译器能够在原始类型之间执行隐式或显式强制转换，例如以下代码。

```csharp
Int32  i = 5;       // Implicit cast from Int32 to Int32
Int64  l = i;       // Implicit cast from Int32 to Int64
Single s = i;       // Implicit cast from Int32 to Single
Byte   b = (Byte) i; // Explicit cast from Int32 to Byte
Int16  v = (Int16) s; // Explicit cast from Single to Int16
```

如果转换是“安全的”，即不可能丢失数据，例如将 Int32 转换为 Int64，C#允许隐式强制转换。但如果转换可能不安全，C#则要求显式强制转换。对于数值类型，“不安全”意味着转换可能导致精度或数量级的损失。例如，从 Int32 转换为 Byte 需要显式强制转换，因为大的 Int32 数字可能会丢失精度；从 Single 转换为 Int16 则需要强制转换，因为 Single 可以表示比 Int16 更大数量级的数字。

请注意，不同的编译器可能生成不同的代码来处理这些强制转换操作。例如，当将值为6.8的 Single 强制转换为 Int32 时，一些编译器可能生成代码将6放入 Int32，而另一些编译器可能通过将结果四舍五入到7来执行转换。顺便说一下，C#总是截断结果。关于C#在强制转换原始类型时遵循的确切规则，请参阅C#语言规范中的“转换”一节。

除了强制转换，原始类型还可以写成字面量。字面量被认为就是类型本身的实例，因此，你可以像下面这样通过使用该实例来调用实例方法。

```csharp
Console.WriteLine(123.ToString() + 456.ToString());   // "123456"
```

另外，如果有一个由字面量组成的表达式，编译器能够在编译时计算该表达式，从而提高应用程序的性能。

```csharp
Boolean found = false;      // Generated code sets found to 0
Int32 x = 100 + 20 + 3;     // Generated code sets x to 123
String s = "a " + "bc";     // Generated code sets s to "a bc"
```

