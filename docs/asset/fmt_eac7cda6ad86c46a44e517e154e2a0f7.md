
在 `<fstream>` 中，标准库提供到文件和来自文件的流：

- `ifstream` 用于从文件读取

- `ofstream` 用于向文件写入

- `fstream` 用于从文件读取和向文件写入

文件流遵循共同模式，因此我只描述 `fstream`：

```
template<typename C, typename Tr=char_traits<C>>
class basic_fstream
: public basic_iostream<C,Tr> {
public:
using char_type = C;
using int_type = typename Tr::int_type;
using pos_type = typename Tr::pos_type; // for positions in file
using off_type = typename Tr::off_type; // for offsets in file
using traits_type = Tr;
// ...
};
```

`fstream` 操作集相当简单：

```
fstream fs {};
fstream fs {s,m};
```

```
fstream fs {fs2}; fs=move(fs2) fs.swap(fs2)
p=fs.rdbuf() p is a pointer to fs’s file stream buffer (basic_filebuf<C,Tr>) fs.is_open() fs.open(s,m)
```

Is `fs` open?

Open a file called `s` with mode `m` and have `fs` refer to it; sets `fs`’s `failbit` if it couldn’t open the file;

`s` can be a string or a C-style string

```
fs.close() Close the file associated with `fs` (if any)
```

# `basic_fstream<C,Tr>` (§iso.27.9)

`fs` is a file stream not attached to a file

`fs` is a file stream opened for a file called `s` with mode `m`; `s` can be a string or a C-style string

Move constructor: `fs2` is moved to `fs`; `fs2` becomes unattached Move assignment: `fs2` is moved to `fs`; `fs2` becomes unattached Exchange the states of `fs` and `fs2`

此外，字符串流重写 `basic_ios` 受保护的虚函数 `underflow()`、`pbackfail()`、`overflow()`、`setbuf()`、`seekoff()` 和 `seekpos()` (§38.6)。

文件流没有复制操作。如果您希望两个名称引用同一个文件流，请使用引用或指针，或仔细操作文件流缓冲区 (§38.6)。

如果 `fstream` 无法打开，流处于 `bad()` 状态 (§38.3)。

在 `<fstream>` 中定义了六个文件流别名：

```
using ifstream = basic_ifstream<char>;
using wifstream = basic_ifstream<wchar_t>;
using ofstream = basic_ofstream<char>;
using wofstream = basic_ofstream<wchar_t>;
using fstream = basic_fstream<char>;
using wfstream = basic_fstream<wchar_t>;
```

您可以在 `ios_base` (§38.4.4) 中指定的几种模式之一打开文件：

# 流模式 (§iso.27.5.3.1.4)

```
ios_base::app
 ios_base::ate
 ios_base::binary
 ios_base::in
 ios_base::out
 ios_base::trunc
```

Append (i.e., add to the end of the file)

“At end” (open and seek to the end)

Binary mode; beware of system-specific behavior For reading

For writing

Truncate the file to 0 length

在每种情况下，打开文件的确切效果可能取决于操作系统，如果操作系统无法满足以某种方式打开文件的请求，结果将是一个处于 `bad()` 状态 (§38.3) 的流。例如：

```
ofstream ofs("target"); // "o" for "output" implying ios::out
if (!ofs)
error("couldn't open ‘target’ for writing");
fstream ifs; // "i" for "input" implying ios::in ifs.open("source",ios_base::in);
if (!ifs)
error("couldn't open ‘source’ for reading");
```

有关在文件中定位，请参阅 §38.6.1。

# 38.2.2 字符串流

在 `<sstream>` 中，标准库提供到字符串和来自字符串的流：

- `istringstream` 用于从字符串读取

- `ostringstream` 用于向字符串写入

- `stringstream` 用于从字符串读取和向字符串写入

字符串流遵循共同模式，因此我只描述 `stringstream`：

```
template<typename C, typename Tr = char_traits<C>, typename A = allocator<C>>
class basic_stringstream
: public basic_iostream<C,Tr> {
public:
using char_type = C;
using int_type = typename Tr::int_type;
using pos_type = typename Tr::pos_type; // for positions in string
using off_type = typename Tr::off_type; // for offsets in string
using traits_type = Tr;
using allocator_type = A;
// ...
```

`stringstream` 操作为：

```
stringstream ss {m}; stringstream ss {}; stringstream ss {s,m};
stringstream ss {s}; stringstream ss {ss2}; ss=move(ss2)
basic_stringstream<C,Tr,A> (§iso.27.8)
```

`ss` is an empty string stream with mode `m`

Default constructor: `stringstream ss {ios_base::out|ios_base::in}`; `ss` is a string stream with its buffer initialized from the string `s` with mode `m`

`stringstream ss {s,ios_base::out|ios_base::in}`;

Move constructor: `ss2` is moved to `ss`; `ss2` becomes empty Move assignment: `ss2` is moved to `ss`; `ss2` becomes empty

```
p=ss.rdbuf() p points to ss’s string stream buffer (a basic_stringbuf<C,Tr,A>) s=ss.str()
```

原因可能是令人惊讶的 `1` 是 `iostream` 会将其状态转换为进行测试：

```cpp
if (iss) { // the last operation of iss succeeded; iss’state is good() or eof()
// …
}
else {
// handle problem
}
```

# 38.3 错误处理

`iostream` 可以处于 `basic_ios` 从 `<ios>` (§38.4.4) 定义的四种状态之一：

**流状态 (§iso.27.5.5.4)**

| State | Description |

|---|---|

| `good()` | The previous `iostream` operations succeeded |

| `eof()` | We hit end-of-input (“end-of-file”) |

| `fail()` | Something unexpected happened (e.g., we looked for a digit and found ‘x’) |

| `bad()` | Something unexpected and serious happened (e.g., disk read error) |

对不处于 `good()` 状态的流进行的任何操作都没有效果；它是无操作。`iostream` 可用作条件。在这种情况下，如果 `iostream` 的状态为 `good()`，条件为真（成功）。这是读取值流的惯用法的基础：

```cpp
for (X x; cin>>x;) { // read into an input buffer of type X
// … do something with x …
}
// we get here when >> couldn’t read another X from cin
```

在读取失败后，我们可能能够清除流并继续：

```cpp
int i;
if (cin>>i) {
// … use i …
} else if (cin.fail()){
cin.clear();
string s;
if (cin>>s) {
// possibly a formatting error
// we might be able to use a string to recover // … use s …
}
}
```

或者，错误可以使用异常处理：

**异常控制: `basic_ios<C,Tr>` (§38.4.4, siso.27.5.5)**

| Expression | Description |

|---|---|

| `st=ios.exceptions()` | `st` is the `iostate` of `ios` |

| `ios.exceptions(st)` | Set `ios`’s `iostate` to `st` |

例如，我们可以使 `cin` 在其状态设置为 `bad()` 时抛出 `basic_ios::failure`

### 第 38.3 节 错误处理 1081

（例如，通过 `cin.setstate(ios_base::badbit)`）：

```cpp
cin.exceptions(cin.exceptions() | ios_base::badbit);
```

例如：

```cpp
struct Io_guard { // RAII class for iostream exceptions
    iostream& s;
    auto old_e = s.exceptions();
    Io_guard(iostream& ss, ios_base::iostate e) : s{ss} {
        s.exceptions(s.exceptions() | e);
    }
    ~Io_guard() { s.exceptions(old_e); }
};
```

```cpp
void use(istream& is) {
    Io_guard guard(is, ios_base::badbit);
    // ... use is ...
}
catch (ios_base::badbit) {
    // ... bail out! ...
}
```

我倾向于使用异常来处理我不期望能够恢复的 `iostream` 错误。这通常意味着所有的 `bad()` 异常。

# 38.4 I/O 操作

I/O 操作的复杂性反映了传统、I/O 性能的需求以及人类期望的多样性。此处的描述基于传统的英文小字符集（ASCII）。不同字符集和不同自然语言的处理方式在第 39 章中描述。

## 38.4.1 输入操作

输入操作由 `istream`（§38.6.2）提供，位于 `<istream>` 中，除了读取到字符串中的那些；那些位于 `<string>` 中。`basic_istream` 主要 intended 作为更具体的输入类的基类，例如 `istream` 和 `istringstream`：

```cpp
template<typename C, typename Tr = char_traits<C>>
class basic_istream : virtual public basic_ios<C,Tr> {
public:
    using char_type = C;
    using int_type = typename Tr::int_type;
    using pos_type = typename Tr::pos_type;
    using off_type = typename Tr::off_type;
    using traits_type = Tr;
    explicit basic_istream(basic_streambuf<C,Tr>* sb);
    virtual ~basic_istream(); // release all resources
    class sentry;
    // ...
protected:
    // move but no copy:
    basic_istream(const basic_istream& rhs) = delete;
    basic_istream(basic_istream&& rhs);
    basic_istream& operator=(const basic_istream& rhs) = delete;
    basic_istream& operator=(basic_istream&& rhs);
    // ...
};
```

对于 `istream` 的使用者来说，`sentry` 类是一个实现细节。它为标准库和用户定义的输入操作提供通用代码。需要先执行的代码（“前缀代码”）——例如刷新绑定的流——作为 `sentry` 的构造函数提供。例如：

```cpp
template<typename C, typename Tr = char_traits<C>>
basic_ostream<C,Tr>& basic_ostream<C,Tr>::operator<<(int i)
{
    sentry s { *this };
    if (!s) { // check whether all is well for output to start
        setstate(failbit);
        return *this;
    }
    // ... output the int ...
    return *this;
}
```

`sentry` 由输入操作的实现者使用，而不是由其使用者使用。

### 38.4.1.1 格式化输入

格式化输入主要由 `>>`（“输入”、“获取”或“提取”）运算符提供：

**格式化输入 (§iso.27.7.2.2, §iso.21.4.8.9)**

- `in >> x` — 根据 `x` 的类型从 `in` 读取到 `x` 中；`x` 可以是算术类型、指针、`basic_string`、`valarray`、`basic_streambuf`，或用户已为其提供合适的 `operator>>()` 的任何类型

- `getline(in,s)` — 从 `in` 读取一行到字符串 `s`

内置类型对 `istream`（和 `ostream`）是“已知”的，因此如果 `x` 是内置类型，`cin >> x` 意味着 `cin.operator>>(x)`。如果 `x` 是用户定义的类型，`cin >> x` 意味着 `operator>>(cin,x)`（§18.2.5）。也就是说，iostream 输入是类型敏感的、固有类型安全的，并且可扩展。新的类型的设计者可以在不直接访问 iostream 实现的情况下提供 I/O 操作。

如果指针到函数是 `>>` 的目标，该函数将被调用并以 `istream` 作为其参数。例如，`cin >> pf` 产生 `pf(cin)`。这是输入操纵器的基础，例如 `skipws`（§38.4.5.2）。输出流操纵器比输入流操纵器更常见，因此该技术在 §38.4.3 中进一步解释。

除非另有说明，`istream` 操作返回其 `istream` 的引用，以便我们可以“链式”操作。例如：
