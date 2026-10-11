
- 新迭代器可以作为基类，以简化新迭代器所需类型的定义。
- [注意：如果新迭代器是基类模板，那么这些别名在迭代器类的定义内部不可见，仅对该类的调用者可见。]
- [示例：如果一个 C++ 程序想要为包含 `double` 的数据结构定义双向迭代器，并且在实现的大型内存上工作，可以这样做：

```cpp
class MyIterator : public iterator<bidirectional_iterator_tag, double, long, T*> {
    // 实现 ++ 等代码
};
```

# ISO/IEC 14882:2017(E)

```cpp
public:
    explicit codevct_utf8(size_t refs = 0);
    ~codevct_utf8();
```

```cpp
template <class Elm, unsigned long Maxime = 0x0ffff, codevct_mode Mode = (codevct_mode)>
class codevct_utf16 : public codevctElem<Elm, char, mbstate_t> {
public:
    explicit codevct_utf16(size_t refs = 0);
    ~codevct_utf16();
};
```

```cpp
template <class Elm, unsigned long Maxime = 0x0ffff, codevct_mode Mode = (codevct_mode)>
class codevct_utf8_utf16 : public codevctElem<Elm, char, mbstate_t> {
public:
    explicit codevct_utf8_utf16(size_t refs = 0);
    ~codevct_utf8_utf16();
};
```

## D.15.2 要求 [depr.locale.stdct.req]

- 1 对于三种转换面 `codevct_utf8`、`codevct_utf16` 和 `codevct_utf8_utf16` 中的每一个：
    - (1.1) `Elm` 是宽字符类型，如 `wchar`、`char16_t` 或 `char32_t`。
    - (1.2) `Maxime` 是转换面在读取或写入时不报告转换错误的最大宽字符。
    - (1.3) 如果满足 (`Mode` & `consumer_header`)，则该转换面在读取多字节序列时，应当消耗一个初始头部序列（如果存在），以确定后续待读取多字节序列的字节序。
    - (1.4) 如果满足 (`Mode` & `generate_header`)，则该转换面在写入多字节序列时，应当生成一个初始头部序列，以处理后续待写入的多字节序列的字节序。
    - (1.5) 如果满足 (`Mode` & `little_endian`)，该转换面应当以小端序而非大端序生成多字节序列。
- 2 对于转换面 `codevct_utf8`：
    - (2.1) 该转换面应在程序内部 UTF-8 多字节序列与 UCS2 或 UCS4（取决于 `Elm` 的大小）之间转换。
    - (2.2) 字节序不影响多字节序列的读取或写入方式。
    - (2.3) 多字节序列可以以文本文件或二进制文件的格式写入。
- 3 对于转换面 `codevct_utf8_utf16`：
    - (3.1) 该转换面应在程序内部 UTF-16 多字节序列与 UCS2 或 UCS4（取决于 `Elm` 的大小）之间转换。
    - (3.2) 多字节序列应当按照上述设置的 `Mode` 标志进行写入或读取。
    - (3.3) 多字节序列只能以二进制文件的格式写入。尝试写入文本文件将产生未定义行为。
- 4 对于转换面 `codevct_utf8_utf16`：
    - (4.1) 该转换面应在程序内部 UTF-8 多字节序列与 UTF-16（一个或两个位代码）之间转换。
    - (4.2) 字节序不影响多字节序列的读取或写入方式。
    - (4.3) 多字节序列可以以文本文件或二进制文件的格式写入。

另见：ISO/IEC 10646-1:1993。

## D.16 弃用的转换接口

`<locale>` 头文件包含以下新增：

```cpp
namespace std {
    template <Codecvt, class E, class Wide_alloc = allocator<char>>
    wstring_convert;
    template <Codecvt, class Elem = wchar_t, class Byte_alloc = allocator<char>>
    wstring_convert;
```

## D.16.1 wstring_convert 类

`wstring_convert` 类用于宽字符串与多字节字符串之间的转换。它允许指定转换面（如 `codecvt`）来执行转换，而不影响 `locale`。如果你想使用转换面写入 UTF-8 字符串，例如：

```cpp
wstring_convert<codevct_utf8> myconv;
myconv.to_bytes(L"Hello");
std::cout << nstring;
```

```cpp
namespace std {
    template <Codecvt, class Elem = wchar_t, class Wide_alloc = allocator<char>>
    class wstring_convert {
    public:
        using byte_string = basic_string<char, char_traits<char>, Byte_alloc>;
        using wstring = basic_string<Elem, char_traits<Elem>, Wide_alloc>;
        using state_type = typename Codecvt::state_type;
        using int_type = typename Codecvt::int_type;
        wstring_convert(Codecvt* pcvt = new Codecvt);
        wstring_convert(Codecvt* pcvt, state_type state);
        wstring_convert(const wstring& wide_err);
        wstring_convert(const wstring& wide_err);
        ~wstring_convert();
        wstring_convert(const wstring_convert&) = delete;
        wstring_convert& operator=(const wstring_convert&) = delete;
        byte_string from_bytes(Elem byte);
        byte_string from_bytes(const char* ptr);
        byte_string from_bytes(const byte_string& str);
        byte_string from_bytes(const char* first, const char* last);
        wstring to_bytes(Elem wchar);
        wstring to_bytes(const wstring& wstr);
        wstring to_bytes(const Elem* first, const Elem* last);
        size_t converted() const noexcept;
        state_type state() const;
    private:
        byte_string byte_err_string;
        wstring wide_err_string;
        Codecvt cvptr;
        state_type cvstate;
        size_t cvcount;
    };
```

# ISO/IEC 14882:2017(E)

## D.16.2 类模板 wbuffer_convert

类模板 `wbuffer_convert` 看起来像一个宽字符流缓冲区，但它通过一个你在构造函数时指定的底层字节流执行所有的 I/O 操作。与类模板 `wstring_convert` 一样，它允许你指定一个转换因子（conversion facet）来执行转换，而不会影响任何状态或区域（locales）。

```cpp
namespace std {
template <class Codec, class E = char, class Tr = char_traits<Elem>>
class wbuffer_convert : public basic_stream<Elem, Tr> {
public:
    using state_type = typename Codec::state_type;
    explicit wbuffer_convert(streambuf* bytebuf, Codec* pcvt = nullptr, state_type state = state_type());
    virtual ~wbuffer_convert();
    wbuffer_convert(const wbuffer_convert&) = delete;
    wbuffer_convert& operator=(const wbuffer_convert&) = delete;
    streambuf* rdbuf() const;
    streambuf* rdbuf(streambuf* bytebuf);
    state_type state() const;
private:
    streambuf* bufptr; // 仅供说明
    Codec* pcvt; // 仅供说明
    state_type cvstate; // 仅供说明
};
```

- 该类模板描述了一个流缓冲区，它控制 `Elem` 元素的传输，其字符特征由类 `Tr` 描述，并由类型为 `streambuf` 的流缓冲区处理。`Elem` 序列与多字节序列之间的转换由 `Codec` 类的对象完成，该对象应满足标准转换因子 `codecvt<Elem, char, mstate_t>` 的要求。

- 该类模板的对象存储了：
    - `bufptr` — 指向底层字节流缓冲区的指针
    - `pcvt` — 指向已分配转换对象的指针（该对象在 `wbuffer_convert` 对象析构时释放）
    - `cvstate` — 一个转换状态对象

```cpp
state_type state() const;
```
返回：`cvstate`。

```cpp
streambuf* rdbuf() const;
```
返回：`bufptr`。

```cpp
streambuf* rdbuf(streambuf* bytebuf);
```
影响：将 `bytebuf` 存储在 `bufptr` 中。
返回：`bufptr` 的 的旧值。

```cpp
using state_type = typename Codecvt::state_type;
```
该类型应为 `Codecvt::state_type` 的别名。

```cpp
explicit wbuffer_convert(streambuf* bytebuf = nullptr, Codecvt* pcvt = new Codecvt, state_type state = state_type());
```
要求：`pcvt != nullptr`。
影响：构造函数构造流缓冲区对象，初始化 `bufptr` 为 `bytebuf`，初始化 `pcvt` 为 `pcvt`，并初始化 `cvstate` 为 `state`。

```cpp
virtual ~wbuffer_convert();
```
影响：析构函数应删除 `pcvt`。
