
```
PerfTest1: 00:00:01.9619358 BeforeFieldInit
PerfTest1: 00:00:06.2374912 Precise
PerfTest2: 00:00:03.1576608 BeforeFieldInit
PerfTest2: 00:00:03.1557822 Precise
```

当 C# 编译器看到一个带有内联初始化静态字段的类（即 `BeforeField` 类）时，编译器会生成该类的类型定义表项，并带有 `BeforeField` 标志。当 C# 编译器看到一个带有静态字段显式初始化的类时，它会生成带有 `BeforeFieldInit` 标志的类型定义表项。运行时静态字段的初始化需要在字段被访问之前完成，而显式类型构造函数可以在精确的时间执行。

从输出可以看出，这种决定带来了巨大的性能影响。当 `PerfTest1` 运行时，顶部执行了 1.96 秒，底部执行了 6.24 秒。当 `PerfTest2` 运行时，时间非常接近，因为 JIT 编译器知道类型构造函数已经执行过了。

如果 C# 允许程序员在源代码中显式设置 `BeforeFieldInit` 标志，而不是由编译器做决定，那就好了。

## 运算符重载方法

某些语言允许运算符重载，并且 CLR 规范要求运算符方法是公共且静态的。此外，C# 要求运算符的至少一个参数必须与运算符方法所在的类型相同。这种限制的原因是为了让 C# 编译器能够在合理的时间找到可能的方法。

以下是在 C# 类中定义运算符的的示例：

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
}
```

编译器会生成一个名为 `op_Addition` 的方法元数据项；该方法项还设置了 `special` 标志，表示这是一个“特殊”方法。语言编译器（包括 C# 编译器）看到源代码中指定的 `+` 运算符时，会查找操作数类型是否定义了与操作数类型兼容的名为 `op_Addition` 的特殊方法。如果该方法存在，编译器就会生成调用方法的代码。如果没有，将发生编译错误。表 8-1 和 8-2 显示了 C# 支持重载的一元和二进制运算符集合，以及编译器生成的对应的通用语言规范（CLS）方法名。

### 表 8-1 C# 一元运算符及其对应的 CLS 规范方法名

| C# 运算符符号 | 特殊方法名 | 建议的 CLS 规范方法名 |
|---|---|---|
| `+` | `op_UnaryPlus` | `Plus` |
| `-` | `op_UnaryNegation` | `Negate` |
| `!` | `op_LogicalNot` | `Not` |
| `~` | `op_OnComplement` | `OnesComplement` |
| `++` | `op_Increment` | `Increment` |
| `--` | `op_Decrement` | `Decrement` |
| `(none)` | `op_True` | `IsTrue { get; }` |
| `(none)` | `op_False` | `IsFalse { get; }` |

### 表 8-2 C# 二进制运算符及其符合 CLS 标准的方法名

| C# 运算符符号 | 特殊方法名 | 建议的符合 CLS 标准的方法名 |
| --- | --- | --- |
| `+` | `op_Addition` | `Add` |
| `-` | `op_Subtraction` | `Subtract` |
| `*` | `op_Multiply` | `Multiply` |
| `/` | `op_Division` | `Divide` |
| `%` | `op_Modulus` | `Mod` |
| `&` | `op_BitwiseAnd` | `BitwiseAnd` |
| `|` | `op_BitwiseOr` | `BitwiseOr` |
| `^` | `op_ExclusiveOr` | `Xor` |
| `<<` | `op_LeftShift` | `LeftShift` |
| `>>` | `op_RightShift` | `RightShift` |
| `==` | `op_Equality` | `Equals` |
| `!=` | `op_Inequality` | `Compare` |
| `<` | `op_LessThan` | `Compare` |
| `>` | `op_GreaterThan` | `Compare` |
| `<=` | `op_LessThanOrEqual` | `Compare` |
| `>=` | `op_GreaterThanOrEqual` | `Compare` |

CLR 定义了许多可以重载的额外运算符，但 C# 并不支持这些额外运算符。因此，它们没有被使用，我不会在此列出它们。如果你对完整列表感兴趣，请参考通用语言基础设施（CLI）的 ECMA 规范（`www.ecma-international.org/publications/standards/Ecma-335.htm`），第一部分，概念与架构，第 10.3.1 节（一元运算符）和 10.3.2 节（二进制运算符）。

> 如果你检查框架类库（FCL）中的核心数值类型（`Int32`、`Int64`、`UInt32` 等），你会发现它们没有定义任何运算符重载方法。部分原因是编译器会专门查找针对这些原始类型的操作，并发出直接操作这些类型实例的 IL 指令。如果这些类型提供了方法，并且编译器生成了调用这些方法的代码，那么方法调用将产生产生运行时性能开销。此外，该方法最终仍然必须执行某些 IL 指令来执行预期的操作。这就是为什么核心 FCL 类型没有定义任何运算符重载方法的原因。这对你来说意味着：如果你使用的编程语言不支持某种核心 FCL 类型，那么你将无法对该类型的实例执行任何操作。

## 运算符与编程语言的互操作性

运算符重载可以是一个非常有用的工具，允许开发者用简洁的代码表达他们的想法。然而，并不是所有的编程语言都支持运算符重载。当使用不支持运算符重载的语言时，语言将不知道如何解释 `+` 运算符（除非该类型是语言中的原始类型），编译器将产生错误。在使用不支持运算符重载的语言时，语言应该允许直接调用所需的 `op_` 方法（例如 `op_Addition`）。

如果你正在使用一种不支持在类型中定义 `+` 运算符重载的语言，显然该类型仍然可以提供 `op_Addition` 方法。从 C# 的角度来看，你可能期望可以使用 `+` 运算符调用这个 `op_Addition` 方法，但不能。当 C# 编译器检测到 `+` 运算符时，它会寻找关联有特殊标记的 `op_Addition` 方法，以便编译器确定该 `op_Addition` 方法用于运算符重载。由于 `op_Addition` 方法是由不支持运算符重载的语言生成的，该方法将不会关联特殊标记，C# 编译器将产生编译错误。当然，在任何语言中都可以显式调用恰好命名为 `op_Addition` 的方法，但编译器不会将 `+` 符号的使用翻译为该方法。

## Jeff 对微软运算符方法命名规则的观点

我确信，所有关于何时可以和不能调用运算符重载的规则看起来非常混乱且过于复杂。如果编译器支持运算符重载只是不发出特殊的元数据标记，规则将会简单得多，程序员在处理提供运算符方法的类型时也会变得更轻松。支持运算符重载的语言将支持运算符语法，而所有语言都支持显式调用各种 `op_` 方法。我找不出微软把这搞得这么复杂的理由，我希望他们在未来的编译器版本中放这些规则。

对于定义了运算符重载方法的类型，微软建议你还要定义更友好的静态方法，在内部调用运算符重载方法。例如，一个重载了 `op_Addition` 方法的类型应该定义一个名为 `Add` 的公共友好方法。表 8-1 和表 8-2 中的第三列列出了每个运算符的建议友好名称。因此，之前所示的 `Complex` 类型应该以此方式定义：

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
    public static Complex Add(Complex c1, Complex c2) { return(c1 + c2); }
}
```

当然，用任何编程语言编写的代码都可以调用任何友好运算符方法，例如 `Add`。微软关于类型提供这些友好方法名称的指南让情况变得更加复杂。我觉得这种额外的复杂性是没有必要的，除非 JIT 编译器会将友好命名方法中的 FCL 内联。否则调用这些友好命名方法会导致额外的性能损失。内联代码将导致 JIT 编译器优化代码，移除额外的方法调用并提高运行时性能。

> 注意：关于重载运算符并使用友好方法名称作为微软设计指南的类型示例，请参阅...

## 转换方法

有时，你需要将一个对象从一种类型转换为另一种类型。在上节中，我讨论了某些编程语言如何提供运算符重载。那么，某些编程语言（如 C#）也提供转换重载。转换运算符是将对象从一种类型转换为另一种类型的方法。你可以使用特殊语法定义转换方法。CLR 规范规定转换重载方法必须是公共且静态的。此外，C#（以及许多其他语言）要求参数或返回类型必须与类相同。这种限制的原因是它让 C# 编译器能够在合理的时间内搜索到可以绑定的运算符方法。以下代码为 `Rational` 类型添加了四个转换运算符：

```csharp
sealed class Rational {
    // 从 Int32 构造 Rational
    public Rational(Int32 num) { ... }
    // 从 Single 构造 Rational
    public Rational(Single num) { ... }
    // 将 Rational 转换为 Int32
    public Int32 ToInt32() { ... }
    // 将 Rational 转换为 Single
    public Single ToSingle() { ... }
    // 隐式从 Int32 构造并返回 Rational
    public static implicit operator Rational(Int32 num) {
        return new Rational(num);
    }
    // 隐式从 Single 构造并返回 Rational
    public static implicit operator Rational(Single num) {
        return new Rational(num);
    }
    // 显式从 Rational 返回 Int32
    public static explicit operator Int32(Rational r) {
        return r.ToInt32();
    }
}
```

```csharp
// 显式地从 Rational 返回 Single
public static explicit operator Single(Rational r) {
    return r.ToSingle();
}
```

对于转换运算符方法，你必须指示编译器是否可以隐式生成代码来调用转换运算符方法，或者源代码是否可以显式地指示编译器何时生成代码来调用转换运算符方法。在 C# 中，你使用 `implicit`（隐式）关键字告诉编译器，源代码不需要出现显式类型转换即可生成调用该方法的代码。`explicit`（显式）关键字允许编译器仅在源代码中存在显式类型转换时才调用该方法。

在 `implicit` 或 `explicit` 关键字之后，你通过指定 `operator` 关键字告诉编译器该方法是一个转换运算符。在 `operator` 关键字之后，你指定对象要转换到的类型；在括号中，你指定对象要转换的源类型。

在前面的 `Rational` 类型中定义转换运算符允许你编写如下代码（C#）：

```csharp
public sealed class Program {
    public static void Main() {
        Rational r1 = 5; // 从 Int32 到 Rational 的隐式转换
        Rational r2 = 2.5; // 从 Single 到 Rational 的隐式转换
        Int32 x = (Int32) r1; // 从 Rational 到 Int32 的显式转换
        Single s = (Single) r2; // 从 Rational 到 Single 的显式转换
    }
}
```

在底层，C# 编译器会检测代码中的强制转换（类型转换），并在内部生成调用由 `Rational` 类型定义的转换方法的 IL 代码。这些方法的名称是什么呢？嗯，编译 `Rational` 类型并检查其元数据可以发现，编译器为每个定义的转换运算符都产生一个方法。对于 `Rational` 类型，四个转换运算符的元数据如下：

```csharp
public static Rational op_Implicit(Int32 num)
public static Rational op_Implicit(Single num)
public static Int32 op_Explicit(Rational r)
public static Int32 op_Explicit(Single r)
```

如你所示，从一种类型转换为另一种类型的方法始终命名为 `op_Implicit` 或 `op_Explicit`。只有在转换过程中不会丢失精度或大小时，你才定义隐式转换运算符，例如将 `Int32` 转换为 `Rational`。然而，如果在转换过程中丢失了精度或大小（当将 `Rational` 对象转换为 `Int32` 时），你应该定义显式转换运算符。如果显式转换失败，你应该通过让显式转换运算符方法抛出 `OverflowException` 或 `InvalidOperationException` 来指示这一点。

> 注意，`op_Explicit` 方法接收相同的参数，即 `Rational`。这些方法的区别在于返回值，一个是 `Int32`，另一个 `Single`。这是两个仅按返回类型不同的方法的示例。CLR 支持定义多个仅按返回类型不同的方法的能力。然而，很少有语言提供这种能力：你可能已经知道，C++、C#、Visual Basic 和 Java 都是不支持定义仅按返回类型不同的多个方法的语言示例。少数语言（如 IL 汇编语言）允许开发者显式地选择调用这些方法中的哪一个。当然，IL 汇编程序员利用了这种能力，因为定义的方法无法从其他编程语言中调用。尽管如此，C# 编译器在类型定义转换运算符方法时在内部利用了这种能力。

C# 对转换运算符有完全支持。当它检测到你正在使用一种类型的对象，而期望使用另一种不同类型的对象时，编译器会搜索能够执行该转换的隐式转换运算符方法，并生成匹配的代码。如果存在隐式转换运算符，编译器会在生成的 IL 中对其进行调用。如果编译器看到显式将对象从一种类型强制转换为另一种类型的源代码，编译器会搜索隐式或显式转换运算符方法。如果存在，编译器将生成对该方法的调用。如果编译器无法找到合适的转换运算符方法，它将发出错误且不编译代码。

> 注意，C# 使用强制转换表达式来生成调用显式转换运算符的代码；当在使用 C# 的 `as` 或 `is` 运算符时，它们永远不会被调用。

为了真正理解理解重载方法和转换运算符方法，我强烈建议你查看 `System.Decimal` 类型并作为模型。`Decimal` 定义了几个构造函数，允许你将各种类型的对象转换为 `Decimal`。它还提供了 `ToXXX` 方法，允许你将 `Decimal` 对象转换为另一种类型。最后，该类型还定义了几个转换运算符和重载方法。

## 扩展方法

理解 C# 扩展方法性的最好方法是通过示例。在第 14 章“字符、字符串与文本处理”的“StringBuilder 成员”部分，我提到 `StringBuilder` 类提供了比 `String` 类更少的用于处理字符串的方法，并提到这很奇怪，考虑到 `StringBuilder` 类是处理字符串的首选方式，因为它是可变的。那么，假设你想要自己定义这些缺失的方法来对 `StringBuilder` 进行操作。例如，你可能想如下定义你的 `IndexOf` 方法：

```csharp
public static class StringBuilderExtensions {
    public static Int32 IndexOf(StringBuilder sb, Char value) {
        for (Int32 index = 0; index < sb.length; index++)
            if (sb[index] == value) return index;
        return -1;
    }
}
```
