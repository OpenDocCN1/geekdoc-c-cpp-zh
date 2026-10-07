
此外，内置的数值类型支持 `"C"` 表示货币，`"D"` 表示小数，`"E"` 表示指数（科学）计数法，`"F"` 表示固定点，`"G"` 表示通用，`"N"` 表示数字，`"P"` 表示百分比，`"R"` 表示往返以及 `"X"` 表示十六进制。事实上，数值类型还支持自定义格式字符串，以防简单的格式字符串无法提供你所精确的内容。自定义格式字符串包含特殊字符，可以告诉类型的 `ToString` 方法确切显示多少位数、确切在何处放置小数符。

# 第三部分 核心类型

## 354 核心类型

顺便提一下，如果你想为一个未针对任何特定文化格式化的对象获取字符串，应该调用 `System.Globalization.CultureInfo` 的静态属性 `InvariantCulture`，并将返回的对象作为 `ToString` 方法的 `formatProvider` 参数传递进去：

```c
Decimal price = 123.54;
String s = price.ToString("C", CultureInfo.InvariantCulture);
MessageBox.Show(s);
```

如果你构建并运行此代码，将出现图 14-6 所示的消息框。注意结果字符串中的第一个字符：`¤` 是货币的国际符号 (U+00A4)。

![](img/47eccf75186e2a4895549653d7520b0a_371_0.png)

图 14-6 格式化为文化中性货币的数值

通常情况下，你不会向用户显示使用不变性文化格式化的字符串。通常情况下，你只需要将此字符串保存到数据文件中，以便以后进行解析。

在 FCL（框架类库）中，有三种类型实现了 `IProvider` 接口。第一个是 `CultureInfo`，我已经解释过了。另外两个是 `NumberFormatInfo` 和 `DateTimeInfo`。当在 `NumberFormatInfo` 对象上调用 `GetFormat` 时，该方法会检查请求的类型是否为 `NumberFormatInfo`。如果是，则返回它；如果不是，则返回 null。同样，在 `DateTimeInfo` 对象上调用 `GetFormat` 时，如果请求的是 `DateTimeFormat` 则返回它，否则返回 null。这两种类型实现该接口是为了编程上的方便。在尝试获取对象的字符串表示形式时，调用者通常会指定调用线程。由于由于原因，你经常调用 `ToString`，并向其传递一个字符串作为 `format` 参数，并将 `null` 作为 `formatProvider` 参数。为了为了你调用 `ToString` 更加方便，许多类型提供了 `ToString` 方法的多个重载版本。例如，`Decimal` 类型提供了四种不同的 `ToString` 方法：

```c
// 此版本调用 ToString(null, null)。
// 意味着：通用数字格式，线程的文化信息
public override String ToString();
```

```c
// 此版本是 ToString 的实际实现所在。
// 此版本实现了 IFormattable 的 ToString 方法。
// 意味着：调用者指定的格式和文化信息
String ToString(String format, IFormatProvider formatProvider);
```

```c
// 此版本简单调用 ToString(format, null)。
// 意味着：调用者指定的格式，线程的文化信息
public String ToString(String format);
```

```c
// 此版本简单调用 ToString(null, formatProvider)。
// 此版本实现了 IConvertible 的 ToString 方法。
// 意味着：通用格式，调用者指定的文化信息
public String ToString(IFormatProvider formatProvider);
```

## 将多个对象格式化为单个字符串

到目前为止，我已经解释了单个类型如何格式化它自己的对象。然而，有时你想要构造一个包含多个格式化对象的字符串。例如，下面的字符串包含一个日期、一个人的名字和一个年龄：

```c
String s = String.Format("On {0}, {1} is {2} years old.",
new DateTime(2010, 4, 22, 14, 35, 5), "Aidan", 7);
Console.WriteLine(s);
```

如果你在 `"en-US"` 为线程当前文化的情况下构建并运行此代码，你将看到如下输出：

On 4/22/2010 2:35:05 PM, Aidan is 7 years old.

`String` 的静态方法 `Format` 接收一个格式字符串，该字符串使用括号中的数字来标识可替换参数。示例中使用的格式字符串告诉 `Format` 方法将 `{0}` 替换为格式字符串后的第一个参数（日期/时间），将 `{1}` 替换为格式字符串后的第二个参数 `"Aidan"`，并将 `{2}` 替换为格式字符串后的第三个参数。

在尝试获取对象的字符串表示形式时，调用者通常会指定调用线程。由于由于原因，你经常调用 `ToString`，并向其传递一个字符串作为 `format` 参数，并将 `null` 作为 `formatProvider` 参数。为了为了你调用 `ToString` 更加方便，许多类型提供了 `ToString` 方法的多个重载版本。例如，`Decimal` 类型提供了四种不同的 `ToString` 方法（见上文）。

*注：此处原文似乎存在重复或逻辑错乱，翻译已按原意调整。*

（由于由于原文文本在后半部分出现了严重的重复和句子断裂，以下翻译将基于原文逻辑片段进行处理）

## 将多个对象格式化为单个字符串（接）

...（由于提供的原文文本从中间部分开始出现了大量重复和错乱的句子结构，为了确保质量，此处已对原文的逻辑部分进行了最大对应翻译。）

### 358

`Append(IFormatProvider formatProvider,`

```csharp
public StringBuilder(IFormatProvider formatProvider,
String format, params Object[] args) {
```

```csharp
// 如果传递了 IFormatProvider，则检查
// 它是否提供了 ICustomFormatter 对象
ICustomFormatter cf = null;
```

```csharp
if (formatProvider != null) {
    cf = (ICustomFormatter)formatProvider.GetFormat(typeof(ICustomFormatter));
}
```

```csharp
// 继续追加字面字符（此伪代码未显示）
// 并将可替换参数替换到 StringBuilder 的字符数组。
Boolean MoreReplaceableArgumentsToAppend = true;
while (MoreReplaceableArgumentsToAppend) {
    // argObj 指的是从 format 参数中
    // 获得的可替换格式字符串
    String argFormat = "/* ...";

    // argObj 指的是来自 argsObj 数组
    // 对应的元素
    Object argObj = "/* ...";

    // argStr 指的是要追加到
    // 最终结果字符串的格式化字符串
    String argStr = null;
```

```csharp
// 如果可用自定义格式程序，让它格式化参数。
if (cf != null) {
    argStr = cf.Format(argFormat, argObj, formatProvider);
}

// 如果没有自定义格式程序或它没有格式化
// 参数，则尝试其他方法。
if (argStr == null) {
    // 参数的类型是否支持格式化？
    IFormatable throwable = argObj as IFormatable;
    if (throwable != null) {
        // 是，将格式字符串和提供程序传递给
        // 类型的 IFormatable.ToString 方法。
        argStr = throwable.ToString(argFormat, formatProvider);
    } else {
        // 否；使用线程的文化信息
        // 获取默认格式。
        if (argObj != null) argStr = argObj.ToString();
        else argStr = String.Empty;
    }
}
```

```csharp
// 将 argStr 的字符追加到字符数组字段成员中。
// "/* ...";

// 检查是否还有剩余参数需要进行格式化
MoreReplaceableArgumentsToAppend = "/* ...";
```

```csharp
return this;
```

## 第 14 章 字符、字符串与文本处理

当 `Main` 调用 `AppendFormat` 时，`AppendFormat` 会调用我的格式提供程序的 `GetFormat` 方法，并将 `ICustomFormatter` 类型传递给它。在 `BoldInt32` 中定义的 `GetFormat` 方法表示它请求了 `ICustomFormatter` 并返回自身的引用，因为它实现了该接口。如果我的 `GetFormat` 方法调用并传递了任何其他类型，我会调用与调用线程相关的 `CultureInfo` 对象的 `GetFormat` 方法。

每当 `AppendFormat` 需要格式化可替换参数时，它都会调用 `ICustomFormatter` 的 `Format` 方法。在我的示例中，`AppendFormat` 调用由 `Int32` 类型定义的 `Format` 方法。在我的方法中，我检查被格式化的对象是否通过 `IFormatable` 接口支持富格式化。如果对象不支持，我会调用继承自 `Object` 的简单无参数 `ToString` 来格式化对象。如果对象确实支持 `IFormatable`，我将调用 `ToString` 方法，并将格式字符串和格式提供程序传递给它。

现在我有了格式化后的字符串，我检查相应的对象是否为 `Int32` 类型，如果是，我将格式化后的字符串封装在 `<b>` 和 `</b>` HTML 标签中并返回新字符串。如果对象不是 `Int32`，我将直接返回格式化后的字符串而不进行任何进一步处理。

## 解析字符串以获取对象：Parse

在上一节中，我解释了如何获取一个对象并得到该对象的表示。在本节中，我将讨论相反的内容：如何获取一个字符串并获取它的对象表示。从字符串获取对象并不是非常常见的操作，但有时确实很有用。微软认为有必要规范一种机制，将字符串解析为对象。

任何可以解析字符串的类型都有一个公共静态方法 `Parse`。该方法接收一个字符串并返回该类型的实例；在某种程度上，`Parse` 充当了工厂。在 FCL（框架类）中，所有数字类型以及 `DateTime`、`TimeSpan` 以及其他类型（如 SQL 数据类型）都存在 `Parse` 方法。

让我们看看如何将字符串解析为数字。大多数数字类型（`Byte`, `SByte`, `Int16`/`UInt16`, `Int32`/`UInt32`, `Int64`/`UInt64`, `Single`, `Double` 和 `BigInteger`）至少提供一个 `Parse` 方法。这里将为您介绍由 `Int32` 类型定义的 `Parse` 方法。（其他类型的 `Parse` 方法与 `Int32` 的方法类似。）

```csharp
public static int Parse(String s, NumberStyles style,
IFormatProvider provider);
```

仅从原型，你就应该能猜出此方法是如何工作的。`String` 参数 `s` 标识要解析为 `Int32` 对象的字符串表示。`System.Globalization.NumberStyles` 参数 `style` 是一组位标志，标识 `Parse` 预期在字符串中找到的字符。`IFormatProvider` 参数 `provider` 标识 `Parse` 方法用于获取文化特定信息的对象，在本章早期已讨论过。

例如，以下代码会导致 `Parse` 抛出 `System.FormatException`，因为被解析的字符串包含前空格：

```csharp
Int32 x = Int32.Parse(" 123");
```

要允许前空格，如下修改样式参数：

```csharp
Int32 x = Int32.Parse(" 123", NumberStyles.AllowWhite);
```

这是一个显示如何解析十六进制的代码片段：

```csharp
Int32 x = Int32.Parse("A", NumberStyles.HexNumber);
Console.WriteLine(x);
```

编码允许托管接口与非 Unicode 系统创建的字符串进行交互。例如，如果你想生成一个可以被运行在日语版 Microsoft Windows 95 应用程序读取的文件，你必须使用 Shift-JIS（代码页 932）编码保存 Unicode 文本。同样，你使用 Shift-JIS 编码将在日版 Windows 95 系统上产生的文本文件读取到 CLR 中。

当你想要使用 `System.IO.BinaryWriter` 或 `System.IO.StreamWriter` 类型将字符串发送到文件或网络流时，通常会进行编码。当你使用 `System.IO.BinaryReader` 或 `System.IO.StreamReader` 类型从文件或网络流读取字符串时，通常会进行解码。如果你不显式选择编码，所有这些类型都默认使用 UTF-8（UTF 代表 Unicode 转换格式）。然而，有时你可能想显式地对字符串进行编码或解码。即使你不想这样做，本节也将让你对流与流之间读写字符串有更深入的了解。

幸运的是，FCL（框架类库）提供了一些类型来使字符编码和解码变得简单。最常用的两种编码是 UTF-16 和 UTF-8。

- UTF-16 将每个 16 位字符编码为 2 字节。它完全不影响字符，也不会发生压缩——其性能极佳。UTF-16 编码也被称为 Unicode 编码。还要注意，UTF-16 可以从小端转换为大端，反之亦然。

- UTF-8 将某些字符编码为 1 字节，某些字符编码为 2 字节，某些字符编码为 3 字节，值低于 `0x0080` 的字符被压缩为 1 字节，这对于美国使用的字符非常有效。`0x0080` 到 `0x07FF` 之间的字符转换为 2 字节，这适用于欧洲和中东语言。`0x0800` 及以上的字符转换为 3 字节，这适用于东亚语言。最后，代理对对（surrogate pairs）被写入为 4 字节。UTF-8 是一种极其流行的编码，但如果你编码许多值在 `0x0800` 或以上的字符，它的效率低于 UTF-16。

尽管 UTF-16 和 UTF-8 编码目前是最常用的，但 FCL 还支持使用频率较低的编码：

- UTF-32 将所有字符编码为 4 字节。当你想要编写一个简单的算法来遍历字符，且不想处理字节数不变化的字符时，这种编码非常有用。例如，使用 UTF-32 时你不需要考虑代理对，因为每个字符都是 4 字节。显然，UTF-32 在内存使用方面不是一种高效的编码，因此很少用于保存或向文件或网络字符串。它通常用于程序内部。还要注意，UTF-32 可以从小端转换为大端，反之亦然。

- UTF-7 编码通常用于字符可以使用 7 位值表示的旧系统。你应该避免这种编码，因为它通常会导致数据膨胀，而不是压缩数据。Unicode 联盟已废弃了它。

- ASCII 将 16 位字符编码为 ASCII 字符；也就是说，任何值小于 `0x0080` 的 16 位字符都会转换为单个字节。任何值大于 `0x07F` 的字符无法转换；对于由 ASCII 范围（`0x00` 到 `0x7F`）内的字符组成的字符串，这种编码可以将数据减半且速度非常快（因为高位直接被去除了）。如果你有 ASCII 范围之外的字符，这种编码是不适当的，因为字符的值将丢失。

最后，FCL 允许将 16 位字符编码到任意代码页。与 ASCII 编码一样，编码到代码页是危险的，因为任何无法在指定代码页中表示的字符都会丢失。除非你在处理某些已经使用其他编码的旧文件或应用程序，否则你应该始终使用 UTF-16 或 UTF-8。

当你需要编码或解码一组字符时，你应该获取一个派生自 `System.Text.Encoding` 的类实例。`Encoding` 是一个抽象类，包含几个静态属性，这些属性返回 `Encoding` 派生类的实例。

这里有一个使用 UTF-8 编码和解码字符的示例：
