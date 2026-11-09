
转换运算符方法必须是公共的静态方法。此外，C#（以及许多其他语言）要求参数或返回类型中必须有一个与定义该转换方法的类型相同。此限制的原因在于，它使 C# 编译器能够在合理的时间内搜索可能绑定到的运算符方法。以下代码向 Rational 类型添加四个转换运算符方法。

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

    // Implicitly constructs and returns a Rational from an Int32
    public static implicit operator Rational(Int32 num) {
        return new Rational(num);
    }

    // Implicitly constructs and returns a Rational from a Single
    public static implicit operator Rational(Single num) {
        return new Rational(num);
    }

    // Explicitly returns an Int32 from a Rational
    public static explicit operator Int32(Rational r) {
        return r.ToInt32();
    }

    // Explicitly returns a Single from a Rational
    public static explicit operator Single(Rational r) {
        return r.ToSingle();
    }
}
```

对于转换运算符方法，你必须指明编译器能否生成隐式调用转换运算符方法的代码，还是源代码必须显式指明编译器应何时生成调用转换运算符方法的代码。在 C# 中，你使用 implicit 关键字向编译器指明：为了生成调用该方法的代码，源代码中不必出现显式强制转换。explicit 关键字则允许编译器仅在源代码中存在显式强制转换时才调用该方法。

在 implicit 或 explicit 关键字之后，你通过指定 operator 关键字来告诉编译器该方法是一个转换运算符。在 operator 关键字之后，你指定对象要转换到的类型；在括号中，你指定对象要从哪个类型转换。

在前面的 `Rational` 类型中定义转换运算符后，你就可以编写如下代码（在 C# 中）。

```csharp
public sealed class Program {
    public static void Main() {
        Rational r1 = 5;         // Implicit cast from Int32 to Rational
        Rational r2 = 2.5F;      // Implicit cast from Single to Rational

        Int32 x = (Int32) r1;    // Explicit cast from Rational to Int32
        Single s = (Single) r2;  // Explicit cast from Rational to Single
    }
}
```

在幕后，C# 编译器会检测代码中的强制转换（类型转换），并在内部生成 IL 代码，以调用由 `Rational` 类型定义的转换运算符方法。但这些方法叫什么名字呢？编译 `Rational` 类型并检查其元数据可以看出，编译器会为每个已定义的转换运算符生成一个方法。对于 `Rational` 类型，四个转换运算符方法的元数据如下所示。

```
public static Rational op_Implicit(Int32 num)
public static Rational op_Implicit(Single num)
public static Int32    op_Explicit(Rational r)
public static Single   op_Explicit(Rational r)
```

如你所见，将对象从一种类型转换为另一种类型的方法始终命名为 `op_Implicit` 或 `op_Explicit`。只有在转换过程中不会丢失精度或数量级时（例如将 `Int32` 转换为 `Rational`），才应定义隐式转换运算符。然而，如果转换过程中会丢失精度或数量级（例如将 `Rational` 对象转换为 `Int32`），则应定义显式转换运算符。如果显式转换失败，应通过让显式转换运算符方法抛出 `OverflowException` 或 `InvalidOperationException` 来指明这一点。

![](img/857bdf6cef9e242b53a37f88df9a1287_222_0.png)

> **注意** 这两个 `op_Explicit` 方法接受相同的参数，即一个 `Rational`。然而，这两个方法的不同之处在于它们的返回类型：一个返回 `Int32`，另一个返回 `Single`。这是一个两个方法仅返回类型不同的示例。CLR 完全支持一个类型定义多个仅返回类型不同的方法。然而，很少有语言公开这种能力。你可能已经知道，C++、C#、Visual Basic 和 Java 都是不支持定义多个仅返回类型不同方法的语言示例。少数语言（例如 IL 汇编语言）允许开发者显式选择调用这些方法中的哪一个。当然，IL 汇编语言程序员不应利用这种能力，因为他们定义的方法无法从其他编程语言调用。尽管 C# 没有向 C# 程序员公开这种能力，但当类型定义转换运算符方法时，编译器确实会在内部利用这种能力。

即 StringBuilderExtensions 类甚至存在。第二个问题是，代码没有反映在 StringBuilder 对象上执行的操作顺序，这使得代码难以编写、阅读和维护。程序员希望先调用 Replace，再调用 IndexOf；但是当你从左到右阅读最后一行代码时，IndexOf 先出现在该行，Replace 则后出现。当然，你可以通过像下面这样重写代码来缓解这个问题，并使代码的行为更易于理解。

```csharp
// First, change period to exclamation mark
sb.Replace('.', '!');
```

```csharp
// Now, get # characters in 1st sentence (5)
Int32 index = StringBuilderExtensions.IndexOf(sb, '!');
```

然而，这段代码的两个版本都存在第三个问题，它会影响对代码行为的理解。StringBuilderExtensions 的使用过于突出，会使程序员分心，无法专注于正在执行的操作：IndexOf。如果 StringBuilder 类定义了自己的 IndexOf 方法，那么我们就可以像下面这样重写上面的代码。

```csharp
// Change period to exclamation and get # characters in 1st sentence (5).
Int32 index = sb.Replace('.', '!').IndexOf('!');
```

哇，看看这在代码可维护性方面有多棒！在 StringBuilder 对象中，我们要把句号替换为感叹号，然后查找该感叹号的索引。

现在，我可以解释 C# 的扩展方法功能是做什么的了。它允许你定义一个静态方法，并可以使用实例方法语法来调用它。或者换句话说，我们现在可以定义自己的 IndexOf 方法，上面提到的三个问题也就消失了。要把 IndexOf 方法变成扩展方法，只需在第一个参数前添加 this 关键字。

```csharp
public static class StringBuilderExtensions {
    public static Int32 IndexOf(this StringBuilder sb, Char value) {
        for (Int32 index = 0; index < sb.Length; index++)
            if (sb[index] == value) return index;
        return -1;
    }
}
```

现在，当编译器看到如下代码时，编译器首先检查 StringBuilder 类或其任何基类是否提供了一个名为 IndexOf、接受单个 Char 参数的实例方法。

```csharp
Int32 index = sb.IndexOf('X');
```

如果存在现有的实例方法，则编译器会生成调用它的 IL 代码。如果不存在匹配的实例方法，则编译器会查看所有定义了名为 IndexOf 的静态方法的静态类，这些静态方法的第一个参数类型与用于调用该方法的表达式的类型匹配。该类型还必须用 this 关键字标记。在此示例中，表达式是 sb，其类型为 StringBuilder。在这种情况下，编译器会专门查找一个接受两个参数的 IndexOf 方法：一个 StringBuilder（用 this 关键字标记）和一个 Char。编译器将找到我们的 IndexOf 方法，并生成调用我们静态方法的 IL 代码。

