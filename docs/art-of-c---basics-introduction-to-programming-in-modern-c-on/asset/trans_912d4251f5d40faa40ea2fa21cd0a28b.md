
```csharp
var b = new int[] { 1, 2 };
AddOneToElements(b);
Console.WriteLine($"b = {{string.Join(", ", b)}}");

static void AddOneToElements(int[] x) {
    for (var i = 0; i < x.Length; i++) {
        x[i]++;
    }
}
```

如果我们运行这个程序，其输出将是`b = {2,3}`。

与前面的示例不同，在这个方法内部更改 `x`（类型为 `int[]`）的值，会改变外部变量 `b` 的值。这被称为“引用语义”（reference semantics）。

当我们调用方法 `AddOneToElements()` 时，`b` 的值，即一个引用，确实被复制了。在方法内部，`x` 与方法参数 `b` 不同。但重要的是，两者都指向同一个底层值 `{1, 2}`。当我们改变引用 `x` 的底层值/数据时，外部变量 `b` 的底层值/数据也随之改变，因为它们指向相同的值/数据。

一个（底层）值可以被多个引用共享，改变其中一个引用（的底层值）会影响所有其他引用（的底层值）。

在支持指针的语言中，指针/引用的“值”是存储底层值的内存位置的地址。C# 使用了类似的东西，虽然它可能并不是确切的内存地址，通常来说，因为 C# 是一种垃圾回收语言。

但这个事实只是次要的。“引用语义”在概念上就是我们这里描述的内容，无论它在特定的编程语言/运行时中实际上是如何实现的。

C# 确实有指针（以及像 `fixed` 这样的关键字），它们可以在“非安全”（unsafe）上下文中使用。如前所述，我们在这本书中不讨论“非安全的 C#”。

引用变量的底层值通常存储在“堆内存”（heap memory）中。堆内存分配给正在运行的程序，并保留到程序终止为止。为了支持引用语义，如前所述，底层值需要存储在某个“持久”位置。

另一方面，值类型的值或引用值（不是底层值）可以并且通常存储在被称为“栈内存”（stack memory）的临时位置。当函数/方法被调用时，会创建一个新的栈帧，所有临时变量或“局部”变量都存储在栈上。当函数/方法返回时，栈帧被销毁，存储在该帧中的所有值都会丢失（除非它们被“复制”到其他位置）。

这些内存位置最重要的区别之一是，在堆上分配内存通常更昂贵，因为它有一些内存管理的开销。相比之下，在栈内存上创建和销毁值要便宜得多。从这个意义上说，值类型的值（几乎总是存储在栈上）更受青睐。

另一方面，复制大型值可能很昂贵。引用是小的值（例如，取决于机器架构，在几个字节的数量级），复制它们的值（不是底层值）可能相当有效。这通常与复制整数值相当。因此，在某些情况下，引用变量比值变量更受青睐。

我们忽略了许多细节，但这是本课程最重要的收获。值在某些情况下可能很有用，值语义在某些情况下也可能很有用。引用在某些情况下可能很有用，引用语义在某些情况下也可能很有用。

作为一名程序员，当你有选择时，你必须弄清楚何时使用什么。

> 如前所述，在许多编程语言如 Java 或 Python 中，你没有太多选择。在 C# 中的选择是一种力量。而且，如你所知，*能力越大，责任越大。* ☺

与那些支持指针的语言不同，在 C# 中，通常，值类型的值遵循值语义，而引用类型或引用的值遵循引用语义。

C# 提供了一种在特定情况下对值使用引用语义的方法。`ref` 关键字（及其两个“兄弟”关键字）可用于将值作为参数传递给方法时，或从方法返回值时。这里有一个例子：

```csharp
var c = 10;
MultiplyByTwo(ref c);
Console.WriteLine($"c = {c}");

static void MultiplyByTwo(ref int c) {
   c *= 2;
}
```

这个程序的输出是 `c = 20`。

这就像是创建了一个包含 `c` 的（单元素）数组，并且该数组被用来调用 `MultiplyByTwo()`，正如前面使用 `AddOneToElements()` 的示例那样。这是引用语义。虽然 `int` 是值类型，并且在这种情况下 `c` 是一个值，但 C# 允许我们在需要/期望的特定情况下使用引用语义。（这有时被称为“引用传递”，与“值传递”相对。）

> 注意，C# 的 `ref return` 有效地提供了“移动语义”。如前所述，复制（大型）值可能很昂贵，而 `in`、`ref` 和 `out` 基本上提供了一种变通方法。

另一方面，如果你想对引用使用值语义，那么在像 Java 和 C# 这样的语言中，约定是覆盖并使用诸如“Object.Clone()”或“Object.MemberwiseClone()”之类的方法来实现“深度复制”逻辑，而不是使用赋值运算符（=），后者执行浅拷贝。

事实上，C# 允许“运算符重载”，我们将在接下来的几课中讨论。因此，我们可以使用 `class`（默认遵循引用语义）创建自定义类型，并使其表现得像值类型。很快我们就会看到，`record`（在 C# 9.0 中引入）为我们做了这件事，而无需我们通过运算符重载等方式来实现值逻辑。

## 第 18 课：股票行情

### 18.1. 简介

我们在前两课中使用 `class` 和 `struct` 创建自定义类型。这次让我们尝试使用 `record`。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_291_0.png)

记录类型最早在 C# 9.0 中引入，现在（截至 C# 10.0）它可以与类（引用类型）和结构体（值类型）一起使用。而且，取决于你通常做什么类型的编程，记录可能是 C# 程序员拥有的最好的事物之一。

编程中最糟糕的事情之一就是反复做同样的事情。例如，我们经常需要创建许多类型，这些类型在很多方面彼此非常相似，但又足够不同以成为单一类型。结果我们会有很多相似的代码，其中许多可以被称为“样板”代码。

C# 的 record 是减少样板代码的努力之一。

总的来说，“更少的代码”是件好事。更少的代码意味着一开始要写的代码更少，要阅读的代码更少，要维护的代码更少。

写更少的代码意味着你将有更多时间做其他事情。或者，你将有更多时间做更多的编码。⋆

### 18.2. 代码审查 - 假股票行情服务

我们在本课中使用一个“假”股票行情应用程序作为示例程序。

主驱动程序每半秒（或 500 毫秒）检查一次（假的）苹果和（假的）微软股票的股价，如果某只股票的股价发生了变化，则打印出该股票代码对应的股票记录。

#### stock-ticker/Program.cs (第 3-22 行)

```csharp
const int intervalMillis = 500;
var symbols = new[] { Prices.AAPL, Prices.MSFT };
var stocks = new Dictionary<string, Stock>() {
	{ Prices.AAPL, new(Prices.AAPL, 0.0m) },
	{ Prices.MSFT, new(Prices.MSFT, 0.0m) },
};
while (true) {
	foreach (var symbol in symbols) {
		var stock = Ticker.Get(symbol);
		if (stock != stocks[symbol]) {
			stocks[symbol] = stock;
			Console.WriteLine(stock);
		}
	}

	await Task.Delay(intervalMillis);
}
```

请注意，该程序通过 `while(true)` 循环无限期运行。

`Ticker` 是一个返回给定股票代码的股票记录的“服务”。它通过调用 `Prices` 服务来更新股价。

#### stock-ticker/Ticker.cs (第 3-13 行)

```csharp
public static class Ticker {
    private static readonly Dictionary<string, Stock> stocks = new() {
        { Prices.AAPL, new(Prices.AAPL, Prices.Stock[Prices.AAPL]) },
        { Prices.MSFT, new(Prices.MSFT, Prices.Stock[Prices.MSFT]) },
    };

    public static Stock Get(string symbol) {
        stocks[symbol] =
            stocks[symbol].UpdatePrice(Prices.Stock[symbol]);
        return stocks[symbol];
    }
}
```

在这个例子中，`Ticker` 被实现为一个静态类，它通过静态方法暴露一个 API，`Get()`。

（假的）“Prices” 服务使用一系列随机生成的数字模拟实时股价变化。

