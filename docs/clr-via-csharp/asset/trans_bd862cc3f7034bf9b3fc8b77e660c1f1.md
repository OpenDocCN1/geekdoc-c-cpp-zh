
## 燕麦云

### 智能文档处理

- 文档管理
- 协作办公
- 安全加密
- 智能搜索

C# 提供了一些特殊语法，帮助你向源代码中输入字面字符串。对于换行、回车和退格等特殊字符，C# 使用 C/C++ 开发者熟悉的转义机制。

```csharp
// String containing carriage-return and newline characters
String s = "Hi\r\nhere.";
```

![](img/3c46ff5b170881db4209d365b1f7a808_349_0.png)

> **重要** 尽管前面的示例将回车符和换行符硬编码到字符串中，但我不推荐这种做法。相反，`System.Environment` 类型定义了一个只读的 **NewLine** 属性，当你的应用程序在 Microsoft Windows 上运行时，该属性会返回由这些字符组成的字符串。然而，**NewLine** 属性对平台敏感，它会返回底层平台获得换行所需的适当字符串。因此，例如，如果公共语言基础结构（CLI）被移植到 UNIX 系统，**NewLine** 属性将返回仅由单个字符 \n 组成的字符串。下面是定义前面字符串的正确方式，使其在任何平台上都能正确工作：
>
> ```csharp
> String s = "Hi" + Environment.NewLine + "there.";
> ```

你可以使用 C# 的 + 运算符将多个字符串连接成一个字符串，如下所示：

```csharp
// Three literal strings concatenated to form a single literal string
String s = "Hi" + " " + "there.";
```

在这段代码中，因为所有字符串都是字面字符串，所以 C# 编译器会在编译时将它们连接起来，最终只在模块的元数据中放入一个字符串——“Hi there.”。对非字面字符串使用 + 运算符会导致连接在运行时执行。要在运行时将多个字符串连接在一起，应避免使用 + 运算符，因为它会在垃圾回收堆上创建多个字符串对象。相反，应使用 `System.Text.StringBuilder` 类型（本章后面我会解释）。

最后，C# 还提供了一种特殊方式来声明字符串，其中引号之间的所有字符都被视为字符串的一部分。这些特殊声明称为逐字字符串，通常用于指定文件或目录的路径，或在使用正则表达式时使用。下面是一些代码，展示了如何在使用和不使用逐字字符串字符（@）的情况下声明同一个字符串。

```csharp
// Specifying the pathname of an application
String file = "C:\\Windows\\System32\\Notepad.exe";

// Specifying the pathname of an application by using a verbatim string
String file = @"C:\Windows\System32\Notepad.exe";
```

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

接受 **CompareOptions** 参数的方法还会强制你显式传入区域性。传入 **Ordinal** 或 **OrdinalIgnoreCase** 标志时，这些 **Compare** 方法会忽略指定的区域性。

许多程序将字符串用于内部编程目的，例如路径名、文件名、URL、注册表项和值、环境变量、反射、可扩展标记语言（XML）标记、XML 属性等。通常，这些字符串不会向用户显示，只在程序内部使用。比较编程字符串时，应始终使用 **StringComparison.Ordinal** 或 **StringComparison.OrdinalIgnoreCase**。这是执行不受任何语言方式影响的比较的最快方法，因为执行比较时不会考虑区域性信息。

另一方面，当你希望以语言正确的方式比较字符串时（通常用于向最终用户显示），应使用 **StringComparison.CurrentCulture** 或 **StringComparison.CurrentCultureIgnoreCase**。

> **重要** 大多数情况下，不应使用 **StringComparison.InvariantCulture** 和 **StringComparison.InvariantCultureIgnoreCase**。尽管这些值会使比较在语言上正确，但使用它们比较编程字符串比执行序数比较耗时更长。此外，固定区域性不区分区域性，这使得在要显示给最终用户的字符串时，它是一个错误的选择。

> **重要** 如果要在执行序数比较之前更改字符串字符的大小写，应使用 **String 的 ToUpperInvariant** 或 **ToLowerInvariant** 方法。规范化字符串时，强烈建议使用 **ToUpperInvariant** 而不是 **ToLowerInvariant**，因为 Microsoft 已优化了执行大写比较的代码。事实上，FCL 在执行不区分大小写的比较之前，会在内部将字符串规范化为大写。我们使用 **ToUpperInvariant** 和 **ToLowerInvariant** 方法，因为 **String** 类不提供 **ToUpperOrdinal** 和 **ToLowerOrdinal** 方法。我们不使用 **ToUpper** 和 **ToLower** 方法，因为这些方法对区域性敏感。

有时，当你以语言正确的方式比较字符串时，你希望指定特定的区域性，而不是使用与调用线程关联的区域性。在这种情况下，可以使用前面所示的 **StartsWith**、**EndsWith** 和 **Compare** 方法的重载，它们都接受 **Boolean** 和 **CultureInfo** 参数。

> **重要** **String** 类型除了前面所示的版本外，还定义了 **Equals**、**StartsWith**、**EndsWith** 和 **Compare** 方法的几个重载。Microsoft 建议避免使用这些其他版本（本书未展示）。此外，**String** 的其他比较方法——**CompareTo**（**IComparable** 接口要求的）、**CompareOrdinal**，以及 **==** 和 **!=** 运算符——也应避免。避免这些方法和运算符的原因是，调用方没有明确指示应如何执行字符串比较，而且你无法从方法名称确定默认比较是什么。例如，默认情况下，**CompareTo** 执行区分区域性的比较，而 **Equals** 执行序数比较。如果你始终明确指示希望如何执行字符串比较，你的代码将更易于阅读和维护。

现在，让我们讨论如何执行语言正确的比较。.NET Framework 使用 **System.Globalization.CultureInfo** 类型来表示语言/国家（地区）对（如 RFC 1766 标准所述）。例如，“en-US”标识在美国书写的英语，“en-AU”标识在澳大利亚书写的英语，“de-DE”标识在德国书写的德语。在 CLR 中，每个线程都有两个与其关联的属性。这两个属性都引用一个 **CultureInfo** 对象。这两个属性是：

- **CurrentUICulture** 此属性用于获取向最终用户显示的资源。它对 GUI 或 Web Forms 应用程序最有用，因为它指示显示 UI 元素（如标签和按钮）时应使用的语言。默认情况下，创建线程时，此线程属性会被设置为一个 **CultureInfo** 对象，该对象使用 Win32 **GetUserDefaultUILanguage** 函数标识应用程序所运行 Windows 版本的语言。如果你运行的是 Windows 的多语言用户界面（MUI）版本，可以通过“区域和语言选项”控制面板设置对话框进行设置。在非 MUI 版本的 Windows 上，语言由所安装操作系统的本地化版本（或已安装的语言包）决定，且语言不可更改。
- **CurrentCulture** 此属性用于 **CurrentUICulture** 未用于的所有方面，包括数字和日期格式、字符串大小写和字符串比较。格式化时，会使用 **CultureInfo** 对象的语言和国家（地区）部分。默认情况下，创建线程时，此线程属性会被设置为一个 **CultureInfo** 对象，其值通过调用 Win32 **GetUserDefaultLCID** 方法确定，而该方法的值在“区域和语言”控制面板小程序中设置。
