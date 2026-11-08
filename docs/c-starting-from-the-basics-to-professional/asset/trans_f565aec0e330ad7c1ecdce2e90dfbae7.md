
-   对于 n 等于 8、16 或 32 的情况，你可以定义 `std::uNstring` 对象来存储 UTF-n 编码的字符串，使用类型为 `char_n_t` 的字符（每个字符至少 n 位，但通常恰好 n 位）。

`<string>` 模块定义了所有这些类型。

> **注意**  `<string>` 模块定义的所有五种字符串类型实际上只是同一个类模板 `std::basic_string<CharType>` 特定实例化的类型别名。例如，`std::string` 是 `std::basic_string<char>` 的别名，而 `std::wstring` 是 `std::basic_string<wchar_t>` 的简写。这就解释了为什么所有字符串类型都提供完全相同的一组函数。在第 17 章学习如何创建自己的类模板之后，你会更好地理解这是如何工作的。

## wchar_t 字符组成的字符串

`<string>` 模块中定义的 `std::wstring` 类型存储由 `wchar_t` 类型字符组成的字符串。使用 `wstring` 类型对象的方式与使用 `string` 类型对象的方式基本相同。你可以用下面这条语句定义一个宽字符串对象：

```cpp
std::wstring quote;
```

包含 `wchar_t` 类型字符的字符串字面量写在双引号之间，但要在前面加上 `L`，以便与包含 `char` 字符的字符串字面量区分开。因此，你可以像这样定义并初始化一个 `wstring` 变量：

```cpp
std::wstring saying {L"The tigers of wrath are wiser than the horses of instruction."};
```

开头双引号前的 `L` 指定该字面量由 `wchar_t` 类型字符组成。如果没有它，你就会得到一个 `char` 字符串字面量，而这条语句将无法编译。

要输出宽字符串，你需要使用 `wcout` 流。下面是一个例子：

```cpp
std::wcout << saying << std::endl;
```

我们在字符串对象上下文中讨论过的几乎所有函数也同样适用于 `wstring` 对象，因此这里不再逐一赘述。其他功能，例如 `to_wstring()` 函数，只是多接受一个用于指定数值类型的参数。在使用 `wstring` 对象时，你必须记得为字符串字面量和字符字面量指定 `L` 前缀，这样就没问题了！

`wstring` 类型的一个问题在于，宽字符串字面量所使用的字符编码，以及接受宽字符字符串的函数所期望的字符编码，是由实现定义的，因此可能因编译器而异。Windows 操作系统的原生 API 通常期望使用 UTF-16 编码的字符串。因此，在为 Windows 编译时，`wchar_t` 字符串通常也会由 2 字节的 UTF-16 编码字符组成。然而，大多数其他实现使用 4 字节的 UTF-32 编码 `wchar_t` 字符。如果你需要支持可移植的多国字符集，那么使用 `u8string`、`u16string` 或 `u32string` 类型可能更好，这些类型将在下一节中介绍。

## 包含 Unicode 字符串的对象

`<string>` 模块还定义了另外三种类型来存储 Unicode 字符组成的字符串。`std::u8string`（C++20 中新增）/ `u16string` / `u32string` 类型的对象分别存储由 `char8_t` / `char16_t` / `char32_t` 类型字符组成的字符串。它们旨在分别包含使用 UTF-8、UTF-16 和 UTF-32 编码的字符序列。与现有对象一样，你可以使用相应类型的字面量来初始化这些类型的对象。下面是一个例子：

```cpp
std::u8string quote {u8"Character is the real foundation of success."}; // char8_t characters
std::u16string question {u"Whither atrophy?"};                    // char16_t characters
std::u32string question {U"This sentence contains three errors."}; // char32_t characters
```

这些语句表明，包含 `char8_t` 字符的字符串字面量要加 `u8` 前缀，包含 `char16_t` 字符的字面量要加 `u` 前缀，而包含 `char32_t` 字符的字面量要加 `U` 前缀。`u8string`、`u16string` 和 `u32string` 类型的对象具有与 `string` 类型相同的一组函数。

原则上，你也可以使用本章中详细介绍过的 `std::string` 类型来存储 UTF-8 字符组成的字符串。事实上，在 C++20 之前，这是存储 UTF-8 字符串的唯一方式，因为 `char8_t` 和 `std::u8string` 类型直到 C++20 才被引入。问题在于，你无法轻松区分使用 UTF-8 编码的字符串和使用实现定义的原始字符编码（通常是 UTF-8，但当然并不总是如此）编码的字符串。

> **提示**  理想情况下，你应始终将 UTF-n 编码的字符串存储在 `std::u8string` 对象中，而将 `std::string` 和 `std::wstring` 留给不需要可移植性的情况，和/或用于与操作系统原生 API 交互。不幸的是，`std::string` 长期以来一直被用于存储 UTF-8 编码的字符串，因此在与尚未升级为使用 `std::u8string` / `char8_t` 的旧式 API 对接时，你可能不得不采取务实做法。

然而，请务必注意，所有字符串类型都完全不了解 Unicode 编码。例如，UTF-8 编码使用一到四个字节来编码单个字符，但操作字符串对象的函数并不会识别这一点。这意味着，例如，如果字符串包含任何需要两到三个字节来表示的字符，`length()` 函数将返回错误的长度，如下面的代码片段所示：

```cpp
std::u8string s {u8"字符串"}; // UTF-8 encoding of the Chinese word for "string"
std::cout << s.length();       // length: 9 code units, and not 3 Chinese characters!
```

> **提示**  在撰写本书时，标准库对操作 Unicode 字符串的支持仍然有限，在某些实现中更是如此。首先，没有 `std::tcout` 或 `std::to_wstring()`，标准正则表达式库也不支持 `uNstrings`。此外，在 C++17 中，标准库提供的用于在各种 Unicode 编码之间进行转换的大多数功能都已被弃用。因此，如果生成和操作可移植的 Unicode 编码文本对你的应用程序很重要，那么使用第三方库会好得多。可行的候选包括 ICU 和 Boost.Locale 库，或 Qt 的 `QString`。

## 原始字符串字面量

如你所知，常规字符串字面量不得包含换行符或制表符。要包含这些特殊字符，必须对它们进行转义——换行符和制表符分别变成 `\n` 和 `\t`。出于显而易见的原因，双引号字符也必须转义为 `\"`。由于这些转义序列的存在，反斜杠字符本身也需要转义为 `\\`。

然而，有时你会发现自己必须定义包含一些甚至许多此类特殊字符的字符串字面量。不得不持续转义这些字符不仅繁琐，而且还会使这些字面量难以阅读。下面是一些例子：

```cpp
auto path{ "C:\\ProgramData\\MyCompany\\MySoftware\\MyFile.ext" };
auto escape{ u8"The \"\\\" escape sequence is a backslash character, \\." };
auto text{ L"First line.\nSecond line.\nThird line.\nThe end." };
std::regex reg{ "\\*+" };  // Regular expression that matches one or more * characters
```

最后一个示例是正则表达式的一个例子——正则表达式是一种定义搜索和转换文本过程的字符串。本质上，正则表达式定义了要在字符串中匹配的模式，而找到的模式可以被替换或重新排序。C++ 通过 `<regex>` 模块支持正则表达式，不过对此的讨论超出了本书的范围。这里的主要要点是，正则表达式字符串经常包含反斜杠字符。不得不为每个反斜杠字符使用转义序列，可能会使正则表达式特别难以正确指定，并且非常难以阅读。

原始字符串字面量正是为解决这些问题而引入的。原始字符串字面量可以包含任何字符，包括反斜杠、制表符、双引号和换行符，因此不需要转义序列。原始字符串字面量在前缀中包含一个 `R`，除此之外，该字面量的字符序列还被圆括号包围。因此，原始字符串字面量的基本形式是 `R"(...)"`。圆括号本身不属于该字面量。你见过的任何类型的字面量都可以通过像之前一样在 `R` 前添加相同的前缀——`L`、`u`、`U` 或 `u8`——来指定为原始字面量。使用原始字符串字面量后，我们之前的示例就变成了下面这样：

```cpp
auto path{ R"(C:\ProgramData\MyCompany\MySoftware\MyFile.ext)" };
auto escape{ u8R"(The "\" escape sequence is a backslash character, \.)" };
auto text
{ LR"(First line.
Second line.
Third line.
The end.)" };
std::regex reg{ R"(\*+)" };  // Regular expression that matches one or more * characters
```

在原始字符串字面量内部，不需要进行任何转义。这意味着你可以直接复制粘贴，例如，将 Windows 路径序列粘贴到其中，甚至可以将一整部莎士比亚戏剧连同引号字符和换行符一起粘贴进去。在后一种情况下，你应注意前导空白和所有换行符，因为它们也会连同周围的 `R"( )"` 定界符之间的所有其他字符一起被包含到字符串字面量中。

请注意，甚至双引号也不需要——甚至不能——被转义，这就引出了一个问题：如果你的字符串字面量本身在某处包含序列 `)"` 会怎样？也就是说，如果它包含一个 `)` 字符，后面跟着一个 `"` 会怎样？下面就是这样一个有问题的字面量：

```cpp
R"(The answer is "(a - b)" not "(b - a)")"  // Error!
```
