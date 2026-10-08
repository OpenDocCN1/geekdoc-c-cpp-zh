
`string_type` `positive_sign()` const;

`string_type` `negative_sign()` const;

`int` `frac_digits()` const;

`pattern` `format()` const;

`pattern` `pos_format()` const;

`pattern` `neg_format()` const;

```
1 这些函数中的每一个都返回调用相应的成员函数 `do_F()` 的结果。
```

### 22.4.6.2 money_punct 虚函数

[locale.money.punct.virtuals]

255 出效率考虑，`pattern::field` 指定为 `char` 数组而非 `part` 数组。

```
char do_decimal_point() const;
```
+ 1 返回：当 `do_frac_digits()` 大于零时使用的进制分隔符。

```
charT do_thousands_sep() const;
```
+ 2 返回：当 `grouping()` 指定数字分组模式时使用的数字分隔符。

```
string do_grouping() const;
```
+ 3 返回：与 `nump<charT>::do_grouping()` 定义完全相同但不一定相等的模式。

```
string_type do_curr_symbol() const;
```
+ 4 返回：用于货币标识符号的字符串。

```
string_type do_positive_sign() const;
```
```
string_type do_negative_sign() const;
```
+ 5 返回：`do_positive_sign()` 返回用于表示正货币值的字符串；`do_negative_sign()` 返回用于表示负值的字符串。

```
int do_frac_digits() const;
```
+ 6 返回：小数点分隔符后的数字数（如果有）。

```
pattern do_format() const;
```
```
pattern do_neg_format() const;
```
+ 7 返回：表 82 (22.3.1.1) 中要求的特化版本，即 `monepunct<charT>`、`moneypunct wchar_t`、`monepunct<char,true>`、`monepunct<charT,true>`，返回一个初始化为 `{symbol, sign, none, value}` 的 `pattern` 对象。

```
### 22.4.6.4 类模板 template_byname

[locale.monepunct.byname]
```
```cpp
template <class charT, bool Int = false>
class class_byname : public monepunct<charT, Int> {
public:
    typedef monepunct_base::pattern type;
    typedef basic_string<charT> string_type;
    explicit monepunct_byname(const char*, size_t ref = 0);
    explicit monepunct_byname(const string&, size_t ref = 0);
protected:
    monepunct_byname();
    };
}
```

## 22.4.7 消息检索分类

[category.messages]

1 `messages<charT>` 类实现了消息目录的检索。

2 在常见的美国区域设置中，这是 ' '，
3 在常见的美国区域设置中，这是 ','。
4 若要按 3 分组，值为 "\003" 而不是 "3"。
5 对于国际特化版本（第二个模板参数为 true），这通常是四个字符长，除非是三个字母加空格。
6 这是空字符串。

# ©ISO/IEC N4296

## 22.4.7.1 类模板消息消息 [locale.messages]

```cpp
namespace std {
    class messages_base {
    public:
        typedef unsigned integer type catalog;
    };
    template <class charT>
    class messages : public locale::facet, public messages_base {
    public:
        typedef charT char_type;
        typedef basic_string<charT> string_type;
        explicit messages(basic_string<char*>& fn, const locale&) const;
        string_type get(size_t ref = 0);
        catalog open(const basic_string<char>&, const locale&) const;
        string_type get(catalog c, int set, int msgid)
            const string_type& default const;
        void close(catalog c) const;
        static locale::id id;
    protected:
        ~messages();
        virtual catalog do_open(const basic_string<char>&, const locale&) const;
        virtual string_type do_get(catalog c, int set, int msgid)
            const string_type& default const;
        virtual void do_close(catalog c) const;
    };
};
```

类型为 `messages_base::catalog` 可可用成员函数 `get` 和 `close` 参数的值只能通过调用成员函数 `open` 获取。

### 22.4.7.1.1 成员 [locale.messages.members]

```cpp
catalog open(const basic_string<char*>& name, const locale& loc) const;
```
- 1 返回：`do_open(name, loc);`
`string_type get(catalog cat, int set, int msgid)` const `string_type& default const;`
- 2 返回：`do_get(cat, int set, msgid)`。
`void close(catalog cat) const;`
- 3 影响：调用 `do_close(cat)`.

### 22.4.7.1.2 虚拟函数 [locale.messages.virtuals]

```cpp
catalog do_open(const basic_string<char>& name,
    const locale& loc) const;
```
- 1 返回：一个值，该值可以传递给 `get()`，以便根据实现定义的映射从字符串名称标识的目录中检索消息。结果可以在传递给 `close()` 之前一直使用。
- 2 如果无法打开此类目录，则返回小于 0 的值。

备注：`locale` 参数在检索消息时用于字符集转换（如果需要的话）。

```cpp
string_type do_get(catalog cat, int set, int msgid,
    const string_type& default) const;
```
要求：`cat` 必须是从 `open()` 获取且尚未关闭的目录。

返回：根据实现定义的映射，由参数 `set` 和 `msgid` 标识的消息。如果找不到此类消息，则返回 `default`。

```cpp
void do_close(catalog cat) const;
```
要求：`cat` 必须是从 `open()` 获取且尚未关闭的目录。

影响：释放与 `cat` 关联的未引用资源。

备注：此类资源的限制（如果有）由实现定义。

## 22.4.7.2 类 messages_byname [locale.messages.byname]

```cpp
namespace std {
    template <class charT>
    class messages_byname : public messages<charT> {
    public:
        typedef messages_base::catalog catalog;
        typedef basic_string<charT> string_type;
        explicit messages_byname(const char*, size_t refs = 0);
        explicit messages_byname(const string&, size_t refs = 0);
    protected:
        ~messages_byname();
    };
} //
```

## 22.4.8 程序定义的区域 [facets.examples]

C++ 程序可以定义区域（facets）并将其添加到 `locale` 中，且以与内置区域相同的方式使用。要创建一个新的区域句接口，C++ 程序只需派自 `locale::facet` 定义一个包含静态成员 `locale::id id` 的类。

> [注：`locale` 成员函数会验证其类型和存储类。 — 备注结束]

> [示例：传统的全局本地化非常简单：]

```cpp
#include <iostream>
#include <locale>
#include <string>
int main() {
    // 示例用法
    return 0;
}
```

（注：提供的 OCR 文本在后几页包含大量重复和碎片化的示例。上述内容已清理，以根据可用片段反映 C++ 标准文档的逻辑结构。）

```cpp
explicit codecvt_utf8_utf16(size_t refs = 0);
-codecvt_utf8_utf16();
```
- 对于三种代码转换 facet 面 `codecvt_utf8`、`codecvt_utf16` 和 `codecvt_utf8-utf16` 中的每一个：
- `Elem` 是宽字符类型，例如 `wchar`、`char16_t` 或 `char32_t`。
- `Maxcode` 是该 facet 面在不报告错误的情况下读取或写入的最大字符编码。
- 如果满足 (`Mode & consumer_header`)，当在读取多字节序列时，该 facet 应当消耗一个初始的头部序列（如果存在），以确定后续要读取的多字节序列的字节序。
- 如果满足 (`Mode & generate_header`)，当在写入多字节序列时，该 facet 应当生成一个初始的头部序列，以标识后续要写入的多字节序列的字节序。
- 如果满足 (`Mode & little_endian`)，该 facet 应当以小端序生成多字节序列，而不是默认的大端序。
- 对于 facet 面 `codecvt_utf8`：
- 该 facet 应当在程序内进行 UTF-8 多字节序列与 UCS2 或 UCS4（取决于 `Elem` 的大小）之间的转换。
- 在读取或写入多字节序列时，字节序不应影响这些序列。
- 多字节序列可以写入文本文件或二进制文件。
- 对于 facet 面 `codecvt_utf16`：
- 该 facet 应当在程序内进行 UTF-16 多字节序列与 UCS2 或 UCS4（取决于 `Elem` 的大小）之间的转换。
- 多字节序列应当按照上述列出的 `Mode` 标志进行读取或写入。
- 多字节序列只能被写入二进制文件。尝试写入文本文件会导致未定义行为。
- 对于 facet 面 `codecvt_utf8_utf16`：
- 该 facet 应当在程序内进行 UTF-8 多字节序列与 UTF-16（一个或两个 16 位位的代码）之间的转换。
- 在读取或写入多字节序列时，字节序不应影响这些序列。
- 多字节序列可以写入文本文件或二进制文件。

参见：ISO/IEC 10646-1:1999。

## 22.6 C 库区域设置 (locales)

表 93 描述了头文件 `<locale>`。

内容与标准 C 库头文件 `<locale.h>` 相同。

对函数 `setlocale` 的调用可能会与其他 `setlocale` 调用或对表 94 中所有函数的调用引入数据竞态 (17.6.5.9)。

参见：ISO C 第 7.4 节。

## 表 93 — <locale> 概览

| 类型 | 名称(s) |
| --- | --- |
| 宏: | LC_ALL LC_COLLATE LC_CTYPE |
| | LC_MONETARY LC_NUMERIC LC_TIME |
| | NULL |
| 结构体: | lconv |
| 函数: | localeconv setlocale || |

## 表 94 — 潜在的 setlocale 数据竞态

| fprintf | isprint | iswdigit | localeconv | tolower |
| fscanf | ispunct | isgraph | mblen | toupper |
| isalnum | isspace | islower | mbstowcs | towlower |
| isalpha | isupper | isprint | mbtwc | towupper |
| isblank | iswalnum | iswpunct | setlocale | wcscoll |
| iscntrl | isalpha | iswpace | strcmp | wcctod |
| isdigit | isisland | isupper | strerror | wcstomb |
| isograph | iswcntrl | iswdigit | strtod | wcxfrm |
| islower | iswtype | iswdigit | strxfrm | wctomb |

## 23 容器库 (Containers library)

### 23.1 通用

1 本节描述了 C++ 程序可能用于组织信息集合的组件。

2 下述子句描述了容器的要求，以及序列容器和关联容器的组件，如表 95 总结所示。

## 表 95 — 容器库总结

| 子类 | 头文件(s) |
| --- | --- |
| 23.2 要求 | <array> |
| 23.3 序列容器 | <deque> <forward_list> <list> <vector> |
| 23.4 关联容器 | <map> <set> |
| 23.5 无序关联容器 | <unordered_map> <unordered_set> |
| 23.6 容器适配器 | <queue> <stack> |

## 23.2 容器要求

### 23.2.1 通用

1 容器是存储其他对象的对象。它们通过构造函数、析构函数、插入和删除操作来控制这些对象的分配和释放。

2 本节中的所有复杂度要求均仅以操作数表述。例如：`vector<int>` 的拷贝构造函数具有线性复杂度，尽管拷贝每个 vector 的复杂度是……（注：原文此处截断，根据逻辑推断为线性)。

*(注：由于原文文本后续存在多处乱码或重复片段，译文已根据 Markdown 结构进行了对齐处理，并遵循了不重复输出原文的原则)*

©ISO/IEC
N4296

```
i = j
i *= j
i < j
i <= j
i >= j
i > j
i - j
```
