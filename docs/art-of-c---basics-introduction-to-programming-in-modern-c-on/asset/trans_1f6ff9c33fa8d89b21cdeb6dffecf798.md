
record 类。类、结构体或 record 类型（record class 和 record struct），以及接口类型，可以继承自零个、一个或多个接口类型。

> 当具体类型实现多于一个接口时，我们仍然可以使用“多重继承”这个术语，就像接口从多个父接口继承时一样。如前所述，并非所有人都可能对这些术语达成一致，但重要的是概念，而不是我们使用的词语。

继承自一个类型的类型也可以被另一个类型所继承。理论上，没有限制。父子层级关系可以像你希望的那样长，或那样深。然而，在实践中，非常大的类型层级关系相当罕见。（如前文所暗示的，继承有一些性能影响。）

C#.NET 中唯一的约束是每个类或 record class 类型都应该直接或间接地继承自 `System.Object`。

如上所述，`enum` 和 `struct`（以及 `record struct`）类型（隐式地）分别继承自 `System.Enum` 和 `System.ValueType`。`System.Enum` 继承自 `System.ValueType`，而 `System.ValueType` 又继承自 `System.Object`。

`enum` 类型不能从 `System.Enum` 以外的任何类型继承。`struct` 类型，包括 `record struct` 类型，只能从 `System.ValueTypes` 以外的接口继承。

派生类型的对象可以用作预期其父类型对象的地方。这被称为“多态性”（Polymorphism）。（或者，“基于接口的多态性”）

特别地，只要类型 X（类、record 或接口）直接或间接地继承自类型 Y，类型 X 的引用变量就可以替代类型 Y 的引用使用。

对于 `struct` 或 `record struct` 这类值类型，我们不能直接使用多态性。但是，可以通过 struct 类型实现的接口来实现，这需要“装箱”（boxing）和“拆箱”（unboxing）。稍后会更详细地讨论这一点。

正如前文所述，由于多态性需要某种形式的“间接引用”，而引用在定义上“指向”其底层数据（这是一种一级间接引用），因此我们只能对引用类型使用多态行为。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_276_0.png)

如果你是 C# 的新手，要消化这些信息可能有点多。但一旦你在 C# 编程中积累了一些经验，这些“规则”就会显得自然。此时你不需要“记忆”它们。

（最终的）基类型 System.Object 定义了以下三个虚方法，以及其他一些方法：

```
public virtual bool Equals (object? obj);
public virtual int GetHashCode ();
public virtual string? ToString ();
```

这些方法在所有类型中都有定义并可用，无论是内置类型还是用户定义类型，因为 .NET 中的每个类型都继承自 System.Object，在 C# 中即 object。换句话说，这些“行为”包含在 C#/.NET 中的所有类型中。

请注意，这三个方法被声明为虚方法（但并非抽象方法），表明它们提供了某些默认实现，这些实现可能完全适合，也可能不完全适合特定的派生类型。

System.ValueType “重写”了以下两个方法（以及其他方法），以提供值类型的默认“值语义”。

在 C# 中，这是通过使用 override 修饰符来完成的。

```
public override bool Equals (object? obj);
public override int GetHashCode ();
```

有时，你可能也需要在你自己的值类型中重写这些方法。`Number.Rational`，一个用 `struct` 定义的值类型，只是使用了 `System.ValueType` 的默认实现。

`System.ValueType` 类型重写了 `System.Object.Equals()` 虚方法，为其子类型 `enum`、`struct` 和 `record struct` 提供“值语义”。当你重写 `Object.Equals()` 方法时，你还需要重写 `Object.GetHashCode()` 方法。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_277_0.png)

我们不会在这本书中详细讨论这个“要求”，但通常，两个具有相同“哈希”值的对象应该彼此相等，反之亦然。因此，你需要重写这两个方法，为你的自定义类型提供一致的实现在实现。

否则，你的自定义类型的对象会表现出许多奇怪、看似随意且不一致的行为。☺（换句话说，你的自定义类型将不具有一般可用性，无法广泛适用于各种用例。）

与使用 `class` 创建的类型一样，`struct` 类型的值可以使用构造函数或对象初始化器进行实例化。

在这个 `Rational` 的特定情况下，我们没有使用任何属性，因此对象初始化器语法的使用受到限制。

我们使用重载的构造函数创建了三个变量 a、b 和 c。

```csharp
var a = new Rational(4, 8);
var b = new Rational(9, 12, true);
var c = new Rational(1, 2);
```

然后，程序测试 `Rational` 数字对之间的四种基本算术运算：加法（+）、减法（–）、乘法（*）和除法（÷）。

最后，它调用 `Rational.Equals()` 来验证这些变量的值语义。

```
$ dotnet run

a = 1/2; b = -3/4
Sum = -1/4
Sub = 5/4
Prod = -3/8
Div = -2/3
c = 1/2
a == c
```

我们按如下方式定义一个新的 struct 类型：

```csharp
struct Rational {
    // ...
}
```

Rational struct 被声明为 `public`。

此外，它还包含一个修饰符 `readonly`。正确定义的 readonly struct 创建一个“不可变”类型。不可变变量的值一旦创建/初始化就不能改变。

使值类型不可变是一个良好的实践。值类型的“身份”由其值决定，*这是定义使然*。处理没有固定值的值会非常麻烦、困难且容易出错。☺

> 正如我们将在整本书中讨论的那样，真正的“readonly struct”不应该包含任何非不可变引用类型字段。

在这个示例中，我们定义 Rational 包含三个值：num 表示分子，den 表示分母，neg 表示符号。（第 4-5 行。）

```
private readonly ulong num, den;
private readonly bool neg;
```

请注意，这些字段都被声明为 `readonly`。并且，如上所述，我们没有通过任何公共属性在外部公开它们。

值类型应该有一个“默认值”。可空引用类型的默认值是 `null`。

所有原始类型都有默认值。例如，所有整数类型的默认值是零（0），`float` 类型（`float` 或 `double`）的默认值也是零（0.0）。`bool` 的默认值是 `false`。

`struct` 类型的（隐式）默认构造函数通常创建该类型的默认值。默认构造函数将其所有字段初始化为各自的默认值。与 `class` 不同，默认构造函数始终由编译器创建（除非被重写），无论 `struct` 是否有其他构造函数。

> 请注意，从 C# 10.0 开始，`struct` 和 `record struct` 的无参默认构造函数可以被重写。然而，与类的情况不同，它们必须是 `public`。

在我们的示例中，`Rational` 的隐式（编译器生成的）默认构造函数默认将 `num` 和 `den` 设置为 0，将 `neg` 设置为 `false`。然而，在这个特定情况下，这不是 `Rational` 类型的有效值。`den` 不能为零。

如果我们使用默认构造函数（不重写它），

```
var d = new Rational();
Console.WriteLine($"default = {d}");
```

它将打印 `0/0`，这是一个无效值。同样，默认运算符 `default(Rational)` 也会产生相同的无效值 `0/0`。

虽然在这个特定的说明中没有使用零值，但我们因此应该通过重写默认构造函数来定义我们自己的默认值（第 7-8 行）。

```
public Rational() : this(0, 1) { }
```

这种 `this(0, 1)` 语法调用了具有两个参数的特定重载构造函数（第 10-11 行），我们将稍后进一步讨论。在需要类型 `Rational` 的默认值的上下文中，我们可以使用 `default` 值，现在它指的是 `0/1`。如上所述，建议确保所有值类型具有正确的默认值。

需要注意的是，你不能在 C# 中重载 `default` 运算符。因此，如果默认实现不适合你的需求，你应该重写无参构造函数。

或者，可以定义一个特殊值，用作默认值。例如，

```
public static readonly Rational Zero = new(0, 1);
```

这样，我们可以显式使用 `Rational.Zero` 而不是 `default` 默认值。然而，既然 C# 10.0 允许重写默认构造函数（不带参数的），这就是实现相同效果的首选方式。

我们为 `Rational` 定义了三个构造函数。如上所述，无参构造函数（第 7-8 行）重写了编译器生成的默认构造函数。

注意一个构造函数调用另一个构造函数的语法。例如，在第 10-11 行，

