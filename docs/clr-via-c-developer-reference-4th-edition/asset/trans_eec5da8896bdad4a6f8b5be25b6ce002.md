

该操作符定义在其内部的。这种限制的原因是它让 C# 编译器能够在合理的时间内搜索到可能的绑定方法。

以下是一个在 C# 类定义中定义的运算符重载方法的示例。

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
}
```

编译器会为一个名为 _Add_ 的条目进入元数据定义；该方法条目还设置了特殊标志，表示这是一个“特殊”方法。当语言编译器（包括 C# 编译器）在源代码中看到指定的 `+` 运算符时，它们会查找操作数类型之一是否定义了名为 _Add_ 的特殊名称方法，且其参数与操作数的类型兼容。如果该方法存在，编译器就会生成指向该方法的代码。如果没有该方法，则会发生编译错误。

表 8-1 和 8-2 显示了 C# 支持重载的一元和二元运算符集、它们的符号以及编译器生成的对应的通用语言规范（CLS）方法名。我将在下一节解释这三列。

## 表 8-1 C 一元运算符及其符合 CLS 的方法名

| C 运算符符号 | 特殊方法名 | 建议的符合 CLS 的方法名 |
|---|---|---|
| + | op_UnaryPlus | Plus |
| - | op_UnaryNegation | Negate |
| ! | op_LogicalNot | Not |
| ~ | op_OnesComplement | OnesComplement |
| ++ | op_Increment | Increment |
| -- | op_Decrement | Decrement |
| (无) | op_True | IsTrue { get; } |
| (无) | op_False | IsFalse { get; } |

## 表 8-2 C 二元运算符及其符合 CLS 的方法名

| C 运算符符号 | 特殊方法名 | 建议的符合 CLS 的方法名 |
|---|---|---|
| + | op_Addition | Add |
| - | op_Subtraction | Subtract |
| * | op_Multiply | Multiply |
| / | op_Division | Divide |
| % | op_Modulus | Mod |
| & | op_BitwiseAnd | BitwiseAnd |
| | | op_BitwiseOr | BitwiseOr |
| ^ | op_ExclusiveOr | Xor |
| << | op_LeftShift | LeftShift |
| >> | op_RightShift | RightShift |
| == | op_Equality | Equals |
| != | op_Inequality | Equals |
| < | op_LessThan | Compare |
| > | op_GreaterThan | Compare |
| <= | op_LessThanOrEqual | Compare |
| >= | op_GreaterThanOrEqual | Compare |

CLR 规范定义了许多可以重载的额外运算符，但 C# 不支持这些额外运算符。因此，它们并未使用，所以我不会列出它们。如果你对完整列表感兴趣，请参考 ECMA 规范（www.ecma-international.org/publications/standards/Ecma-335.html）通用语言基础设施（CLI），第一部分，概念与架构，第 10.3.1 节（一元运算符）和 10.3.2 节（二元运算符）。

> 如果你检查框架类库（FCL）中的核心数值类型（Int32, Int64, UInt32），发现它们没有定义任何运算符方法。它们之所以不定义，是因为编译器规定了这些原始类型的操作方式，并生成直接操作这些类型实例的 IL 指令。如果这些类型提供了方法，并且编译器生成代码来调用这些方法，那么方法调用将产生运行时性能成本。此外，该方法最终仍需要执行某些 IL 指令来执行预期操作。这就是为什么 FCL 类型不定义任何运算符重载方法的原因。这对你意味着：如果你使用的编程语言不支持某种核心 FCL 类型，那么你将无法对该类型的实例执行任何操作。

## 运算符与编程语言的互操作性

运算符重载可以是一个非常有用的工具，允许开发者用简洁的代码表达他们的想法。然而，并不是所有的编程语言都支持运算符重载。在使用不支持运算符重载的语言时，该语言将知道如何解释 `+` 运算符（除非该类型是该语言中的原始类型），而编译器将生成错误。在使用不支持运算符重载的语言时，语言允许你直接调用所需的 op_ 方法（例如 op_Addition）。

如果你正在使用一种不支持在类型中定义 `+` 运算符重载的语言，显然，该类型仍然可以提供 `op_Addition` 方法。从 C# 的角度来看，预计你可以通过 `+` 运算符调用此 `op_Addition` 方法，但实际上不能。当 C# 编译器检测到它时，它会寻找关联特殊元数据标志的 `op_Addition` 方法，以便编译器确定该 `op_Addition` 方法确实是为了作为运算符重载。由于 `op_Addition` 方法是由不支持重载的语言产生的，该方法将没有特殊标志，C# 编译器将产生编译错误。当然，在任何语言中，你都可以显式调用命名恰好为 op_Addition 的方法，但编译器不会将 `+` 符号的使用转换为对该方法的调用。

## Jeff 对微软运算符命名规则的看法

我确定所有关于何时不能调用运算符重载方法的规则看起来都非常困惑且复杂。如果支持运算符重载的编译器不生成特殊元数据标志，规则将会简单得多，程序员处理那些运算符重载方法时也会更轻松。支持运算符重载的语言将支持运算符符号语法，而所有语言都支持显式调用各种 op 方法。我可以想出任何理由来说微软为什么让事情变得如此困难，我希望他们在未来的编译器版本中放宽这些规则。

对于定义运算符方法的类型，微软建议你定义更友好的公共静态方法，在内部调用运算符重载。例如，重载了 `op_Add` 方法的类型应该定义一个友好的命名方法 `Complex Add`。表 8-1 和 8-2 中的第三列列出了每个运算符建议的友好名称。因此，之前显示的 `Complex` 类型应该如下所示定义。

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
    public static Complex Add(Complex c1, Complex c2) { ... }
}
```

## 转换运算符方法

偶尔，你需要将对象从一种类型转换为另一种类型。例如，我确定你曾在某个时候不得不将 Byte 转换为 Int32。当源类型和目标类型都是原始类型时，编译器知道如何生成必要的代码（强制转换）。如果源类型或目标类型不是原始类型，CLR 会检查源对象是否等于目标类型。例如，System.Xml.Linq 类允许你将可扩展标记语言（XML）元素转换为 Boolean、Int32、Int64、Single、Double、Decimal、String、DateTime、TimeSpan、Guid 或这些任何类型的空等效值。你也可以想象 FCL 包含一个 Rational 类型，这对于将 Int32 或 Single 对象转换为 Rational 对象可能非常方便。此外，如果能……

为了实现这些转换，Rational 类型应该定义接收单个参数的公共构造函数：该参数为你正在转换的类型实例。你还应该定义带有参数的公共实例方法（例如非常流行的 `ToString` 方法）。每个方法将把定义类型的实例转换为目标类型。

```csharp
public sealed class Rational {
    // 从 Int32 构造 Rational
    public Rational(Int32 num) { ... }

    // 从 Single 构造 Rational
    public Rational(Single num) { ... }

    // 将 Rational 转换为 Int32
    public Int32 ToInt32() { ... }

    // 将 Rational 转换为 Single
    public Single ToSingle() { ... }
}
```

