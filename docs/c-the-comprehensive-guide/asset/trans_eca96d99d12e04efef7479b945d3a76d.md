
使用 `#ifndef`，你指示预处理器：如果预处理器变量 `MY_MACROS_HPP` 不存在，就包含下面的代码块；如果存在，则忽略它。`#ifndef` 代表 *如果未定义*。预处理器的世界与 C++ 的世界大不相同。它并不真正关心 C++ 标识符。如果你在那里使用了像 `vector` 或 `std` 这样的名称（这是个坏主意），预处理器此时还不会认识它们。只有此前已经让预处理器知道的内容，例如通过 `#define` 定义的内容，才在这里有意义。

`MY_MACROS_HPP` 并没有被定义：`#ifndef MY_MACROS_HPP` 为真。这会使预处理器处理直到相应 `#endif` 或 `#else` 为止的所有文本。

接下来又是一条标准库的 `#include`，然后检查预处理器是否识别 `OUTPUT_TO_STANDARD`。在 `#ifdef`、`#else` 和 `#endif` 之间有两个备选分支，预处理器会选择其中一个，而完全忽略另一个——就好像那些行是空的一样。因为我特意用 `#define` 定义了 `OUTPUT_TO_STANDARD`，所以 `#ifdef` 为真，第一个备选分支 `#define OUT std::cout` 被保留下来。

请注意，我实际上是在与 `#ifdef OUTPUT_TO_STANDARD` 检查不同的文件中设置 `#define OUTPUT_TO_STANDARD` 的。然而，合并各个文件正是预处理器的目的。因此，这两处出现来自不同文件并无影响。预处理器会把所有内容合并成一个连续的流。

`#define OUT std::cout` 向预处理器引入了新名称 `OUT`。这一次，它不只是单纯引入一个名称，而是用 `std::cout` 作为替换文本，这正是我们想要的。从现在起，预处理器会把每次出现的标记 `OUT` 替换为 `std::cout`。预处理器具有与 C++ 类似的分词规则，因此 `SHOUT` 自然不会变成 `SHstd::cout`——但 `std::OUT` 却会变成 `std::std::cout`。预处理器不识别作用域解析运算符 `::`。

接下来是两条简单的 C++ 定义，它们会被包含进输出流中。`container_type` 现在可作为类型别名使用，而 `SIZE` 是一个数值常量。

从被包含的头文件中，还保留下一行相关代码：

```cpp
#define MESSAGE(text) { (OUT) << text << "\n"; }
```

这同样引入了一个预处理器标识符。从现在起，每次出现的 `MESSAGE` 都会被替换为 `{ (OUT) << text << "\n"; }`。不过，预处理器期望调用 `MESSAGE` 时带一个参数，它把这个参数称为 `text`。作为参数提供的文本会完全不变地插入到 `{ (OUT) << text << "\n"; }` 中，与你在调用中指定的完全一致。

回到 macros.cpp 中，这意味着下面这一行

```cpp
MESSAGE("the container has " << data.size() << " elements.");
```

将变成下面这样：

```cpp
{ (std::cout) << "the container has " << data.size() << " elements." << "\n"; }
```

当预处理器完成工作后，会得到一个单一的数据流。随后，这个数据流用于实际的 C++ 编译。除标准库的包含内容外，预处理器之后、C++ 编译器之前的结果如清单 21.3 所示。

```cpp
// https://godbolt.org/z/W4SG5TjTjz
// ...here content of <vector>...
// ...here content of <iostream>...
using container_type = std::vector<int>;
static constexpr unsigned SIZE = 10;
int main() {
    { std::cout << "Program start" << "\n"; }
    container_type data(SIZE);
    { std::cout << "The container has " << data.size() << " elements. " << "\n"; }
    { std::cout << "End of program" << "\n"; }
    { std::cout << "That was a close call.\n"; }
}
```

**清单 21.3** 预处理器运行的结果。

在这个阶段之后，预处理器指令已不复存在。预处理器变量也完全被其等价内容替换。有几个有趣的点值得注意：

- 预处理器的文本替换是精确发生的。它会保留每个分号、圆括号和括号不变，并且不会引入任何新的分号、圆括号或括号。这一点在 `MESSAGE` 中尤其明显：结果中存在块花括号 `{...}` 和分号。`text` 也可以包含由 `<<` 分隔的多个输出元素，C++ 编译器之后可以正确地解释它们。
- `container_type` 和 `SIZE` 不是预处理器标识符。

## 使用“constexpr if”处理编译时代码依赖

在 C++17 中，新增的一项功能使编译器能够从程序中丢弃某个 if 分支。这样一来，在代码变体之间切换时所需的预处理器语法更少，并且可以在 C++ 内部完成。

```cpp
// https://godbolt.org/z/8j9j9KoWx
#include <iostream> // cout, cerr
constexpr int OUTPUT_VARIANT = 0; // Switch between cerr and cout

void message(const char* text) {
    if constexpr(OUTPUT_VARIANT == 1)
        std::cerr << text << "\n";
    else
        std::cout << text << "\n";
}
int main() {
    message("Message");
}
```

**清单 21.4** 使用“constexpr if”，无需预处理器即可在变体之间切换。

在这里，编译器在翻译时决定将两个 if 分支中的哪一个包含到代码中。

## 21.2 当心缺失的括号

特别重要的是，预处理器不会引入或删除括号，而只执行文本替换，尤其是在替换表达式中使用宏参数时。

```cpp
#define SQUARE(x) x*x
int result = SQUARE(3+4)
```

会求值为 19，正如你在这里看到的。然而，SQUARE(3+4) 很可能应该是 7*7，即 49。这非常危险：

```cpp
int result = 3+4*3+4
```

通常，你应当*始终*在替换文本中用括号把每一次参数使用括起来。而且，整个替换文本也常常需要用括号括起来。

```cpp
#define SQUARE(x) ((x)*(x))
int result = SQUARE(3+4)
```

就会变成你想要的结果，因为下面的计算得到 49：

```cpp
int result = ((3+4)*(3+4))
```

像清单 21.1 中的文本这样的例外情况只会印证这条规则。在那里，宏定义中省略括号使得你可以在调用宏时在参数中串联多个流操作 `<<`。

## 21.3 特性宏

在本书中，我偶尔会提到某个特性仅从 C++17、C++20 或 C++23 起才可用。有时，我也会提到某些编译器尚不支持某个特性。从 C++20 起，有一种官方方式可以检查编译器或标准库是否支持某个特性。然后，你可以用 `#if` 或 `#ifdef` 对此类条件作出响应。这些特性宏随后会被定义，并具有类似 201707L 的数值：

```cpp
#if __cpp_generic_lambdas >= 201707L
    // Here you can use generic lambdas with template parameters.
#else
    // Here you have to do without them.
#endif

#ifdef __cpp_lib_as_const
    // Here there is std::as_const(coll).
#else
    // Here not.
#endif
```

目前，编译器对应的列表包含 67 个宏，而标准库的列表包含 214 个宏。

## 21.4 关于源代码的信息

有时，为了分析目的，了解当前执行发生在哪个文件和哪一行会很有用。为此，可以使用 `__FILE__`、`__LINE__` 和 `__func__` 宏。

在 C++20 中，这现在是标准库的一部分。使用 `<source_location>` 头文件，你可以通过 `source_location::current()` 获取所需信息。

```cpp
#include <source_location>
#include <iostream>
int main() {
    const auto loc = std::source_location::current();
    std::cout << "In " << loc.file_name() << " in line " << loc.line()
              << " in function " << loc.function_name() << "\n";
}
```

目前，它为我输出以下内容：

```text
In 11pModularisierung.md in line 687 in function int main()
```
