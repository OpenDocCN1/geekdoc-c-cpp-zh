
```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::floatfield flags);
}
```

1 影响：调用 `out.setf(flags)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::floatfield flags);
}
```

1 影响：调用 `out.unsetf(flags)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::xbase flags);
}
```

1 影响：调用 `out.setf(flags)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::xbase flags);
}
```

1 影响：调用 `out.unsetf(flags)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::fmtflag flags, int mask);
}
```

1 影响：调用 `out.setf(flags, mask)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::fmtflag flags, int mask);
}
```

1 影响：调用 `out.unsetf(flags, mask)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::floatfield flags, int mask);
}
```

1 影响：调用 `out.setf(flags, mask)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::floatfield flags, int mask);
}
```

1 影响：调用 `out.unsetf(flags, mask)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::xbase flags, int mask);
}
```

1 影响：调用 `out.setf(flags, mask)`。

2 返回：`*this`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::xbase flags, int mask);
}
```

1 影响：调用 `out.unsetf(flags, mask)`。

2 返回：`*this`。

`base == 16 ? ios_base::hex :`

`ios_base::setfmtflags(str.flags(), ios_base::basefield);`

}

表达式 `<< setbase(base)` 的类型应为 `basic_ostream<charT, traits>&` 且值为

表达式 `in >> setbase(base)` 的类型应为 `basic_istream<charT, traits>&` 且值为 `in`。

`unspecified setfill(charT c);`

- 返回：一个未指定的类型对象，如果 `out` 是类型为 `basic_ostream<charT, traits>` 的对象且 `c` 的类型为 `charT`，则表达式 `<< setfill(c)` 的行为等同于调用了 `f(out, c)`，其中函数 `f` 定义如下：

```cpp
template<class charT, class traits>
void f(basic_ios<charT,traits>& str, charT c) {
// 填充字符
str.fill(c);
}
```

表达式 `<< setfill(c)` 的类型应为 `basic_ostream<charT, traits>&` 且值为 `value`。

`unspecified setprecision(int n);`

- 返回：一个未指定的类型对象，如果 `out` 是类型为 `basic_ostream<charT, traits>` 的对象，则表达式 `<< setprecision(n)` 的行为等同于调用了 `f(out, n)`，或者如果 `in` 是类型为 `basic_istream<charT, traits>` 的对象，则表达式 `in >> setprecision(n)` 的行为等同于调用了 `f(in, n)`，其中函数 `f` 定义如下：

```cpp
void f(ios_base& str, int n) {
// 设置精度
str.precision(n);
}
```

表达式 `<< setprecision(n)` 的类型应为 `basic_ostream<charT, traits>&` 且值为 `out`，表达式 `in >> setprecision(n)` 的类型应为 `basic_istream<charT, traits>&` 且值为 `in`。

`unspecified setw(int n);`

- 返回：一个未指定的类型对象，如果 `out` 是 `basic_ostream<charT, traits>` 的实例，则表达式 `<< setw(n)` 的行为等同于调用了 `f(out, n)`，或者如果 `in` 是类型为 `basic_istream<charT, traits>` 的对象，则表达式 `in >> setw(n)` 的行为等同于调用了 `f(in, n)`，其中函数 `f` 定义如下：

```cpp
void f(ios_base& str, int n) {
// 设置宽度
str.width(n);
}
```

表达式 `<< setw(n)` 的类型应为 `basic_ostream<charT, traits>&` 且值为 `out`。表达式 `in >> setw(n)` 的类型应为 `basic_istream<charT, traits>&` 且值为 `in`。

## 27.7.5 扩展操纵符

头文件 `iomanip` 定义了多个支持提取器和插入器的函数，允许对货币和时间的序列及值进行解析和格式化。

§ 27.7.5

```cpp
template <class moneyT> unspecified get_money(moneyT& mon, bool intl = false);
```

要求：类型 `moneyT` 应当是 `long double` 或 `basic_string` 模板的特化（第 21 节）。

影响：下述表达式 `in >> get_money(mon, intl)` 的行为类似于格式化输入（第 27.7.2.1 节）。

返回：一个未指定的类型对象，如果 `in` 是类型为 `basic_istream<charT, traits>` 的对象，则表达式 `in >> get_money(mon, intl)` 的行为等同于调用了 `f(in, mon, intl)`，其中函数 `f` 定义为：

```cpp
template <class charT, class traits, class moneyT>
void f(basic_istream<charT, traits>& in, moneyT& mon, bool intl) {
    typedef istreambuf_iterator<charT, traits> Iter;
    typedef money_get<charT, Iter> MoneyGet;

    ios_base::state err = ios_base::goodbit;
    const MoneyGet &mg = use_facet<MoneyGet>(in.getloc());
    mg(Iter(in.strdbuf()), Iter(), intl, err);

    if (in.fail()) {
        in.setstate(err);
    }
}
```

表达式 `in >> get_money(mon, intl)` 的类型应为 `basic_istream<charT, traits>&` 且值为 `in`。

```cpp
template <class moneyT> unspecified put_money(const moneyT& mon, bool intl = false);
```

要求：类型 `moneyT` 应当是 `long double` 或 `basic_string` 模板的特化（第 21 节）。

返回：一个未指定的类型对象，如果 `out` 是类型为 `basic_ostream<charT, traits>` 的对象，则表达式 `<< put_money(mon, intl)` 的行为类似于格式化输出并调用了 `f(out, mon, intl)`，其中函数 `f` 定义为：

```cpp
template <class charT, class traits, class moneyT>
void f(basic_ostream<charT, traits>& out, const moneyT& mon, bool intl) {
    typedef istreambuf_iterator<charT, traits> Iter;
    typedef money_put<charT, Iter> MoneyPut;

    const MoneyPut &mp = use_facet<MoneyPut>(out.getloc());
    const Iter end = mp.put(out.strdbuf()), Iter(), mon, intl);

    if (end.fail()) {
        out.setstate(ios::badbit);
    }
}
```

表达式 `<< put_money(mon, intl)` 的类型应为 `basic_ostream<charT, traits>&` 且值为 `out`。

要求：`out` 应当是指向类型为 `basic_ostream` 对象的有效指针，且 `fmt` 应当是指向类型为 `charT` 且对象数组的有效指针。

```cpp
template <class charT> unspecified get_time(tm& tmb, const charT* fmt);
```

返回：一个未指定的类型对象，如果 `in` 是类型为 `basic_istream<charT, traits>` 的对象，则表达式 `in >> get_time(tmb, fmt)` 的行为类似于调用了 `f(in, tmb, fmt)`，其中函数 `f` 定义为：

```cpp
template <class charT, class traits>
void f(basic_ios<charT, traits>& str, tm* tmb, const charT* fmt) {
    typedef strreambuf_iterator<charT, traits> Iter;
    typedef time_get<charT, Iter> Timeget;

    ios_base::state err = ios_base::goodbit;
    const Timeget& tg = use<Timeget>(str.getloc());
    tg.get(Iter(str.strdbuf()), Iter(), tmb, fmt, err);

    if (err) {
        str.setstate(err);
    }
}
```

表达式 `in >> get_time(tmb, fmt)` 的类型应为 `basic_istream<charT, traits>&` 且值为 `in`。

```cpp
template <class charT> unspecified put_time(tm* tmb, const charT* fmt);
```

返回：一个未指定的类型对象，如果 `out` 是类型为 `basic_ostream<charT, traits>` 的对象，则表达式 `<< put_time(tmb, fmt)` 的行为类似于调用了 `f(out, tmb, fmt)`，其中函数 `f` 定义为：

```cpp
template <class charT, class traits>
void f(basic_ios<charT, traits>& str, tm* tmb, const charT* fmt) {
    typedef strreambuf_iterator<charT, traits> Iter;
    typedef time_put<charT, Iter> TimePut;

    const TimePut tp = use<TimePut>(str.getloc());
    const Iter end = tp.put(str.strdbuf(), Iter(), tmb, fmt);

    if (end.fail()) {
        str.setstate(ios_base::badbit);
    }
}
```

表达式 `<< put_time(tmb, fmt)` 的类型应为 `basic_ostream<charT, traits>&` 且值为 `out`。

## 27.8 基于字符串的流

## 27.8.1 概述

1. 头文件 `<sstream>` 定义了四个类模板和八种类型，将缓冲区与 `basic_string` 类对象关联，参见第 21.3 节。

头文件 `<sstream>` 概要

```cpp
namespace std {
template <class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT >
class basic_stringbuf{
    typedef basic_stringbuf<char> stringbuf;
    typedef basic_stringbuf<wchar_t> wstringbuf;
};
template <class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT >
class basic_stringstream{
    typedef basic_stringstream<char> istringream;
    typedef basic_stringstream<wchar_t> wstringstream;
};
template <class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT >
class basic_ostream{
    typedef basic_ostream<char> ostringream;
    typedef basic_ostream<wchar_t> wstringream;
};
```

## 27.8.2 类模板 basic_stringbuf
