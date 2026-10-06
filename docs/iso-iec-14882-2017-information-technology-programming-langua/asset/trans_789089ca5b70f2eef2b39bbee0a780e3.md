

# ISO/IEC 14882:2017(E)

```cpp
template <class money> unspecified get_money(moneyT& mon, bool intl = false);
```

要求：类型 `money` 应当是 `long double` 或 `basic_string` 模板的特化（第 24 ）。

影响：下述的 `>> get_money(mon, intl)` 中的表达式行为类似于格式化函数 (30.7.2.1)。

返回：一个未指定类型的对象，如果它是类型为 `basic_istream<charT, traits>` 的对象，则 `>> get_money(mon, intl)` 中的表达式行为就如调用了 `f(in, mon, intl)`；其中函数 `f` 定义如下：

```cpp
template <class charT, class traits, class money>
void f(basic_ios<charT, traits>& in, moneyT& mon, bool intl) {
    using Iter = istreambuf_iterator<char>;
    using Money = get_money<charT, Iter>;

    ios_base::istate err = ios_base::goodbit;
    const Money getMon = use<Money>(in.getloc());

    getMon.get(Iter(in.rdbuf()), Iter(), intl, str, err);

    if (Iter(in.rdbuf()) != err || err != fail) {
        in.setstate(err);
    }
}
```

`>> get_money(mon, intl)` 中的表达式类型应为 `basic_istream<charT, traits>&` 并返回值 `in`。

```cpp
template <class money> unspecified put_money(const moneyT& mon, bool intl = false);
```

要求：类型 `money` 应当是 `long double` 或 `basic_string` 模板的特化（第 24 ）。

返回：一个未指定类型的对象，如果它是类型为 `basic_ostream<charT, traits>` 的对象，则 `<< put_money(mon, intl)` 中的表达式行为类似于格式化函数 (30.7.5.2.1)，它调用了 `f(out, mon, intl)`，其中函数 `f` 定义如下：

```cpp
template <class charT, class traits, class money>
void f(basic_ostream<charT, traits>& out, const moneyT& mon, bool intl) {
    using Iter = ostreambuf_iterator<char>;
    using Money = put_money<charT, Iter>;

    const Money mPut = use<Money>(out.getloc());
    Iter end = mPut.put(Iter(out.rdbuf()), intl, str.fill(), mon);

    if (end.failed()) {
        out.setstate(ios_base::badbit);
    }
}
```

`<< put_money(mon, intl)` 中的表达式类型应为 `basic_ostream<charT, traits>&` 并返回值。

```cpp
template <class charT> unspecified get_time(struct tm& tmb, const charT* fmt);
```

要求：`tm mb` 应当是指向 `charT` 类型对象数组的有效指针，该数组元素个数为 `char_traits<charT>::length(fmt)`。

返回：一个未指定类型的对象，如果它是类型为 `basic_istream<charT, traits>` 的对象，则 `>> get_time(tmb, fmt)` 中的表达式行为类似于调用 `f(in, tmb, fmt)`，其中函数 `f` 定义如下：

```cpp
template <class charT, class traits>
void f(basic_ios<charT, traits>& in, istream_iterator<charT> it,
    using TimeGet = get_time<charT, traits>;
    ios_base::istate err = use_facet<TimeGet>(in.getloc());
    TimeGet::get(Iter(in.rdbuf()), Iter(), str, err, tmb,
    fmt, traits::length(fmt));

    if (err != ios_base::goodbit) {
        in.setstate(err);
    }
}
```

`>> get_time(tmb, fmt)` 中的表达式类型应为 `basic_istream<charT, traits>&` 并返回值 `in`。

```cpp
template <class charT> unspecified put_time(const struct tm* tmb, const charT* fmt);
```

要求：参数 `tmb` 应当是指向 `tm` 类型对象的有效指针，且参数 `fmt` 应当是指向 `charT` 类型对象数组的有效指针，该数组元素个数为 `char_traits<charT>::length(fmt)`。

返回：一个对象，如果 `out` 是类型为 `basic_ostream<charT, traits>` 的对象，则 `<< put_time(tmb, fmt)` 的行为类似于调用了 `f(out, tmb, fmt)`，其中函数 `f` 定义如下：

```cpp
template <class charT, class traits>
void f(basic_ostream<charT, traits>& out, const struct tm* tmb, const charT* fmt) {
    using Iter = oambuf_iterator<charT, traits>;
    using TimePut = put_time<charT, traits>;

    const TimePut tp = use_facet<TimePut>(out.getloc());
    const Iter end = tp.put(Iter(out.rdbuf()), tmb, fmt,
    fmt, fmt += traits::length(fmt));

    if (end.failed()) {
        out.setstate(ios_base::badbit);
    }
}
```

`<< put_time(tmb, fmt)` 中的表达式类型应为 `basic_ostream<charT, traits>&` 并返回 `out`。

## 30.7.8 引用操符 (Quoted manipulators)

引用操符提供了带引号字符串的插入和提取（例如 XML）。引用操符用于确保带引号的字符串在 I/O 时保持不变（例如 CSV）。

```cpp
template <class charT> quoted(charT& s, charT delim = '\"');
```

```cpp
template <class charT, class traits> quoted(basic_istream<charT, traits>& s, charT delim = '\"');
```

```cpp
template <class charT, class traits> quoted(basic_string<charT>, charT delim = ' =');
```

返回：一个未指定类型的对象，如果它是类型为 `basic_ostream<charT, traits>` 的对象，则 `<< quoted(s)` 的行为类似于一个格式化函数 (30.7.5.2.1)，它调用了 `f(out, mon, intl)`，其中函数 `f` 定义如下：

```cpp
template <class charT, class traits, class money>
void f(basic_ostream<charT, traits>& out, const moneyT& mon, bool intl) {
    using Iter = ostreambuf_iterator<char>;
    using Money = put_money<charT, Iter>;

    const Money mPut = use<Money>(out.getloc());
    Iter end = mPut.put(Iter(out.rdbuf()), intl, str.fill(), mon);

    if (end.failed()) {
        out.setstate(ios_base::badbit);
    }
}
```

`>> quoted(s)` 中的表达式类型应为 `basic_istream<charT, traits>&` 并返回值 `in`。

`<< quoted(s)` 中的表达式类型应为 `basic_ostream<charT, traits>&` 并返回 `out`。

## 30.7.8 基于字符串的流 (String-based streams)

### 30.8.1 头文件 <sstream> 概要

```cpp
namespace std {
    template <class charT, class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
    class basic_stringbuf{
        using stringbuf = basic_stringbuf<char>;
        using wstringbuf = basic_stringbuf<wchar>;

    template <class charT, class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
    class basic_istream{
        using istream = basic_istream<charT>;
        using wistream = basic_istream<wchar>;
    
    template <class charT, class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
    class basic_ostream{
        using ostream = basic_ostream<charT>;
        using wostream = basic_ostream<wchar>;
    }
}
```

<sstream> 定义四个类模板和八个类型，它们与字符串类关联，如第 24.3 所示。

## 30.8.2 类模板-basic_stringbuf

```cpp
namespace std {
    template <class charT, class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
    class basic_stringbuf : public basic_stringbuf<charT, traits> {
    public:
        using char_type = charT;
        using int_type = typename traits::int_type;
        using pos_type = typename traits::pos_type;
        using off_type = typename traits::off_type;
        using traits_type = traits;
        using Allocator = Allocator;

        // 30.8.2.1. 构造函数
        explicit basic_stringbuf(openmode mode = ios_base::in | ios_base::out);
        explicit basic_stringbuf(const charT&, traits, const Allocator& str,
        ios_base::openmode mode = ios_base::in | ios_base::out);
        basic_stringbuf(const basic_stringbuf& rhs) = delete;
        basic_stringbuf(const basic_stringbuf& rhs) = delete;
```

