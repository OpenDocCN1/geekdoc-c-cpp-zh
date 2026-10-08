
你会发现 `String` 和 `StringBuilder` 类没有完全的方法等性，因为 `String` 拥有 `TLower`、`Upper`、`Trim`、`PadLeft`、`PadRight`。`StringBuilder` 没有提供这些任何一个方法。仅仅因为 `StringBuilder` 不提供所有操作而编写这种代码是既不便又低效的。未来，我希望微软能为 `StringBuilder` 添加更多字符串操作方法，使其成为更完整的类。

```csharp
// 构建一个 StringBuilder 来执行字符串操作。

StringBuilder sb = new StringBuilder();
```

```csharp
// 使用 StringBuilder 执行一些操作

sb.AppendFormat("{0} ({1})", "Jeffrey", "Richter").Replace(' ', '-');
```

```csharp
// 将 StringBuilder 转换为 String。

String s = sb.ToString().ToUpper();
```

```csharp
// 清除 StringBuilder（分配一个新的 Char 数组）。

sb.Length = 0;
```

```csharp
// 将大写字符串加载到 StringBuilder 中
// 执行更多操作。

sb.Append(s);
```

```csharp
// 向用户显示字符串。

Console.WriteLine(s);
```

## 获取对象的字符串表示：ToString

你经常需要获取对象的字符串表示。通常是在你想向用户显示数值类型（如 `Byte`、`Int32` 和 `Single`）或 `DateTime` 对象时。由于 `.NET` 框架是一个面向对象的框架，每个类型都负责提供将实例值转换为字符串的代码。在设计如何显示时，FCL 的设计者设计了一个贯穿始终的模式。在本节中，我将描述这种模式。

可以通过调用 `ToString` 方法获取对象的字符串表示。一个公共虚、无参数的 `ToString` 方法由 `System.Object` 定义，因此可以在任何类型的实例上调用。从语义上说，`ToString` 返回表示对象当前值的字符串，并且该字符串应该根据当前文化进行格式化；也就是说，数字的字符串表示应该使用与分配给调用线程的文化相关的的小数分隔符、数字分组符号和其他元素。

`System.Object` 的 `ToString` 实现简单地返回对象类型的全名。这个值并没有特别有用，但对于许多无法提供合理字符串的类型来说，这是一个合理的默认值。例如，`FileStream` 或 `Hashtable` 的字符串表示应该是什么样？

### 特定的格式与文化

无参数的 `ToString` 方法有两个问题。首先，调用者无法控制字符串的格式化。例如，应用程序可能希望将数字格式化为货币字符串、小数字符串、百分比字符串或十六进制。其次，调用者无法轻松地使用特定的文化来格式化字符串。第二个问题对于服务器端应用程序代码来说，比客户端代码更棘手。在少数情况下，应用程序需要使用与调用线程关联不同的文化来格式化字符串。为了对字符串格式化有更多控制权，你需要一个允许你指定格式和文化信息的 `ToString` 方法版本。

为调用者提供格式和文化选择的类型实现了 `System.IFormattable` 接口。

```csharp
public interface IFormattable
{
    string ToString(string format, IFormatProvider formatProvider);
}
```

在在 FCL（框架类库）中，所有基本类型（`Byte`, `SByte`, `Int16`/`UInt16`, `Int32`/`UInt32`, `Int64`/`UInt64`, `Single`, `Double`, `Decimal` 和 `DateTime`）都实现了此接口。此外，某些类型（如 `Guid`）也实现了它。最后，每个枚举类型定义都会自动实现 `IFormattable` 接口，以便从枚举类型的实例获取有意义的字符串。

`IFormattable` 的 `ToString` 接受两个参数。第一个参数 `format` 是一个字符串，告诉方法应该如何格式化对象。`ToString` 的第二个参数 `formatProvider` 是实现 `System.IFormatProvider` 接口的类型的实例。该类型为 `ToString` 方法提供文化信息。我稍后会讨论。

实现 `IFormattable` 接口的 `ToString` 方法的类型决定了将识别哪些格式字符串。如果你传递了一个该类型无法识别的 `format`，它应该抛出 `System.FormatException`。

此外，在所有内置数值类型的支持中……这些数值类型也支持自定义格式字符串，以防简单格式字符串无法完全提供你所需要的内容。

## 第三部分 核心类型

自定义格式字符串包含特殊字符，这些字符告诉类型的 `ToString` 方法精确应该显示多少位数字、精确在何放置分隔符、分隔符后精确放置多少位数字等。有关格式字符串的完整信息，请参阅 `.NET Framework SDK` 中的“格式化类型（Formatting Types）”。

对于大多数类型，调用 `ToString` 并为格式字符串传递 `null` 与调用 `ToString` 并为格式字符串传递 `"G"` 是等价。换句话说，对象默认使用“通用格式（General format）”进行自我格式化。在实现类型时，选择一个你认为最常用的格式；该格式就是“通用格式”。顺便说，不带参数的 `ToString` 方法确保了调用者调用的是“通用格式”。

现在格式字符串已经解决了，让我们转向文化信息。默认情况下，字符串使用与调用线程关联的文化信息进行格式化。无参数的 `ToString` 方法确实是这样做的，如果你为 `formatProvider` 参数传递 `null`，`IFormattable` 的 `ToString` 也是如此。

文化敏感信息在格式化数字（货币、整数、浮点数、百分比、日期和时间）时适用。指南中有一个 `ToString` 方法返回一个表示其值的字符串。在生成 `Guid` 的字符串时不需要考虑文化，因为 `GUID` 用于程序化目的。

在格式化数字时，`ToString` 方法会看到你传递给 `formatProvider` 参数的是什么。如果传递了 `null`，`ToString` 将通过读取 `System.Threading.Thread.CurrentCulture` 属性来确定与调用线程相关的文化。该属性返回 `System.Globalization.CultureInfo` 类型的实例。

使用此对象，`ToString` 根据正在格式化的是数字还是日期，读取其 `NumberFormat` 或 `DateTime`。这些属性分别返回 `System.Globalization.NumberInfo` 或 `System.Globalization.DateTimeInfo` 的实例。`NumberInfo` 类型定义了一系列属性，例如 `CurrencyDecimalSeparator`、`CurrencySymbol`、`NegativeSign`、`NumberGroupSeparator` 和 `PercentSymbol`。同样，`DateTimeInfo` 类型定义了一组属性，例如 `Calendar`、`DateSeparator`、`DayNames`、`LongDateTimePattern`、`ShortTimePattern` 和 `TimeSeparator`。`ToString` 在构建和格式化字符串时读取这些属性。

调用 `IFormattable` 的 `ToString` 方法时，与其传递 `null`，你可以传递一个实现 `IFormatProvider` 接口类型的对象的引用：

```csharp
public interface IFormattProvider
{
    Object GetFormat(Type formatType);
}
```

### 第14 章 字符、字符串与文本处理 353

`IFormatProvider` 接口后的基本思想是：当一个类型实现此接口时，它表示该类型的实例能够提供特定文化的格式化信息，并且可以忽略与调用线程关联的文化信息。

`System.Globalization.CultureInfo` 类型是 FCL 中少数实现 `IFormatProvider` 接口的类型之一。如果你想为（例如）越南格式化字符串，你将构造一个 `CultureInfo` 对象并作为对象传递给 `ToString` 的 `formatProvider` 参数。以下代码获取一个格式化为适用于越南货币的 `Decimal` 数值的字符串表示：

```csharp
Decimal price = 123.54M;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);
```

如果你构建并运行此代码，将出现图 14-5 所示的对话框。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_370_0.png)

图 14-5 格式化为货币的数值

在内部，`Decimal` 的 `ToString` 方法看到 `formatProvider` 不为 `null`，并调用对象的 `GetFormat`：

```csharp
NumberInfo nfi = (NumberInfo)formatProvider.GetFormat(typeof(NumberInfo));
```

实际上，由于 `GetFormat` 可以识别任何类型，该方法足够灵活，允许请求任何格式信息。但其他类型（如 `DateTime`）只请求数字格式：

```csharp
DateTimeInfo dtfi = (DateTimeInfo)formatProvider.GetFormat(typeof(DateTimeInfo));
```

### 第三部分 核心类型

顺便说，如果你想为特定的文化获取字符串，你应该调用 `System.Globalization.CultureInfo` 的静态属性 `InvariantCulture` 并将其对象作为参数传递：

```csharp
Decimal price = 123.54M;
String s = price.ToString("C", CultureInfo.InvariantCulture);
MessageBox.Show(s);
```

如果你构建并运行此代码，将出现图 14-6 所示的对话框。注意结果字符串中的第一个字符：这是货币的国际符号（U+00A4）。

![](img/0ba8f96d6619cf5f73315fb4561d09b5_371_0.png)

图 14-6 格式化为中性货币的数值

通常，你不会向用户显示由不变文化格式化的字符串。通常，你只会将此字符串保存在数据文件中，以便以后解析。

在 FCL 中，有三个类型实现了 `Provider` 接口。第一个是 `CultureInfo`，我已经解释过了。另外两个是 `NumberInfo` 和 `DateTimeInfo`。当在 `NumberInfo` 对象上调用 `GetFormat` 时，该方法检查请求的类型是否为 `NumberInfo`。如果是，则返回；如果不是，则返回 `null`。同样，在 `DateTimeInfo` 对象上调用 `GetFormat` 如果请求 `DateTimeInfo` 则返回它，否则返回 `null`。这两个类型作为编程便利工具实现了此接口。在尝试获取对象的字符串表示时，调用者指定格式并使用与调用线程相关的文化。由于因此，你经常调用 `ToString`，为格式参数传递字符串并为 `formatProvider` 参数传递 `null`。为了方便你调用 `ToString`，许多类型提供了 `ToString` 方法的多个重载。例如，`Decimal` 类型提供了四个不同的 `ToString` 方法：

```csharp
// 此版本调用 ToString(null, null);
// 含义：通用数值格式，线程的文化信息
public override string ToString()

// 此版本是 ToString 的实际实现所在的地方。
// 此版本实现了 IFormatt 的 ToString 方法。
// 含义：调用者指定的格式和文化信息
public string ToString(string format, IFormatProvider formatProvider);
```

## 第 14 章 字符、字符串与文本处理

```csharp
// 此版本简单地调用 ToString(format, null)。
// 含义：调用者指定的格式，线程的文化信息
public String ToString(String format);
```

```csharp
// 此版本简单地调用 ToString(null, formatProvider)。
// 此版本实现了 IConvertible 的 ToString 方法。
// 含义：通用格式，调用者指定的文化信息
public String ToString(IFormatProvider formatProvider);
```

### 将多个对象格式化为单个字符串

到为止，我已经解释了单个类型如何格式化其对象。然而，有时你想要使用许多格式化对象来构造字符串。例如，下面的字符串包含一个日期、一个姓名和一个年龄：

```csharp
String s = String.Format("{0}, {1} is {2} years old.",
new DateTime(2010, 4, 22, 14, 35, 5), "Aidan", 7);
Console.WriteLine(s);
```

如果你构建并运行此代码（且 `"en-US"` 为线程的当前文化），你将看到如下输出行：

4/22/2010 2:35:05 PM, Aidan is 7 years old.

`String` 的静态 `Format` 方法接收一个格式字符串，该字符串使用大括号中的数字来标识可替换参数。示例中使用的格式字符串告诉 `Format` 方法将 `{0}` 替换为格式字符串后的第一个参数（日期/时间），将 `{1}` 替换为格式字符串后的第二个参数（`"Aidan"`），并将 `{2}` 替换为格式字符串后的第三个参数（7）。

在内部，`Format` 方法会调用每个对象的 `ToString` 方法以获取对象的表示。当所有返回的字符串都拼接在一起后，就会返回最终的完整字符串。这完全没，但意味着所有对象都是使用它们的通用格式和调用线程的文化信息进行格式化的。

如果你在大括号内指定格式信息，那么在格式化对象时你可以拥有更多控制权。例如，下面的代码与上一个示例相同，区别在于向可替换参数 0 和 2 添加了格式信息：

```csharp
String s = String.Format("{0:D}, {1} is {2:E} years old.",
new DateTime(2010, 4, 22, 14, 35, 5), "Aidan", 7);
Console.WriteLine(s);
```
