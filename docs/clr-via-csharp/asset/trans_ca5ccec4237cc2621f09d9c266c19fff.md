
## 特定格式和文化

无参数的 **ToString** 方法有两个问题。第一，调用方无法控制字符串的格式。例如，应用程序可能希望将数字格式化为货币字符串、十进制字符串、百分比字符串或十六进制字符串。第二，调用方无法轻松选择使用特定区域性来格式化字符串。对于服务器端应用程序代码而言，第二个问题比客户端代码更麻烦。在极少数情况下，应用程序需要使用与调用线程关联的区域性不同的区域性来格式化字符串。为了更好地控制字符串格式，你需要一个 **ToString** 方法版本，它允许你指定精确的格式和区域性信息。

为调用方提供格式和区域性选择的类型实现 **System.IFormattable** 接口：

```csharp
public interface IFormattable {
    String ToString(String format, IFormatProvider formatProvider);
}
```

在 FCL 中，所有基类型（**Byte**、**SByte**、**Int16/UInt16**、**Int32/UInt32**、**Int64/UInt64**、**Single**、**Double**、**Decimal** 和 **DateTime**）都实现此接口。此外，一些其他类型（如 **Guid**）也实现它。最后，每个枚举类型定义都会自动实现 **IFormattable** 接口，以便可以从枚举类型的实例获取有意义的字符串符号。

**IFormattable** 的 **ToString** 方法接受两个参数。第一个参数 **format** 是一个字符串，告诉方法应如何格式化对象。**ToString** 的第二个参数 **formatProvider** 是实现 **System.IFormatProvider** 接口的类型的实例。此类型向 **ToString** 方法提供特定的区域性信息。我很快就会讨论如何提供。

实现 **IFormattable** 接口的 **ToString** 方法的类型决定它将识别哪些格式字符串。如果传入该类型无法识别的格式字符串，该类型应抛出 **System.FormatException**。

Microsoft 在 FCL 中定义的许多类型都识别若干格式。例如，**DateTime** 类型支持“d”表示短日期，“D”表示长日期，“g”表示常规，“M”表示月/日，“s”表示可排序，“T”表示长时间，“u”表示 ISO 8601 格式的通用时间，“U”表示完整日期格式的通用时间，“Y”表示年/月，等等。所有枚举类型都支持“G”表示常规，“F”表示标志，“D”表示十进制，“X”表示十六进制。我将在第 15 章“枚举类型和位标志”中更详细地介绍枚举类型的格式化。

此外，所有内置数值类型都支持“C”表示货币，“D”表示十进制，“E”表示指数（科学）记数法，“F”表示定点，“G”表示常规，“N”表示数字，“P”表示百分比，“R”表示往返，“X”表示十六进制。事实上，数值类型还支持图片格式字符串，以防简单格式字符串无法完全满足你的需求。图片格式字符串包含特殊字符，这些字符告诉类型的 **ToString** 方法确切显示多少位数字、确切在何处放置小数分隔符、确切在小数分隔符后放置多少位数字，等等。有关格式字符串的完整信息，请参阅 .NET Framework SDK 中的“格式化类型”。

对于大多数类型，调用 **ToString** 并为格式字符串传递 **null** 与调用 **ToString** 并为格式字符串传递“G”完全相同。换句话说，对象默认使用“常规格式”格式化自身。实现类型时，请选择你认为最常用的格式；此格式就是“常规格式”。顺便说一句，不接受参数的 **ToString** 方法假定调用方想要“常规格式”。

现在格式字符串已经讲完，让我们转向区域性信息。默认情况下，字符串使用与调用线程关联的区域性信息进行格式化。无参数的 **ToString** 方法当然会这样做，如果你为 **formatProvider** 参数传递 **null**，**IFormattable 的 ToString** 也会这样做。

区域性敏感信息适用于格式化数字（包括货币、整数、浮点数、百分比、日期和时间）时。**Guid** 类型有一个 **ToString** 方法，它只返回表示其值的字符串。生成 **Guid 的**字符串时无需考虑区域性，因为 GUID 仅用于编程目的。

格式化数字时，**ToString** 方法会查看你为 **formatProvider** 参数传递的内容。如果传递了 **null**，**ToString** 会通过读取 **System.Threading.Thread.CurrentThread.CurrentCulture** 属性来确定与调用线程关联的区域性。此属性返回 **System.Globalization.CultureInfo** 类型的实例。

使用此对象，**ToString** 会读取其 **NumberFormat** 或 **DateTimeFormat** 属性，具体取决于正在格式化的是数字还是日期/时间。这些属性分别返回 **System.Globalization.NumberFormatInfo** 或 **System.Globalization.DateTimeFormatInfo** 的实例。**NumberFormatInfo** 类型定义了一组属性，例如 **CurrencyDecimalSeparator**、**CurrencySymbol**、**NegativeSign**、**NumberGroupSeparator** 和 **PercentSymbol**。同样，**DateTimeFormatInfo** 类型定义了各种属性，例如 **Calendar**、**DateSeparator**、**DayNames**、**LongDatePattern**、**ShortTimePattern** 和 **TimeSeparator**。**ToString** 在构造和格式化字符串时会读取这些属性。

调用 **IFormattable 的 ToString** 方法时，你可以传递一个类型实现 **IFormatProvider** 接口的对象的引用，而不是传递 **null**：

```csharp
public interface IFormatProvider {
    Object GetFormat(Type formatType);
}
```

下面是 **`IFormatProvider`** 接口背后的基本思想：当某个类型实现此接口时，它表示该类型的实例能够提供区域性特定的格式信息，并且应忽略与调用线程关联的区域性信息。

**`System.Globalization.CultureInfo`** 类型是 FCL 中定义的极少数实现 **`IFormatProvider`** 接口的类型之一。例如，如果你想为越南格式化字符串，你会构造一个 **`CultureInfo`** 对象，并将该对象作为 **`ToString`** 的 **`formatProvider`** 参数传入。以下代码获取一个 **`Decimal`** 数值的字符串表示形式，并将其格式化为适合越南的货币：

```csharp
Decimal price = 123.54M;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);
```

如果生成并运行此代码，将出现图 14-5 所示的消息框。

![](img/3c46ff5b170881db4209d365b1f7a808_370_0.png)

**图 14-5** 数字值已正确格式化以表示越南货币

在内部，**`Decimal`** 的 **`ToString`** 方法会看到 **`formatProvider`** 参数不是 **`null`**，并按如下方式调用该对象的 **`GetFormat`** 方法：

```csharp
NumberFormatInfo nfi = (NumberFormatInfo)
    formatProvider.GetFormat(typeof(NumberFormatInfo));
```

这就是 **`ToString`** 从（**`CultureInfo`**）对象请求适当数字格式信息的方式。数字类型（如 **`Decimal`**）只请求数字格式信息。但其他类型（如 **`DateTime`**）可以像这样调用 **`GetFormat`**：

```csharp
DateTimeFormatInfo dtfi = (DateTimeFormatInfo)
    formatProvider.GetFormat(typeof(DateTimeFormatInfo));
```

实际上，由于 **`GetFormat`** 的参数可以标识任何类型，该方法足够灵活，允许请求任何类型的格式信息。**`.NET Framework`** 中的类型调用 **`GetFormat`** 时只请求数字或日期/时间信息；将来可能会请求其他类型的格式信息。

