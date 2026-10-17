
## 27.8.2 类模板 basic_stringbuf

```cpp
namespace std {
template <class charT, class traits = traits<charT>
    class Allocator = allocator<charT>
class basic_stringbuf : public basic_stringbuf<charT,traits> {
public:
    typedef charT char_type;
    typedef traits::int_type int_type;
    typedef traits::pos_type pos_type;
    typedef traits::off_type off_type;
    typedef traits traits_type;
    typedef Allocator allocator_type;
    // 27.8.2.1 构造函数:
    explicit basic_stringbuf(ios_base::openmode mode
        = ios_base::in | ios_base::out);
    explicit basic_stringbuf(
const basic_stringbuf<charT,traits,Allocator>& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
    basic_stringbuf(const basic_stringbuf& rhs) = delete;
    basic_stringbuf(basic_stringbuf&& rhs) = delete;
    // 27.8.2.2 赋值与交换:
    basic_stringbuf& operator=(const basic_stringbuf& rhs) = delete;
    basic_stringbuf& operator=(basic_stringbuf&& rhs) = delete;
    void swap(basic_stringbuf& rhs);
    // 27.8.2.3 获取与设置:
    basic_stringbuf<charT,traits,Allocator> str() const;
    void str(const basic_stringbuf<charT,traits,Allocator>& k) const = s;
protected:
    // 27.8.2.4 覆盖的虚函数:
    virtual int_type underflow();
    virtual int_type backfail(int_type c = traits::eof());
    virtual int_type overflow(int_type c = traits::eof());
    virtual basic_stringbuf<charT,traits>* setbuf(char* s, size_type size);
    virtual pos_type seekoff(off_type off, ios_base::seekdir dir,
    ios_base::openmode mode
        = ios_base::in | ios_base::out);
    virtual pos_type seekpos(pos_type sp,
    ios_base::openmode mode
        = ios_base::in | ios_base::out);
private:
    ios_base::openmode mode; // 仅用于说明
};
template<class charT, class traits, class Allocator>
void swap(basic_stringbuf<charT, traits, Allocator>& x,
    basic_stringbuf<charT, traits, Allocator>& y);
}}
```

1. 类 `basic_stringbuf` 派生自 `basic_streambuf`，将输入序列（可能是输出序列）与任意字符序列关联。该序列可以从 `basic_string` 对象初始化，或作为该对象提供。

2. 为了说明起见，此处展示了维护的数据：(1) `ios_base::openmode mode`，如果输入序列可以读取，则具有 `in`；如果输出序列可以写入，则具有 `out`。

### 27.8.2.1 basic_stringbuf 构造函数

```cpp
explicit basic_stringbuf(ios_base::openmode mode = ios_base::in | ios_base::out);
```
- 1 影响结果：构造一个 `basic_stringbuf` 对象。
- 2 后置条件：`str() == ""`

```cpp
explicit basic_stringbuf(const basic_stringbuf<charT,traits,Allocator>& s, ios_base::openmode mode = ios_base::in | ios_base::out);
```
- 3 影响结果：构造一个 `basic_stringbuf` 对象，通过 `basic_streambuf(27.8.3)` 初始化该类，并使用 `mode` 初始化。然后调用 `str(s)`。

```cpp
basic_stringbuf(basic_stringbuf& rhs);
```
- 4 影响结果：从 `rhs` 值移动。序列指向 `this`（通过 `eback()`, `egptr()`, `pbase()`, `pptr()`）是否从 `rhs` 获取值取决于实现。它们是否获取值取决于构造后是否分离缓冲区（如果有）。`rhs` 的 `openmode` 被拷贝。5 后置条件：让 `rhs_a` 指向构造前的 `rhs` 状态。
(1) `str() == rhs_a`
(2) `gptr() - rhs_a.gptr()`
(3) `egptr() - rhs_a.egptr()`
(4) `pbase() - rhs_a.pbase()`
(5) `pptr() - rhs_a.pptr()`
(6) `eback() != rhs_a.eback()`
(7) `gptr() != rhs_a.gptr()`
(8) `egptr() != rhs_a.egptr()`
(9) `pbase() != rhs_a.pbase()`
(10) `pptr() != rhs_a.pptr()`
(11) `pptr() != rhs_a.pptr()`

### 27.8.2.2 赋值与交换

```cpp
basic_stringbuf& operator=(const basic_stringbuf& rhs);
```
- 1 影响结果：赋值后 `*this` 具有从 `rhs` 构造时具有的状态。
- 2 返回：`*this`。

```cpp
void swap(basic_stringbuf& rhs);
```
- 影响结果：交换 `*this` 和 `rhs` 的状态。

```cpp
template <class charT, class traits, class Allocator>
void swap(basic_stringbuf<charT, traits, Allocator>& x,
basic_stringbuf<charT, traits, Allocator>& y);
```
- 影响结果：`x.swap(y)`。

### 27.8.2 成员函数

```cpp
basic_string(charT, traits, Allocator&) const;
```
- 返回：一个内容等于 `basic_stringbuf` 层序列的 `basic_string`。如果 `basic_stringbuf` 是以输入模式创建的，则结果 `basic_string` 包含 `[eback(), egptr())`。如果 `basic_stringbuf` 是带有 `ios_base::out` 创建的，则结果 `basic_string` 包含 `[base(), high_mark)`，其中 `high_mark` 表示缓冲区中初始化字符之后的位置。可以通过写入字符串、使用 `basic_string` 构造或调用 `str(basic_string)` 成员函数来初始化。在调用 `str(basic_string)` 成员函数的情况下，之前所有化的字符将重新初始化（除了被新 `basic_string` 替换的部分）。否则，返回一个既不是输入输出模式创建的零长度 `basic_string`。

```cpp
void str(basic_stringbuf<charT, traits, Allocator>& s);
```
- 影响结果：拷贝 `basic_stringbuf` 底层缓冲区的内容并根据其模式初始化输入和输出。
- 后置条件：如果 `ios_base::out` 为真，则 `p()` 指向第一个字符且 `egptr() == p() + s.size()` 成立；如果 `ios_base::ate` 为真，则 `ptr() == p() + s.size()`；否则如果 `p()` 为真且 `ios_base::in` 为真，则 `eback()` 指向第一个字符，且 `ptr() == egptr()` 和 `eback() == eback() + s.size()`。

### 27.8.2.4 覆盖的虚函数 [stringbuf.virtuals]

```cpp
int_type overflow();
```
- 返回：如果序列具有读取位置，返回 `traits::int_type(gptr())`。否则返回 `traits::eof()`。底层缓冲区中任何初始化的字符都被视为输入序列的一部分。

```cpp
int_type pbackfail(int_type c = traits::eof());
```
- 影响结果：将 `c` 指定的字符放回输入序列（如果可能），有三种方式：
- 如果 `traits::eq_int_type(c, traits::eof())` 为假，且输入序列有回退位置，且 `traits::eq_to_char_type(c, gptr()[-1])` 返回真，则将 `gptr() - 1` 赋值给 `gptr`。
- 返回：如果 `traits::eq_int_type(c, traits::eof())` 为假，且输入序列有回退位置，且 `ios_base::ate` 为非零，则将 `c` 赋值给 `*--gptr`。

(2.3) 如果 `traits::eq_type(traits,traits::eof())` 返回 `true` 且输入序列具有回退位置值，则将 `gptr() - 1` 赋值给 `gptr()`。
返回：`traits::not_of(c)`

3 返回：`traits::eof()` 表示失败。

4 备注：如果函数可以通过上述某一种方式成功，则不指定选择哪种方式。

```cpp
int_type overflow(int_type c = traits::eof());
```

5 影响：如果可能，将由 `c` 指定字符追加到输出序列中，有以下两种方式之一：

(5.1) 如果 `traits::eq_type(traits,traits::eof())` 返回 `true`，则输出序列具有写位置，或者函数创建了一个写位置（如下文所述），函数调用 `sputc(c)`。
通过返回 `c` 发送信号。

(5.2) 如果 `traits::eq_type(traits,traits::eof())` 返回 `true`，则没有字符可追加。
通过返回一个非 `traits::eof()` 的值发送信号。

6 备注：任何调用都可能改变可用写位置的数量。

7 返回：`traits::eof()` 表示失败。

8 只有当 `(mode & ios_base::out) != 0` 时，函数才能创建写位置。为了创建写位置，函数会重新分配（或初始化）一个具有足够数量元素的数组，该元素数量至少要能容纳当前数组对象（如果有）以及至少一个额外的写位置。如果 `(mode & ios_base::in) != 0`，函数将改变其反向指针 `egptr()` 使其指向新的写位置。

```cpp
pos_type seekoff(off_type off, ios_base::seekdir,
ios_base::openmode
    = ios_base::in | ios_base::out);
```

9 影响：如果可能，更改受控序列之一中的流位置，如表 130 所示。

表 130 — seek 定位

| 条件 | 结果 |
|---|---|
| `(which & ios_base::in) == ios_base::in` | 对输入序列定位 |
| `(which & ios_base::out) == ios_base::out` | 对输出序列定位 |
| `(which & (ios_base::in | ios_base::out)) == ios_base::in` | 同时对输入和输出序列定位 |
| 且 `way` 为 `ios_base::beg` 或 `ios_base::end` | 定位操作失败。 |

10 对于序列进行定位，如果其下一个指针（`gptr()` 或 `ptr()`）为空指针且新的偏移量基准不零，则定位操作失败。否则，函数如表 131 所示确定 `newoff`。

## 表 131 — newoff 值

| 条件 | newoff 值 |
|---|---|
| `way == ios_base::beg` | 0 |
| `way == ios_base::cur` | 下一个指针减去起始指针 (xnext - xbeg) |
| `way == ios_base::end` | 高位标记指针减去起始指针 (high_mark - xbeg) |

如果 `(newoff + off) < 0`，或者 `newoff + off` 指向一个未初始化的字符（见 27.8.2.3 第 1 段），则定位操作失败。否则，函数将 `newoff + xbeg` 赋值给下一个指针 `xnext`。
返回：由偏移量 `newoff` (`off_type`) 构造的 `pos_type`，如果可能，存储结果流位置。如果定位操作失败，或对象无法恢复流位置，则返回 `pos_type(off_type(-1))`。

```cpp
pos_type seekpos(pos_type, ios_base::openmode
    = ios_base::in | ios_base::out);
```

影响：等于 `seekoff(off_type), ios_base::beg, which`。

返回：`sp` 表示成功，或 `pos_type(off_type(-1))` 表示失败。

```cpp
basic_stringbuf(charT*) = setbuf(charT s, size_t n);
```

实现定义，但 `setbuf(0, 0)` 无影响。

返回：`this`。

## 27.8.3 模板类 basic_istream

```cpp
namespace std {
    template <class charT, class traits = char_traits<charT>
    class Allocator = allocator<charT>;
    class basic_istream : public basic_istream<charT,traits> {
    public:
        typedef charT char_type;
        typedef typename traits::int_type int_type;
        typedef typename traits::pos_type pos_type;
        typedef typename traits::off_type off_type;
        typedef typename traits::type traits;
        typedef Allocator Allocator_type;
```

```cpp
// 27.8.3.1 构造函数
```
