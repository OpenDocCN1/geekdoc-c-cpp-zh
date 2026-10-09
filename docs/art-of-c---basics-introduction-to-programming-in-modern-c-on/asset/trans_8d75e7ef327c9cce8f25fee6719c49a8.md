
## 第17课 有理数

### 17.1. 引言

不同的编程语言对 OOP（面向对象编程）的支持方式各不相同。在 C# 中，一切都是“对象”。至少在语法层面上是这样。这就是我们称其为面向对象编程语言的原因。

如前所述，“静态方法”更像函数。在 Java 和 C# 这类“纯 OOP”语言中，将它们定义在类（或结构体、接口等）内部而非全局范围内，实际上是一种“取巧”的做法。并非所有事物都能完全契合 OOP 风格。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_267_0.png)

尽管如此，与全局定义的函数相比，静态方法确实提供了一些优势。例如，静态类中的静态变量（静态方法可以访问和操纵这些变量）并不是“全局变量”。（至少在技术上是这样，尽管在实际中，大型类/对象的静态变量和实例变量与“全局变量”一样糟糕。）静态方法仍然提供了一定程度的“数据隐藏”。

在上一课中，我们使用类定义了一个类型，即 `Caesar.Cipher`。在本课中，让我们尝试使用结构体（struct）定义一个新的类型。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_268_0.png)

### 17.2. 代码审查

有理数是能表示为两个整数之比（分子和非零分母）的数。

例如，0.6 是有理数，因为它可以表示为 3/5。另一方面，π 不是有理数，因为不存在这样的表示法。如果你需要复习，这里是维基百科关于有理数的文章链接：[Rational Number](https://en.wikipedia.org/wiki/Rational_number)。

在本课中，我们使用 struct 定义一个值类型 `Number.Rational`。主程序展示了 Rational 类型值的几种用法。

rational-number/Program.cs (第 3-17 行)

```csharp
var a = new Rational(4, 8);
var b = new Rational(9, 12, true);
Console.WriteLine($"a = {a}; b = {b}");

var sum = a + b;
Console.WriteLine($"Sum =\t{sum}");

var sub = a - b;
Console.WriteLine($"Sub =\t{sub}");

var prod = a * b;
Console.WriteLine($"Prod =\t{prod}");

var div = a / b;
Console.WriteLine($"Div =\t{div}");
```

rational-number/Program.cs (第 19-26 行)

```csharp
var c = new Rational(1, 2);
Console.WriteLine($"c = {c}");

if (a.Equals(c)) {
    Console.WriteLine("a == c");
} else {
    Console.WriteLine("a != c");
}
```

Rational 类型被定义为公开的 "readonly struct"（只读结构体）：

```csharp
public readonly struct Rational {
    private readonly ulong num, den;
    private readonly bool neg;

    public Rational()
        : this(0, 1) { }

    public Rational(ulong numer, ulong denom)
        : this(numer, denom, false) { }

    public Rational(ulong numer, ulong denom, bool negat) {
        if (denom == 0) {
            throw new ArgumentException("Zero denominator");
        }

        if (numer == 0) {
            (num, den, neg) = (0, 1, false);
        } else {
            var cf = GCD(numer, denom);
            (num, den, neg) = (numer / cf, denom / cf, negat);
        }
    }
}
```

“重载”一元运算符 + 和 -：

```csharp
public static Rational operator +(Rational a) => a;
public static Rational operator -(Rational a) =>
    new(a.num, a.den, !a.neg);
```

“重载”二元运算符 +, -, *, 和 /：

rational-number/Rational.cs (第 30-50 行)

```csharp
public static Rational operator +(Rational a, Rational b) {
    var cf = GCD(a.den, b.den);
    var (f1, f2) = (a.den / cf, b.den / cf);
    var denom = cf * f1 * f2;

    ulong numer;
    bool negat;
    if (a.neg == b.neg) {
        numer = a.num * f2 + b.num * f1;
        negat = a.neg;
    } else {
        var (n1, n2) = (a.num * f2, b.num * f1);
        (numer, negat) = (n1, n2) switch {
            var (x, y) when x == y => (0ul, false),
            var (x, y) when x > y => (n1 - n2, a.neg),
            _ => (n2 - n1, b.neg),
        };
    }

    return new(numer, denom, negat);
}
```

rational-number/Rational.cs (第 52-53 行)

```csharp
public static Rational operator -(Rational a, Rational b) =>
    a + (-b);
```

rational-number/Rational.cs (第 55-56 行)

```csharp
public static Rational operator *(Rational a, Rational b) =>
    new(a.num * b.num, a.den * b.den, a.neg ^ b.neg);
```

rational-number/Rational.cs (第 58-61 行)

```csharp
public static Rational operator /(Rational a, Rational b) =>
    (b.num != 0)
    ? new(a.num * b.den, a.den * b.num, a.neg ^ b.neg)
    : throw new DivideByZeroException();
```

`object.ToString()` 方法被“重写”：

rational-number/Rational.cs (第 63-64 行)

```csharp
public override string? ToString() =>
    $"{(neg ? "-" : "")}{num}/{den}";
```

一个实现“欧几里得算法”以计算最大公约数（GCD）的私有辅助静态方法：

rational-number/Rational.cs (第 66-71 行)

```csharp
private static ulong GCD(ulong a, ulong b) {
    while (b > 0) {
        (a, b) = (b, a % b);
    }
    return a;
}
```

### 17.3. 结对编程 - 值类型、方法重写、运算符重载

所有的值类型，无论是内置值类型还是自定义的 struct 和 enum 类型，都继承自 `System.ValueType`，并最终继承自 `System.Object`。

如前所述，C#（以及 .NET）使用“统一类型系统”。在 C# 中，每个类型都是 object 的子类型，或者在 .NET 中是 `System.Object` 的子类型。换句话说，C# 中的每个类型都直接或间接地“派生”自 `object`。

类型 A 从另一个类型 B *派生*，意味着它包含或“继承”了父类型 B 的所有“行为”。而且，子类型 A 可能还具有父类型中不存在的其他“行为”。

在 C# 中，类型的“行为”由一组公共属性和方法表示。

在 C# 中，使用 `class`、`struct`、`record` 或 `record struct` 定义的类型还可以包含并使用某些内部数据，例如定义在其父类型中的 `public` 或 `protected` 字段。

在 C# 中，使用 `class`、`struct`、`record`、`record struct` 或 `interface` 定义的類型还可以使用其父类型的某些实现，即它们的 `public` 或 `protected` 属性和方法。

请注意，`public` 方法和属性既可以是“行为”，也可以是“实现”。虽然子类型或派生类型不能覆盖或更改行为或契约（例如 API），但如果在允许的情况下，它可以“重写”父类的实现。

非 `sealed` 的类或 record 类可以使用 `virtual` 修饰符在其定义前标记某些属性或方法，从而允许任何子类或子 record 类进行重写。非虚属性和方法的实现不能被重写。

`abstract` 类型（类或 record 类）也可以使用 `abstract` 修饰符在其声明前声明某些属性或方法*必须*由其子类型重写。抽象属性或方法声明不能包含其定义。

或者，换句话说，没有定义的方法或属性必须标记为 `abstract`。包含至少一个抽象方法或属性的类型必须声明为 `abstract` 类型（类或 record 类）。然而，`abstract` 类型不必包含任何抽象属性或抽象方法。无论是否包含任何抽象属性或方法，抽象类或抽象 record 都不能实例化。

接口中的所有公共方法和属性都是隐式的 virtual 或 abstract，具体取决于它们是否具有默认实现，并且它们始终可以被重写。接口中的抽象方法必须在其（非抽象）子类的类、结构体或 record 中实现。

就像抽象类（或 record）一样，接口不能直接实例化。

既然我们可以在接口中包含（默认）实现，抽象类和接口之间几乎没有区别。

主要且本质的区别在于接口不能包含数据（例如，“字段”）。除此之外，在大多数情况下，选择哪一个作为其他自定义类型的基础取决于程序员。一般来说，如果涉及“纯行为”，则首选接口。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_274_0.png)

另一件需要注意的事情是，C# 在处理具体基类型时只支持“单继承”。也就是说，一个具体类型不能有多个具体类型父类。还应该注意的是，结构体可以实现接口，但不能继承其他结构体。因此，从广义上讲，通常首选接口。

继承自接口 I 的非接口子类型 X 可以为其父接口 I 的属性和方法提供实现。如果没有在 I 或其任何祖先中提供默认实现，那么具体子类型 X 必须这样做。在这种情况下，我们说具体类型 X“实现”了接口 I。（也就是说，不使用更通用的术语“继承”。）

正如刚所述，一个类最多只能继承自一个（非 sealed）父类。同样，一个 record 类最多只能继承自一个（非 sealed）父类
