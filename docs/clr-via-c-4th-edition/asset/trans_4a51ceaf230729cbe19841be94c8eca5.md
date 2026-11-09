
这个 Parse 方法接受三个参数。为了方便，许多类型都提供了 Parse 的其他重载，这样就不必传入那么多参数。例如，Int32 提供了四个 Parse 方法的重载。

```csharp
// Passes NumberStyles.Integer for style
// and thread's culture's provider information.
public static Int32 Parse(String s);

// Passes thread's culture's provider information.
public static Int32 Parse(String s, NumberStyles style);

// Passes NumberStyles.Integer for the style parameter.
public static Int32 Parse(String s, IFormatProvider provider);

// This is the method I've been talking about in this section.
public static Int32 Parse(String s, NumberStyles style,
    IFormatProvider provider);
```

DateTime 类型也提供了一个 Parse 方法。

```csharp
public static DateTime Parse(String s,
    IFormatProvider provider, DateTimeStyles styles);
```

这个方法的工作方式与数字类型上定义的 Parse 方法相同，区别在于 DateTime 的 Parse 方法接受由 System.Globalization.DateTimeStyles 枚举类型定义的一组位标志，而不是 NumberStyles 枚举类型。有关这些位标志以及 DateTimeStyles 类型定义的常用组合的完整说明，请参阅 .NET Framework SDK 文档。

为了方便，DateTime 类型提供了三个 Parse 方法的重载。

```csharp
// Passes thread's culture's provider information
// and DateTimeStyles.None for the style
public static DateTime Parse(String s);

// Passes DateTimeStyles.None for the style
public static DateTime Parse(String s, IFormatProvider provider);

// This is the method I've been talking about in this section.
public static DateTime Parse(String s,
    IFormatProvider provider, DateTimeStyles styles);
```

解析日期和时间很复杂。许多开发者发现 DateTime 类型的 Parse 方法过于宽松，因为它有时会解析不包含日期或时间的字符串。因此，DateTime 类型还提供了一个 ParseExact 方法，该方法接受一个图片格式字符串，用于准确指示日期/时间字符串应采用的格式以及应如何解析它。有关图片格式字符串的更多信息，请参阅 .NET Framework SDK 中的 DateTimeFormatInfo 类。

> **注意** 一些开发者向 Microsoft 报告了以下情况：当他们的应用程序频繁调用 Parse，并且 Parse 反复抛出异常（由于无效的用户输入）时，应用程序的性能会受到影响。针对这些对性能敏感的 Parse 用法，Microsoft 为所有数值数据类型、DateTime、DateTimeOffset、TimeSpan 甚至 IPAddress 添加了 TryParse 方法。下面是 Int32 的两个 TryParse 方法重载之一的样子。
>
> ```csharp
> public static Boolean TryParse(String s, NumberStyles style,
>     IFormatProvider provider, out Int32 result);
> ```
>
> 如你所见，此方法返回 true 或 false，指示指定的字符串能否被解析为 Int32。如果该方法返回 true，则通过引用传递给 result 参数的变量将包含解析后的数值。TryXxx 模式将在第 20 章“异常与状态管理”中讨论。

## 编码：在字符和字节之间转换

在 Win32 中，程序员常常不得不编写代码，将 Unicode 字符和字符串转换为多字节字符集（MBCS）字符和字符串。我确实编写过不少这类代码，编写起来非常繁琐，使用起来也容易出错。在 CLR 中，所有字符都表示为 16 位 Unicode 代码值，所有字符串都由 16 位 Unicode 代码值组成。这使得在运行时处理字符和字符串变得容易。

然而，有时你可能希望将字符串保存到文件或通过网络传输。如果字符串主要由英语使用者可读的字符组成，那么保存或传输一组 16 位值的效率并不高，因为写入的字节中有一半会包含零。相反，更高效的做法是将这些 16 位值编码为压缩的字节数组，然后再将字节数组解码回 16 位值数组。

编码还允许托管应用程序与非 Unicode 系统创建的字符串进行交互。例如，如果你希望生成一个可由运行日文版 Windows 95 的应用程序读取的文件，就必须使用 Shift-JIS（代码页 932）编码来保存 Unicode 文本。同样，你会使用 Shift-JIS 编码将日文 Windows 95 系统上生成的文本文件读入 CLR。

当你希望使用 System.IO.BinaryWriter 或 System.IO.StreamWriter 类型将字符串发送到文件或网络流时，通常需要进行编码。当你希望使用 System.IO.BinaryReader 或 System.IO.StreamReader 类型从文件或网络流读取字符串时，通常需要进行解码。如果你没有显式选择编码，所有这些类型都默认使用 UTF-8。（UTF 代表 Unicode Transformation Format。）然而，有时你可能希望显式编码或解码字符串。即使你不想显式这样做，本节也会让你更深入地了解如何从流中读取字符串以及向流中写入字符串。

幸运的是，FCL 提供了一些类型，使字符编码和解码变得容易。最常用的两种编码是 UTF-16 和 UTF-8：

- UTF-16 将每个 16 位字符编码为 2 个字节。它完全不影响字符，也不会发生压缩——其性能极佳。UTF-16 编码也称为 Unicode 编码。另请注意，UTF-16 可用于从小端序转换为大端序，反之亦然。

- UTF-8 将某些字符编码为 1 个字节，某些字符编码为 2 个字节，某些字符编码为 3 个字节，还有一些字符编码为 4 个字节。值低于 0x0080 的字符被压缩为 1 个字节，这对于美国使用的字符非常有效。介于 0x0080 和 0x07FF 之间的字符被转换为 2 个字节，这对于欧洲和中东语言非常有效。值为 0x0800 及以上的字符被转换为 3 个字节，这对于东亚语言非常有效。最后，代理项对会写出为 4 个字节。UTF-8 是一种极其流行的编码，但如果你要编码大量值为 0x0800 或以上的字符，它的效率不如 UTF-16。

尽管 UTF-16 和 UTF-8 编码是迄今为止最常见的，但 FCL 还支持一些使用频率较低的编码：

- UTF-32 将所有字符编码为 4 个字节。当你想要编写一个简单的算法来遍历字符，并且不希望处理字符占用可变字节数时，这种编码很有用。例如，使用 UTF-32 时，你无需考虑代理项，因为每个字符都是 4 个字节。显然，就内存使用而言，UTF-32 不是一种高效的编码，因此很少用于将字符串保存到文件或网络或进行传输。这种编码通常在程序内部使用。另请注意，UTF-32 可用于从小端序转换为大端序，反之亦然。

- UTF-7 编码通常用于处理可用 7 位值表示的字符的较旧系统。你应避免使用这种编码，因为它通常最终会扩展数据而不是压缩数据。Unicode Consortium 已弃用此编码。

- ASCII 将 16 位字符编码为 ASCII 字符；也就是说，任何值小于 0x0080 的 16 位字符都被转换为单个字节。任何值大于 0x007F 的字符都无法转换，因此该字符的值会丢失。对于由 ASCII 范围内的字符（0x00 到 0x7F）组成的字符串，这种编码会将数据压缩一半，并且速度非常快（因为高字节被直接截断）。如果你有超出 ASCII 范围的字符，这种编码就不合适，因为这些字符的值会丢失。

最后，FCL 还允许你将 16 位字符编码到任意代码页。与 ASCII 编码一样，编码到代码页是有风险的，因为任何无法在指定代码页中表示的字符都会丢失。除非你必须处理已经使用其他编码之一的某些旧文件或应用程序，否则应始终使用 UTF-16 或 UTF-8 编码。

