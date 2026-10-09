
`#define PRIDLEASTN` 见下文

`#define PRILEAST6` 见下文

`#define PRILEAST8` 见下文

`#define PRILEAST9` 见下文

`#define PRILEASTX` 见下文

`#define PRILEASTZ` 见下文

`#define SCLEAST1` 见下文

`#define SCNLEASTN` 见下文

`#define SCNLEASTX` 见下文

`#define SCULEASTN` 见下文

`#define PRIDFASTN` 见下文

`#define PRI1FASTN` 见下文

`#define PRIOFASTN` 见下文

`#define PRIUFASTN` 见下文

```cpp
#define PRIXFASTN 见下文

#define SCDdFASTN 见下文

#define SCNIAFASTN 见下文

#define SCNFASTN 见下文

#define SCXFASTN 见下文

#define PridMAX 见下文

#define PRIMAX 见下文

#define PRIUMAX 见下文

#define PRIuMAX 见下文

#define PRIXMAX 见下文

#define SCNAMAX 见下文

#define SCNIMAX 见下文

#define SCNOMAX 见下文

#define SCUMAX 见下文

#define PridPTR 见下文

#define PRIIPPTR 见下文

#define FLIPPTR 见下文

#define PRLIPPTR 见下文

#define PIXPTR 见下文

#define PIXTPTR 见下文

#define SCNIPTR 见下文

#define SCNUPTR 见下文

#define SCNXPTR 见下文
```

1 头文件 `<intypes>` 的内容和含义与 C 标准库头文件 `<intypes.h>` 相同，但有以下更改：

- (1.1) 头文件 `<intypes>` 包含了 `<cstdint>` (17.4.2) 而非 `<stdio.h>`，如果类型 `intmax_t` 指定扩展整数类型 (6.8)，则增加了签名：
```cpp
intmax_t abs(intmax_t);
intmax_t div(intmax_t n, intmax_t q);
```
其语义与函数签名 `intmax_t abs(intmax_t)` 和 `intmax_t imdiv(intmax_t, intmax_t)` 相同。

另参：ISO C 7.8

## 30 正则表达式 [re]

### 30.1 通用 [re.general]

本节描述了 C++ 程序用于执行正则表达式匹配和搜索的组件。后续子节描述了基础表达式模板及其它可以处理的特征类 (21.1) 模板、处理 `char` 和 `wchar_t` 序列的该类的两个特化版本、持有正则表达式匹配结果的类模板、允许正则表达式操作字符序列的一系列算法，以及正则表达式匹配的两种迭代器类型，总结于表 134。

表 134：正则表达式摘要 [tab.re.summary]

| 子类 | 头文件 |
| :--- | :--- |
| 30.2 定义 | |
| 30.3 要求 | |
| 30.5 常数 | |
| 30.6 异常类型 | `<regex>` |
| 30.7 特征 | |
| 30.8 正则表达式模板 | |
| 30.9 子匹配 | |
| 30.10 匹配结果 | |
| 30.11 算法 | |
| 30.12 迭代器 | |

## 30.2 句法 [re.def]

以下定义适用于本节：

- 30.2.1 排序元素 [re.regex.collating.element]：当前区域内一个或多个字符的序列，其排序方式如同它们是单个字符。
- 30.2.2 有限状态机 [re.regex.format.specifier]：用于表示正则表达式的未指定数据结构，允许获取正则表达式匹配。
- 30.2.3 格式说明符 [re.regex.matched]：一个或多个字符的序列，将被正则表达式匹配的某些替换。
- 30.2.4 匹配 [re.regex.primary.equivalence.class]：当序列对应于模式定义的字符序列时，一个或多个字符被正则表达式匹配。
- 30.2.5 主等价类：一个或多个字符的集合，它们共享相同的排序键：即排序键仅取决于字符形状，而不取决于重音、大小写或区域设置。
- 30.2.6 正则表达式：从字符字符串集中选择特定字符串的模式。
- 30.2.7 子表达式：被括号括的表达式子集。

### 30.3 要求

- 1 本子类对表示特征的类定义了要求。[注意 1：在 30.7 中定义的类模板 `regex_traits` 满足这些要求。]
- 2 在 30.8 中定义的类模板 `basic_regex` 是一组用于完成其语义定义的类型和函数。这些类型和函数作为 `basic_regex` 类模板所使用的模板参数的类型定义和函数成员提供。本子类定义了这些成员的语义。
- 3 为字符 `CharT` 及其相关的表达式特征类特化 `basic_regex`，使用 `basic_regex<CharT, Traits>`。
- 4 在表 135 中，`X` 表示为字符类型 `CharT` 定义类型和函数的类；`u` 是 `X` 类型的对象；`v` 是 `const X` 类型的对象；`p` 是 `Char*` 类型的值；`I1` 和 `I2` 是输入迭代器 (23.3.5.3)；`F1` 和 `F2` 是前向迭代器 (23.3.5.5)；`c` 是 `const CharT` 类型的值；`s` 是 `X::string_type` 的对象；`a` 是 `X` 类型的对象；`b` 是 `bool` 类型的值；`cl` 是 `X::char_class_type` 类型的值；`loc` 是 `X::locale_type` 对象。

表 135 正则表达式特征要求类

| 表达式 | 返回类型 | 断言/注意 前后条件 |
| :--- | :--- | :--- |
| `X::type` | | 在类模板 `basic_regex` 实现中使用的字符类型。 |
| `X::string_type` | `basic_` | |
| `X::locale_type` | 可构造类型 | 表示特征类使用的区域设置的类型。 |
| `X::char_class_type` | 位掩码 | 表示字符分类的位掩码 |
| `X::length(p)` | `size_t` | 产生最小的 `p[i] == 0` 的索引。复杂度相对于 `i` 是线性的 |
| `v.translate(c)` | `X::char_type` | 返回一个字符 `d`，使得任何 `c` 都等于 `v.translate(c)` |
| `v.nocase(c)` | | 用于不忽略大小写的匹配。`translate_nocase(c)` |
| `v.transform(F1, F2)` | `X::string_type` | 返回由迭代器 `[F1, F2]` 指定的排序，使得字符序列 `[G, G2]` 在字符序列 `[H1, H2]` 之前排序。`v.transform_primary(G1, G2)`。 |

表 135：等价类（续）

| 表达式 | 返回类型 | 断言/注意 前后条件 |
| :--- | :--- | :--- |
| `v.lookup_collname(F1, F2)` | `X::string_type` | 返回迭代器 `[F1, F2]` 指定的排序元素的序列。如果字符不是有效的排序元素则返回空字符串 |
| `v.lookup_classname(F2, b)` | `X::char_class_type` | 将迭代器指定的字符序列转换为可以位位或的掩码类型；如果 `b` 为真，返回的位掩码适用于不忽略大小写的匹配。返回的值与字符的大小无关。 |
| `v.isctype(c, I)` | `bool` | 如果 `c` 是 `I` 指定的字符类之一的成员则返回 `true`；否则返回 `false` |
| `v.value(c, I)` | `int` | 如果字符 `c` 是基 `I` 中的有效数字，则返回其表示的值；否则返回 `-1`。[注意：`I` 的值只有 8、10 或 16。] |
| `v.imbue(loc)` | `X::locale_type` | 注入区域设置 `loc` 并返回之前使用的区域设置 |
| `v.getloc()` | `X::locale_type` | 返回 `v` 当前使用的区域设置，如果有。 |

## 30.4 头文件摘要

```cpp
#include <complex>               // sec 17.11.1
#include <initializer_list>      // sec 17.10.2
namespace std {
namespace regex_constants {
    using syntax_option_type = T1;
    using match_flag_type = T2;
    using error_type = T3;
}
// 30.6. class regex_error
class regex_error;
}
```

```cpp
// 30.7, class template regex_traits
template<class charT> struct regex_traits;
// 30.8, class template basic_regex
template<class charT, class traits = regex_traits<charT>> class basic_regex;
using regex = basic_regex<char>;
using wregex = basic_regex<wchar_t>;
// 30.8.6, basic_regex swap
template<class charT, class traits>
void swap(basic_regex<charT, traits>& e1, basic_regex<charT>& e2);
// 30.9, class template sub_match
template<class BidirectionalIterator>
class sub_match {
using sub_match = sub_match<const char*>;
using wchar_match = sub_match<const wchar*>;
using sub_match = sub_match<const string::const_iterator>;
using wstring_match = sub_match<wstring::const_iterator>;
// 30.9.3, class match non-member operators
template<class Bilter>
class Bilter{
    bool operator=(const sub_match<Bilter>& lhs, const sub_match<Bilter>& rhs);
};template<class Bilter>
auto operator<>(const sub_match<Bilter>& lhs, const sub_match<Bilter>& rhs);
template<class Bilter, class ST, class SA>
bool operator==(
const sub_match<Bilter>& lhs,
const basic_string<iterator_traits<Bilter>::value_type, ST, SA>& rhs);
template<class Bilter, class ST, class SA>
auto operator!(
const sub_match<Bilter>& lhs,
const basic_string<iterator_traits<Bilter>::value_type, ST, SA>& rhs);
template<class Bilter>
bool operator<==(const sub_match<Bilter>& lhs,
const typename iterator_traits<Bilter>::value_type* rhs);
template<class Bilter>
auto operator<=>(const sub_match<Bilter>& lhs,
const typename iterator_traits<Bilter>::value_type* rhs);
template<class Bilter>
bool operator>=(const sub_match<Bilter>& lhs,
const typename iterator_traits<Bilter>::value_type* rhs);
template<class Bilter>
auto operator>=(const sub_match<Bilter>& lhs,
const typename iterator_traits<Bilter>::value_type* rhs);
template<class charT, class ST, class Bilter>
basic_ostream<charT, ST>&operator<<=(basic_ostream<charT, ST>& os, const sub_match<charT>& m);
// 30.10, class template match_results
template<class BidirectionalIterator, class Allocator = sub_match<BidirectionalIterator>>
class match_results {
using cmatch = match_results<const char*>;
using watch = match_results<const wchar*>;
using match = match_results<const string::const_iterator>;
using wstring = match_results<wstring::const_iterator>;
# ISO/IEC 14882:2020(E)
// match_results comparisons
template<class BidirectionalIterator, class Allocator>
bool operator==(const match_results<BidirectionalIterator, Allocator>& m1,
           const match_results<BidirectionalIterator, Allocator>& m2);
// 30.10.8 match_results swap
template<class BidirectionalIterator, class Allocator>
void swap(match_results<BidirectionalIterator, Allocator>& m1,
           match_results<BidirectionalIterator, Allocator>& m2);
// 30.11.2. function template regex_match
template<class BidirectionalIterator, class Allocator, class charT, class Traits>
bool regex_match(BidirectionalIterator first, BidirectionalIterator last,
                  const regex& m, Allocator& alloc,
                  const basic_regex_traits<charT>& traits = Traits(), 
                  regex_constants::match_flag_type flags = regex_constants::match_default);
template<class BidirectionalIterator, class Allocator, class charT, class Traits>
bool regex_match(BidirectionalIterator first, BidirectionalIterator last,
                  const regex& m, Allocator& alloc,
                  const basic_regex_traits<charT>& traits = Traits(),
                  regex_constants::match_flag_type flags = regex_constants::match_default);
template<class charT, class Allocator>
bool regex_match(const charT* first, const charT* last, const regex& m, Allocator& alloc,
                  const basic_regex_traits<charT>& traits = Traits(),
                  regex_constants::match_flag_type flags = regex_constants::match_default);
template<class ST, class SA, class charT, class Traits>
```
