
> **重要** 尽管前面的示例将回车符和换行符硬编码到字符串中，但我不推荐这种做法。相反，System.Environment 类型定义了一个只读的 NewLine 属性，当你的应用程序在 Windows 上运行时，该属性返回由这些字符组成的字符串。然而，NewLine 属性对平台敏感，它返回底层平台获得换行所需的相应字符串。因此，例如，如果公共语言基础设施 (CLI) 被移植到 UNIX 系统，NewLine 属性将返回仅由单个字符 `\n` 组成的字符串。以下是在任何平台上都能正确工作的前述字符串的恰当定义方式。

```csharp
String s = "Hi" + Environment.NewLine + "there.";
```

你可以使用 C# 的 + 运算符将多个字符串连接成一个字符串，如下所示。

```csharp
// Three literal strings concatenated to form a single literal string
String s = "Hi" + " " + "there.";
```

在这段代码中，因为所有字符串都是字面字符串，所以 C# 编译器会在编译时连接它们，最终只在模块的元数据中放置一个字符串——“Hi there.”。对非字面字符串使用 + 运算符会导致在运行时执行连接。若要在运行时将多个字符串连接在一起，应避免使用 + 运算符，因为它会在垃圾回收堆上创建多个字符串对象。相反，应使用 System.Text.StringBuilder 类型（我将在本章后面解释）。

最后，C# 还提供了一种特殊的字符串声明方式，其中引号之间的所有字符都被视为字符串的一部分。这些特殊声明称为逐字字符串，通常用于指定文件或目录的路径，或在使用正则表达式时使用。下面是一些代码，展示如何分别使用和不使用逐字字符串字符 (@) 来声明同一个字符串。

```csharp
// Specifying the pathname of an application
String file = "C:\\Windows\\System32\\Notepad.exe";

// Specifying the pathname of an application by using a verbatim string
String file = @"C:\Windows\System32\Notepad.exe";
```

你可以在程序中使用前面任意一行代码，因为它们在程序集的元数据中生成相同的字符串。不过，第二行字符串前面的 @ 符号告诉编译器该字符串是逐字字符串。实际上，这告诉编译器将反斜杠字符视为反斜杠字符而不是转义字符，从而使路径在源代码中更易读。

现在你已经了解了如何构造字符串，接下来让我们讨论一些可以对 String 对象执行的操作。

```csharp
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length,
    StringComparison comparisonType)
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length,
    CultureInfo culture, CompareOptions options)
static Int32 Compare(String strA, Int32 indexA, String strB, Int32 indexB, Int32 length,
    Boolean ignoreCase, CultureInfo culture)

Boolean StartsWith(String value, StringComparison comparisonType)
Boolean StartsWith(String value,
    Boolean ignoreCase, CultureInfo culture)

Boolean EndsWith(String value, StringComparison comparisonType)
Boolean EndsWith(String value, Boolean ignoreCase, CultureInfo culture)
```

排序时，应始终执行区分大小写的比较。原因是，如果仅大小写不同的两个字符串被视为相等，那么每次排序时它们的顺序可能不同；这会让用户感到困惑。

comparisonType 参数（在前面的多数方法中）是 StringComparison 枚举类型定义的值之一，该枚举定义如下。

```csharp
public enum StringComparison {
    CurrentCulture = 0,
    CurrentCultureIgnoreCase = 1,
    InvariantCulture = 2,
    InvariantCultureIgnoreCase = 3,
    Ordinal = 4,
    OrdinalIgnoreCase = 5
}
```

options 参数（在前面的两个方法中）是 CompareOptions 枚举类型定义的值之一。

```csharp
[Flags]
public enum CompareOptions {
    None = 0,
    IgnoreCase = 1,
    IgnoreNonSpace = 2,
    IgnoreSymbols = 4,
    IgnoreKanaType = 8,
    IgnoreWidth = 0x00000010,
    Ordinal = 0x40000000,
    OrdinalIgnoreCase = 0x10000000,
    StringSort = 0x20000000
}
```

接受 CompareOptions 参数的方法还会强制你显式传入区域性。当传入 Ordinal 或 OrdinalIgnoreCase 标志时，这些 Compare 方法会忽略指定的区域性。

许多程序将字符串用于内部编程目的，例如路径名、文件名、URL、注册表项和值、环境变量、反射、可扩展标记语言 (XML) 标记、XML 属性等。通常，这些字符串不会显示给用户，仅在程序内部使用。在比较程序化字符串时，应始终使用

现在，让我们讨论如何执行语言学上正确的比较。.NET Framework 使用 `System.Globalization.CultureInfo` 类型来表示语言/国家对（如 RFC 1766 标准所述）。例如，“en-US” 标识在美国书写的英语，“en-AU” 标识在澳大利亚书写的英语，“de-DE” 标识在德国书写的德语。在 CLR 中，每个线程都有两个与之关联的属性。这两个属性都引用一个 CultureInfo 对象。这两个属性是：

- **CurrentUICulture** 此属性用于获取显示给最终用户的资源。它对 GUI 或 Web Forms 应用程序最有用，因为它指示显示 UI 元素（如标签和按钮）时应使用的语言。默认情况下，创建线程时，此线程属性被设置为一个 CultureInfo 对象，该对象使用 Win32 GetUserDefaultUILanguage 函数标识应用程序所运行 Windows 版本的语言。如果你运行的是 Windows 的多语言用户界面 (MUI) 版本，可以通过“区域和语言选项”控制面板设置对话框进行设置。在非 MUI 版本的 Windows 上，语言由所安装操作系统的本地化版本（或已安装的语言包）决定，并且语言不可更改。

- **CurrentCulture** 此属性用于 CurrentUICulture 未用于的所有情况，包括数字和日期格式设置、字符串大小写转换和字符串比较。格式设置时，会使用 CultureInfo 对象的语言和国家/地区两部分。默认情况下，创建线程时，此线程属性被设置为一个 CultureInfo 对象，其值通过调用 Win32 GetUserDefaultLCID 方法确定，而该方法的值在“区域和语言”控制面板小程序中设置。

对于上述两个线程属性，当新线程使用 AppDomain 默认值创建时，可以通过设置 CultureInfo 的静态 DefaultThreadCurrentCulture 和 DefaultThreadCurrentUICulture 属性来覆盖系统使用的默认值。

在许多计算机上，线程的 CurrentUICulture 和 CurrentCulture 属性会被设置为同一个 CultureInfo 对象，这意味着它们使用相同的语言/国家/地区信息。不过，它们可以设置为不同的值。例如：在美国运行的应用程序可以对其所有菜单项和其他 GUI 元素使用西班牙语，同时正确显示美国的货币和日期格式。为此，线程的 CurrentUICulture 属性应设置为使用语言“es”（西班牙语）初始化的 CultureInfo 对象，而线程的 CurrentCulture 属性应设置为使用语言/国家对“en-US”初始化的 CultureInfo 对象。

在内部，CultureInfo 对象有一个字段引用 System.Globalization.CompareInfo 对象，该对象封装了由 Unicode 标准定义的该区域性的字符排序表信息。下面的代码演示了执行序数比较与区分区域性的字符串比较之间的差异。

```csharp
using System;
using System.Globalization;

public static class Program {
    public static void Main() {
```
