
最后，可以使用组合将 `uncurriedRelevantSalesVolumes` 与 `avgCalculator` 结合。结果如下：

```csharp
var salesVolumeAverage = Functional.Compose(uncurriedRelevantSalesVolumes, avgCalculator);
```

这就是最终结果。`salesVolumeAverage` 现在是一个符合之前讨论的函数：

```csharp
var avg = salesVolumeAverage(GetCustomers(), 3);
```

# 总结

本章将这些函数构造技术推向了极限并超越了极限。组合和部分应用是允许函数视为构建块的工具，尽管它们与目的类似的面向对象技术相比，但它们有自己的优先级和优势。取决于你的工作环境和团队、项目和任务，以及许多因素，你将在多程度上使用本章的技术。无论你如何决定，你现在了解你的选择，也知道限制在哪里。

# 15 可选值

本章内容：

- 表达值的缺失
- `Option` 类型的实现

## 无的概念

在处理计算机数据时，总是面临着表示“无”的困境。这个问题确实很特殊，因为在处理计算世界之外的数据时，这很少成为问题。想象一张纸质表单，上面有值字段。简单地什么都不做——不填写任何字段——该字段就会自动表示无。不需要额外的步骤就能让阅读表单的人明显看出该字段没有被填写。

对于计算机来说，情况则不同，这回溯到一个事实（不涉及物理原理）：计算机内存中的任何字节始终有一个值。这个值的初始值可能是完全随机的，取决于你所使用的内存管理系统，当它提供给程序员时，它可能有一个标准的默认值。但点在于：始终有一个值。没有内置的方法可以表示“这个字节不包含任何内容”。

许多命令式语言，特别是那些元素追溯到 C 语言的语言，都将值 0（零）专门挑选出来表示“无”。当然，这种值必须与所有其他表示“某些东西”的值区分开来。我确定你还记得写过某些算法，在开始时会给某个整数变量赋值为 -1（或类似的值）的魔术值，作为默认值或起始值。广义地说，在内存位置通常存储指向内存位置指针的假设下，零值是一个好主意，因为在大多数现代模型中，零指针不是有效指针，对于“无”的情况来说似乎是安全的。对于那些零实际上是有效指针的架构，C 语言引入了 `null` 来表示空指针——当然，它不需要在 C 语言针对的每一个平台上都等于 0，但其概念是相同的。

对于许多情况来说，`null` 这个值显然是没用的。如果一个人的所有内存位置中只存储指向内存位置指针，那么在数据方面你将剩下什么呢？虽然只有少数几种类型可用（字节的解释不同），但许多后来的语言都带了大量的数据类型。语言设计者并没有注意到这些类型缺乏语言支持的“无”官方值的问题。

在 C# 2.0 和 .NET 中，微软引入了可空类型（nullable types）。这些本质上是上述问题的解决方案，并且与本章后续部分将讨论的 `Option` 类型实现非常相似。它也反映了许多函数式语言中存在的一种机制。它将“无”的理解从源自 C 的 `null` 值中移开，尽管在一个本身没有意义的语言中，这本身就很有意义。与可空类型相比，`Option<T>` 既可以用于引用类型，也可以用于值类型——在这些情况下存在某些混淆的可能，但拥有统一系统的优势似乎超过了这些问题。

应该提到的是，F# 中有一个 `Option<T>`，它在某种程度上被用作 C# 实现的模板。为了防止任何关于代码复制的投诉，C# 类型是从零开始实现的，以支持类似的公共 API。

### 实现可选（OPTIONAL）值

`Option<T>` 类的基本结构是显而易见的：除了一个值 `T` 之外，它还存储了一个标记，表示该值是否已设置。`Option` 是不可变的，因此这个决定是在构造期间做出的：新实例代表一个实际值还是“无”？

为任何类型 `T` 创建大量代表“无”的 `Option<T>` 新实例是没有意义的。因此，“无”的情况由类的单个实例涵盖，该实例通过名为 `None` 的公共字段提供。以下是该类可能的样子（这并不是 FSLib 中的实际内容），请继续阅读：

```csharp
public sealed class Option<T>{
    private readonly T value;
    public T Value {
        get { return value; }
    }
    private readonly bool hasValue;
    public bool HasValue {
        get { return hasValue; }
    }
    public bool IsSome {
        get { return hasValue; }
    }
    public bool IsNone {
        get { return !hasValue; }
    }
    public Option(T value) {
        this.value = value;
        this.hasValue = true;
    }
    private Option() {
    }
    public static readonly Option<T> None = new Option<T>( );
}
```

要创建一个选项实例类型，代码看起来如下：

```csharp
var intVal = new Option<int>(42);
var intValNothing = Option<int>.None;
```

在两种情况下，都有必要显式指定实际类型，因为类型推断在这些场景下不起作用。可以创建一个辅助函数来创建 `Option<T>` 实例，如果该函数使用方法泛型参数而不是类，它就可以从类型推断中获益。这是 `Option` 类（非泛型）的第一版本，结合了这样的辅助方法：

```csharp
public sealed class Option {
    public static Option<T> Some(T value) {
        return new Option<T>(value);
    }
}
```

这允许你创建包含值的 `Option<T>` 实例，如下：

```csharp
var intVal = Option.Some(42);
var doubleVal = Option.Some(37.5);
var boolVal = Option.Some(false);
```

到目前为止的实现，仍然存在易用性问题。例如，相等性并不是它应该有的。看这段代码：

```csharp
var intVal = Option.Some(5);
var intVal2 = Option.Some(5);
if (intVal == intVal2)
    Console.WriteLine("Values are equal");
```

在这个例子中，`intVal` 和 `intVal2` 应该被视为相等是一个合理的预期，但事实上它们并不相等。`Option<T>` 类需要以下方法来考虑相等性：

```csharp
public static bool operator ==(Option<T> a, Option<T> b) {
    return a.HasValue == b.HasValue &&
    EqualityComparer<T>.Default.Equals(a.Value, b.Value);
}
public static bool operator !=(Option<T> a, Option<T> b) {
    return !(a == b);
}
```

```csharp
public override int GetHashCode() {
    // Implementation for hash code
}
```

```cs
return hashCode;
}
public override bool Equals(object obj) {
    return base.Equals(obj);
}
```

`FCSLib` 包含了额外的扩展方法，用于帮助构建 `Option<T>` 值。这里有一段演示实例化和检查的简单代码：

```cs
var intOpt1 = new Option<int>(10);
var intOpt2 = 10.ToOption();
var stringOpt1 = Option.Some("text");
var stringOpt2 = "text".ToOption();
var noneOpt = Option.None;
```

```cs
// 检查相等性:
Console.WriteLine("intOpt1 = " + intOpt2 + " " + 
(intOpt1 == intOpt2)); // True
Console.WriteLine("stringOpt1 = " + stringOpt2 + " " + 
(stringOpt1 == stringOpt2)); // True
Console.WriteLine("intOpt1 = " + noneOpt + " " + 
(intOpt1 == noneOpt)); // False
Console.WriteLine("stringOpt2 = " + noneOpt + " " + 
(stringOpt2 == noneOpt)); // False
```

`Option<T>` 相比 `null` 和可空类型的一个重要优势在于，如果你愿意，`null` 可以被视为有效值。与其使用一个与有效值处于同一范围的“特例情况”来表示无效情况，不如 `Option<T>` 提供了独立的信息来区分“有值”和“无值”两种情况。C# 的可空类型工作方式类似，但仅适用于值类型。另一方面，`Option<T>` 在所有类型上都使用相同的方法。

`FCSLib` 允许你区分两种情况，其中一种既不是有效值也不是特例情况。

```cs
// null 值可以是一个有效值:
string nullStringOpt = null;
var nullStringOpt1 = nullStringOpt.ToOption();
Console.WriteLine("nullStringOpt1 = noneOpt: " + 
(nullStringOpt1 == noneOpt)); // False
```

```cs
// 或者它可以被认为等于 None:
var nullStringOpt2 = nullStringOpt.ToNotNullOption();
Console.WriteLine("nullStringOpt2 = noneOpt: " + 
(nullStringOpt2 == noneOpt)); // True
```

为了清晰起见，这里是两个扩展方法 `ToOption` 和 `ToNotNullOption`：

```cs
public static Option<T> ToOption<T>(this T val) {
  return Option.Some(val);
}
```

```cs
public static Option<T> ToNotNullOption<T>(this T val) where T : class {
  return val != null ? val.ToOption() : Option.None;
}
```

# 总结

使用 `Option<T>` 类型代替 `null` 值是处理信息缺失很重要情况的另一种策略。`Option<T>` 类型是处理 `null` 值的一种更整洁的方法，因为它们在值类型和引用类型中的用法没有区别。它们更加强大，因为它们采用了一种“元数据”方法来存储关于值的额外信息，从而能够充分利用类型的范围（包括其本身）。

支持 `Option<T>` 的另一个重要论点是可以将其视为单ad（monad），这使得能够进行操作链式调用，而不需要显式的分类处理。这一主题在第 17 章中进行了深入讨论。

# 16 保持数据不变

**本章包含内容？**

- 为什么变化并不总是好事
- 简单的不可变类型
- 带有修改的克隆
- 不可变容器结构
- 不可变类型的替代方案

数据是可变的，这在现实生活中确实发生，并在主流编程中被视为事实。但数据的可变性引发了许多问题，因此程序员们对此产生了怀疑。在函数式编程世界中，数据传统上是不可变的，数据结构往往是持久的（persistent）。“持久”一词很容易被误解，因为它似乎指向在文件系统、数据库或类似的存储单元中存储数据的持久性。但这里指的是瞬时的（ephemeral），意味着短寿命的，不应暗示数据的任何存储机制。

### 变化是好事——并不如此！

持久数据结构背后的思想很简单。对于一个特定的目的——也许是一个执行线程、一个进程、单一算法实现，换句话说，该词的字面意思——知道工作单元使用的数据不能发生变化是很有用的。从另一个角度看，它似乎发生了变化；这没关系。但工作单元应该能够从头到尾执行其任务，而不必担心数据发生潜在变化。如果数据结构保证了这种行为，它们就被称为持久的。

只使用持久数据结构的编程风格具有许多实际优势。首先，如果不需要为算法中间发生意外情况的情况做准备，代码将变得更容易编写。更简单的代码结构导致更少的编程错误、更好的可维护性、更强的封装性，以及更容易防错的调试和测试。泛指函数式编程推崇的无副作用编程的理念得到了不可变数据思想的精辟支持，结果是使用持久数据结构的函数更容易并行化和模块化，而无需担心执行顺序、锁定以及命令式编程中的类似技术。

接下来的示例展示了两个容器类的典型（尽管是简单的）实现：`MutableProduct` 和 `MutableOrderLine`：

```cs
public class MutableProduct {
    public string Name { get; set; }
    public decimal Price { get; set; }
}
public class MutableOrderLine {
    public MutableProduct Product { get; set; }
    public int Count { get; set; }
    public decimal GetValue() {
        return Product.Price * Count;
    }
}
```

```cs
[TestFixture]
public class EphemeralTests {
    [Test]
    public void TestOrderLine() {
        var product = new MutableProduct { Name = "Rubber boat", Price = 16.99m };
        var line = new MutableOrderLine { Product = product, Count = 3 };
        Assert.AreEqual(50.97m, line.GetValue());
    }
}
```

这里还有一个单元测试，检查了对象值的组合，业务逻辑函数 `GetValue()` 返回了正确的结果。示例比实际应用简单得多，但细节是相似的。

### 错误的假设

这个示例中有趣的地方在于做了一个假设：“在计算 `OrderLine` 过程中，`MutableProduct.Price` 和 `MutableOrderLine.Count` 的值不会发生变化。”在这个简单测试的范围内，这个假设是正确的，但在这样的人工上下文中，这无法得到保证。数据结构的定义使得其包含的数据可以在任何时间发生变化。当然，这在现实中只有当数据跨线程共享时才会发生。在微软 .NET 数据类型的文档中，有一个章节说明每个数据类型是安全的还是否。标记为线程安全的数据结构通常具有锁定或其他访问保护/协调机制以防止冲突访问。

在示例场景中，假设在整个 `GetValue` 函数表示的工作单元中保持一致的数据位于两个不同的对象中。这些对象理论上可以对其单个属性实现锁定，但并不足够。算法可能需要在函数级别进行锁定，在计算值之前获取两个独立的锁。或者，使用 `Count` 这样简单字段的老值或新值可能并不重要。场景确实显示了时间是可以变化的。这对程序是否有影响取决于算法本身，也取决于数据结构的复杂性。

### 静态是好事

锁定和其他访问控制机制的替代方案是按照上述数据类的方式实现数据结构，使其符合函数式编程词汇中的持久性定义。

```csharp
[Test]
public void TestOrderLineValue() {
    var product = new PersistentProduct("Rubber boat", 16.99);
    var line = new PersistentOrderLine(product, 3);
    Assert.AreEqual(50.97, line.GetValue());
}
```
