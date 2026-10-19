

# ISO/IEC 14882:2020(E)

## 28.4.8.3 类模板 messages_byname [locale.messages.byname]

```
namespace std {
    template<class charT>
        class messages_byname : public messages<charT> {
        public:
            using catalog    = messages_base::catalog;
            using string_type = basic_string<charT>;

            explicit messages_byname(const char*, size_t refs = 0);
            explicit messages_byname(const string&, size_t refs = 0);

        protected:
            ~messages_byname();
        };
    }
```

## 28.5 C 库本地化 [c.locales]

## 28.5.1 头文件 <clocale> 概要 [clocale.syn]

```
namespace std {
    struct lconv;

    char* setlocale(int category, const char* locale);
    lconv* localeconv();
}
```

#define NULL see 17.2.3
#define LC_ALL see below
#define LC_COLLATE see below
#define LC_CTYPE see below
#define LC_MONETARY see below
#define LC_NUMERIC see below
#define LC_TIME see below

1 头文件 <clocale> 的内容和含义与 C 标准库头文件 <locale.h> 相同。

## 28.5.2 数据竞争 [clocale.data.races]

1 对函数 setlocale 的调用可能会引入数据竞争（16.4.6.10），与对 setlocale 的其他调用或与表 114 中列出的函数调用发生竞争。

另请参阅：ISO C 7.11

表 114：潜在的 setlocale 数据竞争 [tab:setlocale.data.races]

| fprintf | isprint | iswdigit | localeconv | tolower |
| fscanf | ispunct | iswgraph | mblen | toupper |
| isalnum | isspace | iswlower | mbstowcs | towlower |
| isalpha | isupper | iswprint | mbtowc | towupper |
| isblank | iswalnum | iswpunct | setlocale | wcscoll |
| iscntrl | iswalpha | iswspace | strcoll | wcstod |
| isdigit | iswblank | iswupper | strerror | wcstombs |
| isgraph | iswcntrl | iswxdigit | strtod | wcsxfrm |
| islower | iswctype | isxdigit | strxfrm | wctomb |
| islower | iswctype | isxdigit | strxfrm | wctomb |

## 29.2.2 定位类型限制 [iostream.limits.pos]

1 第 29 条款中具有模板参数 charT 和 traits 的类，如果 traits::pos_type 和 traits::off_type 分别为 streampos 和 streamoff，则按所述方式行为。除非下面明确说明，否则当 traits::pos_type 和 traits::off_type 为其他类型时的行为是实现定义的。

2 在第 29 条款的类中，模板参数 charT 表示包含 char、wchar_t 以及任何其他实现定义的字符类型的集合的成员，这些字符类型满足可在其上实例化任何 iostream 组件的字符要求。

## 29.2.3 线程安全 [iostream.threadsafety]

1 多个线程对流对象（29.8、29.9）、流缓冲对象（29.6）或 C 库流（29.12）的并发访问，除非另有规定（29.4），否则可能导致数据竞争（6.9.2）。

> [Note 1: 数据竞争会导致未定义行为（6.9.2）。 — end note]

2 如果一个线程进行写入流值的库调用 a，并且因此另一个线程通过库调用 b 从流中读取该值，使得这不会导致数据竞争，则 a 的写入与 b 的读取同步。

## 29.3 前向声明 [iostream.forward]

## 29.3.1 头文件 <iosfwd> 概要 [iosfwd.syn]

```
namespace std {
  template<class charT> struct char_traits;
  template<> struct char_traits<char>;
  template<> struct char_traits<char8_t>;
  template<> struct char_traits<char16_t>;
  template<> struct char_traits<char32_t>;
  template<> struct char_traits<wchar_t>;

  template<class T> class allocator;

  template<class charT, class traits = char_traits<charT>>
    class basic_ios;
  template<class charT, class traits = char_traits<charT>>
    class basic_streambuf;
  template<class charT, class traits = char_traits<charT>>
    class basic_istream;
  template<class charT, class traits = char_traits<charT>>
    class basic_ostream;
  template<class charT, class traits = char_traits<charT>>
    class basic_iostream;

  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_stringbuf;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_istringstream;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_ostringstream;
  template<class charT, class traits = char_traits<charT>,
           class Allocator = allocator<charT>>
    class basic_stringstream;

  template<class charT, class traits = char_traits<charT>>
    class basic_filebuf;
  template<class charT, class traits = char_traits<charT>>
    class basic_ifstream;
  template<class charT, class traits = char_traits<charT>>
    class basic_ofstream;
  template<class charT, class traits = char_traits<charT>>
    class basic_fstream;
}
```

# ISO/IEC 14882:2020(E)

(3.1) — static int index，指定为程序私有使用的整数或指针数组维护的下一个可用唯一索引，初始化为未指定值；

(3.2) — long* iarray，指向为程序私有使用维护的任意长度 long 数组的第一个元素；

(3.3) — void** parray，指向为程序私有使用维护的任意长度指针数组的第一个元素。

— end note]

## 29.5.3.2 类型 [ios.types]

## 29.5.3.2.1 类 ios_base::failure [ios.failure]

```
namespace std {
class ios_base::failure : public system_error {
public:
    explicit failure(const string& msg, const error_code& ec = io_errc::stream);
    explicit failure(const char* msg, const error_code& ec = io_errc::stream);
};
}
```

1 实现可以定义 ios_base::failure 为与本小节中所示的类 ios_base::failure 功能等效的类的同义词。

> [Note 1: 当 ios_base::failure 是另一个类型的同义词时，该类型需要提供嵌套类型 failure 以模拟注入类名。 — end note]

类 failure 定义了由 iostreams 库中的函数在流缓冲操作期间检测到错误时作为异常抛出的所有对象的类型的基类。

2 在抛出 ios_base::failure 异常时，实现应提供标识失败具体原因的 ec 值。

> [Note 2: 源自操作系统的错误通常会作为 system_category() 错误报告，其错误值为操作系统报告的错误号。源自流库内部的错误通常会作为 error_code(io_errc::stream, iostream_category()) 报告。 — end note]

```
explicit failure(const string& msg, const error_code& ec = io_errc::stream);
```

3 效果：使用 msg 和 ec 构造基类。

```
explicit failure(const char* msg, const error_code& ec = io_errc::stream);
```

4 效果：使用 msg 和 ec 构造基类。

## 29.5.3.2.2 类型 ios_base::fmtflags [ios.fmtflags]

```
using fmtflags = T1;
```

1 类型 fmtflags 是一个位掩码类型（16.3.3.3.4）。设置其元素的效果如表 116 所述。

2 类型 fmtflags 还定义了表 117 中指示的常量。

## 29.5.3.2.3 类型 ios_base::iostate [ios.iostate]

```
using iostate = T2;
```

1 类型 iostate 是一个位掩码类型（16.3.3.3.4），包含表 118 中指示的元素。

2 类型 iostate 还定义了常量：

+   (2.1) — goodbit，值为零。

## 29.5.3.2.4 类型 ios_base::openmode [ios.openmode]

```
using openmode = T3;
```

1 类型 openmode 是一个位掩码类型（16.3.3.3.4）。它包含表 119 中指示的元素。

## 29.5.3.2.5 类型 ios_base::seekdir [ios.seekdir]

```
using seekdir = T4;
```

1 类型 seekdir 是一个枚举类型（16.3.3.3.3），包含表 120 中指示的元素。

