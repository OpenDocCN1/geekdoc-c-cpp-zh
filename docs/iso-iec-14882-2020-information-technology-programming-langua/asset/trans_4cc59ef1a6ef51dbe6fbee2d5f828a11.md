

## ISO/IEC 14882:2020(E)

2 [注1：类模板 basic_filebuf 将文件视为字节的源或汇。在使用大字符集的环境中，文件通常保存多字节字符序列，basic_filebuf 对象会将这些多字节序列转换为宽字符序列。— 结束注]

3 在子条款 29.9 中，接受 const filesystem::path::value_type* 参数的成员函数仅在 filesystem::path::value_type（29.11.6）不是 char 的系统上提供。

> [注2：这些函数使类 path 能够支持具有本机宽路径字符类型（如 wchar_t）的系统。— 结束注]

## 29.9.2 类模板 basic_filebuf [filebuf]

### 29.9.2.1 概述 [filebuf.general]

```
namespace std {
template<class charT, class traits = char_traits<charT>>
class basic_filebuf : public basic_streambuf<charT, traits> {
public:
    using char_type = charT;
    using int_type = typename traits::int_type;
    using pos_type = typename traits::pos_type;
    using off_type = typename traits::off_type;
    using traits_type = traits;

    // 29.9.2.2, constructors/destructor
    basic_filebuf();
    basic_filebuf(const basic_filebuf&) = delete;
    basic_filebuf(basic_filebuf&& rhs);
    virtual ~basic_filebuf();

    // 29.9.2.3, assign and swap
    basic_filebuf& operator=(const basic_filebuf&) = delete;
    basic_filebuf& operator=(basic_filebuf&& rhs);
    void swap(basic_filebuf& rhs);

    // 29.9.2.4, members
    bool is_open() const;
    basic_filebuf* open(const char* s, ios_base::openmode mode);
    basic_filebuf* open(const filesystem::path::value_type* s, ios_base::openmode mode); // wide systems only; see 29.9.1
    basic_filebuf* open(const string& s, ios_base::openmode mode);
    basic_filebuf* open(const filesystem::path& s, ios_base::openmode mode);
    basic_filebuf* close();

protected:
    // 29.9.2.5, overridden virtual functions
    streamsize showmanyc() override;
    int_type underflow() override;
    int_type uflow() override;
    int_type pbackfail(int_type c = traits::eof()) override;
    int_type overflow (int_type c = traits::eof()) override;

    basic_streambuf<charT, traits>* setbuf(char_type* s, streamsize n) override;
    pos_type seekoff(off_type off, ios_base::seekdir way, ios_base::openmode which = ios_base::in | ios_base::out) override;
    pos_type seekpos(pos_type sp, ios_base::openmode which = ios_base::in | ios_base::out) override;
    int sync() override;
    void imbue(const locale& loc) override;
};

template<class charT, class traits>
    void swap(basic_filebuf<charT, traits>& x,
              basic_filebuf<charT, traits>& y);
}
```

1 类 basic_filebuf<charT, traits> 将输入序列和输出序列均与文件关联。

2 对由 basic_filebuf<charT, traits> 类对象控制的序列进行读写时，其限制与使用 C 标准库 FILE 进行读写时相同。

3 特别地：

- (3.1) — 如果文件未以读取方式打开，则不能读取输入序列。
- (3.2) — 如果文件未以写入方式打开，则不能写入输出序列。
- (3.3) — 输入序列和输出序列共同维护一个联合文件位置。

4 若 traits::pos_type 为 fpos<traits::state_type>，则 basic_filebuf 实例的行为如 29.9.2 所述。否则行为未定义。

5 为了支持文件 I/O 以及多字节/宽字符转换，转换使用某个 facet 的成员执行，以下子条款中称之为 a_codecvt，该 facet 按以下方式获得：

```
const codecvt<charT, char, typename traits::state_type>& a_codecvt =
    use_facet<codecvt<charT, char, typename traits::state_type>>(getloc());
```

### 29.9.2.2 构造函数 [filebuf.cons]

```
basic_filebuf();
```

1 效果：使用 basic_streambuf<charT, traits>()（29.6.3.2）初始化基类。

2 后置条件：is_open() == false。

```
basic_filebuf(basic_filebuf&& rhs);
```

3 效果：*this 中的序列指针（eback()、gptr()、egptr()、pbase()、pptr()、epptr()）是否获得 rhs 原有的值由实现定义。无论是否获得，构造之后 *this 和 rhs 均引用各自的缓冲区（如果有的话）。此外，*this 引用 rhs 在构造前引用的文件，而 rhs 在构造后不引用任何文件。rhs 的 openmode、locale 及任何其他状态也会被复制。

4 后置条件：令 rhs_p 指代此次构造之前 rhs 的状态，令 rhs_a 指代此次构造之后 rhs 的状态。

- (4.1) — is_open() == rhs_p.is_open()
- (4.2) — rhs_a.is_open() == false
- (4.3) — gptr() - eback() == rhs_p.gptr() - rhs_p.eback()
- (4.4) — egptr() - eback() == rhs_p.egptr() - rhs_p.eback()
- (4.5) — pptr() - pbase() == rhs_p.pptr() - rhs_p.pbase()
- (4.6) — epptr() - pbase() == rhs_p.epptr() - rhs_p.pbase()
- (4.7) — if (eback()) eback() != rhs_a.eback()
- (4.8) — if (gptr()) gptr() != rhs_a.gptr()
- (4.9) — if (egptr()) egptr() != rhs_a.egptr()
- (4.10) — if (pbase()) pbase() != rhs_a.pbase()
- (4.11) — if (pptr()) pptr() != rhs_a.pptr()
- (4.12) — if (epptr()) epptr() != rhs_a.epptr()

```
virtual ~basic_filebuf();
```

5 效果：调用 close()。如果在对象销毁期间发生异常，包括调用 close() 时，该异常会被捕获但不会重新抛出（见 16.4.6.13）。

### 29.9.2.3 赋值与交换 [filebuf.assign]

```
basic_filebuf& operator=(basic_filebuf&& rhs);
```

1 效果：调用 close()，然后从 rhs 进行移动赋值。移动赋值后，*this 具有若从 rhs 移动构造本应具有的可观察状态（见 29.9.2.2）。

2 返回：*this。

```
void swap(basic_filebuf& rhs);
```

3 效果：交换 *this 与 rhs 的状态。

```
template<class charT, class traits>
    void swap(basic_filebuf<charT, traits>& x,
        basic_filebuf<charT, traits>& y);
```

4 效果：等价于：x.swap(y)。

### 29.9.2.4 成员函数 [filebuf.members]

```
bool is_open() const;
```

1 返回：若先前对 open 的调用成功（返回非空值）且其间未调用 close，则为 true。

```
basic_filebuf* open(const char* s, ios_base::openmode mode);
basic_filebuf* open(const filesystem::path::value_type* s,
    ios_base::openmode mode); // wide systems only; see 29.9.1
```

2 前置条件：s 指向一个 NTCTS（3.32）。

3 效果：如果 is_open() != false，返回空指针。否则，按需初始化 filebuf。然后，如果可能，打开 s 所解析到的文件，如同调用 fopen 一样，第二个参数根据表 126 由 mode & ~ios_base::ate 确定。如果 mode 不是表中所示标志的某种组合，则打开失败。

表 126：文件打开模式 [tab:filebuf.open.modes]

| 二进制 | 输入 | 输出 | 截断 | 追加 | stdio 等价 |
|--------|----|-----|-------|-----|------------------|
|        |    |  +  |       |     | "w"              |
|        |    |  +  |       |  +  | "a"              |
|        |    |     |       |  +  | "a"              |
|        |    |  +  |   +   |     | "w"              |
|        |  + |     |       |     | "r"              |
|        |  + |  +  |       |     | "r+"             |
|        |  + |  +  |   +   |     | "w+"             |
|        |  + |  +  |       |  +  | "a+"             |
|        |  + |     |       |  +  | "a+"             |
|    +   |    |  +  |       |     | "wb"             |
|    +   |    |  +  |       |  +  | "ab"             |
|    +   |    |     |       |  +  | "ab"             |
|    +   |    |  +  |   +   |     | "wb"             |
|    +   |  + |     |       |     | "rb"             |
|    +   |  + |  +  |       |     | "r+b"            |
|    +   |  + |  +  |   +   |     | "w+b"            |
|    +   |  + |  +  |       |  +  | "a+b"            |
|    +   |  + |     |       |  +  | "a+b"            |

4 如果打开操作成功且 mode 中设置了 ios_base::ate，则将文件定位到末尾（如同调用 fseek(file, 0, SEEK_END) 那样，其中 file 是调用 fopen 返回的指针）。326

> 326) 宏 SEEK_END 在 <cstdio>（29.12.1）中定义，函数签名 fopen(const char*, const char*) 和 fseek(FILE*, long, int) 在 <cstdio>（29.12.1）中声明。

```
explicit basic_ifstream(const filesystem::path& s,
    ios_base::openmode mode = ios_base::in);
basic_ifstream(const basic_ifstream&) = delete;
basic_ifstream(basic_ifstream&& rhs);

// 29.9.3.3, assign and swap
basic_ifstream& operator=(const basic_ifstream&) = delete;
basic_ifstream& operator=(basic_ifstream&& rhs);
void swap(basic_ifstream& rhs);

// 29.9.3.4, members
basic_filebuf<charT, traits>* rdbuf() const;

bool is_open() const;
void open(const char* s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
void open(const string& s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
void close();
private:
    basic_filebuf<charT, traits> sb;    // exposition only
};

template<class charT, class traits>
void swap(basic_ifstream<charT, traits>& x,
    basic_ifstream<charT, traits>& y);
```

1 类 basic_ifstream<charT, traits> 支持从命名文件读取。它使用 basic_filebuf<charT, traits> 对象来控制关联序列。为了便于说明，所维护的数据在此展示为：

- (1.1) — sb，即 filebuf 对象。

### 29.9.3.2 构造函数 [ifstream.cons]

```
basic_ifstream();
```

1 效果：使用 basic_istream<charT, traits>(addressof(sb))（29.7.4.2.2）初始化基类，并使用 basic_filebuf<charT, traits>()（29.9.2.2）初始化 sb。

```
explicit basic_ifstream(const char* s,
    ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
```

2 效果：使用 basic_istream<charT, traits>(addressof(sb))（29.7.4.2.2）初始化基类，并使用 basic_filebuf<charT, traits>()（29.9.2.2）初始化 sb，然后调用 rdbuf()->open(s, mode | ios_base::in)。如果该函数返回空指针，则调用 setstate(failbit)。

```
explicit basic_ifstream(const string& s,
    ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path& s,
    ios_base::openmode mode = ios_base::in);
```

3 效果：等价于：basic_ifstream(s.c_str(), mode)。

```
basic_ifstream(basic_ifstream&& rhs);
```

4 效果：移动构造基类和所包含的 basic_filebuf。然后调用 basic_istream<charT, traits>::set_rdbuf(addressof(sb)) 安装所包含的 basic_filebuf。

