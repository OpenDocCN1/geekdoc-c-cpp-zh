
```cpp
namespace std {
template <class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT >
public:
class basic_stringbuf : public basic_stringbuf<charT,traits>{
protected:
    typedef traits::char_type char_type;
    typedef typename traits::int_type int_type;
    typedef typename traits::pos_type pos_type;
    typedef typename traits::off_type off_type;
    typedef traits traits;
    typedef Allocator Allocator;
};
```

```cpp
// 27.8.2.1 构造函数:
explicit basic_stringbuf(ios_base::openmode which
    = ios_base::in | ios_base::out);
basic_stringbuf(const basic_stringbuf<charT, Allocator&>& str,
ios_base::openmode which = ios_base::in | ios_base::out);
basic_stringbuf(const basic_stringbuf& rhs) = delete;
basic_stringbuf(const basic_stringbuf&& rhs) = delete;
```

```cpp
// 27.8.2.2 赋值与交换:
basic_stringbuf& operator=(const basic_stringbuf& rhs) = delete;
basic_stringbuf& operator=(basic_stringbuf&& rhs);
void swap(basic_stringbuf& rhs);
```

# ISO/IEC 14882:2011(E)

```cpp
// 27.8.2.3 Get and set:
basic_string<charT,traits,Allocator> str() const;

void str(const basic_string<charT,traits,Allocator>& s);

protected:

// 27.8.2.4 Overridden functions:
virtual int_type underflow();
virtual int_type pbackfail(int_type c = traits::eof());
virtual int_type overflow(int_type c = traits::eof());
virtual basic_stringbuf(charT,traits) setbuf(charT*, streamsize);

virtual pos_type seekoff(off_type off, off_type type, ios_base::seekdir dir,
    ios_base::openmode which = ios_base::in | ios_base::out);
virtual pos_type seekpos(pos_type pos, ios_base::openmode which = ios_base::in | ios_base::out);

private:
ios_base::openmode mode; // exposition only
};

template <class charT, class traits, class Allocator>
void swap(basic_stringbuf<charT,traits, Allocator>& x,
basic_stringbuf<charT,traits, Allocator>& y);
```

- 1 类 `basic_stringbuf` 派生自 `basic_stringbuf`，用于将可能的输入序列和可能的输出序列与任意字符序列关联。该序列可以从 `str` 初始化，也可以作为 `str` 可。

- 2 出于对象的考虑，此处展示了维护的数据：`ios_base::openmode mode` ，如果输入序列可读则 `in` 位被设置，如果输出序列可写则 `out` 位被设置。

## 27.8.2.1 basic_stringbuf 构造函数 [stringbuf.cons]

```cpp
explicit basic_stringbuf(ios_base::openmode which = ios_base::in | ios_base::out);
```

- 1 效果：构造一个 `basic_stringbuf` 类的对象，使用 `basic_nreambuf(27.6.3.1)` 初始化基类，并用 `which` 初始化 `mode`。

- 2 后置条件：`str() == ""`;

```cpp
explicit basic_stringbuf(const basic_string<charT,traits, Allocator>& s,
ios_base::openmode mode = ios_base::in | ios_base::out);
```

- 3 效果：构造一个 `basic_stringbuf` 类的对象，使用 `basic_nreambuf(27.6.3.1)` 初始化基类，并用 `mode` 初始化 `mode`。调用 `str(s)`。

```cpp
basic_stringbuf(basic_stringbuf& rhs) =
```

- 效果：`*this*` 从右值 `rhs` 移动。`*this*` 中的序列指针（`eback()`, `gptr()`, `egptr()`, `pbase()`, `pptr()`, `eptr()`）是否获得了 `rhs` 拥有的值由实现定义。无论是否获得，在构造完成后，`*this*` 和 `rhs` 引用的是独立的缓冲区（如果有的话）。`rhs` 的 `openmode` 以及任何其他其他状态都会被复制。

- 条件：让 `rhs_p` 指向此构造发生之前 `rhs` 的状态，让 `rhs_a` 指向此构造之后 `rhs` 的状态。

```cpp
str() == rhs_p.str()
gptr() == eback() == rhs_p.gptr() - rhs_p.eback()
egptr() == eback() == rhs_p.egptr() - rhs_p.eback()
pptr() == pbase() == rhs_p.pptr() - rhs_p.pbase()
eptr() == pbase() == rhs_p.eptr() - rhs_p.pbase()
if (eback()) != rhs_a.eback()
if (gptr()) gptr() != rhs_a.gptr()
if (egptr()) egptr() != rhs_a.egptr()
if (pbase()) pbase() != rhs_a.pbase()
if (pptr()) pptr() != rhs_a.pptr()
if (eptr()) eptr() != rhs_a.eptr()
```

## 27.8.2.2 赋值与交换

```cpp
basic_string& operator=(basic_string& rhs);
```

- 效果：移动赋值后，`*this*` 拥有从 `rhs` 移动过来的状态（见 27.8.2.1）。

- 返回：`*this`。

```cpp
void swap(basic_string& rhs);
```

- 效果：交换 `*this` 和 `rhs` 的状态。

```cpp
template <class charT, class CharT, class Allocator>
void swap(basic_string<charT, CharT, Allocator>& x,
basic_string<charT, CharT, Allocator>& y)
{
    x.swap(y);
}
```

## 27.8.2.3 成员函数

```cpp
basic_string<charT, CharT, Allocator> str() const;
```

- 返回：一个内容等于底层字符序列的 `basic string` 对象。如果 `basic string` 是仅用 `input` 模式创建的，生成的 `string` 包含 `[eback(), gptr())` 范围内的字符序列。如果 `basic string` 是带 `ios_base::out` 创建的，则生成的 `string` 包含 `[pbase(), high_mark)` 范围内的字符序列，其中 `high_mark` 表示缓冲区中最后一个初始化字符之后的位置。可以通过写入字符串、使用 `basic string` 构造或调用 `str(string)` 成员函数来初始化字符。在调用 `str(basic string)` 成员函数的情况下，调用之前的所有字符现在被视为未初始化（除了由新 `string` 初始化的）。否则返回一个零长度的 `string`。

```cpp
void str(const basic_string<charT,Traits,Allocator>& s);
```

- 效果：将 `s` 的内容拷贝到 `basic_stringbuf` 并根据 `mode` 初始化输入输出序列。

- 后置条件：如果 `mode & ios_base::out` 为真，则 `ptr() >= base() + s.size()`；此外，如果 `mode & ios_base::ate` 为真，则 `ptr() == base() + s.size()`；否则 `pptr() == base()`。如果 `mode & ios_base::in` 为真，则 `eback()` 指向第一个字符且 `egptr() == eback() + s.size()`

## 27.8.2.4 重写的虚函数

```cpp
int_type underflow();
```

- 返回：如果输入序列有读取位置，返回 `traits::to_inttype(*gptr())`。否则返回 `traits::eof()`。缓冲区中任何已初始化的字符都被视为输入序列的。

```cpp
int_type pbackfail(int_type c = traits::eof());
```

- 效果：通过三种方式将 `c` 指定字符放入输入序列：

- 如果 `traits::eq_int_type(c,traits::eof())` 为假且输入序列有回溯位置，且 `traits::eq_to_type(c), gptr())` 为真，则将 `gptr() --1`。

- 返回：`c`。

- 如果 `traits::eq_int_type(c,traits::eof())` 为假且输入序列有回溯位置，且 `mode & ios_base::out` 非零，则将 `c` 赋值给 `--gptr()`。

- 返回：`c`。

- 返回：`traits::not_eof(c)`。

- 注意：如果函数可以在这些项中的多个成功，则未指定选择哪一个。

```cpp
int_type overflow(int_type c = traits::eof());
```

- 效果：如果可能，通过两种方式之一将 `c` 指定字符追加到输出序列：

- 如果 `traits::eq_int_type(c,traits::eof())` 为假且输出序列有写入位置或函数提供了写入位置（如需文所示），则函数调用 `sputc(c)`。

- 返回 `c` 表示成功。

- 如果 `traits::eq_int_type(c,traits::eof())` 为真，则没有字符需要追加。

- 返回 `traits::eof()` 以外的值表示成功。

- 注意：函数可能会由于任何调用改变可用写入位置的数量。

- 返回：`traits::eof()` 表示失败。

- 函数只有在 `(mode & ios_base::out) != 0` 时才能提供写入位置。为了提供写入位置，函数会重新分配（可能分配）任何具有大量元素的对象来存储当前数组加上一个额外的写入位置。如果 `(mode & ios_base::in) != 0`，则函数会更改结束指针 `egptr()` 指向新写入位置之后。

```cpp
seekoff(off_type off, off_base::seekdir dir,
             ios_base::openmode mode
             ios_base::in | ios_base::out);
```

- 效果：如表 130 所示，如果可能，更改控制序列之一中的流位置。

表 130 — seekoff 定位

| 条件 | 结果 |
| --- | --- |
| `(which & ios_base::in) == ios_base::in` | 定位输入序列 |
| `(which & ios_base::out) == ios_base::out` | 定位输出序列 |
| `(which & ios_base::in | ios_base::out)) == (ios_base::in | ios_base::out)` | 同时定位输入和输出序列 |
| 且 way 为 `ios_base::beg` 或 `ios_base::end` | 操作位置 |
| 其他 |  |

对于要定位的序列，如果其 next (`egptr()` 或 `pptr()`) 为空指针且偏移量 `newoff` 非零，则定位失败。否则，函数如表 131 所示确定 `newoff`。

表 131 — newoff 值

| 条件 | newoff 值 |
| --- | --- |
| `way == ios_base::cur` | 0；后续指针减去起始指针 (`xnext - xbeg`) |
| `way == ios_base::end` | 高标记指针减去起始指针 (`high_mark - xbeg`) |

如果 `(newoff + off) < 0` 或者 `newoff + off` 指向未初始化的字符（如 27.8.2.3 第 1 段定义），则定位失败。否则，函数将 `xbeg + newoff + off` 赋值给后续指针 `xnext`。

返回：`pos_type(newoff)`，由结果 `newoff`（类型为 `off_type`）构造，如果可能，它存储了结果位置。如果定位操作失败，或者构造的对象无法表示结果位置，则返回 `pos_type(off_type(-1))`。

`pos_type seekpos(pos_type sp, ios_base::opemode mode = ios_base::in | ios_base::out);`

影响：等同于 `seekoff(off_type(sp), ios_base::beg, which)`。

```cpp
basic_streambuf<charT,traits>* setbuf(charT* s, size_t n);
```

影响：由实现定义，但 `setbuf(0,0)` 无影响。

返回：`*this*`

## 27.8.3 类模板 basic_istream

```cpp
namespace std {
    template <charT, traits = char_traits<charT>>
    class Allocator = allocator<charT>
    class basic_istream : public basic_istream<charT,traits> {
    public:
        typedef char_type char_type;
        typedef int_type int_type;
        typedef pos_type pos_type;
        typedef off_type off_type;
        typedef traits_type traits_type;
        typedef Allocator Allocator;
```

```cpp
// 27.8.3.1 构造函数：
    explicit basic_istream(ios_base::opemode mode = ios_base::in);
    explicit basic_istream(const basic_string<charT,traits,Allocator>& str,
                           const basic_string<charT,traits,Allocator>& s = const,
                           ios_base::opemode mode = ios_base::in);
    basic_istream(const basic_istream& rhs) = delete;
    basic_istream(basic_istream&& rhs) = delete;
```

```cpp
// 27.8.3.2 赋值与交换：
    basic_istream& operator=(const basic_istream& rhs) = delete;
    basic_istream& operator=(basic_istream&& rhs) = delete;
    void swap(basic_istream&& rhs);
```
