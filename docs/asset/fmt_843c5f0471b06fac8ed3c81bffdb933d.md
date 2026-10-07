
```cpp
bool regex_search(BidirectionalIterator first, BidirectionalIterator last,
             match_results<BidirectionalIterator, Allocator>& m,
             const basic_regex_constants<traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class BidirectionalIterator, class charT, class traits>
bool regex_search(BidirectionalIterator first, BidirectionalIterator last,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class charT, class Allocator, class traits>
bool regex_search(const charT*, Allocator>& m,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class charT, class traits>
bool regex_search(const charT* str,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class ST, SA, class traits>
bool regex_search(const basic_string<charT, ST>, SA>& e,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class ST, SA, class Allocator, class charT, class traits>
bool regex_search(const basic_string<charT, ST>, SA>& e,
             match_results<typename basic_string<charT, ST>::const_iterator,
                 Allocator>& m,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
```

```cpp
// 28.11.4, function template regex_replace:
template <class Output, BidirectionalIterator,
             class traits, class charT, class SA>
OutputIterator
regex_replace(OutputIterator out,
             BidirectionalIterator first, BidirectionalIterator last,
             const basic_regex<charT, traits>& e,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class Output, BidirectionalIterator,
             class traits, class charT>
OutputIterator
regex_replace(OutputIterator out,
             BidirectionalIterator first, BidirectionalIterator last,
             const basic_regex<charT, traits>& e,
             const charT* fmt,
             regex_constants::match_flag_type flags =
             regex_constants::match_default);
template <class traits, class charT, class ST, SA, class FST, class FSA>
basic_string<charT, ST, SA>
regex_replace(const basic_string<charT, ST, SA>& s,
              const regex<charT, traits>& e,
              const basic_string<charT, FSA>& fmt,
              regex_constants::match_flag_type flags = regex_constants::match_default);
template<class traits, class charT, class ST, class SA>
basic_string<charT, ST, SA>
regex_replace(const basic_string<charT, ST, SA>& s,
              const regex<charT, traits>& e,
              const char* fmt,
              regex_constants::match_flag_type flags = regex_constants::match_default);
template<class traits, class charT, class ST, class SA>
basic_string<charT>
regex_replace(const basic_regex<charT, traits>& e,
              const basic_string<charT, ST, SA>& fmt,
              regex_constants::match_flag_type flags = regex_constants::match_default);
template<class traits, class charT>
basic_string<charT>
regex_replace(const charT* s,
              const basic_regex<charT, traits>& e,
              const basic_string<charT, ST, SA>& fmt,
              regex_constants::match_flag_type flags = regex_constants::match_default);
```

```cpp
// 28.12.1. class template regex_iterator:
template<class BidirectionalIterator>
using charT = typename iterator_traits<BidirectionalIterator>::value_type;
using traits = regex_traits<charT>;
class regex_iterator {
public:
    typedef regex_iterator<const char*> cregrex_iterator;
    typedef regex_iterator<const wchar*> wgrex_iterator;
    typedef regex_iterator<const string, const_iterator> sregex_iterator;
    typedef regex_iterator<const wstring, const_iterator> wsregex_iterator;
};
```

```cpp
// 28.12.2. class template regex_token_iterator:
template<class BidirectionalIterator>
using charT = typename iterator_traits<BidirectionalIterator>::value_type;
using traits = regex_traits<charT>;
class regex_token_iterator {
    typedef regex_token_iterator<const char*> cregrex_iterator;
    typedef regex_token_iterator<const wchar*> wgrex_iterator;
    typedef regex_token_iterator<const string, const_iterator> sregex_iterator;
    typedef regex_token_iterator<const wstring, const_iterator> wsregex_iterator;
};
```

## 28.4

## 28.5 空间 `std::regex_constants`

`std::regex_constants` 命名空间包含了正则表达式库使用的符号常量。该命名空间提供了三种类型：`syntax_option_type`、`match_flag_type` 和 `error_type`，并带有这些类型的若干常量。

### 28.5.1 位掩码类型 `syntax_option_type`

```cpp
namespace std {
    namespace regex_constants {
        typedef T syntax_option_type;
        static const syntax_option_type icase = unspecified;
        static const syntax_option_type nosubs = unspecified;
        static const syntax_option_type optimize = unspecified;
        static const syntax_option_type collate = unspecified;
        static const syntax_option_type ECMAScript = unspecified;
        static const syntax_option_type basic = unspecified;
        static const syntax_option_type extended = unspecified;
        static const syntax_option_type awk = unspecified;
        static const syntax_option_type grep = unspecified;
        static const syntax_option_type egrep = unspecified;
    }
}
```

`syntax_option_type` 是一个实现定义的位掩码（17.5.2.1）。其值必须是 `ECMAScript`、`basic`、`extended`、`awk`、`grep` 或 `egrep` 之一。在匹配序列时，`syntax_option_type` 的效果见表 138。

### 28.5.2 位掩码类型 `regex_constants::match_flag_type`

```cpp
namespace std {
    namespace regex_constants {
        typedef T match_flag_type;
        static const match_flag_type match_default = 0;
        static const match_flag_type match_not_bol = unspecified;
        static const match_flag_type match_not_box = unspecified;
        static const match_flag_type match_not_eol = unspecified;
        static const match_flag_type match_not_any = unspecified;
        static const match_flag_type match_not_null = unspecified;
        static const match_flag_type match_continuous = unspecified;
        static const match_flag_type match_prev_avail = unspecified;
        static const match_flag_type format_default = unspecified;
        static const match_flag_type format_sed = unspecified;
        static const match_flag_type format_copy = unspecified;
        static const match_flag_type format_only = unspecified;
    }
}
```

`regex_constants::match_flag_type` 是一个实现定义的位掩码（17.5.2.1）。在匹配字符序列 `[first,last]` 时，`match_flag_type` 的效果见表 139。

表 138 — `syntax_option_type`

| 元素 | 设置后的效果 |

|---|---|

| `icase` | 指定对字符序列的正则表达式匹配时不区分大小写。 |

| `nosubs` | 指定当匹配正则表达式时，不将子表达式匹配项存储在匹配结果中。 |

| `optimize` | 指定正则表达式引擎应更关注构造正则表达式的速度，否则对程序输出没有可检测的影响。 |

| `collate` | 指定 `"a-b"` 形式的字符范围是区域敏感的。 |

`ECMAScript` 指定由正则表达式引擎使用的语法应为 ECMA-262，如 28.13 所修改。

`basic` 指定由正则表达式引擎使用的语法应为 POSIX 基础表达式，见 POSIX 第 9 节。

`extended` 指定由正则表达式引擎使用的语法应为 POSIX 扩展表达式，见 POSIX 第 9 节。

`awk` 指定由正则表达式引擎使用的语法应为 POSIX 中的 awk 工具。

`grep` 指定由正则表达式引擎使用的语法应为 POSIX 中的 grep 工具。

`egrep` 指定由正则表达式引擎使用的语法应为 POSIX 中给定 `-E` 选项的 egrep 工具。

表 139 — `regex_constants::match_flag_type` 在匹配字符序列 `[first,last]` 时的效果

| 元素 | 设置后的效果 |

|---|---|

| `match_not_bol` | 序列 `[first,last]` 中的第一个字符被处理为不在行首，因此正则表达式中的 `^` 不匹配 `[first,first)`。 |

| `match_not_col` | 序列 `[first,last]` 中的最后一个字符被处理为不在行尾，因此正则表达式中的 `$` 不匹配 `[last,last)`。 |

| `match_not_bow` | 表达式 `"b"` 不匹配子序列 `[first,last]`。 |

| `match_not_cow` | 表达式 `"w"` 不匹配子序列 `[first,last]`。 |

| `match_any` | 如果存在多个匹配，则任何一个匹配都是可以接受的结果。 |

| `match_not_null` | 表达式不匹配空序列。 |

| `match_continuous` | 表达式仅匹配从 `first` 开始的子序列。 |

| `match_prev_avail` | `--first` 是有效的迭代器位置。当设置此标志时，正则表达式算法 28.11 和迭代器 28.12 将忽略 `match_not_bol` 和 `match_bow`。 |

# ISO/IEC 14882:2011(E)
