
## 22.4.6.4 `moneypunct_byname`

```cpp
namespace std {
template <charT, bool Int = false>
class moneypunct : public moneypunct<charT, Int> {
public:
    typedef money_base::pattern;
    typedef basic_string<charT> string_type;

    explicit moneypunct(const char*, size_t refs = 0);
    explicit moneypunct_byname(const string&, size_t refs = 0);
protected:
    moneypunct_byname();
};
}
```

## 22.4.7 消息检索

1 `messages<charT>` 实现从消息目录中检索字符串。

### 22.4.7.1 `messages` 类

```cpp
namespace std {
class messages_base {
public:
    typedef int catalog;
};

template <charT>
class messages : locale::facet, public messages_base {
public:
    typedef charT char_type;
    typedef basic_string<charT> string_type;

    explicit messages(size_t refs = 0);
};
```

§ 22.4.7.1

```cpp
catalog open(const basic_string<char>& fn, const locale&) const;
string_type get(catalog c, int set, int msgid,
    const string_type& dfault) const;
void close(catalog c) const;
    static locale::id id;
```

```cpp
protected:
    messages();
    virtual catalog do_open(const basic_string<char>&, const locale&) const;
    virtual string_type do_get(catalog c, int set, int msgid,
        const string_type& dfault) const;
    virtual void do_close(catalog) const;
}
```

+1 `messages::catalog` 类型的值可以作为成员参数，并通过调用成员 `open` 获取。

## 22.4.7.1 `messages` 成员 [locale.messages.members]

```cpp
catalog open(const basic_string<char>& name
```

+1 返回：`do_open(name, loc);`

```cpp
string_type get(catalog cat, int set, int msgid,
    const string_type& dfault) const;
```

+2 返回：`do_get(cat, set, msgid, dfault).`

```cpp
void close(catalog cat) const;
```

+3 影响：调用 `do_close(cat)`。

## 22.4.7.2 `messages` 虚函数 [locale.messages.virtuals]

```cpp
catalog open(const basic_string<char>& name,
    const locale& loc) const;
```

+1 返回一个可以传递给 `get()` 以根据实现定义的映射从字符串标识的消息目录检索消息。结果在传递给 `close()` 之前都可以使用。

+2 如果无法打开此类目录，返回小于 0 的值。

+3 备注：在检索消息时，区域参数 `loc` 用于字符代码转换。

```cpp
string_type do_get(catalog cat, int set, int msgid,
    const string_type& dfault) const;
```

+4 要求：`cat` 应该是从 `open()` 获取且尚未关闭的。

+5 返回：根据实现定义的映射通过参数 `set`、`msgid` 和 `dfault` 标识的消息。如果找不到此类消息，则返回 `dfault`。

```cpp
void do_close(catalog cat) const;
```

## 22.4.7.2 `messages_bname` 类模板 [locale.messages.bname]

```cpp
namespace std {
template <charT>
class messages_bname : public messages<charT> {
public:
    typedef messages_base::catalog;
    typedef basic_string<charT> string_type;

    explicit messages_bname(const char*, size_t refs = 0);
    explicit messages_bname(const string&, size_t refs = 0);
protected:
    messages_bname();
};
}
```

```cpp
cout.imbue(locale::classic());
double f;
while (cin >> f) cout << f << endl;
return (cin.fail() != 0);
}
```

在欧洲区域设置下，输入 `3.456,78`，输出为 `3456.78`。 — 示例结束

+ 5 这对于简单的程序可能很重要，它可以帮助以固定格式写入数据文件，无论用户的偏好如何。

+ 6 [示例：`Date.h` 是在库函数中使用区域设置（locale）的一个示例。

```cpp
// file: Date.h
#include <iostream>
#include <string>
#include <locale>

class Date {
public:
    Date(unsigned day, unsigned month, unsigned year);
    std::string asString(const std::locale& loc = std::locale());
};

std::istream& operator>>(std::istream& s, Date& d);
std::ostream& operator<<(std::ostream& s, const Date& d);
```

+ 7 这说明了类 `locale` 的两种架构上的用法。

+ 8 第一种是在 `Date::asString()` 和 `>>` 中的默认参数，其中默认值是全局的（假设是用户偏好的）区域设置。

+ 9 第二种是在运算符 `<<` 和 `>>` 中，其中区域设置“搭便车”在另一个对象上（在本例中是流），直到需要它。

```cpp
// file: Date.C
#include "Date"
// includes <time>
#include <iostream>
std::string asString(const std::locale& l) {
    using namespace std;
    ostream s; s.imbue(l);
    s << *this << ": "; return s.str();
}

std::istream& operator>>(std::istream& s, Date& d) {
    using namespace std;
    istream::sentry cerberos(s);
    ios_base::xstate err = goodbit;
    struct tm t;
    use_facet<time_get<char>>(s.getloc()).get_date(s, 0, s, &t);
    if (!err) d = Date(t.tm_day, t.tm_mon + 1, t.tm_year + 1900);
    s.setstate(err);
    return s;
}
```

# ISO/IEC 14882:2011(E)

- 示例结束

+ 10 区域设置对象可以通过构造一个派自 `locale::facet` 的类的实例来简单地扩展一个新的区域面（facet）。C++ 程序必须定义的唯一成员是静态成员 `id`，它将该类的接口识别为新的区域面。

+ 11 [示例：对日语字符分类：

```cpp
// File: <ctype>
#include <locale>
namespace My {
    using namespace std;
    class JType : public locale::facet {
    public:
        static locale::id id; // 用作新区域面时需要
        bool is_kanji(wchar_t c) const;
        JType();
    protected:
        ~JType() {}
    };
}
```

```cpp
// File: filt.C
#include <iostream>
#include <locale>
#include "ctype" // 上述
std::locale::id My::JType::id; // 声明的静态 JType 成员。

int main() {
    using namespace std;
    typedef ctype<wchar_t> wctype;
    locale loc(""); // 用户偏好的区域设置 ...
    new My(loc); // 以及一个新特性 ...
    wchar_t c = use_facet<wctype>(loc).widen('!');
    if (!loc.facet<JType>(loc).is_kanji(c))
        cout << "no it isn't!" << endl;
    return 0;
}
```

+ 12 新的区域面的用法与内置区域面完全相同。 — 示例结束

+ 13 [示例：替换偶数区域面也是偶数。代码没有定义成员，因为它在使用 `npunct<char>` 接口：

```cpp
// File: my_bool.C
#include <iostream>
#include <locale>
#include <string>
namespace My {
    using namespace std;
    typedef npunct<char> cnpunct;
    class BoolNames : public npunct {
    protected:
        string do_truename() const { return "Oui Due!"; }
        string do_falsename() const { return "Mais Non!"; }
    public:
        BoolNames() {
        }
    };
}
```

§ 22.4.8

© ISO/IEC 2011 – 版权所有

```cpp
BoolNames(const char* name) : npunctcount(name) { 
}
int main(int argc, char** argv) {
  using namespace std;
  // 使用用户偏好的区域设置，除了...
  locale loc(locale(""), new My::BoolNames(""));
  cout.imbue(loc);
  cout << boolalpha << "Any arguments today?" << (argc > 1) << endl;
  return 0;
}
```

# 22.5 标准代码转换区域面

[locale.stdcvt]

+ 1 头文件 `<codecvt>` 为各种字符编码提供了代码转换区域面。

+ 2 头文件 `<codecvt>` 梗览

```cpp
namespace std {
  enum codecvt_mode {
    consume_header = 4,
    generate_endian = 2,
    little_endian = 1
  }

template<class Elem, unsigned long Maxcode = 0xffffff,
         codecvt_mode Mode = (codecvt_mode)0>
class codecvt_utf8 : public facet<Elem, char, mbstate_t> {
  // 未规定

template<class Elem, unsigned long Maxcode = 0xffffff,
         codecvt_mode Mode = (codecvt_mode)0>
class codecvt_utf16 : public facet<Elem, char, mbstate_t> {
  // 未规定

template<class Elem, unsigned long Maxcode = 0xffffff,
         codecvt_mode Mode = (codecvt_mode)0>
class codecvt_utf86 : public facet<Elem, char, mbstate_t> {
  // 未规定
};
```

+ 3 对于三个代码转换区域面 `codecvt_utf8`、`codecvt_utf16` 和 `codecvt_utf86`：

  - `Elem` 是宽字符类型，如 `wchar`、`char16_t` 或 `char32_t`。

  - `Maxcode` 是区域面在读取或写入时不报告转换错误的最宽字符代码。

# 22.5 ISO/IEC 14882:2011(E)

- 如果 `(Mode & consume_header)`，区域面在读取多字节序列时应消耗头部，以确定后续多字节序列的字节序。

- 如果 `(Mode & generate_header)`，区域面在写入多字节序列时应生成头部，告知后续多字节序列的字节序。

- 如果 `(Mode & little_endian)`，区域面应生成小端序的多字节序列，而不是大端序。

+ 4 对于区域面 `codecvt_utf8`：

- 区域面在程序中在 UTF-8 多字节序列与 UCS2 或 UCS4（取决于 `Elem` 的大小）之间转换。

- 字节序不影响多字节序列的读取或写入。

- 多字节序列可以渲染为文本文件或二进制文件。

+ 5 对于区域面 `codecvt_utf16`：

- 区域面在程序中在 UTF-16 多字节序列与 UCS2 或 UCS4（取决于 `Elem` 的大小）之间转换。

- 多字节序列根据上述 `Mode` 标志进行读取或写入。

- 多字节序列只能作为二进制文件写入。尝试写入文本会导致未定义行为。

+ 6 对于区域面 `codecvt_utf86`：

- 区域面在程序中在 UTF-8 多字节序列与 UTF-16（一个或两个16位代码）之间转换。

- 字节序不影响多字节序列的读取或写入。

- 多字节序列可以渲染为文本文件或二进制文件。

另：ISO/IEC 10646-1:1993。

# 22.6 C 库区域设置

[c.locales]

1 表 93 描述了头文件 `<locale>`。

表 93 — 头文件 `<locale>` 梗览

| 类型 | 名称(s) |

|---|---|

| 宏: | LC_ALL LC_COLLATE LC_CTYPE LC_MONETARY LC_NUMERIC LC_TIME |

| | NULL |

| 结构体: | lconv |

| 函数: | localeconv setlocale |

2 内容与标准 C 库头文件 `<locale>` 相同。

3 调用函数 `setlocale` 可能会与其他 `setlocale` 调用或第 94 节列出的函数调用产生数据竞态 (17.6.5.9)。

另：ISO C 章节 7.4。

# ISO/IEC 14882:2011(E)

| 表 94 — 潜在的 setlocale 数据竞态 |

| fprintf | isprint | isdigit | localeconv | tolower |

| --- | --- | --- | --- | --- |

| fscanf | ispunct | isgraph | mblen | toupper |

| isnalnum | isspace | islower | mbstowcs | towlower |

| isalpha | is | is | mbtow | towupper |

| isblank | is | ispununct | setlocale | wcscoll |

| iscntrl | isalpha | iswprint | mbstowcs | wcstod |

| isdigit | iswblank | isupper | stderr | wcstombs |

| isgraph | iswcntrl | iswdigit | strcoll | wcexfrm |
