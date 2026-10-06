
虽然只需查找字符就足够了，但 Qt 提供了在 Qt 程序中输入 Unicode 字符串的方便方法，我们将在本节稍后的部分介绍。

Qt 4 的文本引擎在所有平台上都支持以下文字系统：阿拉伯语、中文、西里字母、希伯来语、日语、韩语、老挝语、拉丁语语和越南语。它还支持所有不需要特殊处理的 Unicode 4.1 脚本。此外，带有 Fontconfig 的 X11 以及最近版本的 Windows 还支持以下文字系统：孟加拉语、天城文、古吉拉语、旁遮加语、高棉语、马拉雅拉语、叙利亚语、泰米尔语、塔纳语（尔维希语）和藏语。最后，X11 支持奥里亚语，Windows XP 支持蒙古语和僧哈尔语。假设系统上安装了正确的字体，Qt 可以使用这些文字系统的任何一种渲染文本。假设了正确的输入法，用户可以在 Qt 应用程序中输入这些文字系统的文本。

使用 `QChar` 编程与使用 `char` 编程略有不同。要获取 `QChar` 的值，调用 `unicode()`。要获取 `QChar` 的 ASCII 或 Latin-1 值（作为 `char`），调用 `toLatin1()`。对于非 Latin-1 字符，`toLatin1()` 返回 `'\0'`。

如果我们知道程序中的所有字符串都是 ASCII，我们可以使用标准的 `<cctype>` 函数对 `toLatin1()` 的返回值进行判断，例如 `isalpha()`、`isdigit()` 和 `isspace()`。然而，通常情况下，使用 `QChar` 的成员函数来执行这些操作更好，因为它们适用于任何 Unicode 字符。`QChar` 提供的函数有 `isPrint()`、`isPunct()`、`isSpace()`、`isMark()`、`isLetter()`、`isNumber()`、`isLetterOrNumber()`、`isDigit()`、`isSymbol()`、`isLower()` 和 `isUpper()`。例如，这里有一种测试测试字符是否为数字或大写字母的方法：

```
if (ch.isdigit() || ch.isUpper())
...
```

这是针对每个区分大小写字母的字母表（包括拉丁字母、希腊字母和西里字母）的代码段。

一旦我们有了 Unicode 字符串，就可以在 Qt API 中任何期望 `QString` 的地方使用它。然后，由 Qt 负责正确显示它，并在与操作系统通信时转换为相关的编码。

在读写文件时需要特别小心。文本文件可以使用多种编码，通常无法从其内容推测文本文件的编码。默认情况下，`QTextStream` 在读取和写入时都使用系统的本地 8 位编码（通过 `QText::encodeForLocale()` 获取）。对于美国和西方区域，这通常意味着 Latin-1。

如果我们设计了自己的文件格式，并希望能够读写任意的 Unicode 字符，我们可以通过以下代码将数据保存为 Unicode：
```
stream.setCodec("UTF-16");
stream.setGenerateByteMark(true);
```
在写入 `QTextStream` 之前。数据将保存为 UTF-16 格式，该格式每个字符需要两个字节，并以一个 16 位的值（Unicode 字节序标记，0xFFFF）开头，用于标识该文件是否为 Unicode 格式以及字节是大小端还是大端序。UTF-16 格式与 `QString` 的内存表示相同，因此在 UTF-16 中读写 Unicode 字符串可以非常快。另一方面，在 UTF-16 格式中保存 ASCII 没有固有的开销，因为它每个字符存储两个字节而不是一个字节。

可以通过调用 `QTextCodec` 上的 `codec()` 指定其他编码。Codec 是一个在 Unicode 和编码之间转换的对象。它在多种上下文中使用 `QTextCodec`。在内部，它们被用于支持字体、输入法、剪贴板、拖放和文件名。但当我们使用 Qt 应用程序时，也可以使用它们。

在读取文本文件时，如果文件以字节序标记开头，`QTextStream` 会自动检测 UTF-16。这种行为可以通过调用 `autoDetectUnicode(false)` 关闭。如果数据是 UTF-16 但不能假设它以字节序标记开头，最好在读取之前调用 `codec("UTF-16")`。

另一种支持 Unicode 世界的编码是 UTF-8。它相比 UTF-16 的主要优势是它是 ASCII 的超集。0x00 到 0x7F 范围内的任何字符都表示为单字节。其他字符（0x7F 以上的 Latin-1 字符）由多字节序列表示。对于大部分是 ASCII 的文本，UTF-8 消耗的空间大约是 UTF-16 的一半。要在 `QTextStream` 中使用 UTF-8，在读写之前设置 `codec("UTF-8")` 为编码名称。

如果我们希望忽略用户的本地区域进行读写，可以在 `QTextStream` 上设置 ISO 8859-1 编码。例如：

```
QTextStream in(&file);
setCodec("ISO 8859-1");
```

某些格式在其头部中指定其编码。头部通常是 ASCII，以确保无论使用什么编码（只要是 ASCII 的超集）都能正确读取。XML 文件格式是一个有趣的例子。XML 文件通常被编码为 UTF-8 或 UTF-16。读取它们的正确方法是调用 `setCodec("UTF-8")`。如果格式是 UTF-16，`QStream` 将自动检测并进行调整。XML 文件的 `<?xml?>` 头部包含一个编码参数，例如：

```
<xml version="1.0" encoding="EUC-KR">
```

由于 `QStream` 不允许在启动后更改编码，遵循显式编码的正确方法是重新开始读取文件，使用正确的 `QTextCodec`（通过 `QTextCodec::codecForName()` 获取）。在 XML 的情况下，我们可以使用第 16 章描述的 Qt 类来避免自己处理编码。

`QTextCodec` 的另一个用途是指定源代码中字符串的编码。例如，考虑一个由日本程序员组成的团队，他们正在编写一个针对日本市场的应用程序。这些程序员可能在使用 EUC-JP 或 Shift-JIS 等编码的文本编辑器中编写源代码。这种编辑器允许他们无缝地输入日语字符，以便他们编写如下代码：

```
QPushButton *button = new QPushButton(tr("日本語"));
```

默认情况下，Qt 将 `tr()` 的参数解释为 Latin-1。要更改这一点，调用 `QTextCodec::codecForTr()` 静态函数。例如：

```
QTextCodec::codecForTr(QTextCodec::codecForName("EUC-KR"));
```

这必须在第一次调用 `tr()` 之前完成。通常，我们会在 `main()` 中这样做，在创建 `QCoreApplication` 或 `QApplication` 对象之后立即。上述技术可以应用于任何非 Latin-1 语言，包括中文、韩语和俄语。

或者，如果他们想在这些字符串中输入日语，可以使用 `QTextCodec` 将其显式转换为 Unicode：

```
QString text = japaneseCodec->toUnicode("日本語");
```

程序中指定的其他字符串仍将被解释为 Latin-1，除非调用：

```
QCodec::codecForCStrings("EUC-JP");
```

以下是 Qt 4.3 支持的编码列表：

- Apple Roman
- Big5
- Big5-HKSCS
- EUC-JP
- EUC-KR
- GB18030-0
- IBM 850
- IBM 866
- IBM 874
- ISO 2022-JP
- ISO 8859-1
- ISO 8859-2
- ISO 8859-3
- ISO 8859-4
- ISO 8859-5
- ISO 8859-6
- ISO 8859-7
- ISO 8859-8
- ISO 8859-9
- ISO 8859-10
- ISO 8859-13
- ISO 8859-14
- ISO 8859-15
- ISO 8859-16
- Ascii-Bng
- Ascii-Dev
- Ascii-Gjr
- Ascii-Knd
- Ascii-MLM
- Ascii-Ori
- Ascii-Pnj
- Ascii-Tlg
- Ascii-Tml
- JIS X 0201
- JIS X 0208
- KOI8-R
- KOI8-U
- MuleLao-1
- ROMAN8
- Shift-JIS
- TIS-620
- TSCII
- UTF-8
- UTF-16
- UTF-16BE
- UTF-16LE
- Windows-1250
- Windows-1251
- Windows-1252
- Windows-1253
- Windows-1254
- Windows-1255
- Windows-1256
- Windows-1257
- Windows-1258
- WINSAMI2

可以通过子类 `QTextCodec` 来支持其他编码。
