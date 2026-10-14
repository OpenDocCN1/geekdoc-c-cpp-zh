
我们引入了一个私有数据成员，可供这些属性中的每个属性使用。这样做避免了属性转发，但也允许我们为所有三个属性使用表达式体。这在很大程度上是一个美观上的选择；采用属性转发的另一种最明显的选择如下所示：

```csharp
public double InMetersPerSecond { get; }
public double InKmPerSecond     => InMetersPerSecond / 1000.0;
public double InKmPerHour       => InMetersPerSecond / 1000 * 3600;
```

无论我们选择哪种方法，我们实际上都是将模糊的 `Amount` 属性重命名为 `InMetersPerSecond`，其目的是返回 `Speed` 的内部值。新的名称更好地表达了属性的含义，与其他属性使用的命名约定相匹配，并与类工厂方法 `FromMetersPerSecond` 相呼应。

通过为 From... 方法和 In... 属性使用相似的命名约定，我们提高了 `Speed` 接口的清晰度。当我们看到像 `FromKmPerHour` 这样的方法时，我们自然会期望存在一个对应的方法和属性来提供反向转换。

类工厂方法和对应的属性提供了一种紧凑的方式来在两个方向上表达单位，并且迫使我们在使用 `Speed` 时有意识地明确自己的含义。

## 使单位显式化

`Displacement` 方法并不直接使用 `Speed` 的单位，因为它们被封装在我们为 `Speed` 和 `TimeSpan` 创建的乘法运算符中。`Displacement` 确实使用了角度的单位，尽管这些单位目前在 `Angle.Size` 属性中是隐含的，如 Listing 1-31 所示。

```csharp
var x = speed * elapsedTime * Math.Cos(angle.Size);
--snip--
```

Listing 1-31: Displacement 中的角度

`Math.Cos` 和 `Math.Sin` 都需要以弧度为单位的角度测量值，弧度是测量角度的 SI 单位。在 Listing 1-32 中，我们将 `Size` 属性重命名为 `InRadians` 以使单位显式化，并同时添加了到度和从度的转换。

```csharp
public readonly struct Angle
{
    private Angle(double size)
        => radians = size;

    public static Angle FromRadians(double size)
        => new (size);

    public static Angle FromDegrees(double size)
        => new (size * Math.PI / 180);

    public double InRadians => radians;
    public double InDegrees => radians * 180 / Math.PI;

    private readonly double radians;
}
```

Listing 1-32: 为 Angle 添加单位转换

正如我们对 `Speed` 所做的那样，我们添加了类工厂方法以使用度或弧度创建 `Angle`，并提供了对应的属性来获取任一单位的值。现在我们可以使用 `Angle` 轻松地与需要弧度值的方法一起使用，并且对于习惯以度思考的用户来说，使用 `Angle` 也更加方便。

## 选择最自然的使用方式

`Math.Cos` 和 `Math.Sin` 方法接受一个 `double` 参数，因此我们需要显式访问 `Angle.InRadians` 属性来调用这些方法。我们无法更改这些方法的参数类型，因为它们是标准库的一部分，但我们可以向 `Angle` 的接口添加同名方法，从而封装显式表达单位的需求。我们可以采用三种主要方法，每种方法都有其优点和缺点，并且每种方法都将 `Angle` 值以弧度形式转发给 `Math` 静态类中的对应静态 `Sin` 和 `Cos` 方法。

最直接的方法是为 `Angle` 引入 `Sin` 和 `Cos` 实例方法，将 `size` 字段值传递给对应的 `Math` 方法，如下所示：

```csharp
public readonly struct Angle
{
    --snip--

    public double Sin() => Math.Sin(size);
    public double Cos() => Math.Cos(size);

    private readonly double size;
}
```

这种方法之所以可行，是因为我们选择了弧度作为 `Angle` 的底层单位，并且提供了到度和从度的转换方法。

Listing 1-33 显示了我们在 `Displacement` 方法中如何使用这些实例方法。与 Listing 1-31 中直接调用 `Math.Cos` 的情况进行比较。

```csharp
var x = speed * elapsedTime * angle.Cos();
var y = speed * elapsedTime * angle.Sin()
    - 0.5 * Gravity.Earth * Math.Pow(elapsedTime.TotalSeconds, 2);
```

Listing 1-33: 调用我们新的实例三角方法

我们的第二个选项是提供一个镜像 `Math` 类的静态类，其中包含静态 `Sin` 和 `Cos` 方法，它们接受 `Angle` 而不是普通的 `double` 作为参数。每个方法都需要访问 `InRadians` 属性，因为它无法访问私有的 `size` 字段。虽然这种方法遵循了静态 `Math` 类建立的常见约定，但我们失去了调用成员方法的更紧凑用法。

第三种替代方案是定义扩展方法，它们在使用上如同实例方法，但定义在单独的静态类中。Listing 1-34 定义了 `Sin` 和 `Cos` 扩展方法以扩展 `Angle` 的接口。

```csharp
public static class AngleExtensions
{
    public static double Cos(this Angle angle)
        => Math.Cos(angle.InRadians);

    public static double Sin(this Angle angle)
        => Math.Sin(angle.InRadians);
}
```

Listing 1-34: 为 Angle 定义扩展方法

静态 `AngleExtensions` 类中的 `Cos` 和 `Sin` 方法使用特殊语法 `this Angle` 作为其参数，这告诉编译器该方法是 `Angle` 的扩展。每个方法只是将角度的 `InRadians` 属性转发给 `Math` 命名空间中的对应方法。我们以与 Listing 1-33 中调用实例方法版本完全相同的方式使用扩展方法。

有时被忽视的一个好处是，静态和扩展方法实现都不依赖于 `Angle` 的内部表示。实例成员方法也可以以 `InRadians` 属性为基础实现，但如果方法不依赖于 `Angle` 的私有实现，将方法提取到单独的类型中，可以使 `Angle` 的定义更小、更易于理解。第 6 章更详细地探讨了这一主题。

无论我们选择哪种方法，我们都将封装显式访问 `angle.InRadians` 属性以调用 `Math` 三角函数方法的需要，从而使任何人都可以轻松使用我们的 `Angle` 类型。

## 由单位隐含的返回类型

类工厂方法，例如我们为 `Speed` 和 `Angle` 引入的那些，是一种简化值类型创建的常见方法。标准库在 `TimeSpan` 类型中使用了这种技术，该类型具有诸如 `FromSeconds` 与 `TotalSeconds` 属性配对的方法。这些方法在其名称中编码了单位，因此创建值实例非常直接：

```
var speed = Speed.FromKmPerHour(234.0);
var angle = Angle.FromDegrees(30.0);
var seconds = TimeSpan.FromSeconds(4.0);
```

当我们初始化这些变量时，我们明确指出了期望的类型以及单位，但 234.0kmh 的值必须是速度。我们不能直接表达这一点，但我们可以通过使用扩展方法来接近。

值 `234.0` 是一个 `double`，虽然我们不能改变其内置定义，但我们可以为 `double` 类型创建扩展方法，如清单 1-35 所示。

```
public static class DoubleExtensions
{
    public static Speed Kmh(this double amount)
        => Speed.FromKmPerHour(amount);
    public static Angle Degrees(this double amount)
        => Angle.FromDegrees(amount);
    public static TimeSpan Seconds(this double amount)
        => TimeSpan.FromSeconds(amount);
    --snip--
}
```

清单 1-35：扩展 double 的接口

每个扩展方法都返回一个由方法名称中单位隐含的类型的新实例，因此 `Kmh` 方法返回一个使用 `Speed.FromKmPerHour` 类工厂方法创建的 `Speed`。我们像这样使用新的 `double` 扩展方法：

```
var speed = 234.0.Kmh();
var angle = 30.0.Degrees();
var seconds = 4.0.Seconds();
```

为了避免对整数必须显式添加小数点，我们也可以添加扩展 `int` 的重载。虽然这种技术对于允许文字值的紧凑语法可能很有用，但对于像这样的变量效果较差：

```
double value = 234.0;

--snip--

var speed = value.Kmh();
```

无论我们如何选择表示测量单位，它们都是这些类型的基本且固有的部分。没有单位，一个数字只是一个数字，即使类型的名称具有描述性。如果我们使值类型的单位易于定义，并且同样重要的是，使在常见单位之间转换变得容易，我们的自定义值类型将更易于使用和理解。

## 一个完全形成的封装值

冗长的参数列表是不明确代码的标志。它们通常表明一个方法没有一个清晰的职责，因此需要重构。一些或全部参数可能以某种方式相关，表明缺少抽象。在任何一种情况下，减少方法参数列表都是提高代码清晰度的另一种方法。

本章中使用的 `Displacement` 方法确实有一个单一、清晰的职责，并且只有三个参数。然而，其中两个参数是相关的：速度是速度和方向的组合。我们已经定义了丰富的类型来表示速度和角度，现在可以将其组合以用自己的类型表示速度。清单 1-36 显示了我们新的 `Velocity` 结构体。

```
public readonly struct Velocity
{
    public Velocity(Speed speed, Angle angle)
        => (Speed, Direction) = (speed, angle);

    public Speed Speed { get; }
    public Angle Direction { get; }
}
```

清单 1-36：定义封装的 Velocity 类型

`Displacement` 方法不再需要单独的速度和角度值，因为它们现在由 `Velocity` 类型处理：

```
public static (Distance, Distance)
Displacement(Velocity v0, TimeSpan elapsedTime)
{
    --snip--
```

将 `Speed` 和 `Angle` 包装到 `Velocity` 中有两个相关的好处。首先，像 `Displacement` 这样需要两个参数来表示速度的方法现在只需要一个。其次，`Velocity` 是一个新的抽象，表示一个不同的概念。我们可以为 `Velocity` 提供自己特定的行为和语义集，并独立于其他任何事物测试这些语义。

## 决定是否抽象类型

引入像 `Velocity` 这样新类型并不总是合适的方法。例如，考虑 `Displacement` 方法的返回值：

```
public static (Distance, Distance) Displacement(
--snip--
```

随着我们关于使用类型表示概念的讨论，将 `Distance` 值的元组抽象为新类型似乎很有吸引力。但我们应该考虑几个因素，包括值将如何使用，是否希望将任何领域特定行为与独立类型关联，以及添加新类型是否会增加清晰度或使其模糊。

如果一个值只在少数地方使用，创建自定义类型来表示它可能不值得，除非这样做也会减少代码重复。如果有我们想要封装的行为，我们将受益于将该行为定位在一个地方并能够在一个地方测试它。

是否能为新类型赋予有用的名称是另一个重要考虑。例如，两 `Distance` 值的元组类似于坐标点，其中 `x` 和 `y` 值表示从原点在两个维度上移动的距离。然而，名称 `Coordinate` 会具有误导性，因为坐标的元素是位置或点而不是距离。然而，现在我们已经创建了 `Velocity` 类型，我们可能会考虑重新审视 `Displacement` 的实现，以尝试解决我们在引入 `Distance` 类型时指出的设计问题。我们的示例不值得涉及的额外复杂性，因此，我们将采用更简单的方法。

在 `Displacement` 返回的值中，元组组件的名称比为新类型命名更重要。与其定义一个完全新的类型作为 `Displacement` 的返回类型，不如我们利用 C# v7.0 及更高版本中丰富的元组支持，直接将返回值“解包”到命名变量中，如清单 1-37 所示。

```
var (range, elevation) = Displacement(velocity, TimeSpan.FromSeconds(0.9));
Assert.That(range.InMeters, Is.EqualTo(19.09).Within(.01));
Assert.That(elevation.InMeters, Is.EqualTo(18.78).Within(.01));
```

清单 1-37：解包元组值

在此示例中，我们使用元组解构，为返回元组值的每个成员赋予自己的名称。编译器从元组中的值推断 `range` 和 `elevation` 变量的类型，因此在此示例中它们都是 `Distance` 类型的实例。这具有既紧凑又足够描述性的优点，适用于许多目的。

## 总结

> 我们将抽象定义为选择性无知——专注于与手头任务相关的思想，忽略其他一切。[...] 如果抽象设计良好且选择得当，我们相信即使我们不理解它们的工作细节，我们也可以使用它们。我们不需要成为汽车工程师就能驾驶汽车。

> —Andrew Koenig 和 Barbara Moo，《Accelerated C++》

C# 提供了一些原始类型，特别是数值类型，使用它们本身可能很诱人。然而，只接受长列表 `double` 参数的方法可能难以解读。这个问题不仅限于 `double`；参数列表很长的 `string` 或 `bool` 方法也存在同样的陷阱，但治疗方法大致相同。

内置类型旨在适用于广泛的问题，并用作更复杂类型的构建块。毕竟，C# 是一种面向对象的语言，它允许我们使用领域特定类型来建模问题。

用我们自己的类型替换原始值有几个实际好处。它可以通过确保方法参数明确来减少代码中偶然的误用和缺陷。这使我们能够利用编译器的类型检查。如果我们错误地调换参数，我们的代码将无法编译。这种早期失败可以防止这些错误在运行时导致问题，或者更糟糕的是，进入实时生产系统并让我们感到尴尬。

创建即使是简单的类型也允许我们提供描述性名称，使代码更具自描述性。反过来，这使我们免于必须生成大量单独的解释性文档，而这些文档往往会过时。

通过将类型的行为与使用它的算法分离，并将该行为封装在类型本身中，我们可以独立于这些算法对其进行测试。该类型更具内聚性，算法更清晰且通常更简单。这些算法本身也更容易供我们测试，而无需同时测试领域类型抽象所捕获的假设和实现。

## 值类型和引用类型

![](img/47f0004b0ac0322f285ca59a19bca333_56_0.png)

我们可以在 C# 中通过多种方式创建新类型，并且需要考虑每种方法的个体特征，以确定哪种方法最适合我们的目标。特别是，了解值类型与引用类型的区别有助于我们选择正确的前进方向，因为这些差异在我们定义自己的类型时具有重大且有时未被考虑的影响。某些权衡会影响我们如何设计类型以及可以用它做什么。在本章中，我们将研究这些差异以及它们对程序的意义。

我们将探讨以下内容：

- 创建自己的类型时我们有哪些选择

- 为什么 C# 同时具有引用类型和值类型

- 选择其中之一如何影响构造、空值检查和其他类型行为

- 为什么值类型不等于值语义

- 不同类型在内存中的存储位置以及这如何影响对象的生命周期

## 用户定义的类型

大多数现代编程语言允许你创建自定义类型。C# 中用户定义类型的基本原则对许多其他语言的程序员来说都很熟悉，但某些细节是不同的。因此，在本节中我们将研究四种用户定义的类型：结构体、类，以及较新的记录和记录结构体（分别在 C# v9.0 和 v10.0 中引入）。

重要的是要认识到这些类型的行为在很大程度上依赖于它们是引用类型还是值类型。让我们带着这些差异简要地查看每种用户定义的类型。

### 结构体和类

清单 2-1 定义了一个简单的结构体来表示颜色。

```
public readonly struct Color
{
    public Color(int r, int g, int b)
        => (Red, Green, Blue) = (r, g, b);

    public int Red { get; }
    public int Green { get; }
    public int Blue { get; }
}
```

清单 2-1：定义一个简单的结构体
