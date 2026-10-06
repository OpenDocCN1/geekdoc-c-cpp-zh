

# ISO/IEC 14882:2017(E)

```cpp
ios_base::nouppercase(ios_base& str);
ios_base::unitbuf(ios_base& str);
ios_base::nounitbuf(ios_base& str);
// 30.5.6.2. adjustfield
ios_base::internal(ios_base& str);
ios_base::left(ios_base& str);
ios_base::right(ios_base& str);
}
// 30.5.6.3. basefield
ios_base::dec(ios_base& str);
ios_base::hex(ios_base& str);
ios_base::oct(ios_base& str);
// 30.5.6.4. floatfield
ios_base::fixed(ios_base& str);
ios_base::scientific(ios_base& str);
ios_base::hexfloat(ios_base& str);
ios_base::defaultfloat(ios_base& str);
// 30.5.6.5. error reporting
enum class io_errc {
    stream = 1;
};

template <class> struct is_error_code_enum<io_errc> : public true_type { };

error_code make_error_code(io_errc e) noexcept;
error_condition make_condition(io_errc e) noexcept;
const category& iostream_category(0);
```

## 30.5.2 类型

using streamoff = implementation-defined;

- 1 streamoff 是其中一种有符号整数类型的别名，其大小足以表示操作系统下最大可能的文件大小。
- 2 using streamsize = implementation-defined; 类型 streamsize 是其中一种有符号整数类型的别名。它用于表示在 I/O 操作中传输的字符数，或 I/O 缓冲区的大小。

> 290) 通常为 long。在大多数 ISO C 使用 size_t 的地方，都使用了 streamsize，但除了 strebuf 构造函数外，这些地方都使用 streamsize，它可以携带负值。它可能应该是与 size_t 对应的有符号类型（这就是 Posix2 中称为 size_t 的类型）。

## 30.5.3 类 ios_base

```cpp
namespace std {
class ios_base {
public:
class failure; // 下文
// 30.5.9.2. flags
using long flags = 71;
```

```cpp
static const fmtflags boolalpha = unspecified;
static const fmtflags deg = unspecified;
static const fmtflags fixed = unspecified;
static const fmtflags hex = unspecified;
static const fmtflags internal = unspecified;
static const fmtflags left = unspecified;
static const fmtflags oct = unspecified;
static const fmtflags right = unspecified;
static const fmtflags scientific = unspecified;
static const fmtflags showbase = unspecified;
static const fmtflags showpoint = unspecified;
static const fmtflags showpos = unspecified;
static const fmtflags skip = unspecified;
static const fmtflags unified = unspecified;
static const fmtflags uppercase = unspecified;
static const fmtflags adjustfield = see below;
static const fmtflags basefield = see below;
static const fmtflags floatfield = see below;
```

```cpp
// 30.5.3.3, iostate
using iostate = t72;
static const iostate badbit = unspecified;
static const iostate eofbit = unspecified;
static const iostate failbit = unspecified;
static const iostate goodbit = see below;
```

```cpp
// 30.5.3.4, openmode
using openmode = t73;
static const openmode app = unspecified;
static const openmode ate = unspecified;
static const openmode binary = unspecified;
static const openmode in = unspecified;
static const openmode out = unspecified;
static const openmode trunc = unspecified;
```

```cpp
// 30.5.3.5, seekdir
using seekdir = t74;
static const seekdir beg = unspecified;
static const seekdir cur = unspecified;
static const seekdir end = unspecified;
```

```cpp
class Insert;
// 30.5.3.2, fmtflags
fmtflags flags() const;
fmtflags flags(fmtflags m);
fmtflags setf(fmtflags f);
fmtflags setf(fmtflags f, fmtflags mask);
void unset(fmtflags mask);
```

```cpp
streamsize precision() const;
streamsize precision(streamsize prec);
streamsize width() const;
streamsize width(streamsize wide);
```

```cpp
// 30.5.9.3, locales
locale imbue(const locale& loc);
locale getloc() const;
```

```cpp
// 30.5.9.5, storage
static int xalloc();
long* iword(int index);
void* pword(int index);
```

```cpp
// 析函数
virtual ~ios_base();
```

```cpp
// 30.5.6.6, callbacks
enum event { erase_event, imbue_event, copy_event };
using event_callback = void (*)(event, ios_base, int);
void register_callback(event_callback fn, int index);
```

```cpp
ios_base(const ios_base&) = delete;
ios_base& operator=(const ios_base&) = delete;
static bool sync_with_stdio(bool sync = true);
```

protected:
ios_base()();

private:
static int index; // 仅用于说明
long* array; // 仅用于说明
void** array; // 仅用于说明
}

1 ios_base 定义了几个成员类型：
- (1.1) - 一个类型 failure，定义为派自 system_error 的类，或派自 system_error 的类的别名；
- (1.2) - 一个类；
- (1.3) - 三种位掩码类型 fmtflags, iostate, openmode；
- (1.4) - seekdir。

2 ios_base 维护了若干数据：
- (2.1) - 状态信息；
- (2.2) - 关于如何解释序列；
- (2.3) - 用于生成序列的信息。

> 注意：为了说明，这里维护的数据如下：

3 (3.1) static index 仅用于说明，初始化为未指定值；
- long* array 指向未指定的整数数组，仅用于说明；
- void** array 指向未指定的指针数组，仅用于说明。

## 3.0.5.3 类型

### 30.5.3.1 类 ios_base::failure [ios::failure]

```cpp
namespace std {
    class ios_base::failure : public system_error {
    public:
        explicit failure(const string& m, error_code ec);
        explicit failure(const char* m, error_code ec);
    };
}
```

实现允许将 ios_base::failure 定义为与 ios_base::failure 功能等同的子类的别名。当 ios_base::failure 异常发生时，应通过 ec 的值来识别失败的具体原因。

[注意：来自操作系统的错误通常会被报告为 system_category()，其错误值为操作系统报告的错误值。来自流库的错误通常会被报告为 error_code(io_errc::stream, iostream_category())。]

```cpp
explicit failure(const string& m, error_code ec);
```
影响：通过 msg 和 ec 构造类对象。

```cpp
explicit failure(const char* m, error_code ec);
```
影响：通过 msg 和 ec 构造类对象。

### 30.5.3.1.2 类型 ios_base::fmtflags [ios::fmtflags]

- using fmtflags = 73;
类型 fmtflags 是位掩码类型（20.4.2.1.4）。设置其元素的影响见表 107。

- 类型 fmtflags 还定义了表 108 中的常量。

### 30.5.3.1.3 类型 ios_base::iostate [ios::iostate]

- using iostate = 72;
类型 iostate 是位掩码类型（20.4.2.1.4），包含了表 109 所示的元素。
类型 iostate 还定义了常量 good，其值为零。

### 30.5.3.1.4 类型 ios_base::openmode [ios::openmode]

- using openmode = 73;
类型 openmode 是位掩码类型（20.4.2.1.4）。它包含了表 110 所示的元素。

