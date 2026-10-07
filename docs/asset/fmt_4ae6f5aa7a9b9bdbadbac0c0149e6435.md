
表 139 针对字符容器序列 `[first, last)` 进行匹配时，`regex_constants::match_flag_type` 的影响。（续表）

| 元素 | 设置后的效果 |
|------|------|
| `format_default` | 当将正则表达式匹配项替换为新字符串时，新字符串应使用 ECMA-262 中 15.5.4.11 `String.prototype.replace` 的 ECMAScript `replace` 函数所使用的规则来构造。此外，在搜索和替换操作期间应定位并替换，输入中未匹配表达式的部分将将原封不动地复制到输出字符串中 |
| `format_sed` | 当将正则表达式匹配项替换为新字符串时，新字符串应使用 POSIX 中 `sed` 工具所使用的规则来构造 |
| `format_no_copy` | 在搜索和替换操作期间，被搜索字符容器中不匹配正则表达式的部分不应复制到输出字符串中 |

### 28.5.3 实现定义的 error_type [re.err]

```cpp
namespace std {
namespace regex_constants {
    typedef T3 error_type;
    static constexpr error_type_collate = unspecified;
    static constexpr error_type_ctype = unspecified;
    static constexpr error_type_escape = unspecified;
    static constexpr error_type_backref = unspecified;
    static constexpr error_type_paren = unspecified;
    static constexpr error_type_brace = unspecified;
    static constexpr error_type_badbrace = unspecified;
    static constexpr error_type_range = unspecified;
    static constexpr error_type_space = unspecified;
    static constexpr error_type_badrepeat = unspecified;
    static constexpr error_type_complexity = unspecified;
    static constexpr error_type_stack = unspecified;
}
}
```

`error_type` 是一个实现定义的枚举类型（17.5.2.1.2）。`error_type` 的值表示表 140 中描述的条件：

表 140 — C 语言环境下的 `error_type` 值

| 值 | 错误条件 |
|---|---|
| `error_collate` | 表达式包含无效的排序元素名称。 |
| `error_ctype` | 表达式包含无效的字符类名称。 |
| `error_escape` | 表达式包含无效的转义字符，或尾随转义。 |

表 140 — C 语言环境下的 `error_type` 值（续表）

| 值 | 错误条件 |
|---|---|
| `error_backref` | 表达式包含无效的反向引用。 |
| `error_brack` | 表达式包含不匹配的 { 和 }。 |
| `error_paren` | 表达式包含不匹配的 { 和 }。 |
| `error_brace` | 表达式在 { expression 中包含无效的范围。 |
| `error_badbrace` | 表达式包含无效的字符范围，例如匹配中的 [b-a]。 |
| `error_range` | 内存不足以将表达式转换为有限状态机。 |
| `error_space` | 其中一个* 前面没有跟正则表达式。 |
| `error_badrepeat` | 对正则表达式尝试匹配的复杂度超过了预设水平。 |
| `error_stack` | 内存不足以判断正则表达式是否能匹配指定的字符序列。 |

### 28.6 类 regex_error [re.badexpp]

```cpp
class regex_error : public std::runtime_error {
public:
    explicit regex_error(regex_constants::error_type ecode);
    regex_constants::error_type code() const;
};
```

- 1 类 `regex_error` 定义了作为异常抛出的对象类型，用于报告正则表达式库的错误。

```cpp
regex_error(regex_constants::error_type ecode);
```

影响：构造一个 `regex_error` 类的对象。
- 3 后置条件：`ecode == code()`

```cpp
regex_constants::error_type code() const;
```

- 4 返回：传递给构造函数的错误代码。

### 28.7 模板类 regex_traits [re.traits]

```cpp
namespace std {
template <class charT>
struct regex_traits {
    typedef charT char_type;
    typedef std::basic_string<charT> string_type;
    typedef locale locale_type;
    typedef std::bitmask_unsigned class_type;

    regex_traits();
    static std::size_t length(const char_type* p);
    charT translate(charT c) const;
```

```cpp
charT translate_nocase(charT c) const;
template <class ForwardIterator>
string_type transform(ForwardIterator first, ForwardIterator last) const;
template <class ForwardIterator>
string_type transform_primary(
ForwardIterator first, ForwardIterator last) const;
template <class ForwardIterator>
string_type lookup_collatname(
ForwardIterator first, ForwardIterator last) const;
template <class ForwardIterator>
char_type lookup_classname(
ForwardIterator first, ForwardIterator last, bool icase = false) const;
bool isctype(charT c, char_type f) const;
int value(charT ch, int radix) const;
locale_type imbue(locale_type loc);
locale_type getloc() const;
};
```

- 1 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 2 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 3 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 4 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 5 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 6 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 7 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 8 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 9 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 10 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。
- 11 `regex_traits<char>` 和 `regex_traits<wchar>` 的特化通过 `*this` 提供了缓存数据。

# ISO/IEC 14882:2011(E)

## 28.8 类模板 basic_regex

1 对于类字符类型的 `charT`，类模板 `basic_regex` 的特化版本表示由 `char` 字符序列构造的正则表达式。在 28.8 的其余部分，`charT` 表示给定的类型。正则表达式的存储由类 `basic_regex` 的成员函数进行分配和释放。

2 `basic_regex` 特化类型赋值的对象负责将 `charT` 对象序列转换为内部表示。标准未规定这种表示法采用何种形式，也未规定操作正则表达式的算法如何访问它。[注：实现中通常会将某些函数声明为 `basic_regex` 的模板来实现这一点 —— 备注结束]

3 本类报告中描述的函数通过抛出 `regex_error` 类型的异常来报告错误。
