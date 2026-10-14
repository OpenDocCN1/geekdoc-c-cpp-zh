
第二种类型则不然。派生类在语法上可替代其基类，因为存在从特定类型到其任意父类型的自然隐式转换。

我们可以实现自己的类型转换，以模拟两个原本无关类型之间的可替换性。无论是通过隐式还是显式转换，将变量强制转换为不同类型可能很方便，但这样做可能会掩盖表面之下的一些问题。然而，如果谨慎使用，无关类型之间的转换可以成为表达设计的有效且简洁的方式。

为了演示我们尚未探索的隐式转换的一些问题，清单 7-33 在 `TranslucentColor` 中实现了一个隐式转换运算符，用于将实例转换为 `Color` 类型。

```
public readonly record struct TranslucentColor(Color Color, int Alpha)
{
    --snip--
    public static implicit operator Color(TranslucentColor color)
        => color.Color;
}
```

清单 7-33：隐式转换运算符

`TranslucentColor` 中的转换运算符是一种向外转换：我们正在将实现类型的实例转换为其他类型。它允许我们在手头有 `TranslucentColor` 时调用一个期望 `Color` 值的方法，就像我们在清单 7-34 中调用 `EqualViaColor` 方法时那样。

```
public bool EqualViaColor(Color left, Color right)
    => left.Equals(right);

var red = new TranslucentColor(0xFF, 0, 0, 0);
var blue = new TranslucentColor(0, 0, 0xFF, 0);

Assert.That(EqualViaColor(red, blue), Is.False);
```

清单 7-34：隐式转换的实际应用

由于隐式转换运算符，当我们把 `red` 和 `blue` 变量作为参数传递给 `EqualViaColor` 方法时，它们会被转换为 `Color` 实例。这种转换是无形中发生的，因为转换运算符被定义为 `implicit`。

我们可以通过在 `Color` 类型上定义一个接受 `TranslucentColor` 参数的向内转换运算符来达到同样的效果。区别仅在于我们选择在哪里定义运算符。由于 `TranslucentColor` 已经依赖于 `Color` 类型，而 `Color` 本身并不知道 `TranslucentColor`，因此在 `TranslucentColor` 中定义向外转换在这里更合理。

然而，我们必须小心所有转换，尤其是隐式转换。如你在第 1 章中所见，隐式转换可能隐藏复杂性，甚至可能导致非预期行为。用户定义的强制转换并不完全等同于从派生类型到其基类型的隐式引用转换。

## 加宽转换与收窄转换

当 `TranslucentColor` 继承自 `Color` 时，我们可以将 `TranslucentColor` 引用传递给期望 `Color` 的方法，但它仍然是同一 `TranslucentColor` 实例的引用，只会复制引用本身。在清单 7-33 中，`TranslucentColor` 和 `Color` 是记录结构体，因此是值类型。当我们调用 `TranslucentColor` 的转换运算符时，实际上是在创建一个新的 `Color` 实例，因此副本丢失了 `TranslucentColor` 特有的一些信息——即 `Alpha` 属性。

从派生类引用到基类引用的转换是一种加宽转换。我们可以使用更通用（基类）的类型来引用特定实例，但不会丢失任何信息。我们仍然能够将基类引用显式强制转换回原始派生实例，尽管那是一种相对昂贵的运行时操作。我们通过自定义运算符方法从 `TranslucentColor` 结构体到 `Color` 的隐式转换则是收窄的：两种类型并没有哪一个更具体或更通用，它们是独立的值，但转换行为会丢失信息。

虽然我们复制了从派生类转换为基类的行为，但这并没有给我们同样的灵活性。转换后的值实际上只是一个 `Color`，如果我们需要恢复 `TranslucentColor` 的额外属性，就需要其他手段来捕获它们。

转换不适合试图复制继承的特征，但它们在其他场景下可能很有用。

## 用于表示

当两个类型具有相同的含义但不同的表示时，无关类型之间的转换更有意义。例如，我们可能需要使用一个外部 API，该 API 使用常见的 `int` 表示颜色的十六进制 RGB 值。改变值的表示通常最好实现为显式转换，而不是隐式转换，如清单 7-35 所示。然而，任何转换——无论是显式还是隐式——都需要仔细考虑替代方案。

```
public readonly struct Color
{
    --snip--
    public static explicit operator int(Color color)
        => color.Red << 16 | color.Green << 8 | color.Blue;
}
```

清单 7-35：转换为不同的类型表示

在清单 7-36 中，我们通过将 `plum` 值强制转换为 `int` 来测试显式转换运算符的实现，以便将其作为参数传递给接受 `int` 参数的方法。

```
int Converted(int color)
{
    return color;
}

var plum = new Color(0xDD, 0xA0, 0xDD);

Assert.That(Converted((int)plum), Is.EqualTo(0xDDA0DD));
```

清单 7-36：测试显式转换

这个局部 `Converted` 函数接受一个 `int` 参数，并且为了测试目的，直接返回其参数值。由于转换运算符是显式的，我们在调用 `Converted` 方法时必须强制转换 `Color` 值；如果我们尝试直接将 `Color` 值作为 `Converted` 的参数，编译器会报错。编译器也会捕获任何无意中不合适这样的表达式：

```
var blue = new Color(0, 0, 0xFF);
var green = new Color(0, 0xFF, 0);

Assert.That(blue < green, Is.True);
```

如果我们将转换运算符设为 `Color` 中的隐式转换，这段代码可以编译，但会比较两个 `int` 值，结果很可能是意外的。

清单 7-36 中的强制转换为 `int`，虽然在代码中显式且明显，但并没有说明转换背后的意图，这在某种程度上是通过使用来暗示的。我们可能会考虑用方法或属性来替换这样的显式向外转换，以更明确地描述转换的意图，或许可以将其命名为 `ToWebColor`。

为转换命名可以让我们更好地表达我们的含义和原因，使代码更具自文档性，而不会比显式强制转换更突兀或语法复杂。使用命名属性而非强制转换的一个经常被忽视的好处是，如果我们需要查找所有使用该属性的地方，属性名更容易搜索。

## 用于目的

转换运算符，即使是隐式转换，并非完全是糟糕的选择。转换通常用于允许值由支持不同操作的无关类型表示，尽管该值本身具有共同的表示。例如，`Color` 是一个不可变值类型，但我们可能希望增量地构建其值。`Color` 有多个属性，有时单独设置它们可能比在构造函数中一次性设置所有属性更方便。

与其通过为 `Color` 的属性添加 set 访问器来损害其不可变性，我们引入一个新的伴生类型，它看起来非常像 `Color`，只是允许其属性被修改。当值处于最终状态时，我们可以将可变类型的实例具体化为不可变的 `Color`。关键在于我们可以轻松地从伴生类型转换为目标值类型。清单 7-37 展示了这样一个 `Color` 的可变伴生类型，它允许隐式转换为不可变的目标值。

```
public class ColorBuilder
{
    public int Red { get; set; }
    public int Green { get; set; }
    public int Blue { get; set; }

    public static implicit operator Color(ColorBuilder color)
        => new Color(color.Red, color.Green, color.Blue);
}
```

清单 7-37：`Color` 的可变伴生类型

`ColorBuilder` 类型本身并非值类型；其唯一目的是为 `Color` 值提供一种工厂。

可变伴生模式的应用相当常见，我们在标准库中可以看到 `string` 和 `StringBuilder`。`string` 类型是不可变的，当我们需要从多个部分构建一个字符串变量时，使用其可变伴生类型 `StringBuilder` 是高效的。当我们完成字符串的“构建”后，再将其转换为不可变状态。

与 `ColorBuilder` 不同，我们必须调用 `StringBuilder` 的 `ToString` 方法将其转换为字符串，但在这里使用隐式转换也能产生良好效果。由于 `ColorBuilder` 可以隐式转换为 `Color`，我们可以使用 `ColorBuilder` 值调用接受 `Color` 参数的方法，正如我们在清单 7-38 中看到的，我们用 `ColorBuilder` 和 `Color` 值调用 `RelativeLuminance` 方法。

```
public static double RelativeLuminance(Color color)
    => 0.2126 * color.Red + 0.7152 * color.Green + 0.0722 * color.Blue;

var background = new Color(0, 0, 0);

var builder = new ColorBuilder();
builder.Red = 0xFF;
builder.Green = 0xFF;
builder.Blue = 0;

if(RelativeLuminance(builder) < RelativeLuminance(background))
    background = builder;
```

清单 7-38：转换伴生类型

我们在清单 7-37 中为 `ColorBuilder` 定义的隐式转换运算符允许我们将可变的 `builder` 变量作为参数传递

