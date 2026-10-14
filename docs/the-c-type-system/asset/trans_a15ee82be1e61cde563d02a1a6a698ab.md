

如果我们使用类或 record，而不是结构体或 record struct，就可以防止默认值，并强制用户在创建实例时指定正确的单位。不过，类和 record 都是引用类型，这意味着变量可能具有 null 值。在 C# v8.0 及更高版本中，我们可以尽可能充分地利用不可为 null 的引用来缓解这一问题，但这可能无法阻止所有可能的误用。

尽管如此，当我们在类和 record 之间进行选择，以便为具有类似值特征的类型建模时，record 几乎总是更可取的。Record 专门用于定义具有值语义的类型，并且编译器会根据所比较实例的状态，为 record 提供默认的相等行为。

## 实现自定义行为与生成行为

如果我们希望类具有基于值的相等性，就必须自行定义。至少，我们应该重写 Equals(object?) 和 GetHashCode 方法；不过，正如第 5 章所述，更完整的定义还包括实现 IEquatable<T> 接口，并重载 operator== 及其配套的 operator!=，从而使相等比较自然且易于使用。

对于大多数类似值的类型，只要注意避免常见错误，实现这些方法并不困难。然而，如果我们使用 record 而不是 class，编译器会为所有这些方法生成实现。这会使 record 类型定义更加简短、易于理解，也使我们不必记住所有潜在的陷阱。

对于设想中的 Temperature 类型，我们可以考虑使用位置 record，从而省去编写完整定义的麻烦。Temperature 作为位置 record 的临时实现可能如清单 6-15 所示，但位置 record 存在一些需要考虑的限制。

```
public sealed record Temperature(double InCelsius)
{
    public static Temperature FromCelsius(double val)
        => new Temperature(val);

    public double InFahrenheit => InCelsius * 1.8 + 32;
    public static Temperature FromFahrenheit(double val)
        => new Temperature((val - 32) / 1.8);
};
```

清单 6-15：位置 Temperature record

编译器会使用 Temperature 定义中的参数，自动生成一个名为 InCelsius 的属性，但我们必须自行编写 InFahrenheit 属性，以便添加执行转换的代码。用户可以调用类工厂方法，使用不同单位创建 Temperature 实例，但编译器为 Temperature 生成的构造函数是公共的。生成的构造函数也不会验证参数，而我们可能希望确保 Temperature 不能低于绝对零度。

如果我们希望用户明确指定单位，就需要强制他们使用这些类工厂方法，因此位置 record 无法满足我们的需求。出于相同原因，位置语法也不适用于清单 6-14 中 Velocity 使用的 Speed 和 Angle 类型。

## 重写生成的方法

当位置 record 语法无法满足我们的需求时，我们可以使用完整的 record 定义，它不包含位置类型参数。然后，我们可以提供自己的私有构造函数，并使用它验证初始值。

由于必须自行编写 InCelsius 属性，我们会牺牲使用位置 record 的部分便利性，因为编译器只会为位置 record 生成属性。清单 6-16 中的 record 定义展示了如何为 record 类型定制行为，同时继续享受编译器提供的其他代码所带来的好处。

```
public sealed record Temperature
{
    private const double ZeroKelvin = -273.15;

    private Temperature(double celsius)
        => value = celsius switch
        {
            Double.PositiveInfinity or < ZeroKelvin
                => throw new ArgumentOutOfRangeException( --snip-- ),

            double.NaN => throw new ArgumentException( --snip-- ),

            _ => celsius
        };

    public double InCelsius => value;
    public static Temperature FromCelsius(double val)
        => new Temperature(val);

    public double InFahrenheit => value * 1.8 + 32;
    public static Temperature FromFahrenheit(double val)
        => new Temperature((val - 32) / 1.8);

    public static Temperature AbsoluteZero
        => new Temperature(ZeroKelvin);

    private readonly double value;
}
```

清单 6-16：Temperature 的完整 record 定义

对于非位置 record，编译器仍会生成实现基于值相等性的方法，因此我们可以专注于正确实现 Temperature 这类 record 类型特有的其他行为。

当我们可以接受位置语法的所有默认行为时，record 和 record struct 分别相较于类和结构体能提供最大的好处。清单 6-4 中的 Color 类型就是一个很好的例子；将其定义为位置 record struct 后如下所示：

```
public readonly record struct Color(int Red, int Green, int Blue);
```

对于 Color，默认初始化的实例是一个有效的 Color，并且会与所有属性均为 0 的实例比较为相等，如以下示例所示：

```
var background = new Color();
var black = new Color(0, 0, 0);

Assert.That(background == black, Is.True);
```

我们不必添加任何自定义方法或属性，因此位置语法非常简洁，并且恰好实现了我们所需的功能。

Record 和 record struct 对于定义 Color 这类简单值类型非常方便，不过编译器可能无法提供类型所需的全部功能。尤其是，如果我们需要比较两个值，以判断其中一个是否小于另一个，就必须始终自行提供这种比较的实现。

## 用于排序的比较

基于值的相等性原则是定义“值”含义的唯一要素。当我们讨论某个东西是否为值类型时，实际上是在简略地询问：两个实例是根据其状态相等，还是根据其身份相等。以状态作为相等性的依据，是所有值固有的特征。不过，有些值可能是等价的，却不一定相等。

通常，如果两个值具有完全相同的状态，它们就相等。清单 6-17 中的 LogEntry record struct 的两个实例，如果所有属性也都相等，则它们相等；而单个 LogEntry 实例的身份并不重要。

```
public enum Severity { Debug, Info, Warning, Error }

public readonly record struct LogEntry(DateTime stamp,
    Severity Level,
    string Message);
```

清单 6-17：值类型相等性

有些值具有自然顺序，但并非所有值都如此；自然顺序使我们能够对值的集合进行排序。排序算法有很多种，但它们通常都会将集合中的每个项目依次与其他项目进行比较，以确定一个项目是否小于另一个项目。如果左侧的值小于右侧的值，就认为这些项目处于正确顺序。

我们可以根据自己的需求自定义*小于*以及因此而来的*处于顺序中*的含义。在 C# 中，定义*小于*的协议是 `IComparable<T>` 接口，该接口要求我们为类型实现一个名为 `CompareTo` 的方法。如果左侧参数小于右侧参数，`CompareTo` 将返回负整数；如果右侧参数小于左侧参数，结果为正数。否则，结果为 0。

当我们比较两个 `LogEntry` 值以判断它们是否相等时，会使用所有属性。然而，对于排序，我们可能只关心 `TimeStamp` 属性，因为我们只是想按照日志记录的先后顺序排列条目。按照消息对 `LogEntry` 值排序没有太大意义，而按照严重性排序也不符合我们的使用场景。

`LogEntry` 的 `TimeStamp` 属性是一个 `DateTime` 实例，而 `DateTime` 本身实现了 `IComparable` 接口，因此清单 6-18 只需比较 `TimeStamp` 属性，即可为 `LogEntry` 实现 `CompareTo`。

```
public readonly record struct LogEntry(DateTime TimeStamp,
    Severity Level,
    string Message)
: IComparable<LogEntry>
{
    public int CompareTo(LogEntry other)
        => TimeStamp.CompareTo(other.TimeStamp);
}
```

*清单 6-18：为 LogEntry 值定义基于 TimeStamp 的排序*

通常，我们不会直接在 `LogEntry` 实例上调用 `CompareTo`；在对 `LogEntry` 值集合进行排序时，通常会间接调用它。除非我们明确指定用于排序的其他比较方式，否则系统将使用 `CompareTo` 方法来确定如何排列 `LogEntry` 元素，因此 `LogEntry` 值的默认排序完全基于 `TimeStamp` 属性。

值具有*外延性*：如果两个实例具有相同的可观察属性，那么它们就相等。这不一定等同于具有相同的结构定义，后者称为*内涵性*。虽然相对少见，但有时可能需要额外数据，而这些数据并没有以有意义的方式构成该值，因此不会用于相等性测试。这类数据通常也是实现的私有细节。

当我们不仅希望比较值是否相等，还希望对它们进行排序时，内涵性与外延性之间的区别会变得更加重要。对值进行排序需要一种不同但密切相关的比较，这种比较可能导致两个不相等的值在排序意义上被视为等价。

## 等价与相等

对于大多数值类型，如果 `CompareTo` 返回 0，那么两个值确实相等，调用 `Equals` 也会返回 true。底层的 `TimeStamp` 属性为 `DateTime` 值时就是这种情况。然而，尽管这通常是我们所期望的结果，但这并不是严格要求。`CompareTo` 方法

