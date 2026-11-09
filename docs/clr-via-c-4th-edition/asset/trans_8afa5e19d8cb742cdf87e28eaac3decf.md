
运算符方法定义于其中。此限制的原因是，它使 C# 编译器能够在合理的时间内搜索到可绑定的运算符方法。

下面是一个在 C# 类定义中定义的运算符重载方法示例。

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
}
```

编译器会为名为 op_Addition 的方法生成元数据方法定义项；该方法定义项还设置了 specialname 标志，表明这是一个“特殊”方法。当语言编译器（包括 C# 编译器）在源代码中看到指定的 + 运算符时，它们会检查操作数类型之一是否定义了名为 op_Addition 的 specialname 方法，且其参数与操作数类型兼容。如果该方法存在，编译器会生成调用该方法的代码。如果不存在这样的方法，则会发生编译错误。

表 8-1 和表 8-2 展示了 C# 支持重载的一元运算符和二元运算符集合、它们的符号，以及编译器生成的对应公共语言规范（CLS）方法名。我将在下一节解释这些表格的第三列。

**表 8-1 C# 一元运算符及其符合 CLS 的方法名**

| C# 运算符符号 | 特殊方法名 | 建议的 CLS 兼容方法名 |
| --- | --- | --- |
| + | op_UnaryPlus | Plus |
| - | op_UnaryNegation | Negate |
| ! | op_LogicalNot | Not |
| ~ | op_OnesComplement | OnesComplement |
| ++ | op_Increment | Increment |
| -- | op_Decrement | Decrement |
| （无） | op_True | IsTrue { get; } |
| （无） | op_False | IsFalse { get; } |

**表 8-2 C# 二元运算符及其符合 CLS 的方法名**

| C# 运算符符号 | 特殊方法名 | 建议的 CLS 兼容方法名 |
| --- | --- | --- |
| + | op_Addition | Add |
| - | op_Subtraction | Subtract |
| * | op_Multiply | Multiply |
| / | op_Division | Divide |
| % | op_Modulus | Mod |
| & | op_BitwiseAnd | BitwiseAnd |
| &#124; | op_BitwiseOr | BitwiseOr |
| ^ | op_ExclusiveOr | Xor |
| `<<` | `op_LeftShift` | `LeftShift` |
| `>>` | `op_RightShift` | `RightShift` |
| `==` | `op_Equality` | `Equals` |
| `!=` | `op_Inequality` | `Equals` |
| `<` | `op_LessThan` | `Compare` |
| `>` | `op_GreaterThan` | `Compare` |
| `<=` | `op_LessThanOrEqual` | `Compare` |
| `>=` | `op_GreaterThanOrEqual` | `Compare` |

CLR 规范定义了许多可重载的额外运算符，但 C# 不支持这些额外运算符。因此，它们并未被主流使用，所以我不会在此列出。如果你对完整列表感兴趣，请参阅通用语言基础设施（CLI）的 ECMA 规范（www.ecma-international.org/publications/standards/Ecma-335.htm），第 I 部分“概念与体系结构”，第 10.3.1 节（一元运算符）和第 10.3.2 节（二元运算符）。

> **注意** 如果你检查框架类库（FCL）中的核心数值类型（Int32、Int64、UInt32 等），你会发现它们没有定义任何运算符重载方法。它们不定义的原因是，编译器会专门查找对这些基元类型的操作，并生成直接操作这些类型实例的 IL 指令。如果这些类型提供方法，并且编译器生成代码来调用这些方法，那么方法调用会带来运行时性能开销。此外，方法最终无论如何都必须执行一些 IL 指令来执行预期操作。这就是核心 FCL 类型不定义任何运算符重载方法的原因。这对你意味着：如果你使用的编程语言不支持某个核心 FCL 类型，你就无法对该类型的实例执行任何操作。

## 运算符与编程语言互操作性

运算符重载可以是非常有用的工具，让开发人员用简洁的代码表达自己的想法。然而，并非所有编程语言都支持运算符重载。当使用不支持运算符重载的语言时，该语言将不知道如何解释 + 运算符（除非该类型是该语言中的基元类型），编译器将生成错误。当使用不支持运算符重载的语言时，该语言应允许你直接调用所需的 `op_*` 方法（例如 op_Addition）。

如果你使用的语言不支持在类型中定义 + 运算符重载，那么显然，该类型仍可以提供 op_Addition 方法。从 C# 中，你可能会期望可以通过 + 运算符调用这个 op_Addition 方法，但你不能。当 C# 编译器检测到 + 运算符时，它会查找关联了 specialname 元数据标志的 op_Addition 方法，以便编译器确定该 op_Addition 方法旨在作为运算符重载方法。由于 op_Addition 方法是由不支持运算符重载的语言生成的，因此该方法不会关联 specialname 标志，C# 编译器将生成编译错误。当然，任何语言中的代码都可以显式调用一个恰好名为 op_Addition 的方法，但编译器不会将 + 符号的使用转换为对该方法的调用。

### 杰夫对微软运算符方法命名规则的看法

我相信，所有这些关于何时可以、何时不能调用运算符重载方法的规则看起来都非常令人困惑且过于复杂。如果支持运算符重载的编译器干脆不生成 specialname 元数据标志，规则就会简单得多，程序员使用提供运算符重载方法的类型时也会更轻松。支持运算符重载的语言将支持运算符符号语法，而所有语言都将支持显式调用各种 op_ 方法。我想不出微软为什么要把这件事弄得如此困难，我希望他们能在未来版本的编译器中放宽这些规则。

对于定义运算符重载方法的类型，微软建议该类型还定义更友好的公共静态方法，并在内部调用这些运算符重载方法。例如，重载 op_Addition 方法的类型应定义一个名为 Add 的公共友好命名方法。表 8-1 和表 8-2 的第三列列出了每个运算符建议的友好名称。因此，前面展示的 Complex 类型应按以下方式定义。

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
    public static Complex Add(Complex c1, Complex c2) { return(c1 + c2); }
}
```

当然，用任何编程语言编写的代码都可以调用任何友好运算符方法，例如 Add。微软关于类型应提供这些友好方法名的指导方针让情况更加复杂。我认为这种额外的复杂性是不必要的，并且调用这些友好命名的方法会导致额外的性能损失，除非 JIT 编译器能够内联友好命名方法中的代码。内联代码会使 JIT 编译器优化代码，移除额外的方法调用并提升运行时性能。

**注意** 关于重载运算符并按照微软设计指南使用友好方法名的类型示例，请参见 FCL 中的 `System.Decimal` 类。

## 转换运算符方法

有时，你需要将某个类型的对象转换为另一种类型的对象。例如，我确信你在某个时候一定需要将 Byte 转换为 Int32。当源类型和目标类型都是编译器的基元类型时，编译器知道如何生成必要的代码来转换对象。

如果源类型或目标类型不是基元类型，编译器会生成让 CLR 执行转换（强制转换）的代码。在这种情况下，CLR 只检查源对象的类型是否与目标类型相同（或派生自目标类型）。然而，有时希望将一个类型的对象转换为一种完全不同的类型是很自然的。例如，`System.Xml.Linq.XElement` 类允许你将可扩展标记语言（XML）元素转换为 Boolean、(U)Int32、(U)Int64、Single、Double、Decimal、String、DateTime、DateTimeOffset、TimeSpan、Guid，或这些类型中任意类型的可空等效类型（String 除外）。你还可以想象 FCL 包含一个 Rational 数据类型，并且将 Int32 对象或 Single 对象转换为 Rational 对象可能很方便。此外，将 Rational 对象转换为 Int32 或 Single 对象可能也不错。

要进行这些转换，Rational 类型应定义接受单个参数的公共构造函数：即你要从中转换的类型的实例。你还应定义不接受任何参数的公共实例 ToXxx 方法（就像非常流行的 ToString 方法一样）。每个方法都会将定义类型的实例转换为 Xxx 类型。以下是正确定义 Rational 类型的转换构造函数和方法的方式。

```csharp
public sealed class Rational {
    // Constructs a Rational from an Int32
    public Rational(Int32 num) { ... }

    // Constructs a Rational from a Single
    public Rational(Single num) { ... }

    // Converts a Rational to an Int32
    public Int32 ToInt32() { ... }

    // Converts a Rational to a Single
    public Single ToSingle() { ... }
}
```

通过调用这些构造函数和方法，使用任何编程语言的开发人员都可以将 Int32 或 Single 对象转换为 Rational 对象，并将 Rational 对象转换为 Int32 或 Single 对象。执行这些转换的能力可能非常方便，在设计类型时，你应认真考虑哪些转换构造函数和方法对你的类型有意义。

在上一节中，我讨论了某些编程语言如何提供运算符重载。那么，某些编程语言（如 C#）还提供转换运算符重载。转换运算符是将对象从一种类型转换为另一种类型的方法。你使用特殊语法定义转换运算符方法。CLR 规范要求转换
