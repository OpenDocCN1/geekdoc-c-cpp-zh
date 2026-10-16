

# 第 38.3 节 错误处理 1081

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

我倾向于使用异常来处理我不期望能够恢复的 iostream 错误。这通常意味着所有的 `bad()` 异常。

## 38.4 I/O 操作

I/O 操作的复杂性反映了传统、I/O 性能的需求以及人类期望的多样性。此处的描述基于传统的英文小字符集（ASCII）。不同字符集和不同自然语言的处理方式在第 39 章中描述。

### 38.4.1 输入操作

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

对于 `istream` 的使用者来说，`sentry` 类是一个实现细节。它为标准库和用户定义的输入操作提供通用代码。需要先执行的代码（“前缀代码”）——例如刷新绑定的流——作为 sentry 的构造函数提供。例如：

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

- `in >> x` — 根据 `x` 的类型从 `in` 读取到 `x` 中；`x` 可以是算术类型、指针、`basic_string`、`valarray`、`basic_streambuf`，或用户已为其提供合适的 `operator>>() ` 的任何类型
- `getline(in,s)` — 从 `in` 读取一行到字符串 `s`

内置类型对 `istream`（和 `ostream`）是“已知”的，因此如果 `x` 是内置类型，`cin >> x` 意味着 `cin.operator>>(x)`。如果 `x` 是用户定义的类型，`cin >> x` 意味着 `operator>>(cin,x)`（§18.2.5）。也就是说，iostream 输入是类型敏感的、固有类型安全的，并且可扩展。新的类型的设计者可以在不直接访问 iostream 实现的情况下提供 I/O 操作。

如果指针到函数是 `>>` 的目标，该函数将被调用并以 `istream` 作为其参数。例如，`cin >> pf` 产生 `pf(cin)`。这是输入操纵器的基础，例如 `skipws`（§38.4.5.2）。输出流操纵器比输入流操纵器更常见，因此该技术在 §38.4.3 中进一步解释。

除非另有说明，`istream` 操作返回其 `istream` 的引用，以便我们可以“链式”操作。例如：

```cpp
template<typename T1, typename T2>
void read_pair(T1& x, T2& y)
{
    cin >> c1 >> x >> c2 >> y >> c3;
    if (c1 != '{' || c2 != ',' || c3 != '}') { // unrecoverable input format error
        cin.setstate(ios_base::badbit); // set badbit
        throw runtime_error("bad read of pair");
    }
}
```

默认情况下 `>>` 跳过空白。例如：

```cpp
for (int i; cin >> i && 0 < i;)
    cout << i << '\n';
```

这将读取一系列由空白分隔的正整数并逐行打印它们。空白的跳过可以使用 `noskipws`（§38.4.5.2）抑制。

输入操作不是虚函数。也就是说，用户不能执行 `in >> base`，其中 `base` 是一个类层次结构并自动将 `>>` 解析为对适当派生类的操作。然而，一个简单的技术可以提供这种行为；参见 §38.4.2.1。此外，可以将这种方案扩展以能够从输入流中读取本质上任意类型的对象；参见 §22.2.4。

### 38.4.1.2 未格式化输入

未格式化输入可用于更精细地控制读取并可能提高性能。未格式化输入的一种用途是实现格式化输入：

**未格式化输入 (§iso.27.7.2.3, §iso.27.7.2.3)**

- `x = in.get()` — 从 `in` 读取一个字符并返回其整数值；文件结束时返回 `EOF`
- `in.get(c)` — 从 `in` 读取一个字符到 `c`
- `in.get(p,n,t)` — 从 `in` 读取最多 `n` 个字符到 `[p:...)`；将 `t` 视为终止符
- `in.get(p,n)` — `in.get(p,n,'\n')`
- `in.getline(p,n,t)` — 从 `in` 读取最多 `n` 个字符到 `[p:...)`；将 `t` 视为终止符；从 `in` 中移除终止符
- `in.getline(p,n)` — `in.getline(p,n,'\n')`
- `in.read(p,n)` — 从 `in` 读取最多 `n` 个字符到 `[p:...)`
- `x = in.gcount()` — `x` 是最近一次对 `in` 的未格式化输入操作读取的字符数
- `in.putback(c)` — 将 `c` 放回 `in` 的流缓冲区
- `in.unget()` — 将 `in` 的流缓冲区后退一个，以便下一次读取的字符与上一个字符相同
- `in.ignore(n,d)` — 从 `in` 提取字符并丢弃它们，直到丢弃了 `n` 个字符或找到了 `d`（并丢弃）
- `in.ignore(n)` — `in.ignore(n, traits::eof())`
- `in.ignore()` — `in.ignore(1, traits::eof())`
- `in.swap(in2)` — 交换 `in` 和 `in2` 的值

如果有选择，请使用格式化输入（§38.4.1.1）而不是这些低级输入函数。简单的 `get(c)` 在你需要从字符组成值时很有用。其他的 `get()` 函数和 `getline()` 将字符序列读入固定大小的区域 `[p:...)`。它们读取直到达到最大字符数或找到其终止符字符（默认为 `'\n'`）。它们在写入的字符（如果有）末尾放置一个 `0`；`getline()` 从输入中移除其终止符（如果找到），而 `get()` 不会。例如：

```cpp
void f() // low-level, old-style line read
{
    char word[MAX_WORD][MAX_LINE]; // MAX_WORD arrays of MAX_LINE char each
    int i = 0;
    while (cin.getline(word[i++], MAX_LINE, '\n') && i < MAX_WORD)
        /* do nothing */ ;
    // ...
}
```

对于这些函数，读取终止的原因并不立即明显：

- 我们找到了终止符。
- 我们读取了最大数量的字符。
- 我们遇到了文件结束。
- 发生了非格式输入错误。

最后两种情况通过查看文件状态（§38.3）来处理。通常，对于这些情况，适当的动作是截然不同的。

`read(p,n)` 不会在数组的字符后写入 `0`。显然，格式化输入运算符比未格式化的运算符更简单且不易出错。

以下函数依赖于流缓冲区（§38.6）与真实数据源之间详细的交互，只有在必要时并且非常谨慎地使用：

**未格式化输入 (§iso.27.7.2.3)**

- `x = in.peek()` — `x` 是当前输入字符；`x` 不从 `in` 的流缓冲区中提取，并且将是下一个读取的字符
- `n = in.readsome(p,n)` — 如果 `rdbuf()->in_avail() == -1`，调用 `setstate(eofbit)`；否则读取最多 `min(n, rdbuf()->in_avail())` 个字符到 `[p:…)`；`n` 是读取的字符数
- `x = in.sync()` — 同步缓冲区：`in.rdbuf()->pubsync()`
- `pos = in.tellg()` — `pos` 是 `in` 的 get 指针的位置
- `in.seekg(pos)` — 将 `in` 的 get 指针放置在位置 `pos`
- `in.seekg(off,dir)` — 将 `in` 的 get 指针放置在方向 `dir` 中的偏移量 `off` 处

## 38.4.2 输出操作

输出操作由 `ostream`（§38.6.1）提供，位于 `<ostream>` 中，除了写入 `string` 的那些；那些位于 `<string>` 中：

```cpp
template<typename C, typename Tr = char_traits<C>>
class basic_ostream : virtual public basic_ios<C,Tr> {
public:
    using char_type = C;
    using int_type = typename Tr::int_type;
    using pos_type = typename Tr::pos_type;
    using off_type = typename Tr::off_type;
    using traits_type = Tr;

    explicit basic_ostream(basic_streambuf<char_type,Tr>* sb);
    virtual ~basic_ostream(); // release all resources
    class sentry; // see §38.4.1

    // ...
protected:
    // move but no copy:
    basic_ostream(const basic_ostream& rhs) = delete;
    basic_ostream(basic_ostream&& rhs);
    basic_ostream& operator=(basic_ostream& rhs) = delete;
    basic_ostream& operator=(const basic_ostream&& rhs);
    // ...
};
```

`ostream` 提供格式化输出、未格式化输出（字符输出）以及对其 `streambuf`（§38.6）的简单操作：

**输出操作 (§iso.27.7.3.6, §iso.27.7.3.7, §iso.21.4.8.9)**

- `out << x` — 根据 `x` 的类型将 `x` 写入 `out`；`x` 可以是算术类型、指针、`basic_string`、`bitset`、`complex`、`valarray`，或用户已定义合适的 `operator<<()` 的任何类型
- `out.put(c)` — 将字符 `c` 写入 `out`
- `out.write(p,n)` — 将字符 `[p:p+n)` 写入 `out`
- `out.flush()` — 将字符缓冲区清空到目标
- `pos = out.tellp()` — `pos` 是 `out` 的 put 指针的位置
- `out.seekp(pos)` — 将 `out` 的 put 指针放置在位置 `pos`

