

## 18.2. 代码审查 - 模拟股票行情服务

*stock-ticker/Prices.cs* (第 3-19 行)

```csharp
sealed class Prices {
    internal const string AAPL = "AAPL";
    internal const string MSFT = "MSFT";

    private static readonly Prices instance = new();
    internal static Prices Stock => instance;

    private Random rand;
    private Dictionary<string, decimal> prices;

    private Prices() {
        rand = new();
        prices = new() {
            { AAPL, 100m },
            { MSFT, 200m },
        };
    }
```

```csharp
// stock-ticker/Prices.cs (第 21-36 行)
internal decimal this[string symbol] {
    get {
        var delta = rand.Next(0, 100) switch {
            >= 95 => 0.2M,
            >= 80 => 0.1M,
            >= 70 => -0.1M,
            >= 65 => -0.2M,
            _ => 0M,
        };

        var newPrice = prices[symbol] + delta;
        prices[symbol] = newPrice > 0 ? newPrice : 0M;
        return prices[symbol];
    }
}
```

对于股票记录，我们使用 C# record 类定义了一个新类型 Stock。

```csharp
// stock-ticker/Stock.cs (第 3-12 行)
public record Stock(string Symbol, decimal Price, decimal PreviousPrice = 0M) {
    public string Trend => (Price - PreviousPrice) switch {
        > 0 => "Up",
        < 0 => "Dn",
        _ => "--", // 无变化
    };

    public Stock UpdatePrice(decimal newPrice) =>
        this with { Price = newPrice, PreviousPrice = Price };
}
```

![](img/25af69ec45b3c0b589a8dccd0c2a88be_297_0.png)

显然，C# 选择 *record* 这个词来命名其可用于创建“数据类型”的新语法结构并非巧合。在计算机领域以及普通英语中，“record”一词都带有“数据”的含义。

## 18.3. 结对编程 - 主构造函数、switch 表达式、异步方法

*record*（或 *record class*）提供了一种在 C# 中创建引用类型的新方式。实际上，当使用 *record*（class）声明创建类型时，编译器会在幕后使用 class 创建一个引用类型。

编译器还会生成一些合成方法，以使 record 类型遵循值相等语义。

Record 通常用于“数据”类型，其用途与只读 struct 类似。Struct 通常适用于“小型”值类型，因为复制大型值可能开销很大。

另一方面，record 是引用类型。它们主要遵循引用语义，但数据（引用所指向的对象）不需要被复制，这使得它们在“大型”数据类型中使用时更加高效。

Record 遵循值相等语义。在许多情况下，它们的行为更像值而非引用。

与 struct 类似，record 主要用于创建不可变类型。截至 C# 10.0，还可以创建 record struct，它是一种值类型（struct），在语法上与 record class 相似。编译器也为 record struct 生成相同的一组方法。

可以按以下方式创建 record 类型：

```csharp
record Stock {
    // ...
}
```

或者，

```csharp
record class Stock {
    // ...
}
```

这两种语法是等价的。

Record 可以像 class 或 struct 类型一样包含只读或可读写的属性以及静态和实例方法等。

Record（包括 record class 和 record struct）支持一种特殊的语法，允许在类型名后的括号中包含一个或多个只读属性。

> “只读属性”是指仅具有 getter 的属性。在某些上下文中，init-only 属性也可以被视为只读。在其他某些上下文中，具有私有 setter 的属性也可以被视为只读。

例如，

```csharp
record Stock(/* 这里放只读属性 */) {
    // ....
}
```

这实质上为 record 类型定义了一个构造函数。

在 record 类型不包含其他方法或其他属性的情况下，整个代码块可以省略。

```csharp
record Stock(/* ... */);
```

使用这种语法定义的 record 称为“位置 record”（positional record）。请注意，语句末尾使用的是分号，而不是通常的大括号代码块。

在示例代码中，如果 `Stock` 不包含其他属性或方法，它本可以声明如下：

```csharp
record Stock(string Symbol, decimal Price, decimal PreviousPrice = 0M);
```

注意其语法。只读属性列在一对括号中，就像构造函数的参数一样。可以使用类似构造函数可选参数的语法来设置属性的初始/默认值。

位置 record 语法确实为该类型定义了一个构造函数。它被称为 record 的“主构造函数”。还可以定义额外的构造函数。

Record 也可以像 `struct` 和 `class` 一样使用对象初始化语法创建。

`Stock` record 类定义了四个属性：`Symbol`、`Price`、`PreviousPrice` 和 `Trend`。

其中三个是使用位置或构造函数语法声明的。`Trend` 只读属性使用更传统的 `get` 属性语法定义：

```csharp
public string Trend {
    get => (Price - PreviousPrice) switch {
        > 0 => "Up",
        < 0 => "Dn",
        _ => "--",   // 无变化
    };
}
```

由于它是只读属性（即没有 setter），我们在示例代码中使用了简写表示法，采用表达式体。

注意在 `Trend` getter 实现中使用了 `switch` 表达式。它就像使用三元表达式一样简单，并且不限于两种替代情况。

由于 `Trend` 属性返回一个计算值，将其包含在位置/构造函数参数中可能没有意义。它是一个只读属性（没有 `init`），因此不能包含在对象初始化器中。

请注意，（非可选的）位置参数需要通过构造函数语法提供。

例如，使用命名参数的以下所有代码都是有效的：

```csharp
var stock = new Stock(Symbol: "AMZN", Price: 1.0M);
```

```csharp
var stock = new Stock(Symbol: "AMZN", Price: 1.0M, PreviousPrice: 1.0M);
```

```csharp
var stock = new Stock(Symbol: "AMZN", Price: 1.0M) {
    PreviousPrice = 1.0M,
};
```

如果偏好对象初始化语法，可以将主构造函数的所有或大多数参数设为可选。或者，可以提供需要更少或不需要参数的额外构造函数。

*Stock* record 包含一个实例方法，`UpdatePrice()`：

```csharp
public Stock UpdatePrice(decimal newPrice) => this with { Price = newPrice, PreviousPrice = Price };
```

该实现使用了所谓的“非破坏性变更”（non-destructive mutations）。当我们调用 `UpdatePrice()` 时，*Stock* 对象的数据不会改变。相反，它返回一个*新的* *Stock* 对象。

`with` 关键字用于创建现有对象（在此情况下是 *this* 对象）的副本，并修改其中少数选定的属性值（大括号内部）。

可以想象，这在处理大型不可变 record 类型时非常有用。不使用可能需要初始化许多变量的构造函数或对象初始化器，而是简单地使用现有的 record 作为“模板”。

此外，这种语法清晰地表明了底层意图：以此方式创建的新对象（或 record）是“基于”这个特定的现有对象/record。任何未通过这种非破坏性变更语法显式覆盖的属性都将具有与“模板”对象相同的值。

我们之前见过 *this* 关键字的用法，即在定义扩展方法的上下文中。那是一个比较特殊的案例。

一般来说，关键字 *this* 用于在类、record 或 struct 定义内部指代“当前对象”或“自身”。特别地，*this* 对象在所有实例属性和实例方法中都是可用的。

我们在整本书中一直谨慎地使用“类型”和“对象”这两个词。不幸的是，C# 中基类的名称是 *object*。这个 *object* 是一个类型。

但是，通常我们使用术语“对象”来指代类型的实例。事实上，C# 中的任何类型都是 object 类型的子类型，因此 C# 中任何类型的实例都是一个“对象”。

更具体地说，我们经常使用术语“对象”来指代引用类型的实例。通常不会将像 3 这样的 int 字面量称为对象。但无论如何，从概念上讲，C# 中的每个值或引用都是一个“对象”。

“类型”可以说是一个创建对象的模板或蓝图。也就是说，同一类型的每个对象都是根据相同的蓝图创建的。

在类型（例如，class、struct 或 interface）的定义中，关键字 this 指的是由该类型创建的对象，或“对象蓝图”。

例如，在 sealed class Prices 的定义中，我们声明了几个实例字段，即 rand 和 prices。

（正如之前多次指出的，任何“static”的东西与“对象”关系不大。静态字段、静态属性和静态方法不属于“对象蓝图”，至少截至 C# 10.0 是如此。）

可以使用“点表示法”来引用这些实例字段（或简称为字段），其中我们使用 this 关键字来指代（无名的）对象。

例如，构造函数可以写成如下形式：

```csharp
private Prices() {
    this.rand = new();
    this.prices = new() { { AAPL, 100m }, { MSFT, 200m } };
}
```

this 关键字经常可以省略，因为在许多情况下，我们（以及编译器）都很清楚指的是哪个对象。也就是说，this.rand 指的是

