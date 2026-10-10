
```cpp
// https://godbolt.org/z/e1dgdWbe9
#include <iostream>
#include <string>
#include <tuple>
using std::tuple; using std::cout; using std::string;

int main() {
    tuple<int,string> a {12, "gnorf" };
    tuple b { 666 };
    tuple<double,double,string> c { 77.77, 33.33, "frong" };
    tuple<int,string,int,double,string> r = std::tuple_cat(a, b, c);
    cout << std::get<2>(r) << "\n"; // 输出: 666
}
```

# 列表 28.8 将多个小 `tuple` 合并为一个大的 `tuple`

同样——可能更好——你也可以写 `r = ...` 并让编译器确定正确的类型。除了 `tuple`，你也可以给 `tuple_cat` 传递 `pair` 作为参数。在大多数情况下，这些类型是兼容的。

# 警惕带有引用的 `tuple`

你不允许向标准容器中填充引用。这样做是有充分理由的：`vector<T>` 在内部会对引用进行赋值，而其结果可能并不符合你的预期。

然而，在原则上 `tuple<T&>` 是被允许的，因为标准库需要它来实现 `tie`。我建议你不要自己使用 `tuple<T&>`——特别是不要用它存储指向数据的引用，这无如履薄冰。

编译器不会阻止你使用 `vector<tuple<T&>>`，但在这里，你所踩的冰已经融化了。

对于 `tuple` 仍然有一些非常有用的工具。例如，你可以通过 `tuple_size<tuple<>>::value` 确定元组的大小。如果你“忘记”了元素的类型，你始终可以通过 `tuple_element<I, tuple<...>>::type` 找回各个类型。

对于具体的 `tuple`，这并不那么有趣，但如果你允许 `tuple` 作为模板参数，那么这些类型性性（type traits）就是非常有用的辅助工具。它们在第 23 章中详细讨论过。

```cpp
// https://gdbbolt.org/z/Psdz9sGc
#include <iostream>
#include <string>
#include <tuple>
using namespace std;
template<typename Tuple>
auto back(Tuple&&tuple) {
    using Noref = typename remove_reference<Tuple>::type; // 以防引用
    Tuple&
    constexpr auto sz = tuple_size<Noref>::value;
    return get<sz-1>(forward<Tuple>(tuple));
}
int main() {
    tuple<string,int,string> enterprise = make_tuple("NCC", 1701, "D");
    cout << back(enterprise) << "\n"; // 输出: D
}
```

# 列表 28.9 有用的 `tuple` 类型性性

通过 `back`，你始终可以获取任何元组的最后一个元素。虽然还需要其他东西，但 `tuple_size` 是核心：

- 像往常一样，你使用 `get` 来访问元组元素。`sz-1` 始终是最后一个元素的索引。
- `auto` 自动推导出函数的返回值。如果没有 `auto`，这会很困难但并非不可能。
- 你需要 `remove_reference` 是因为 `tuple_size` 无法处理元组的引用。
- 参数中的 `&&` 和 `forward` 确保了该模板适用于值、引用和临时值（temp-values）。

## 28.2 正则表达式

C++ 现在原生支持正则表达式。通过它们，你可以在字符串中搜索模式并提取其中的部分内容。

```cpp
// https://godbolt.org/z/TlYMMoMSas
#include <string>
#include <iostream>
#include <regex>

using std::regex; using std::iterator; using std::string;
const regex rgxMobile("(01567\(6,10))"); // 手机 0151-0179
bool isMobilephone(const string &text) {
    return std::regex_match(text, rgxMobile); // 是否完全匹配？
}
bool containsMobilephone(const string &text) {
    return std::regex_search(text, rgxMobile); // 在文本某处是否存在？
}
void listMobilephones(const string &text) {
    sregex_iterator begin(text.begin(), text.end(), rgxMobile);
    sregex_iterator end;
    for(auto it = begin; it != end; ++it) {
        std::cout << it->str() << " "; // 匹配的文本
    }
} // "xyz01780999 abc 016188766 vww -> "016188766"
```

**列表 28.10** 使用正则表达式进行匹配、搜索和枚举。

当 `regex_match` 检查文本是否完全匹配模式时，`regex_search` 测试模式是否出现在文本中。

通过像 `sregex_iterator` 这样的类，你可以迭代字符串中的匹配项。

虽然 `regex_match` 检查文本是否完全匹配模式，但 `regex_search` 测试模式是否出现在文本的任何地方。

```cpp
// https://godbolt.org/z/E9hc4
#include <regex>
#include <string>
#include <iostream>
using std::regex; using std::regex_match; using std::regex_search;
int main() {
    std::cout << std::boolalpha;
    regex pattern("hello");
    std::string text = "Hello world";
    auto b1 = regex_match(text.begin(),text.end(), pattern); // 不匹配
    std::cout << b1 << "\n"; // 输出: false
    auto b2 = regex_search(text.begin(),text.end(), pattern); // 找到
    std::cout << b2 << "\n"; // 输出: true
}
```

### 28.2.1 匹配与搜索

列表 28.2.1 搜索与匹配。

### 28.2.2 结果与部分

我在 28.12 中将搜索结果存储在 `cmatch` 实例中。但这实际上只是字符串搜索的 `match_results` 模板别名。对于其他的搜索类型，还有其他定义的别名：

- `smatch` 用于搜索 `string`
- `cmatch` 用于搜索 `const char*`
- `wsmatch` 用于搜索 `wstring`
- `wcmatch` 用于搜索 `const wchar*`

### 28.2.3 找到

```cpp
// https://godbolt.org/z/Yz39
#include <regex>
#include <string>
#include <iostream>
using std::string;
using std::regex;
using std::regex_match_search;
using std::regex_replace;
int main() {
    string text = "Title,Artist";
    regex pattern(",");
    string new_str = regex_replace(text, pattern, "");
    std::cout << new_str << "\n"; // 输出: TitleArtist
}
```

### 28.2.4 丰富的变体

我们已经看到，要搜索的文本可以用不同的方式传递。这些函数对于各种需求非常灵活。例如，`regex_search` 的变体可以：

- 要搜索的文本，例如 `string`、`const char*` 或迭代器对
- 可选的 `match_results`，如 `cmatch`
- 作为 `regex` 的搜索模式
- 可选的标志，默认为 `regex_constants::default`

### 28.2.5 迭代器

内部，`regex_iterator` 使用 `regex_search` 函数进行搜索，它仅仅是所提供的迭代器的适配器类。因此，它们指向相应的 `match_result` 实例。

如果你想枚举字符串中的所有匹配项，建议使用迭代器变体而不是带有 `regex_match` 的循环。在某些情况下，否则可能会导致无限循环；而 `regex_iterator` 可以防止这种情况。因此，特别是对于可能匹配“空字符串”的正则表达式，例如 `"(abc)*"`，使用迭代器变体更好。

## 28.2.6 匹配项可以不仅仅是使用 `str()` 输出找到的字符串，如列表 28.10 所示。

你可以使用 `length()` 和 `position()` 来查找匹配在文本中的具体位置。匹配项前后的文本通过调用 `prefix().str()` 和 `suffix().str()` 提供。正如你已经在列表 28.12 中看到的，可以使用运算符 `operator[]` 获取子表达式。

## 28.2.7 选项正则表达式存在许多不同的变体。除非另有指定，C++ 支持 ECMAScript 语法——这种语法在 JavaScript 中也为人熟悉，并与 Perl 正则表达式语法有本质联系。熟悉其中任何一种的人都能快速在 C++ 中找到方法。实现层可以可选地支持其他变体，并通过构造函数调用进行选择：

```
regex rgx(R"...", regex_constants::Syntax);
```

这里，`Syntax` 是一个用于选择某些语法变体的位掩码。标准规定了 ECMAScript、basic、extended、awk、grep 和 egrep 等选项。实现可以自由提供更多。

位掩码可以通过一些修饰符微调语法：

- `- icase` 忽略大小写敏感性。
- `- nosubs` 不在匹配结果中存储子表达式。
- `- optimize` 优先考虑匹配速度。
- `- coll` 对于如 `[a-z]` 等表达式考虑本地区域设置。

使用 `optimize` 选项时，注意算法会处理正则表达式。这在某些情况下可能会花费更长的时间并消耗大量内存。然而，在执行搜索时结果会更快。原则上讲，应用正则表达式的频率是一种权衡：

- 如果表达式只传递给 `regex_search` 或 `regex_match` 等函数一次或两次，那么 `optimize` 的努力并不值得。
- 如果你使用正则表达式应用搜索和替换函数十次或更多，确实可以节省大部分时间。

通常情况下，你不需要担心这个。对于普通表达式，差异非常小。这种情况可能发生在具有许多歧义且自身存在重叠的长长、复杂的表达式上。一个歧义例如 `(abc|abd)`，因为 `ab` 被多个子表达式匹配。一个简单的自重叠发生在 `ababa` 中：对于 `abab`，与 `ab` 的可能匹配也会同时开始。尽管如此，此类情况通常是完全无关紧要的，无论是否优化，算法都能很好地处理它们。对于巨大的、不可管理且不特定的表达式，优化可能需要更长的时间和大量的内存——但由于执行速度更快，多次应用时这种努力仍然是值得的。

## 28.2.9 标准语法，简短版

由于默认是 ECMAScript 正则表达式语法，我在表 28.1 中提供了该语法最重要元素的要概述。

通过 `[class]`，你可以描述组中的一个字符。你可以枚举字符如 `[abcd]`，定义范围 `[A-Za-z]`，反转 `[^]`（除 own之外的所有内容），并使用像 `[[:alpha:]]` 这样的类名。支持类名；具体取决于所使用的 `regex_traits`。至少存在 `alnum`、`alpha`、`blank`、`cntrl`、`digit`、`graph`、`lower`、`print`、`punct`、`space`、`upper`、`xdigit`、`d`、`s` 和 `w`。它们对应于 C 函数名，例如 `isalnum()`。

| 模式 | 含义 | 模式 | 含义 |
|---|---|---|---|
| ab | a 后接 b | a{n,m} | n 到 m 次 a |
| a|b | 备选项 | () | 分组 |
| . | 任意字符 | ^ $ | 字符串的开始和结束 |
| a? | 0 次或 1 次 a | [class] | 类字符 |
| a* | 0 次或多次 | \d \w \s | 类简写 |
| a+ | 1 次或多次 | \b | 单词边界 |

**表 28.1** ECMAScript 正则表达式语法的简要概述。

你还可以组合并取反枚举项和类名——例如：

- `[[:alpha:]]` 匹配任何字母。
- `[abc[:digit:]]` 匹配字母 a、b、c 和任何数字。
- `[[:space:]]` 匹配任何非空白字符。

某些类名有缩写。例如，你可以用 `\d` 代替 `[[:digit:]]`。你可以在表 28.2 中详细查看缩写。`\w` 中的 `w` 代表 **word**（单词），即可以出现在单词中的字母。

| 缩写 | 代表 | 缩写 | 代表 |
|---|---|---|---|
| \d | [[:digit:]] | \D | ^[:digit:]] |
| \s | [[:space:]] | \S | ^[:space:]] |
| \w | [[:alnum:]] | \W | ^[:alnum:]] |

**表 28.2** 字符类的缩写。

为了支持国际化，有专门命名的名称。通过排序（collation），可以在西班牙语、法语等语言中匹配 `e`、`é` 和 `ê` 等字符。

## 28.2.10 C++ 正表达式注意事项

对于大多数应用程序，正则表达式的微妙之处可能无关紧要。比较 POSIX 和 ECMAScript 的结果：

| 模式 | 文本 | POSIX | ECMAScript |
|---|---|---|---|
| a|ab | xaby | ab | a |
| *.a|ayy | zxay | zxay | a |
| (:alnum:) | abc def | abc | a |

**表 28.3** POSIX 和 ECMAScript 区别。

谁没有尝试过用匹配闭合元素的正则表达式来在 HTML 文本中寻找开启元素，例如 `<font>...</font>`？使用 `<font[^]*>.*</font>` 实现此点的尝试在上述两种情况下都失败了，因为 `.*` 会尽可能多地消耗内容——包括额外的标签。在 ECMAScript 语法中，与 POSIX（例如）相比，你可以通过附加 `?` 让表达式中原本“贪婪”的部分变为非贪婪的。因此，`<font[^*]>..*</font>` 完成了任务。在有疑问的情况下，`.*` 现在将以尽可能短的内容消耗文本。

# 可读的正则表达式

我在日常生活中大量的正则表达式，你会对它们出现的频率和用途感到惊讶。它们是强大的工具，但也有自己的陷阱。根据我的经验，你应该*始终*将搜索、匹配或替换算法外包到一个易于测试的函数中，并提供一组有意义的测试用例。比通常情况下，你在正则表达式上更容易忽略某些问题。

所以，吧，你写了函数，它包含一个很棒的正则表达式。你还有了测试——哇！但三周后，最棘手的陷阱会找上门：你不再理解那个表达式了。你想扩展或纠正它，但无论你修改什么，算法都会崩溃。

从一开始就是易读的。

假设你有许多这样的消息：

score 400 for 2 nights at Minas Tirith Airport

在这里，文本和数字可能会变化。你需要提取出数字 400 和 2，以及位于 at 之后的酒店名称 Minas Tirith Airport。正则表达式可以如下：

```cpp
const string pattern = R"(\^\s+(\d+)\s+for\s+(\d+)\s+nights?\s+at\s+(.*))";
```

在程序中，它看起来如下列表所示。
