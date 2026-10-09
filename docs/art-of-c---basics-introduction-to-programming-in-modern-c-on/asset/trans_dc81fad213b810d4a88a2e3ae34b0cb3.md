
# 19.3. 结对编程 - 数据类型，switch 表达式，只初始化属性

在 C# 中，你可以使用 `class`、`struct`、`record`/`record class` 或 `record struct` 中的任意一种来定义对象类型。

如前所述，`struct` 和 `record struct` 创建的是值类型，遵循值语义。特别是，结构类型的值会被“复制”，其相等性基于其值本身进行评估，仅基于其值。

引用对象类型可以使用 `class` 或 `record` 创建。引用类型的对象遵循引用语义。也就是说，即使引用被复制，它们仍然指向相同的底层数据。

如前一课所述，值类型需要遵循“值相等语义”。对于值对象而言，其值就是其“身份”，两个值对象是否相同应仅取决于它们的值，而不取决于其他任何东西。也就是说，3 就是 3。

对于 C# 中的所有值类型，无论是内置的还是用户定义的，默认情况下通过 `System.ValueType.Equals()` 的实现来强制实施值相等性。

对于 C# 中的引用类型，情况并非如此。默认情况下，通过 `System.Object.Equals()` 的实现，所有引用类型对象仅遵循引用相等语义。

请注意，相等语义主要对数据类型对象很重要。在 C# 中，`record` 是一种特殊的类，默认遵循值相等语义。

我们将通过基于 class、struct、record 和 record struct 的三种不同类型来演示 `Equals()` 或 `==` 的行为。

在 `SNumeral` 的 `Main()` 方法中，我们创建了三个值 r1、r2 和 r3，并比较它们的值。

如果运行该程序，如下所示：

```bash
dotnet build -t:Rebuild -p:StartupObject=Roman.SNumeral
dotnet run
```

以下是一个示例输出：

```bash
$ dotnet run

r1 = MCCXXXIV
r2 = MMXXII
r3 = MMXXII

r1 != r2
r2 == r3
```

r1 与 r2 不同，r2 与 r3 相同，这与预期一致。

尽管 r2 和 r3 的创建方式不同，且它们是不同的变量，但它们的值相同，因此彼此相等。

在 `SNumeral` 结构中，我们确实重写了 `Equals()`、`operator ==()` 和 `operator !=()`。但这只是为了方便，以便我们可以使用 `r2 == r3` 这种语法。如果我们没有重写这些方法，而是直接使用 `r2.Equals(r3)`，我们仍然会得到相同的结果。

对于值类型，重写这三个方法和/或实现 `IEquatable<T>` 接口是一种良好的实践。

在 `CNumeral` 的 `Main()` 方法中，我们也以完全相同的方式创建了三个值 r1、r2 和 r3，并比较它们的值。

如果运行该程序，如下所示：

```bash
dotnet build -t:Rebuild -p:StartupObject=Roman.CNumeral
dotnet run
```

我们得到以下输出：

```bash
$ dotnet run

r1 = MCCXXXIV
r2 = MMXXII
r3 = MMXXII

r1 != r2
r2 != r3
```

尽管 r2 和 r3 具有相同的值（或者，它们包含相同的数据），但相等性测试返回 `false`。这不是值相等语义。

如前所述，这并不一定是一个问题。在许多情况下，这无关紧要。然而，对于“数据”类型，值相等语义是期望的特性。

C# 现在拥有了一种特殊的类，它是引用类型，但开箱即用地支持值相等语义。接下来我们将查看一种记录类型，`RcNumeral`。

在 `RcNumeral` 的 `Main()` 方法中，我们尝试了相同的事情。

这一次，我们使用构造函数和对象初始化器语法创建三个对象 r1、r2 和 r3，只是为了变换一下方式，并比较它们的值。

如果像之前一样运行程序：

```bash
dotnet build -t:Rebuild -p:StartupObject=Roman.RcNumeral
dotnet run
```

这里是示例输出：

```bash
$ dotnet run

r1 = RcNumeral { Number = 1234, Roman = MCCXXXIV }
r2 = RcNumeral { Number = 2022, Roman = MMXXII }
r3 = RcNumeral { Number = 2022, Roman = MMXXII }

r1 != r2
r2 == r3
```

尽管这些是引用变量，但它们遵循值相等语义。特别是，r2 和 r3 是不同的引用变量，它们指向两个不同的底层数据（例如，位于两个不同的内存位置），在此使用 record 的实现中，它们默认被认为相等。

请注意，当我们使用 record 时，我们会免费获得 `ToString()` 方法的合理实现（基于我们声明的两个公共属性 `Number` 和 `Roman`）（这与 struct 或 class 的情况不同）。

如果需要不同的输出格式，我们仍然可以重写此方法。例如，与之前一样：

```csharp
public override string ToString() =>
    NumeralHelper.ToNumeralString(number);
```

注意在定义 `RcNumeral` 记录时的有趣语法：

```csharp
public record RcNumeral() {
    // ..
}
```

这使用了没有任何属性参数的位置记录语法。此声明仍为我们提供了一个作为主构造函数的构造函数（无参数）。

在示例 `Main()` 方法中，我们使用对象初始化器语法，例如：

```csharp
var r1 = new RcNumeral { Number = 1234 };
```

如果没有显式定义默认构造函数（通过位置参数语法），我们就不能使用这种语法。

对于 `struct` 类型，编译器总是创建默认的（无参数）构造函数，并且它们不能被重写。

对于 `class` 和 `record` 类型，当类型定义中没有显式定义其他构造函数时，会创建默认构造函数。如果存在任何构造函数，则不会生成默认构造函数。

对于 `record structs`，它们与 `structs` 一样是值类型，遵循相同的值语义。在语法等方面，它们比普通的 `structs` 提供了一些便利。

为了完整性，如果我们构建并运行示例程序，以 `RsNumeral` 作为主类：

```bash
dotnet build -t:Rebuild -p:StartupObject=Roman.RsNumeral
dotnet run
```

我们得到以下输出，与 `SNumeral` 和 `RcNumeral` 的输出相同：

```bash
r1 = RsNumeral { Number = 1234, Roman = MCCXXXIV }
r2 = RsNumeral { Number = 2022, Roman = MMXXII }
r3 = RsNumeral { Number = 2022, Roman = MMXXII }

r1 != r2
r2 == r3
```

在本课中，我们使用四种不同的构造类、struct、record 和 record struct 实现了“罗马数字”类型。在这个特定示例中，使用 struct 或 record struct 似乎最为合理。它是一个“小”类型，对于数字类型使用值语义相当自然。

## 摘要

通过实现一种罗马数字类型，我们对 class、struct、record class 和 record struct 进行了简单的比较。使用 struct/record struct 或 record 创建的类型遵循值相等语义，最适合“数据类型”。

# 第 20 课。欧几里得距离

## 20.1. 简介

C# 的新 record class 似乎提供了两全其美的方案，即值类型和引用类型。（或者，真的是这样吗？）

我们将再次尝试使用 struct 和 record（本质上只是具有特殊编译器支持的 class）来实现数据类型。

经验法则是使用 struct 或 record struct 来实现“纯”值类型或“小”数据类型，使用 record 来实现“大”数据类型。

> 我们在整本书中经常使用“小”和“大”等不精确的术语。不幸的是，读者必须通过经验发展出一定的“直觉”。这些概念是依赖上下文的，无法真正精确定义。

在本课中，我们将实现一个小类型“point”来表示二维空间中的一个点。根据情况，一个点可以被视为纯值类型，如复数，或者数据类型，如地理坐标。

我们也在本课中引入了接口的重要概念。我们将使用一个简单的接口为我们使用 struct 和 record（class）创建的点类型提供多态行为。

> 我们在本课中使用的示例似乎有点“人为”。在实践中，我们很少会在同一个程序中为完全相同的底层概念定义多于一种类型。尽管如此，此代码示例除了展示 struct 与 record 的一些基本用法外，还说明了接口的重要用途。

