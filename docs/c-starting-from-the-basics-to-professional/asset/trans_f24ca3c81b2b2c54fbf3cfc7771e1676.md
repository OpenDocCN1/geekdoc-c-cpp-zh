
这会产生以下输出：

```
ch is 'E' which is code 0x45
```

我们使用参数索引 (0) 将同一个字符值格式化两次——一次使用默认格式，另一次使用小写十六进制格式 (x) 的替代形式 (#)。

当使用 >> 从流读入 char 类型的变量时，第一个非空白字符将被存储。这意味着不能用这种方式读取空白字符；它们会被直接忽略。此外，不能将数值读入 char 类型的变量；如果尝试这样做，存储的将是第一个数字的字符编码。

## 使用 Unicode 字符

对于使用拉丁字符的国家语言字符集，ASCII 通常足够。然而，如果要同时处理多种语言的字符，或者要处理许多非英语语言的字符集，256 个字符编码远远不够，而 Unicode 就是答案。可以参考第 1 章了解 Unicode 和字符编码的介绍。

类型 wchar_t 是一种基本类型，用于单个字符无法放入一个字节的字符集。因此得名：wchar_t 源自 wide character（宽字符），因为字符比通常的一字节字符“更宽”。相比之下，类型 char 被称为“窄”字符，因为可用字符编码的范围有限。

定义宽字符字面量的方式与 char 类型的字面量类似，但需要加上前缀 L。例如：

```
wchar_t z {L'Z'};
```

这将 z 定义为 wchar_t 类型，并将其初始化为 Z 的宽字符表示。

键盘上可能没有用于表示其他国家语言字符的按键，但仍可以使用十六进制表示法创建它们。例如：

```
wchar_t cc {L'\x00E7'}; // Initialized with the wide-character encoding of cedilla (ç)
```

单引号之间的值是一个转义序列，指定字符编码的十六进制表示。反斜杠表示转义序列的开始，反斜杠后的 x 或 X 表示编码为十六进制（另见第 1 章）。

wchar_t 类型的问题在于其大小高度依赖具体实现，编译器用于宽字符字面量的编码也是如此。二者通常对应目标平台首选的宽字符编码。因此在 Windows 上，wchar_t 通常为 16 位宽，宽字符字面量使用 UTF-16 编码；在大多数其他平台上，wchar_t 为 32 位宽，宽字符字面量使用 UTF-32 编码。虽然这使 wchar_t 非常适合与原生 Unicode API 交互，但它不适合编写可跨不同平台移植的代码。

因此，除非要与基于 wchar_t 的 API 交互，否则建议改用 char8_t、char16_t 或 char32_t 类型。这些类型的值分别用于存储以 UTF-8、UTF-16 或 UTF-32 编码的字符，并且它们在所有常见平台上的大小相同（我们相信你能猜到这些大小……）。以下是这三种类型的一些示例变量：

```
char8_t yen {u8'\x00A5'};  // Initialized with UTF-8 code for the yen sign (¥)
char16_t delta {u'\x0394'}; // Initialized with UTF-16 code for Greek Delta (Δ)
char32_t ya {U'\x044F'};    // Initialized with UTF-32 code for cyrillic letter ya (я)
```

字面量的前缀 u8、u 和 U 分别表示它们是 UTF-8、UTF-16 和 UTF-32。如果你的编辑器和编译器能够处理 Unicode 字符，并且你知道如何在键盘上输入这些字母，也可以不使用转义序列来定义 Unicode 字符变量（见第 1 章）：

```
wchar_t cc {L'ç'};
char8_t yen {u8'¥'};
char16_t delta {u'Δ'};
char32_t ya {U'я'};
```

由于 UTF-8 和 UTF-16 是可变宽度编码，并非所有字母都能用单个字符表示。例如，希腊字母 Δ 在 UTF-8 中需要两个字节的序列来编码。

```
char8_t delta8 {u8'Δ'};  /* Error: Δ (code point U+0394) encoded as 2 UTF-8 code units */
```

> **注意**  `char8_t` 类型是在 C++20 中引入的。因此，大多数旧代码和库仍将使用 `char` 来表示 UTF-8 编码的字母。这有时会令人困惑，因为同一类型也用于存储窄字符（通常为 ASCII 编码）字母。因此，新代码应尽可能转向使用 `char8_t`。

标准库提供了标准输入和输出流 `wcin` 和 `wcout`，用于读写 `wchar_t` 类型的字符，但库中没有提供处理 `char8_t`、`char16_t` 或 `char32_t` 字符数据的功能。我们将在第 7 章讨论字符串时简要回到处理 Unicode 字符的话题。

## auto 关键字

使用 `auto` 关键字表示编译器应推导变量的类型。以下是一些示例：

```
auto m {10};                 // m has type int
auto n {200uL};              // n has type unsigned long
auto p {std::numbers::pi};   // p has type double
```

编译器将根据你提供的初始值推导 m、n 和 p 的类型。也可以对 `auto` 的初始值使用函数式或赋值表示法：

```
auto m = 10;                 // m has type int
auto n = 200uL;              // n has type unsigned long
auto p(std::numbers::pi);    // p has type double
```

话虽如此，这并不是 `auto` 关键字真正预期的用法。定义基本类型的变量时，通常不妨显式指定类型。你将在本书后面再次见到 `auto` 关键字，在那里它会被更恰当、更有用地应用。

> **警告** 将花括号初始化器与 auto 关键字一起使用时需要小心。例如，假设你这样写（注意等号）：

```
auto m = {10};             // m has type std::initializer_list<int>
```

那么为 m 推导出的类型将不是 int，而是 std::initializer_list<int>。提供一些背景：这与在花括号之间使用元素列表时得到的类型相同：

```
auto list = {1, 2, 3};     // list has type std::initializer_list<int>
```

你稍后会看到，此类列表通常用于指定容器（如 std::vector）的初始值。从 C++17 起，这是你需要注意的唯一一个小怪癖。但是，如果使用较旧的编译器，在许多情况下可能会推导出意料之外的类型来代替 auto。以下是概览：

```
/* C++11 and C++14 */
auto i {10};                 // i has type std::initializer_list<int> !!!
auto pi = {3.14159};         // pi has type std::initializer_list<double>
auto list1{1, 2, 3};          // list1 has type std::initializer_list<int>
auto list2 = {4, 5, 6};       // list2 has type std::initializer_list<int>
```

```
/* C++17 and later */
auto i {10};                 // i has type int
auto pi = {3.14159};         // pi has type std::initializer_list<double>
auto list1{1, 2, 3};          // error: does not compile!
auto list2 = {4, 5, 6};       // list2 has type std::initializer_list<int>
```

总结一下，如果你的编译器正确支持 C++17，只要不将其与赋值结合，就可以使用花括号初始化以单个值初始化任何变量。但是，如果你的编译器尚未完全更新，就应完全不要将花括号初始化器与 auto 一起使用。相反，要么显式声明类型，要么使用赋值或函数式表示法。

## 小结

在本章中，我们介绍了 C++ 中计算的基础知识。你了解了该语言提供的大多数基本数据类型。到目前为止讨论的要点如下：

- 任何类型的常量都称为字面量。所有字面量都有类型。
- 可以将整数字面量定义为十进制、十六进制、八进制或二进制值。
- 浮点字面量必须包含小数点或指数，或两者兼有。如果两者都没有，则指定的是整数。
- 存储整数的基本类型是 short、int、long 和 long long。它们存储有符号整数，但也可以在这些类型名中的任意一个前面使用类型修饰符 unsigned，以生成占用相同字节数但存储无符号整数的类型。
