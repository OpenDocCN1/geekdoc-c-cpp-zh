
String s = "Hi" + Environment.NewLine + "there.";

```
你可以使用 C# 的 `+` 算符如下将字符串连接成单个字符串：
```

```csharp
// 将三个字面量字符串连接成单个字面量字符串
String s = "Hi" + " " + "there.";
```

在此代码中，由于所有字符串都是字面量字符串，C# 编译器会在编译时将它们连接起来，并在模块元数据中放置一个字符串——"Hi there."。在非字面量字符串上使用 `+` 算符会导致连接在运行时执行。要在运行时连接字符串，请避免使用 `+` 算符，因为它会在垃圾回收堆上创建多个字符串对象。相反的，请使用 `System.Text.StringBuilder` 类型（我将在本章稍后的部分解释它）。

最后，C# 还提供了一种特殊方法来声明字符串，其中引号之间的所有字符都被视为字符串的一部分。这些特殊声明称为字面字符串（verbatim strings），通常在处理正则表达式时指定文件或目录路径时使用。以下代码显示了如何使用和不使用字面字符串（@）来声明相同的字符串。

```csharp
// 指定应用程序的路径
String file = "C:\Windows\System32\Notepad.exe";
```

```csharp
// 使用字面字符串指定应用程序的路径
String file = @"C:\Windows\System32\Notepad.exe";
```

## 第 14 章 字符、字符串与文本处理 333

你可以在程序中使用上述任何一行代码，因为它们在程序集元数据中产生相同的字符串。然而，字符串前的 `@` 符号使代码更具可读性。

### 字符串是不可变的

关于 `String` 需要知道的最重要的一点它是不可变的。也就是说，一旦创建，字符串永远不会变长、变短或更改任何字符。不可变字符串具有几个用处：首先，出于性能考虑，`String` 类型与 CLR 紧密集成。具体来说，不可变性意味着操作字符串时没有同步问题。其次，CLR 可以通过字符串池（interning，后文将讨论）共享相同的字符串内容，从而节省内存。`String` 类是密封的，这意味着你不能将其作为基类。如果你定义自己的类型，可能会破坏某些假设。

### 比较字符串

比较可能是字符串上执行的最常见操作。有两个比较字符串的原因。我们比较字符串是为了确定相等性或进行排序（通常是为了给用户）。

在确定字符串相等性或比较字符串时，强烈建议调用这些方法（由 `String` 类定义）：

```csharp
Boolean Equals(String value, StringComparison comparisonType)
static Boolean Equals(String a, String b, StringComparison comparisonType)
static Int32 Compare(String strA, String strB, StringComparison comparisonType)
static Int32 Compare(String strA, String strB, Boolean ignoreCase, CultureInfo culture, CompareOptions options)
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length, CultureInfo culture, StringComparison comparisonType)
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length, CultureInfo culture, CompareOptions options)
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length, Boolean ignoreCase, CultureInfo culture)
Boolean StartsWith(String value, StringComparison comparisonType)
static Boolean StartsWith(String value, Boolean ignoreCase)
Boolean EndsWith(String value, StringComparison comparisonType)
static Boolean EndsWith(String value, Boolean ignoreCase, CultureInfo culture)
```

在排序时，你应该始终执行大小敏感的比较。原因是如果两个仅大小大小不同的字符串被视为相等，那么它们的排序顺序可能会不同；这会困扰用户。

比较参数（上述大多数方法中的）是 `StringComparison` 枚举类型定义的值，该类型定义如下：

```csharp
public enum StringComparison {
    CurrentCulture = 0,
    CurrentCultureIgnoreCaseCase = 1,
    InvariantCultureCulture = 2,
    InvariantCultureIgnoreCaseCase = 3,
    Ordinal = 4,
    OrdinalIgnoreCaseCase = 5
}
```

`CompareOptions` 参数（上述两个方法中的）是 `CompareOptions` 枚举类型定义的值之一：

## 第 14 章 字符、字符串与文本处理 335

```csharp
[Flags]
public enum CompareOptions {
    None = 0,
    IgnoreCase = 1,
    IgnoreSpace = 2,
    IgnoreSymbols = 4,
    IgnoreKanaType = 8,
    IgnoreWidth = 0x00000010,
    Ordinal = 0x04000000,
    OrdinalIgnoreCase = 0x01000000,
    StringSort = 0x02000000
}
```

接受 `CompareOptions` 参数的方法还会强制你显式传递一个 `Culture`。当使用 `Ordinal` 或 `OrdinalIgnoreCase` 标志时，这些比较方法会忽略指定的区域。

许多程序使用字符串用于内部程序目的，例如路径名、名称、URL、键和值、环境变量、反射、可扩展标记语言 (XML) 标签、XML 属性等。通常，这些内容不会显示给用户，仅在程序内部使用。在比较字符串时，你应该始终使用 `StringComparison.Ordinal` 或 `StringComparison.OrdinalIgnoreCase`。这是执行不受任何语言影响比较的最快方法，因为在执行比较时没有考虑区域信息。

相反，当你想要以符合语言习惯正确的方式比较字符串（通常是为了显示给最终用户）时，你应该使用 `StringComparison.CurrentCulture` 或 `StringComparison.CurrentCultureIgnoreCase`。

> 在绝大多数情况下，不应使用 `StringComparison.InvariantCulture` 和 `StringComparison.InvariantCultureIgnoreCase`。虽然这些值使得比较在语言上是正确的，但使用它们来比较程序化字符串比执行序数比较耗时。此外，不变区域（invariant culture）与区域无关，这在处理你想显示给最终用户的字符串时，它是一个错误的选择。

> 如果你想在执行序数比较之前更改字符串字符的大小写，应该使用 `String` 的 `ToUpperInvariant` 或 `ToLowerInvariant` 方法。在归一化字符串时，强烈建议使用 `ToUpperInvariant` 而不是 `ToLowerInvariant`，因为微软对执行大写比较的代码进行了优化。事实上，FCL（框架类库）在内部执行大小写比较之前会对字符串进行归一化。`String` 类没有提供 `ToUpperOrdinal` 和 `ToLowerOrdinal` 方法。我们不使用 `ToUpper` 和 `ToLower` 方法，因为这些是区域敏感的。

## 第三部分 基础类型 336

有时，当你以符合语言习惯正确的方式比较字符串时，你可能指定特定的区域，而不是使用与调用线程关联的区域。在这种情况下，你可以使用之前显示的 `StartWith`、`EndsWith` 和 `Compare` 方法的重载，这些方法都接受 `Boolean` 和 `CultureInfo` 参数。

> 重要：除了之前显示的版本，`String` 定义了 `Equals`、`StartsWith` 和 `Compare` 方法的多个重载。微软建议避免这些其他版本（书中未显示）。此外，`String` 的其他方法——`CompareTo`（`IComparable` 接口要求）、`CompareOrdinal` 以及 `==` 和 `!=` 运算符也应该被避免。避免这些方法和运算符会导致调用者没有显式指示字符串比较是如何执行的，你无法确定默认比较将是什么。默认情况下，`CompareTo` 执行区域敏感的比较，而 `Equals` 执行序数比较。如果你始终指明如何执行字符串比较，你的代码将易于阅读和维护。

现在，让我们来谈如何执行符合语言习惯的比较。.NET Framework 使用 `System.Globalization.CultureInfo` 类型来表示语言/国家对（如 RFC 1766 标准所述）。例如，“en-US”标识在美国编写的英语，“en-AU”标识在澳大利亚编写的英语，“de-DE”标识在德国编写的德语。在 CLR 中，每个线程都有与其关联的两个属性。这两个属性指向 `CultureInfo` 对象：

- `CurrentUICulture`：此属性用于获取显示给最终用户的资源。它对于 GUI 或 Web Forms 非常有用，因为它指示了在显示 UI 元素作为标签和按钮时应该使用的语言。默认情况下，当你创建一个线程时，该线程属性被设置为 `CultureInfo` 对象，该对象通过 Win32 `GetDefaultUILanguage` 函数识别应用程序运行的 Windows 版本的语言。如果你运行多语言用户界面（MUI）版本的 Windows，可以通过“区域和语言选项”控制面板设置对话框进行设置。在非 MUI 版本的 Windows 上，语言由操作系统的本地化版本（或安装的语言包）决定，且语言不可更改。

- `CurrentCulture`：此属性用于所有 `CurrentUICulture` 未涵盖的场景，包括数字和日期格式化、字符串大小写以及字符串比较。在格式化时，会使用 `CultureInfo` 对象的语言和国家部分。默认情况下，当你创建一个线程时，该线程属性被设置为 `CultureInfo` 对象，其值通过调用 Win32 `GetUserLCID` 方法决定，该值在“区域和语言”控制小程序中设置。

在许多计算机上，线程的 `CurrentCulture` 和 `UICulture` 属性会被设置为同一个 `CultureInfo` 对象，这意味着它们使用相同的语言-国家信息。然而，它们可以被设置为不同。例如：在美国的一个应用程序可以使用西班牙语处理所有的项目和 UI 元素，同时显示所有针对美国的货币和日期格式。要实现这一点，线程的 `CurrentCulture` 属性应设置为用语言为“es”（西班牙语）初始化的 `CultureInfo` 对象，而 `UICulture` 属性应设置为用语言为“en-US”初始化的 `CultureInfo` 对象。

在某些少数情况下，当比较字符串的相等性或排序时，你可能需要更多的控制。这种额外的控制可以通过 `CultureInfo` 对象的 `CompareInfo` 属性访问。如前所述，`CompareInfo` 封装了区域的比较表，并且每个区域只有一个 `CompareInfo` 对象。

## 第 14 章 字符、字符串与文本处理 339

```csharp
// 为线程的文化进行字符串排序
c1 = Thread.CurrentThread.CurrentCulture;
x = String.Compare(s1, s2, c1.CompareInfo, true);
output += String.Format("{0} Compare: {1} {3} {2}",
c1.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine + Environment.NewLine;
```

下面的代码演示了如何使用 `CompareInfo.Compare` 的高级选项处理两个日语字符串。其中一个字符串代表日本高速高铁“新干”（shinkansen）的平假名（日语写作的一种子类型），另一个代表同一个单词的片假名（日语写作的另一种子类型）。

```csharp
s1 = "\u3088\u3063\u3093\u30b3\u3053\u3093"
s2 = "\u30b7\u30f3\u30f3\u30bb\u30f3"
```

```csharp
// 这里是默认比较的结果
c = new CultureInfo("ja-JP")
x = String.Compare(s1, s2, true, c1);
output += String.Format("{0} Compare: {1} {3} {2}",
c1.Name, s1, s2, symbol[x + 1]);
output += Environment.NewLine;
```

```csharp
// 这里是忽略假名类型（日语写作的一种）的比较结果
CompareInfo compareInfo = CompareInfo.GetCompareInfo("ja-JP")
x = String.Compare(s1, s2, compareInfo, CompareOptions.IgnoreKanaType);
output += String.Format("{0} Compare: {1} {3} {2}",
c1.Name, s1, s2, symbol[x + 1]);
```

```csharp
MessageBox.Show(output("Comparing Strings For Sorting:"));
```

> 注意：此文件无法保存为 ANSI 格式，否则日语字符将丢失。要在 Microsoft Visual Studio 中保存此文件，请进入“另存为”对话框，点击“保存”按钮旁边的箭头并选择“使用编码保存”。我选择了“Unicode（带 BOM 的 UTF-8）——代码页 65001”。Microsoft 的 C# 编译器可以成功解析使用此代码页的源代码。

生成用于排序的字符串的代码产生了图 14-1 所示的输出。

![](img/bd0526960dc8576a05e40e1f7f03c458_356_0.png)

图 14-1 字符串排序结果

## 第三部分 基本类型

除了 `Compare` 之外，`CompareInfo` 类提供了 `IndexOf`、`LastIndexOf`、`IsPrefix` 和 `IsSuffix` 方法。由于这些方法都提供了接受 `CompareOptions` 枚举作为参数的重载，它们提供了比 `String` 类定义的 `Compare`、`IndexOf`、`LastIndexOf`、`StartsWith` 和 `EndsWith` 方法更多的控制权。此外，你应该意识到 FCL（框架类库）包含了 `System.StringComparer` 类，你也可以用它执行比较。当你需要对许多不同的字符串重复执行相同的比较时，该类非常有用。

### 字符串池（String Interning）

正如我在上一节提到的，检查字符串相等性是许多应用程序的常用操作——这项任务可能会严重损害性能。在执行顺序检查（ordinal check）时，CLR 会快速测试两个字符串是否具有相同数量的字符。如果不是，字符串绝对不相等；如果是，则字符串可能相等，此时 CLR 必须比较每个单独字符以确定。在执行文化感知比较（culturally aware comparison）时，CLR 必须始终比较所有单独字符，因为不同长度的字符串可能被认为相等。

此外，如果你在内存中存在多个重复的相同字符串实例，你就会浪费内存，因为字符串是不可变的。如果内存中只有一个字符串实例，且所有需要引用该字符串的变量都指向该对象，你使用内存将将高效得多。

如果你的应用程序频繁使用区分大小的顺序比较来检查字符串相等性，或者你预计会有许多具有相同值的字符串对象，那么利用 CLR 的字符串池机制可以大幅提高性能。当 CLR 初始化时，它会创建一个内部哈希表，其中键是字符串，值是对托管堆中 String 对象的引用。初始时，该表是空的。`String` 类提供了两个方法允许你访问此内部哈希表：

```csharp
public static String Intern(String str);
public static bool IsInterned(String str);
```
