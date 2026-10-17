
`this, SLOT(updateWindowTitle());`

```cpp

textBrowser->setSearchPaths(QStringList() << path << "::/images");

textBrowser->setSource(page);

```

我们设置了 `Qt::WA_GroupLeader` 属性，是因为我们希望除了主窗口之外，还能从模态对话框弹出 `HelpBrowser`。对话框通常会阻止用户与应用程序中的任何其他窗口交互。然而，请求帮助后，显然必须允许用户同时与模态对话框和帮助浏览器交互。设置 `Qt::WA_GroupLeader` 属性使得这种交互成为可能。

我们提供了两个搜索路径：文件系统中包含应用程序文档的第一个路径，以及图像资源位置的第二个路径。HTML 可以以正常方式引用文件系统中的图像，并使用以 `:/` 头的路径引用图像资源。`page` 参数是文档文件名，并带有一个可选的 HTML 锚点。

```cpp

void HelpBrowser::updateWindowTitle()

{

  setWindowTitle(tr("Help: %1").arg(textBrowser->documentTitle()));

}

```

每当源页面发生变化时，就会调用 `updateWindowTitle()` 槽。`documentTitle()` 函数返回页面 `<title>` 标签中指定的文本。

```cpp

void HelpBrowser::showPage(const QString &page)

{

  QString path = directoryOf("doc").absolutePath();

  HelpBrowser *browser = new HelpBrowser(path, page);

  browser->resize(500, 400);

  browser->show();

}

```

在 `showPage()` 静态函数中，我们创建 `HelpBrowser` 窗口然后显示它。当用户关闭它时，它会被销毁，我们在 `HelpBrowser` 构造函数设置了 `Qt::WA_DeleteClose` 属性。在本示例中，我们假设文档位于应用程序的 `doc` 目录下。传递给 `showPage()` 函数的所有页面将从该子目录获取。

现在我们准备好从应用程序调用帮助浏览器了。在应用程序的主窗口中，我们将创建一个帮助动作并将其连接到 `help()` 槽，该槽可能如下：

```cpp

void MainWindow::help()

{

    HelpBrowser::showPage("index.html");

}

```

这假设主文件是 `index.html`。对于对话框，我们将帮助按钮连接到一个 `help()` 槽，该槽可能如下：

```cpp

void EntryDialog::help()

{

    HelpBrowser::showPage("forms.html#editing");

}

```

这里我们查看另一个帮助文件 `forms.html` 并滚动到 `editing` 锚点。

也可以使用 Qt 资源系统将帮助文件及其关联图像直接嵌入可执行文件中。实现此点的唯一更改是对应用程序的 `.qrc` 文件添加条目，并使用资源路径 `::doc/forms.html#editing`。

在本示例中，我们使用了两种方法：嵌入图标，因为应用程序本身也会使用，并将 HTML 文件留在文件系统中。

## 使用 Qt Assistant 提供强大的帮助

`Qt Assistant` 是提供的在线帮助。它的主要优点是支持索引和全文搜索，并且可以处理多个应用程序的文档集。为了使用 `Qt Assistant`，我们必须在应用程序中包含必要的代码，并让 `Qt Assistant` 感知我们的文档。

* `Qt 4.4` 预计将推出全新的帮助系统，这将更容易集成我们的文档

`Qt` 应用程序与 `Qt Assistant` 之间的通信由 `AssistantClient` 类处理，该类位于单独的库中。将此库与应用程序链接，我们必须在应用程序的 `.pro` 文件中添加此行：

```
CONFIG += assistant
```

我们现在查看使用 `Qt Assistant` 的新 `HelpBrowser` 类代码：

```cpp

class HelpBrowser

{

public:

    static void showPage(const QString &page);

private:

    static QDir directoryOf(const QString &subdir);

    static AssistantClient *assistant;

};

```

这是新的 `showPage()` 实现：

```cpp

QAssistantClient *HelpBrowser::assistant = 0;

void HelpBrowser::showPage(const QString &page)

{

    QString path = directoryOf("doc").absoluteFilePath(page);

    if (!assistant)

        assistant = new AssistantClient("");

    assistant->showPage(path);

}

```

`QAssistantClient` 构造函数接受路径字符串作为第一个参数，它用此定位 `Qt Assistant` 可执行文件。通过传递一个空字符串，我们定

`QAssistantClient` 会在 `PATH` 变量中查找可执行文件。`QAssistantClient` 有一个 `showPage()` 函数，它可以接受一个带有可选 HTML 锚点的页面名称。

下一步是为文档准备目录和索引。这是通过创建一个 `Qt Assistant` 配置文件并编写一个提供文档信息的 `.dcf` 文件来实现的。所有这些内容在 `Qt Assistant` 的在线文档中都有解释，我们不会在这里重复这些信息。

使用 浏览器、`QTextBrowser` 或 `Qt Assistant` 的替代方案是使用平台特定的方法提供在线帮助。对于 Windows 应用程序，可能希望创建 Windows HTML Help 文件并使用 Microsoft Internet Explorer 访问它们。你可以使用 Qt 的 `QProcess` 类或 ActiveQt 框架来实现。在 Mac OS X 上，Apple Help 提供了与 `Qt Assistant` 的功能。

我们现在到了第二部分的结束。第三部分的后续章节将介绍 `Qt` 更高级、更专门的功能。它们所提供的 C++ 和 `Qt` 代码并没有我们在第二部分提供的代码那么复杂，但在那些对你来说全新的领域，某些概念和想法可能更有挑战性。

# 第三部分：高级 Qt

## 18. 国际化

![](img/5a524abdf0b0d58fa99d30abb4463611_664_0.png)

- 使用 Unicode 工作
- 使应用程序具备翻译感知
- 动态语言切换
- 翻译应用程序

除了用于英语和许多欧洲语言的拉丁字母外，`Qt 4` 还提供了对世界上其他文字系统的广泛支持：

- `Qt` 在整个 API 和内部都使用 Unicode。无论我们为用户界面使用什么语言，应用程序都可以平等地支持所有用户。
- `Qt` 的文本引擎可以处理所有主要的非拉丁文字系统，包括阿拉伯语、中文、西里尔语、希伯来语、日语、韩语、泰语和印度语言。
- `Qt` 的布局引擎支持阿拉伯语和希伯来语等语言从右到左布局。
- 某些语言需要特殊的输入方法来输入文本。`QLineEdit` 和 `QText` 等编辑器小部件与用户系统中安装的任何输入方法配合得很好。

通常，允许用户以原生语言输入文本是不够的，整个用户界面也必须翻译。`Qt` 让这变得简单：只需将所有用户可见的字符串封装在 `tr()` 函数中，正如我们在前面的章节中所做的那样，并使用 `Qt` 的工具准备所需语言的翻译文件。`Qt` 提供了一个名为 `Linguist` 的 GUI 工具供翻译人员使用。`Qt Linguist` 由两个命令行程序 `update` 和 `lrelease` 补充，这些程序通常由应用程序开发者运行。

对于大多数应用程序，翻译文件在启动时根据用户的本地设置加载。但在少数，用户需要在运行时切换语言。这在 `Qt` 中是完全可能的，尽管这需要额外的工作。得亏 `Qt` 的布局系统，当翻译后的文本比原始文本长时，各种用户界面组件将自动调整以为翻译文本留空间。

### 使用 Unicode

`Unicode` 是一种字符编码标准，支持世界上大多数文字系统。`Unicode` 的原始想法是，使用 16 位存储字符而不是 8 位，就可以编码大约 65000 个字符而不是只有 256 个。* `Unicode` 将 `ASCII` 和 `ISO 8859-1` `Latin-1` 作为子集包含在相同的代码位置上。例如，字符 `'A'` 在 `ASCII` 和 `Latin-1` 中的值为 `0x41`，而字符 `'Ñ'` 在 `Latin-1` 和 `Unicode` 中的值均为 `0xD1`。

> * 这些字符可以使用由两个 16 位值组成的序列称为“代理对”`surrogate pairs` 来表示。

大于 65535 的 `Unicode` 标准字符值的数值版本。这些字符可以使用由两个 16 位值组成的序列称为“代理对”来表示。

`Qt` 的 `QString` 类将字符串存储为 `Unicode`。`QString` 中的每个字符都是 16 位的而不是 8 位的。这里是设置字符串第一个字符为 `'A'` 的两种方法：

```
str[0] = 'A';
str[0] = QChar(0x41);
```

如果源文件编码为 `Latin-1`，则指定 `Latin-1` 字符同样简单：

```
str[0] = 'Ñ';
```

如果源文件有另一种编码，数值值也可以正常工作：

```
str[0] = QChar(0xD1);
```

我们可以通过数值值指定任何 `Unicode` 字符。例如，这里是指定希腊大写字母 sigma `Σ` 和欧元货币符号 `€` 的方法：

```
str[0] = QChar(0x03A3);
str[0] = QChar(0x20AC);
```

`Unicode` 支持的所有字符的数值值列在 http://www.unicode.org/standard/。如果你很少需要非 `Latin-1` 的 `Unicode`，查找字符就足够；但 `Qt` 提供了更方便的方法在 `Qt` 程序中输入 `Unicode` 字符串，正如我们在本节稍后将看到的。

`Qt 4` 的文本引擎在所有平台上支持以下文字系统：阿拉伯语、中文、西里尔语、希伯来语、日语、韩语、老挝、拉丁、泰语和越南语。它还支持所有不需要特殊处理的 `Unicode 4.1` 脚本。此外，在带有 `Fontconfig` 的 X11 和最近版本的 Windows 上还支持以下文字系统：孟加拉语、天城语文、古吉拉特语、旁遮普语、卡纳达达语、高棉语、马拉雅姆语、叙利亚语、泰米尔语、泰卢固语、Thaana 迪维语 和西藏语。最后，X11 支持 Ori，Windows XP 支持蒙古语和辛罗拉语。假设系统中安装了正确的字体，`Qt` 可以使用这些文字系统中的任何一种。假设安装了正确的输入方法，用户将能够在其 `Qt` 应用程序中使用这些文字系统输入文本。

使用 `QChar` 编程与使用 `char` 编程略有不同。要获取 `QChar` 的数值，调用 `unicode()`。要获取 `QChar` 的 `ASCII` 或 `Latin-1` 值，作为 `char`，调用 `toLatin1()`。对于非 `Latin-1` 字符，`toLatin1()` 返回 `\0`。

如果我们知道程序中的所有字符串都是 `ASCII`，可以使用标准的 `<cctype>` 函数进行猜测，例如对 `toLatin1()` 的返回值使用 `isalpha()`、`isdigit()` 和 `isspace()`。然而，通常使用 `QChar` 的成员函数来执行这些操作更好，因为它们适用于任何 `Unicode` 字符。`QChar` 提供的函数 `isPrint()`、`isPunct()`、`isSpace()`、`isMark()`、`isLetter()`、`isNumber()`、`isLetterNumber()`、`isdigit()`、`isSymbol()`、`isLower()` 和 `isUpper()`。例如，这里是测试字符是否为数字或大写字母的一种方法：

```
if (ch.isdigit() || ch.isUpper())
...
```

该代码段适用于任何区分大写和小写的字母表，包括拉丁语、希腊语和西里尔语。

一旦我们有了 `Unicode` 字符串，我们可以在 `Qt` API 中任何期望 `QString` 的地方使用它。这时 `Qt` 的职责是正确显示它，并在与操作系统通信时将其转换为相关的编码。

在读写文本文件时需要特别小心。文本文件可以使用多种编码，通常无法从其内容判断文件编码。默认情况下，`QTextStream` 读写都使用系统的本地 8 位编码，通过 `QTextCodec::codeForLocale()` 获取。对于美国和西方本地化地区，这通常意味着 `Latin-1`。

如果我们设计了自己的文件格式并希望能够读取和写入任意字符，可以将数据保存为 `Unicode`，调用：
`stream.setCodec("UTF-16");`
`stream.generateByteMark(true);`

在写入 `QText` 之前数据将以 `UTF-16` 保存，这是一种每个字符需要两个字节的格式，并带有一个 16 位的值 字节标记，标识文件为 `Unicode` 以及是小端序还是大端序。`UTF-16` 格式与 `QString` 的内存表示相同，因此读取和写入 `Unicode` 字符串可以非常快。另一方面，在 `UTF-16` 中保存 `ASCII` 没有固有的开销，因为它每个字符存储两个字节而不是一个。

可以通过在 `QTextCodec` 上调用 `codec()` 指定其他编码。`Codec` 是在 `Unicode` 和编码之间转换的对象。它们在内部用于支持字体、输入方法、剪贴板、拖放和文件名。但在我们使用 `Qt` 时也可用。

读取文本文件时，如果文件以字节标记开头，`QTextStream` 会检测 `UTF-16`。这种行为可以通过调用 `autoDetectUnicode(false)` 关闭。如果数据是 `UTF-16` 但不能假设它以字节标记开头，最好在读取之前调用 `codec("UTF-16")`。

另一种支持 `Unicode` 世界编码是 `UTF-8`。它相对于 `UTF-16` 的主要优势是它是 `ASCII` 的超集。`0x00` 到 `0x7F` 范围内的任何字符都表示为单字节。其他字符 `0x7F` 以上的 `Latin-1` 字符 由多字节序列表示。对于大部分是 `ASCII` 的文本，`UTF-8` 占据的空间是 `UTF-16` 的一半。要在 `QTextStream` 中使用 `UTF-8`，在读写之前将 `"UTF-8"` 设置为编码名称。

如果我们希望无视用户的本地化设置进行读写，可以在 `QTextStream` 上设置 `ISO 8859-1` 编码。例如：

```
QTextStream in(&file);
setCodec("ISO-8859-1");
```

某些格式在其头部中指定其编码。头部通常是 `ASCII`，以确保无论使用什么编码都能被正确读取。

它是 `ASCII` 的超集。`XML` 格式是这种情况下的一个有趣例子。`XML` 文件通常被编码为 `UTF-8` 或 `UTF-16`。读取它们的正确方法是调用 `setCodec()` 并传入 `"UTF-8"`。如果格式是 `UTF-16`，`QStream` 将自动检测并进行调整。`XML` 文件的 `<?xml?>` 头部有时会包含一个编码参数，例如：

```xml

<xml version="1.0" encoding="EUC-KR"?>

```

由于 `QStream` 在启动后不允许您更改编码，因此尊重显式编码的正确方法是重新读取文件，使用 `QTextCodec::codecForName()`。在 `XML` 的情况下，我们可以通过使用第 16 节中描述的 `Qt` 类来避免自己处理编码。

`QTextCodec` 的另一个用途是指定源代码中出现的字符串的编码。让我们考虑例如，一个由日本程序员组成的团队，他们正在编写一个针对日本本土市场的应用程序。这些程序员很可能会在使用 `EUC-JP` 或 `Shift-JIS` 等编码的文本编辑器中编写源代码。此类编辑器允许他们无缝地输入日语字符，从而编写出如下代码：

```cpp

QPushButton *button = new QPushButton(tr("ボタン"));

```

默认情况下，`Qt` 将 `tr()` 的参数解释为 `Latin-1`。要更改此设置，请调用静态函数 `QTextCodec::codecForTr()`。例如：

```cpp

QTextCodec::codecForTr(QTextCodec::codecForName("EUC-JP"));

```

这必须在第一次调用 `tr()` 之前完成。通常，我们会在 `main()` 中在创建 `QCoreApplication` 或 `QApplication` 对象后立即执行。

程序中指定的其他字符串仍然是 `Latin-1` 字符串。如果程序员还想在这些字符串中输入日语字符，可以使用 `QTextCodec` 将它们显式转换为 `Unicode`：

```cpp

QString text = japaneseCodec->toUnicode("日本語語理");

```

或者，他们可以通过调用 `QTextCodec::setCodecForCStrings()` 让 `Qt` 在 `const char *` 和 `QString` 之间转换时使用特定的编码：

```cpp

QCodec::codecForCStrings(QCodec::codecName("EUC-JP"));
```
