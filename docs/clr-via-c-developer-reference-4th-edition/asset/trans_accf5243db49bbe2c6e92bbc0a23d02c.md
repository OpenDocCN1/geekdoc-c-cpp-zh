
重载公有方法和静态方法。此外，C#（以及许多其他语言）要求参数类型或返回类型必须与定义转换方法的类型相同。这种限制的原因是它能让 C# 编译器在合理的时间内搜索可能的绑定的操作符方法。以下代码为 `Rational` 类型添加四个转换操作符方法：

```csharp
public sealed class Rational {
    // 从 Int32 构造 Rational
    public Rational(Int32 num) { ... }

    // 从 Single 构造 Rational
    public Rational(Single num) { ... }

    // 将 Rational 转换为 Int32
    public Int32 ToInt32() { ... }

    // 将 Rational 转换为 Single
    public Single ToString() { ... }

    // 从 Int32 隐式构造并返回 Rational
    public static implicit operator Rational(Int32 num) {
        return new Rational(num);
    }

    // 从 Single 隐式构造并返回 Rational
    public static implicit operator Rational(Single num) {
        return new Rational(num);
    }

    // 从 Rational 显式返回 Int32
    public static explicit operator Int32(Rational r) {
        return r.ToInt32();
    }

    // 从 Rational 显式返回 Single
    public static explicit operator Single(Rational r) {
        return r.ToString();
    }
}
```

对于转换操作符方法，你必须指示编译器是可以隐式地生成代码调用转换操作符方法，还是必须在源代码中显式指示编译器何时生成代码调用转换操作符方法。在 C# 中，使用 `implicit` 关键字告诉编译器，源代码中不需要出现显式强制转换即可生成调用该方法的代码。`explicit` 关键字允许编译器仅在源代码中存在显式强制转换时才调用该方法。

在 `implicit` 或 `explicit` 关键字之后，通过指定 `operator` 关键字告诉编译器该方法是一个转换操作符。在 `operator` 关键字之后，你指定对象要转换的类型；在括号中，你指定对象转换自类型。

在前面的 `Rational` 类型中定义转换操作符，允许你编写如下代码（在 C# 中）。

```csharp
public sealed class Program {
    public static void Main()
    {
        Rational r1 = 5; // 从 Int32 到 Rational 的隐式转换
        Rational r2 = 2.5F; // 从 Single 到 Rational 的隐式转换

        Int32 x = (Int32) r1; // 从 Rational 到 Int32 的显式转换
        Single s = (Single) r2; // 从 Rational 到 Single 的显式转换
    }
}
```

在底层，C# 编译器会检测代码中的强制转换（类型转换），并在内部生成调用 `Rational` 类型定义的转换操作符方法的 IL 代码。但这些方法的名称是什么呢？编译 `Rational` 类型并检查其数据显示，编译器为为定义的每个转换操作符生成一个方法。对于 `Rational` 类型，四个转换操作符方法的元数据所示：

```csharp
public static Rational op_Implicit(Int32 num)
public static Rational op_Implicit(Single num)
public static Int32 op_Explicit(Rational r)
public static Single op_Explicit(Rational r)
```

你可以看到，将对象从一个类型转换为另一个类型的方法总是命名为 `op_Implicit` 或 `op_Explicit`。当转换过程中不会丢失精度或数量级时（例如将 `Int32` 转换为 `Rational`），你应该定义一个隐式转换操作符。如果在转换过程中丢失了精度或数量级（当将 `Rational` 对象转换为 `Int32`），你应该定义一个显式转换操作符。如果显式转换失败，你应该通过让转换操作符方法抛出 `OverflowException` 或 `InvalidOperationException` 来指示这一点。

> 这两个 `op_Explicit` 方法接收相同的参数，即 `Rational`。然而，方法的返回类型不同，分别为 `Int32` 和 `Single`。这是一个仅返回类型不同的方法示例。CLR 完全支持定义仅返回类型不同的方法。然而，很少有语言 这种这种能力。你可能知道，C++、Visual Basic 和 Java 都是不支持定义仅返回类型不同的方法的语言示例。少数语言（如 IL 汇编）允许开发者显式选择调用这些方法中的一个。IL 汇编程序员不应该利用这种能力，因为它们是从其他语言可调用的。尽管 C# 没有将这种能力暴露给程序员，但编译器在定义转换操作符方法时内部利用了这种能力。

![](img/0ce3b78d061e3d3095fa554b1adf222_0.png)

C# 对转换操作符有完全的支持。当它检测到代码中使用一种类型的对象并期望另一种类型时，它会搜索能够执行转换的方法并生成调用该方法的代码。如果存在隐式转换操作符方法，编译器会在 IL 代码中发射方法的调用。如果编译器发现从一种类型到另一种类型的显式转换代码，它会搜索隐式或显式转换操作符方法。如果找不到合适的转换操作符方法，它会发出错误且不编译代码。

> 注意：C# 在使用强制转换表达式时会生成调用显式转换操作符的代码；或者不调用。要真正理解重载方法和转换操作符方法，我强烈建议你检查 `System.Decimal`。`Decimal` 定义了几个构造函数，允许你从各种类型转换为 `Decimal`。它还提供了让 `Decimal` 对象转换为另一种类型的方法。最后，类型定义了隐式转换操作符和重载方法。

## 扩展方法

理解 C# 扩展方法的最佳方法是通过示例。在第 14 章“字符、字符串和文本处理”的“StringBuilder 成员”部分，我提到 `StringBuilder` 类比 `String` 类提供了更好的方法来操作和处理字符串，因为它是可变的。所以，假设你想在 `StringBuilder` 上自己定义一些缺失的方法。如下所示：

```csharp
public static class StringBuilderExtensions {
    public static Int32 IndexOf(StringBuilder sb, char value) {
        for (Int32 index = 0; index < sb.Length; index++) {
            if (sb[index] == value) return index;
        }
        return -1;
    }
}
```

现在你定义了这个方法，可以像下面的代码所示使用它：

```csharp
StringBuilder sb = new StringBuilder("Hello. My name is Jeff."); // 初始字符串
// 将点替换为感叹号并查找 '#'
Int32 index = StringBuilderExtensions.IndexOf(sb.Replace('.', '!'), '#');
```

这段代码运行良好良好，但从程序员的角度来看并不理想。第一个问题是，想要获取 `StringBuilder` 中字符索引的程序员必须知道 `StringBuilderExtensions` 类的存在。第二个问题是代码没有反映在 `StringBuilder` 对象上执行的操作顺序，导致代码难以编写、读取和维护。程序员想要先调用 `Replace` 然后调用 `IndexOf()`；但当你从左到右读取最后一行代码时，`IndexOf` 先出现，`Replace` 后出现。当然，你可以通过如下重写代码使其行为更易于理解来缓解这个问题：

```csharp
// 首先将点替换为感叹号
sb.Replace('.', '!');
```

```csharp
// 现在查找 '#'
Int32 index = StringBuilderExtensions.IndexOf(sb, '!');
```

然而，这两个版本的代码都存在第三个问题，影响代码的行为。使用 `StringBuilderExtensions` 是过强的，并分散了程序员对执行的操作——`IndexOf` 的注意力。如果 `StringBuilder` 类定义了自己的 `IndexOf` 方法，那么我们就可以如下重写代码：

```csharp
// 将点替换为感叹号并查找 '#'
Int32 index = sb.Replace('.', '!').IndexOf('!');
```

现在，我可以解释 C# 扩展方法功能是如何工作的。它允许你定义一个静态方法，但像使用实例方法一样调用它。换句话说，我们可以定义我们的 `IndexOf` 方法，上述三个问题都消失了。只需将 `this` 关键字作为第一个参数即可。

```csharp
public static class StringBuilderExtensions {
    public static Int32 IndexOf(this StringBuilder sb, char value) {
        for (Int32 index = 0; index < sb.Length; index++) {
            if (sb[index] == value) return index;
        }
        return -1;
    }
}
```

现在，当编译器看到下面的代码时，首先检查 `StringBuilder` 类或其任何基类是否有一个接受单个 `Char` 参数的名为 `IndexOf` 的实例方法。

```csharp
Int32 index = sb.IndexOf('!');
```

如果存在现有方法，编译器将查看任何静态类，以寻找名为 `IndexOf` 的静态方法，该方法的第一个参数类型与用于调用方法的表达式类型匹配。该类型也必须标记为 `this` 关键字。例如，表达式是 `sb`，它是 `StringBuilder` 类型。在这种情况下，编译器专门寻找一个接受两个参数的 `IndexOf` 方法：`StringBuilder`（标记为 `this`）和一个 `Char`。编译器将找到我们的 `IndexOf` 方法并产生调用我们静态方法的 IL。

