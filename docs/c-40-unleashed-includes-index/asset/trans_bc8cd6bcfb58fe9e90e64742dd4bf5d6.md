
```
    public interface IFormattable
    {
        string ToString(string format, IFormatProvider formatProvider);
    }
```

事实上，在介绍数值和 DateTime 等大量基元类型时，我们已经多次看到这类方法。在讨论中，我们了解了 `IFormatProvider` 接口如何由 `System.Globalization` 中的 `CultureInfo` 类实现，从而允许我们控制用于格式化对象文本表示的区域性。例如：

```
    Console.WriteLine(123.45.ToString(new CultureInfo("en-US")));
    Console.WriteLine(123.45.ToString(new CultureInfo("nl-BE")));
```

在前面的示例中，第一行打印 123.45，而第二行使用逗号作为小数分隔符（打印 123,45）。请注意，这个 `ToString` 重载并非来自 `IFormattable` 实现，而是一个单参数快捷方式，它省略了我们接下来要讨论的 format 参数。

## 格式字符串

文本格式化一直是嵌入在 C、C++、C# 和 Visual Basic 等大型通用语言中的迷你语言的传统领域。例如，具有原生代码背景的开发人员会知道 `printf` 的格式字符串语法：

```
    printf("The value is %d", 42);
```

.NET 在这方面也不例外，它定义了格式字符串的概念，可用于在值到文本的转换中控制文本格式化。让我们通过接触一些最常用的格式化说明符来看看这些功能。

首先，重要的是要认识到每种数据类型都可以定义自己的格式化样式，这些样式与数据的领域很好地契合。例如，对于数值小数，定义小数点表示法的概念是合理的，而日期和时间值可以根据值的组成部分（例如年份和分钟）来定义格式。由于数字是程序中经常使用的样本，我们先来看看它们。以下代码展示了同一个数字以多种方式进行格式化：

```
    var enUS = new CultureInfo("en-US");
    var nlBE = new CultureInfo("nl-BE");
    var jaJP = new CultureInfo("ja-JP");

    double d = 123.456;
    int i = 1234;
    long l = 123456789;
```

```text
// Zero placeholders
// Inserts zeros if no digit appears at the given position
Console.WriteLine(i.ToString("00000", enUS)); // 01234

// Decimal point
// Here mixed used with trailing zero padding
Console.WriteLine(d.ToString("0###.##", enUS)); // 0123.46
```

还有其他自定义说明符可用，其文档可在 MSDN 上找到。其中一些非常强大，但因此有时语法相当晦涩。

## 迷你语言

不幸的是，格式字符串是那种容易侵入框架的遗留迷你语言之一。由此带来的一个不幸影响是，开发人员需要将它们与所使用的编程语言分开学习。此外，语言并不关心这些不透明的字符串，也不会对它们执行任何类型的编译时检查。

消除这类魔法字符串一直是一个好趋势；例如，通过 LINQ（而不是使用 T-SQL 之类）甚至 C# 4.0 dynamic（而不是将方法指定为字符串之类）等语言特性来实现。一等数学说明符可能会相当复杂，但可能行得通。

在另行通知之前，格式字符串是一种必要的恶，如果使用了不支持的说明符，或者以不恰当的方式使用它们（例如，在小数上使用 D），就可能导致运行时错误信号。

格式化不仅适用于数字。许多其他类型也有自己的格式化方案。这里展示了几个示例：

```text
// Date patterns without time
// Others include date/time, UTC, year/month, roundtrip, etc.
var bd = new DateTime(1983, 2, 11);
Console.WriteLine(bd.ToString("d", nlBE)); // 11/02/1983
Console.WriteLine(bd.ToString("D", nlBE)); // vrijdag 11 februari 1983

// Custom date/time specifiers
// ddd = short day of week; dd = day of month; MM = month
Console.WriteLine(bd.ToString("ddd dd/MM", enUS)); // Fri 11/02
```

在这里复制 MSDN 文档没有意义。最重要的是对格式化的丰富性有所熟悉，足以鼓励你更详细地探索格式字符串。

我们还需要看的一点是，在单个字符串中一次格式化多个值的能力。这称为复合格式化。在本书前面的各种场合，我们在使用 `Console.WriteLine` 方法更高级的重载之一时曾粗略涉及过这一点：

```
Console.WriteLine("{0} costs {1}", product, price);
```

可以猜到，`{0}` 和 `{1}` 子字符串充当后续参数中传入值的占位符。这里的第一个参数充当复合格式字符串，后面跟着一个 `params` 数组：

```
public static void WriteLine(string format, params object[] arg) { ... }
```

复合格式字符串可用于许多地方，`WriteLine` 方法只是其中之一。可能最通用的一个是 `System.String` 类本身的静态 `Format` 方法，其签名与刚刚展示的类似。

## 可本地化的应用程序

使用格式字符串应该成为每个有自尊的 .NET 开发人员的基因，因为它是实现应用程序可本地化的主要方式。简单的字符串拼接无法胜任，因为句子中单词的顺序在不同语言中常常不同。

显然，如果需要翻译格式字符串，就不会把它们保留在编译后的二进制文件中。相反，会使用本地化表，这些表可以通过 BCL 设施加载和查询，我们在此不详述。如果你需要编写可本地化的软件（如今谁不需要呢？），请务必查看这一点。

除了仅填充复合格式字符串的占位符之外，你还可以做更多事情。此外，每个所谓的格式项都可以有一个可选的格式字符串来格式化相应的参数值，以及一个可选的对齐方式。格式项具有以下语法：

```
{index[,alignment][:formatString]}
```

其中，我们已经看到了索引（从零开始）以及一些可用于各种对象的格式字符串。例如，将索引的使用与 C（表示货币）格式字符串结合，我们可以编写以下代码：

```
Console.WriteLine("{0} costs {1:C}", "Chai", 123.45);
```

这会打印此处显示的输出，具体依赖于当前用户的文化设置（实际上可以通过 `System.Globalization` 功能以编程方式调整）：

Chai 的价格为 $123.45

```
foreach (var product in products)
    Console.WriteLine("{0,-30} {1,8:C}", product.Name, product.Price);
```

在前面的示例中，我们使用 30 个字符作为产品名称的宽度，这些名称以左对齐方式打印。价格以最大宽度八个字符右对齐（足以容纳一个货币符号、价格非小数部分的四位数字、一个小数点分隔符以及另外两位表示美分的数字）。在前两行中，我们还打印了具有相同对齐方式的表头，并使用字符串构造函数将短横线字符重复若干次。考虑以下输入：

```
var products = new[] {
    new { Name = "Chai", Price = 1.25m },
    new { Name = "Expensive lawn mower", Price = 495.95m },
    new { Name = "Chang", Price = 5m },
};
```

使用这个 products 集合，会打印以下内容：

| 产品名称 | 价格 |
|---|---|
| Chai | $1.25 |
| 昂贵的割草机 | $495.95 |
| Chang | $5.00 |

这展示了丰富的格式项在实际工作，使用了必需的索引、对齐方式以及（对于价格）格式字符串。如你所见，框架可以代表你完成大量格式化工作，同时使本地化更容易。

## 将文本解析为对象

将对象转换为文本表示是一回事，处理用户（或文本文件等）输入并将其转换为丰富对象则是另一回事。你已经看到了一整套 `Parse`、`TryParse` 和 `Exact` 变体，但还有几点需要注意。

有时，在对象和文本之间来回转换并不是无损转换。在这种情况下，框架通常会提供一个名为 R 的格式字符串，以生成一种文本表示，在使用 `Parse` 方法时可以恢复原始值。一个很好的例子是浮点数，其十进制表示并不精确：

```
double value = 1.0 / 3.0;

string text = value.ToString();
Console.WriteLine(text);            // 0.33333333333333
double res1 = double.Parse(text);
Console.WriteLine(res1);
Console.WriteLine(value == res1);    // False
```
