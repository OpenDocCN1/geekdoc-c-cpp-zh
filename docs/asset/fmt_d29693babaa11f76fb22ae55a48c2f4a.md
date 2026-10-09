
你会发现 `String` 和 `StringBuilder` 类并没有完全的方法对等，`String` 有 `ToUpper`、`EndWith`、`PadLeft`、`PadRight` 等。`StringBuilder` 提供了所有这些方法。遗憾的是目前这些类之间还没有完全对应。例如，为了构建一个字符串并将所有字符转换为大写，你必须使用 `StringBuilder` 来完成某些任务。例如，为了构建这样一个字符串：

```csharp
// 构造一个 StringBuilder 来执行字符串操作
StringBuilder sb = new StringBuilder();

// 通过 StringBuilder 执行一些字符串操作
sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "-");

// 将 StringBuilder 转回 String
String s = sb.ToString().ToUpper();
```

[第 367 页]

```csharp
// 清空字符串（分配一个新的 Char 数组）。
sb.Length = 0;

// 将大写字符串加载到 StringBuilder
sb.Append(8, "Marc-");

// 将 StringBuilder 转换为 String。
s = sb.ToString();

// 将字符串显示给用户。
Console.WriteLine(s); // "JEFFREY-MARC-"
```

仅仅因为 `StringBuilder` 没有提供所有操作就编写这种代码既不方便也不高效。在未来，我希望微软能为 `StringBuilder` 添加更多字符串操作方法，使其更完善。

## 获取对象的字符串表示

你经常需要获取对象的字符串表示。通常，当你想要向用户显示数值类型（如 `Byte`、`Int32`、`Single`）或 `DateTime` 对象时，这是必要的。因为 .NET 框架是一个面向对象的框架，每个类型都负责提供将实例值转换为字符串的代码。在设计类型如何遵循这一点时，FCL 的设计者定义了一个一致的模式。在本节中，我将描述这种模式。

你可以通过调用 `ToString` 方法获取任何对象的字符串表示。公共虚拟无参数 `ToString` 方法由 `System.Object` 定义，因此可以使用任何类型的实例调用。语义上，`ToString` 返回一个表示对象当前值的字符串，并且该字符串应该根据调用线程的区域进行格式化；也就是说，数字的字符串表示应该使用与区域分隔符、数字分组符号以及分配给调用线程的区域相关的元素。

`System.Object` 的 `ToString` 实现简单返回对象的值的全名。这并不特别，但对于许多无法提供合理字符串的类型来说，这是一个合理的默认。例如，`FileStream` 或 `Hashtable` 的字符串表示应该是什么样的？

所有提供表示对象当前值的合理字符串方法的类型都应该覆盖 `ToString` 方法。FCL 内置的所有类型（`Byte`、`Int32`、`UInt64`、`Double` 等）都覆盖了它们的 `ToString` 方法并返回区域感知字符串。在 Visual Studio 调试器中，当鼠标悬停在特定变量上时会显示数据提示。数据提示中的文本是通过调用对象的 `ToString` 方法获取的，因此你应该始终覆盖 `ToString` 方法以获得良好的调试支持。

### 特定格式与文化

无参数的 `ToString` 方法存在两个问题。首先，调用者无法控制字符串的格式。例如，应用程序可能将数字格式化为货币字符串、小数字符串、百分比字符串或十六进制字符串。其次，调用者无法轻松使用特定文化来格式化字符串。第二个问题对于服务器端应用代码来说，比客户端代码更具棘手。在少数情况下，应用程序需要使用与调用线程关联不同的文化来格式化字符串。为了对字符串格式化有更多控制权，你需要一个允许指定格式和文化信息的 `ToString` 方法版本。

为调用者提供格式和文化选择的类型实现了 `System.IFormattable` 接口：

```c
public interface IFormattable {
    ToString(string format, IFormatProvider formatProvider);
}
```

在 FCL 中，所有基本类型（`Byte`、`SByte`、`Int16`/`UInt16`、`Int32`/`UInt32`、`Int64`/`UInt64`、`Single`、`Double`、`Decimal` 和 `DateTime`）都实现了此接口。此外，其他类型（如 `Guid`）也实现了它。最后，每个枚举类型定义都将自动实现 `IFormattable` 接口，以便从枚举类型的实例获取有意义的字符串。

`IFormattable` 的 `ToString` 接受两个参数。第一个参数 `format` 是一个告诉方法应如何格式化对象的字符串。`ToString` 的第二个参数 `formatProvider` 是实现 `System.IFormatProvider` 接口的类型的实例。这为 `ToString` 方法提供了特定的文化信息。我稍后会讨论这一点。

实现 `IFormattable` 接口的类型的 `ToString` 方法决定了它将识别哪些格式字符串。如果你传递了一个类型不识别的格式，它本认为应该抛出 `System.FormatException`。

FCL 中的许多类型都识别多种格式。例如，`DateTime` 类型支持 `"D"` 表示短日期、`"d"` 表示长日期、`"g"` 表示通用、`"M"` 表示月份、`"s"` 表示可排序、`"T"` 表示长时间、`"U"` 表示 ISO 8601 格式的通用时间、`"Y"` 表示年/月的通用时间等。所有枚举类型都支持 `"G"` 表示通用、`"F"` 表示标志（flags）、`"D"` 表示小数和 `"X"` 表示十六进制。我将在第 15 章“枚举类型与位标志”中详细介绍枚举类型的格式化。

此外，所有内置数值类型都支持 `"C"` 表示货币、`"D"` 表示小数、`"E"` 表示指数（科学）计数、`"F"` 表示固定点、`"G"` 表示通用、`"N"` 表示数字、`"P"` 表示百分比、`"R"` 表示往返（round-trip）以及 `"X"` 表示十六进制。事实上，数值类型还支持自定义格式字符串，以防简单格式字符串无法满足你的需求。自定义格式字符串包含特殊字符，告诉类型的 `ToString` 方法精确显示多少数字、精确在何处放置小数点分隔符、分隔符后精确放置多少数字等。有关格式字符串的完整信息，请参阅 .NET Framework SDK 中的“格式化类型”。

对于大多数类型，调用 `ToString` 并为格式字符串传递 `null` 与调用 `ToString` 并传递 `"G"` 是等同。换句话之，对象默认使用“通用格式”（General format）进行格式化。在实现类型时，你可以选择一个你认为最常用的格式；该格式就是“通用格式”。顺便提一下，无参数的 `ToString` 方法确保了调用者调用的是“通用格式”。

现在格式字符串已经过了，让我们转向文化信息。默认情况下，字符串使用与调用线程关联的文化信息进行格式化。无参数的 `ToString` 方法确实是这样，如果你为 `formatProvider` 参数传递 `null`，`IFormattable.ToString` 也是如此。

当你格式化数字（包括货币、整数、浮点数、百分比、日期和时间）时，适用文化敏感信息。`Guid` 有一个返回表示其字符串的 `ToString` 方法。生成 `Guid` 字符串不需要考虑文化，因为 GUID 用于编程目的。

在格式化字符串时，`ToString` 方法会看到你传递给 `formatProvider` 参数的内容。如果传递 `null`，`ToString` 将确定与调用线程 `System.Threading.Thread.CurrentCulture` 属性关联的文化。该属性返回 `System.Globalization.CultureInfo` 类的实例。使用此对象，`NumberFormatInfo` 类型定义了诸许多属性，如 `CurrencySymbol`（货币符号）、`NegativeSign`（负号）、`NumberGroupSeparator`（数字分组分隔符）、`CurrencyGroupSeparator`（货币分组分隔符）、`CurrencyDigitSeparator`（货币数字分隔符）和 `PercentSymbol`（百分比符号）。同样，`DateTimeInfo` 类型定义了如 `Calendar`（日历）、`DayNames`（名称）、`LongDatePattern`（长日期模式）、`ShortDatePattern`（短日期模式）和 `TimePattern`（时间模式）。

## 第三部分 类型

## 字符、字符串与文化操作

`System.Globalization.CultureInfo` 类是 FCL 中少数实现 `IFormatProvider` 的类型之一。如果你想为（例如）越南格式化字符串，你会构造一个 `CultureInfo` 对象并将其传递给 `ToString`：

```csharp
Decimal price = 123.54;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);
```

如果你构建并运行此代码，将显示图 14-5 中的消息框。注意结果字符串中的第一个字符：这是国际货币符号（U+0A4）。

在内部，`ToString` 方法看到 `formatProvider` 参数不是 `null`。如果是，它将返回 `NumberFormatInfo` 类型的实例如下：

```csharp
NumberInfo nfi = (NumberInfo)culture.GetFormat(typeof(NumberFormat));
```

实际上，由于 `GetFormat` 足够灵活允许任何类型，你也可以这样请求日期信息：

```csharp
DateTimeInfo dtfi = (DateTimeInfo)culture.GetFormat(typeof(DateTimeInfo));
```

顺便提一下，如果你想获取一个不针对特定文化格式化的字符串，你应该调用 `CultureInfo` 的静态属性 `InvariantCulture` 并将其传递给 `ToString`：

```csharp
Decimal price = 123.54;
String s = price.ToString("C", CultureInfo.InvariantCulture);
MessageBox.Show(s);
```

如果你构建并运行此代码，将显示图 14-6 中的消息框。

# 第 14 章 字符、字符串与文本处理

```csharp
// 此版本简单调用 ToString(format, null)。
// 含义：调用者指定的格式，线程的文化信息
public String ToString(String format);
```

```csharp
// 此版本简单调用 ToString(null, formatProvider)。
// 此版本实现了 IConvertible 的 ToString 方法。
// 含义：通用格式，调用者指定的文化信息
public String ToString(IFormatProvider formatProvider);
```

## 将多个对象格式化为单个字符串

到目前为止，我已经解释了单个类型如何格式化其对象。然而，在某些情况下，你可能想要构建包含许多许多格式化对象的字符串。例如，下面的字符串包含一个日期、一个姓名和一个年龄：

```csharp
String s = String.Format("On {0}, {1} is {2} years old.",
 DateTime(2010, 4, 22, 14, 35, 5), "Aidan", 7);
Console.WriteLine(s);
```

如果你在线程当前文化为 `"en-US"` 的环境下构建并运行此代码，你将看到以下输出行：

4/22/2010 2:35:05 PM, Aidan is 7 years old.

`String` 的静态 `Format` 方法接收一个格式字符串，该字符串使用大括号中的数字来标识可替换参数。示例中使用的格式字符串告诉 `Format` 方法将 `{0}` 替换为格式字符串后的第一个参数（日期/时间），将 `{1}` 替换为格式字符串后的第二个参数 `"Aidan"`，并将 `{2}` 替换为格式字符串后的第三个参数（7）。

在内部，`Format` 方法调用每个对象的 `ToString` 来获取该对象的表示。返回的字符串将将追加在一起，并返回完整的最终字符串。这本身很好且没问题，但意味着所有对象都是使用它们的通用格式和调用线程的文化信息进行格式化的。

如果你在大括号内指定了格式化信息，那么在格式化对象时就可以获得更多控制权。例如，下面的代码与上一个示例相同，区别在于我对可替换参数 0 和 2 添加了格式化说明：

```csharp
String s = String.Format("On {0:D}, {1} is {2:E} years old.",
 DateTime(2010, 4, 22, 14, 35, 5), "Aidan", 7);
Console.WriteLine(s);
```

如果你在线程当前文化为 `"en-US"` 的环境下构建并运行此代码，你将看到以下输出行：

Thursday, April 22, 2010, Aidan is 7.000000E+000 years old.

当 `Format` 方法解析格式字符串时，它看到可替换参数 0 应该调用其 `Formattable` 接口的 `ToString` 方法 `"D"`，且其参数为 `null`。同样地，`Format` 调用可替换参数 2 的 `IFormattable ToString` 方法，传递 `"E"` 和 `null`。如果该类型没有实现 `IFormattable` 接口，`Format` 将调用其继承自 `Object`（并可能被重写）的无参数 `ToString` 方法，并将默认格式追加到结果字符串中。

`String` 类提供了 `String` 方法的几个重载。其中一个版本接收一个实现了 `IProvider` 接口的对象，这样你就可以使用调用者特定的文化信息来格式化所有可替换参数。显然，`Format` 调用每个对象的 `IFormattableToString` 方法，传递传递给 `Format` 的任何 `IProvider` 对象。

如果你使用 `StringBuilder` 而不是 `String` 来构建字符串，可以调用 `StringBuilder` 的 `AppendFormat` 方法。该方法的工作原理与 `String` 的 `Format` 方法完全相同，只是它格式化字符串并将其追加到 `StringBuilder` 的字符数组中。与 `String` 的 `Format` 一样，`AppendFormat` 接收字符串，并且有一个版本接收 `IProvider`。

`System.Console` 提供了 `Write` 和 `WriteLine` 方法，它们也接收格式字符串和可替换参数。然而，`Console` 的 `Write` 和 `WriteLine` 方法没有针对特定文化的字符串重载，你可以先调用 `String` 的 `Format` 方法，首先传递所需的 `IProvider` 对象，然后将生成的字符串传递给 `Console` 的 `Write` 或 `WriteLine` 方法。这不应该是什么大问题，正如我之前提到的，客户端使用与调用线程关联的特定文化来格式化字符串的情况非常罕见。

## 提供你自己的自定义格式化器

现在可以确定，.NET Framework 中的格式化能力设计旨在为你提供极大的灵活性和控制力。然而，我们还没有完全结束。你可以定义一个方法，当 `StringBuilder` 的 `AppendFormat` 方法将任何对象格式化为字符串时都会调用该方法。换句话说，而不是为每个对象调用 `ToString`，`AppendFormat` 可以调用你定义的函数，允许你按任何的方式格式化所有对象。我即将描述的内容也适用于 `String` 的 `Format` 方法。

让我通过一个示例来解释这种机制。假设你正在格式化用户将在浏览器中查看的 HTML 文本。你希望所有的 `Int32` 值都加粗。为了实现这一点，每当将 `Int32` 值转换为字符串时，你都希望字符串周围带有 HTML 加粗标签：`<B>` 和 `</B>`。下面的代码演示了这样做有多简单：
