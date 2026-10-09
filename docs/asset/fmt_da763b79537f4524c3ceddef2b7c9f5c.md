
## 28.4.8 消息检索分类

[category.messages]

## 28.4.8.1 通用

[category.messages.general]

类 `messages<charT>` 实现从消息目录（message catalogs）中检索字符串。

## 28.4.8.2 类模板 messages

[locale.messages]

## 28.4.8.2.1 通用

[locale.messages.general]

```cpp
namespace std {

    class messages_base {

    public:

        using catalog = unspecified integer type;

    };

}
```

283 要指定通过 `s` 分组，其值为 `"\u003"` 而不是 `"3"`。

284 这通常是空字符串。

285 在美国区域中，此值为 2。

§ 28.4.8.2.1

©ISO/IEC 2020 – 版权所有

1372

# ISO/IEC 14882:2020(E)

```cpp
template<class char>
class messages : public locale::facet, public messages_base {
public:
    using char_type = char;
    using string_type = basic_string<char_type>;
    explicit messages(size_t ref = 0);
    catalog open(const string& fn, const locale& loc) const;
    string_type get(const catalog c, int set, int msgid);
    const string_type& default(catalog c) const;
    void close(catalog c) const;
    static locale::id id;
protected:
    ~messages();
    virtual catalog do_open(const string& name, const locale& loc) const;
    virtual string_type do_get(const catalog c, int set, int msgid);
    const string_type& do_default(catalog c) const;
    virtual void do_close(catalog c) const;
};
```

+ 类型为 `messages_base::catalog` 的值作为 `get` 和 `close` 的参数，只能通过调用 `open` 获取。

## 28.4.8.2.2 成员

[locale.messages.messages]

`catalog open(const string& name, const locale& loc) const;`

+ 1 返回：`do_open(name, loc)`.

`string_type get(const catalog cat, int set, int msgid, const string_type& default) const;`

+ 2 返回：`do_get(const cat, int set, msgid, default)`.

`void close(catalog cat) const;`

+ 3 影响：调用 `do_close(cat)`.

## 28.4.8.2.3 虚函数

[locale.messages.virtuals]

`catalog open(const string& name, const locale& loc) const;`

+ 1 返回一个可以传递给 `get()` 的值，用于根据实现定义的映射从字符串名称标识的目录中检索消息。结果在使用传递给 `close()` 之前一直有效。
+ 2 如果无法打开此类目录，则返回小于 0 的值。
+ 3 备注：区域设置参数 `loc` 在检索消息时（如果需要）用于字符集转换。

`string_type_get(const catalog cat, int set, int msgid, const string_type& default) const;`

+ 4 前提条件：`cat` 从 `open()` 获取。
+ 5 返回：根据 `set`、`msgid` 和 `default` 标识的消息，具体取决于实现。

`void_close(catalog cat) const;`

+ 6 前提条件：`cat` 已获取。
+ 7 影响：释放与 `cat` 相关的资源。
+ 8 备注：取决于实现。

## 28.4.8.3 类模板 messages_byname

[locale.messages.byname]

```cpp
namespace std {
  template<class char>
  class messages_byname : public messages<char> {
  public:
    using pattern;
    using string_type<char>;
    explicit messages_byname(const char* str, size_t refs = 0);
    explicit messages_byname(const string& str, size_t refs = 0);
  protected:
    ~messages_byname();
  };
}
```

## 28.5 区域设置

[locale.locale]

## 28.5.1 头文件

[locale.synopsis]

```cpp
namespace std {
  struct lconv {
    char* locale(int);
    ~lconv();
  };
#define NULL see 17.2
#define LC_ALL see
#define LC_COLLATE see
#define LC_CTYPE see
#define LC_MONETARY see
#define LC_TIME see
}
```

`<locale>` 的内容与 `<locale>` 相同。

## 28.5.2 数据竞争

[locale.races]

调用 `locale` 可能会与 `setlocale (16.4.10)` 或表 14 中的函数产生数据竞争。

参见：7.11

| 表 14: 潜在区域竞争 |
|---|---|---|
| fprintf | isprint | widigit | localeconv | tolower |
| fscanf | ispunct | iswgraph | mlen | toupper |
| isnum | isspace | islower | mboc | towlower |
| isalpha | isnum | isupper | mtowoc | toupper |
| isblank | isalpha | isdigit | strtod | wcoll |
| iscntrl | isblank | iswidigit | strftime | wcomb |
| isigit | iscntrl | islocale | strftime | wctomb |
| isgraph | isigit | isctype | strftime | wcrm |
| islower | isgraph | islocale | strftime | wcomb |
28.5.2 结束

# ISO/IEC 14882:2020(E)

## 29 输入输出库 [input.output]

## 29.1 通用 [input.output.general]

本节描述了 C++ 程序用于输入输出操作的组件。

以下子类描述了流参数，以及 iostreams 前置声明、预定义对象、基类、流缓冲、流格式和操作符、字符串流以及流文件，如表 115 所示。

表 115：输入输出摘要 [tab:iostreams.summary]

| 子类 | 头文件 |
|---|---|
| 29.2 要求 | <iosfd> |
| 29.3 前置声明 | <iostream> |
| 29.4 标准流对象 | <iostream> |
| 29.5 基类 | <ios> |
| 29.6 流缓冲 | <streambuf> |
| 29.7 格式和操作符 | <iomanip>, <iostream> |
| 29.8 字符串流 | <sstream> |
| 29.9 文件 | <fstream> |
| 29.10 同步输出流 | <syncstream> |
| 29.11 文件系统 | <filesystem> |
| 29.12 C 库 | <cstdio>, <cctype> |

> 注 1：图 7 阐明了节描述的各种类型之间的关系。从 A 到 B 的线表示 A 是 B 的类型或 A 基于 B 定义。

![](img/8560a8c2b4b044fb6041ef0de2f9fb30_1386_0.png)

* 结束注释*

## 29.2 iostreams 要求 [iostreams.requirements]

## 29.2.1 嵌入限制 [iostream.limits.imbue]

在 29 节描述的函数中，除了 `ios_base::imbue` 和 `basic_filebuf::imbue` 之外，没有函数会调用 `basic_ios::imbue` 或 `basic_streambuf::imbue`。如果从 29 节声明的函数或作为 29 节声明的任何类的覆盖虚函数调用的用户函数调用了 `imb`，行为是未定义的。

## 29.2.2 位置类型限制

如果 `traits::pos_type` 和 `traits::off_type` 分别为 `std::stream::pos_type` 和 `std::stream_off_type`，则第 29 条中具有模板 `charT` 和 `traits` 的类行为如所述。正如下文明确指出的，当 `traits::pos_type` 和 `off_type` 为其他类型时，它们的行为由实现定义。

在第 29 条的类中，名为 `char` 的模板参数表示包含 `char_t` 的类型集合中的成员，以及任何其他满足可用于任何 `istream` 类实例化的字符要求的、由实现定义的字符类型。

## 29.2.3 线程安全

多个线程并发访问流对象 (29.8, 29.9)、流缓冲区 (29.6) 或 C 库流 (29.12) 会导致数据竞态 (6.9)，除非另有规定 (29.4)。

[注 1：数据竞态会导致未定义行为 (6.92) — 注结束]

如果两个线程执行了一个向流写入值的库调用，并导致另一个线程通过不会导致数据竞态的库调用 `b` 从流中读取该值，则 `a` 的写入与 `b` 的读取是同步的。

## 29.3 前向声明

### 29.3.1 头文件 <ioswd> 概要

```cpp
namespace std {
template<class charT> struct char_traits;
template<class charT> struct char_traits<char>;
template<class charT> struct char_traits<char8_t>;
template<class charT> struct char_traits<char16_t>;
template<class charT> struct char_traits<char32_t>;
template<class charT> struct char_traits<wchar_t>;
template<class T> class allocator;
```

```cpp
template<class charT, class traits = char_traits<charT>>
class basic_ios;
template<class charT, class traits = char_traits<charT>>
class basic_streambuf;
template<class charT, class traits = char_traits<charT>>
class basic_istream;
template<class charT, class traits = char_traits<charT>>
class basic_ostream;
template<class charT, class traits = char_traits<charT>>
class basic_ostream;
template<class charT, class traits = char_traits<charT>>
class basic_istreambuf;
template<class charT, class traits = char_traits<charT>>
class Allocator = allocator<charT>;
class basic_stringbuf;
template<class charT, class traits = char_traits<charT>>
class Allocator = allocator<charT>;
class basic_stringstream;
template<class charT, class traits = char_traits<charT>>
class Allocator = allocator<charT>;
class basic_string_ostream;
template<class charT, class traits = char_traits<charT>>
class Allocator = allocator<charT>;
class basic_stringstream;
template<class charT, class traits = char_traits<charT>>
class basic_filebuf;
template<class charT, class traits = char_traits<charT>>
class basic_istream;
template<class charT, class traits = char_traits<charT>>
class basic_ofstream;
template<class charT, class traits = char_traits<charT>>
class basic_fstream;
```

# ISO/IEC 14882:2020(E)

```cpp
template<class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT>
class basic_syncbuf;
template<class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT>
class basic_osstream;
template<class charT, class traits = char_traits<charT>>
class istreambuf_iterator;
template<class charT, class traits = char_traits<charT>>
class ostreambuf_iterator;
using ios = basic_ios<char>;
using wins = basic_ios<char>;
using istreambuf = basic_istreambuf<char>;
using istream = basic_istream<char>;
using ostream = basic_ostream<char>;
using iostream = basic_iostream<char>;
using stringbuf = basic_stringbuf<char>;
using istringstream = basic_stringstream<char>;
using ostrestream = basic_ostringstream<char>;
using stringstream = basic_stringstream<char>;
using filebuf = basic_filebuf<char>;
using ifstream = basic_ifstream<char>;
using ofstream = basic_ofstream<char>;
using fstream = basic_fstream<char>;
using syncbuf = basic_syncbuf<char>;
using osyncstream = basic_osyncstream<char>;
using wstreambuf = basic_wstreambuf<wchar_t>;
using wistream = basic_wistream<wchar_t>;
using wostream = basic_ostream<wchar_t>;
using wiostream = basic_iostream<wchar_t>;
using wfilebuf = basic_wfilebuf<wchar_t>;
using wstream = basic_wifstream<wchar_t>;
```
