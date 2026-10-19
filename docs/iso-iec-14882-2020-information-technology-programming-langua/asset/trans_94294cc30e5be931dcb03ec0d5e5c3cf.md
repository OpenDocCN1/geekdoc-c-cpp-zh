

# 29.9.3.3  赋值与交换

`void swap(basic_ifstream& rhs);`

*Effects:* 通过调用 `basic_istream<charT, traits>::swap(rhs)` 和 `sb.swap(rhs.sb)` 交换 `*this` 和 `rhs` 的状态。

```
template<class charT, class traits>
    void swap(basic_ifstream<charT, traits>& x,
              basic_ifstream<charT, traits>& y);
```

*Effects:* 等价于：`x.swap(y)`。

# 29.9.3.4  成员函数

`basic_filebuf<charT, traits>* rdbuf() const;`

*Returns:* `const_cast<basic_filebuf<charT, traits>*>(addressof(sb))`。

`bool is_open() const;`

*Returns:* `rdbuf()->is_open()`。

```
void open(const char* s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, value_type* s,
          ios_base::openmode mode = ios_base::in);  // wide systems only; see 29.9.1
```

*Effects:* 调用 `rdbuf()->open(s, mode | ios_base::in)`。如果该函数未返回空指针则调用 `clear()`，否则调用 `setstate(failbit)`（可能抛出 `ios_base::failure`）(29.5.5.4)。

```
void open(const string& s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
```

*Effects:* 调用 `open(s.c_str(), mode)`。

```
void close();
```

*Effects:* 调用 `rdbuf()->close()`，如果该函数返回空指针，则调用 `setstate(failbit)`（可能抛出 `ios_base::failure`）(29.5.5.4)。

# 29.9.4  类模板 basic_ofstream

# 29.9.4.1  通用

```
namespace std {
    template<class charT, class traits = char_traits<charT>>
    class basic_ofstream : public basic_ostream<charT, traits> {
    public:
        using char_type   = charT;
        using int_type    = typename traits::int_type;
        using pos_type    = typename traits::pos_type;
        using off_type    = typename traits::off_type;
        using traits_type = traits;

        // 29.9.4.2, constructors
        basic_ofstream();
        explicit basic_ofstream(const char* s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const filesystem::path::value_type* s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const string& s,
                                ios_base::openmode mode = ios_base::out);
        explicit basic_ofstream(const filesystem::path& s,
                                ios_base::openmode mode = ios_base::out);
        basic_ofstream(const basic_ofstream&) = delete;
        basic_ofstream(basic_ofstream&& rhs);

        // 29.9.4.3, assign and swap
        basic_ofstream& operator=(const basic_ofstream&) = delete;
```

```
void open(
    const char* s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
void open(
    const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in|ios_base::out);    // wide systems only; see 29.9.1
void open(
    const string& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
void open(
    const filesystem::path& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
void close();

private:
    basic_filebuf<charT, traits> sb;    // exposition only
};

template<class charT, class traits>
    void swap(basic_fstream<charT, traits>& x,
              basic_fstream<charT, traits>& y);
```

1 类模板 basic_fstream<charT, traits> 支持从命名文件进行读写。它使用一个 basic_filebuf<charT, traits> 对象来控制关联的序列。为便于说明，此处维护的数据表示为：

+   (1.1) — sb，basic_filebuf 对象。

# 29.9.5.2 构造函数 [fstream.cons]

```
basic_fstream();
```

1 Effects: 使用 basic_iostream<charT, traits>(addressof(sb)) (29.7.4.7.2) 初始化基类，并使用 basic_filebuf<charT, traits>() 初始化 sb。

```
explicit basic_fstream(
    const char* s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
explicit basic_fstream(
    const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in | ios_base::out);    // wide systems only; see 29.9.1
```

2 Effects: 使用 basic_iostream<charT, traits>(addressof(sb)) (29.7.4.7.2) 初始化基类，并使用 basic_filebuf<charT, traits>() 初始化 sb。然后调用 rdbuf()->open(s, mode)。如果该函数返回空指针，则调用 setstate(failbit)。

```
explicit basic_fstream(
    const string& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
explicit basic_fstream(
    const filesystem::path& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
```

3 Effects: 等价于：basic_fstream(s.c_str(), mode)。

```
basic_fstream(basic_fstream&& rhs);
```

4 Effects: 移动构造基类和包含的 basic_filebuf。然后调用 basic_istream<charT, traits>::set_rdbuf(addressof(sb)) 安装包含的 basic_filebuf。

# 29.9.5.3 赋值与交换 [fstream.assign]

```
void swap(basic_fstream& rhs);
```

1 Effects: 通过调用 basic_iostream<charT,traits>::swap(rhs) 和 sb.swap(rhs.sb) 交换 *this 和 rhs 的状态。

```
template<class charT, class traits>
    void swap(basic_fstream<charT, traits>& x,
              basic_fstream<charT, traits>& y);
```

Effects: 等价于：x.swap(y)。

# 29.9.5.4 成员函数 [fstream.members]

```
basic_filebuf<charT, traits>* rdbuf() const;
```

Returns: const_cast<basic_filebuf<charT, traits>*>(addressof(sb))。

```
bool is_open() const;
```

Returns: rdbuf()->is_open()。

```
void open(
    const char* s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
void open(
    const filesystem::path::value_type* s,
    ios_base::openmode mode = ios_base::in | ios_base::out); // wide systems only; see 29.9.1
```

Effects: 调用 rdbuf()->open(s, mode)。如果该函数未返回空指针则调用 clear()，否则调用 setstate(failbit)（可能抛出 ios_base::failure）(29.5.5.4)。

```
void open(
    const string& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
void open(
    const filesystem::path& s,
    ios_base::openmode mode = ios_base::in | ios_base::out);
```

Effects: 调用 open(s.c_str(), mode)。

```
void close();
```

Effects: 调用 rdbuf()->close()，如果该函数返回空指针，则调用 setstate(failbit)（可能抛出 ios_base::failure）(29.5.5.4)。

# 29.10 同步输出流 [syncstream]

# 29.10.1 头文件 <syncstream> 概要 [syncstream.syn]

```
#include <ostream> // see 29.7.2
```

```
namespace std {
    template<class charT, class traits = char_traits<charT>, class Allocator = allocator<charT>>
        class basic_syncbuf;

    using syncbuf = basic_syncbuf<char>;
    using wsyncbuf = basic_syncbuf<wchar_t>;

    template<class charT, class traits = char_traits<charT>, class Allocator = allocator<charT>>
        class basic_osyncstream;

    using osyncstream = basic_osyncstream<char>;
    using wosyncstream = basic_osyncstream<wchar_t>;
}
```

头文件 <syncstream> 提供了使多个执行代理写入同一流同步的机制。

# 29.10.2 类模板 basic_syncbuf [syncstream.syncbuf]

# 29.10.2.1 概述 [syncstream.syncbuf.overview]

```
namespace std {
template<class charT, class traits = char_traits<charT>, class Allocator = allocator<charT>>
class basic_syncbuf : public basic_streambuf<charT, traits> {
public:
    using char_type    = charT;
```

# 29.10.2.3 赋值与交换 [syncstream.syncbuf.assign]

```
basic_syncbuf& operator=(basic_syncbuf&& rhs) noexcept;
```

Effects: 调用 emit() 然后从 rhs 移动赋值。移动赋值后 *this 具有的可观察状态与从 rhs 移动构造时相同 (29.10.2.2)。

Returns: *this。

Postconditions:

+   - rhs.get_wrapped() == nullptr 为真。
+   - 当 allocator_traits<Allocator>::propagate_on_container_move_assignment::value 为真时，this->get_allocator() == rhs.get_allocator() 为真；否则分配器保持不变。

Remarks: 此赋值运算符使 rhs 与其包装的流缓冲区分离，确保销毁 rhs 时不会产生输出。

```
void swap(basic_syncbuf& other) noexcept;
```

Preconditions: allocator_traits<Allocator>::propagate_on_container_swap::value 为真，或 this->get_allocator() == other.get_allocator() 为真。

Effects: 交换 *this 和 other 的状态。

# 29.10.2.4 成员函数 [syncstream.syncbuf.members]

```
bool emit();
```

Effects: 原子地将 *this 的关联输出传输到流缓冲区 *wrapped，使其在输出流中作为连续的字符序列出现。仅当自最近一次调用 emit() 以来（如果有）已调用 sync() 时，才会调用 wrapped->pubsync()。

Returns: 仅当以下所有条件都成立时返回 true；否则返回 false：

+   - wrapped == nullptr 为假。
+   - 所有关联输出中的字符都已成功传输。
+   - 对 wrapped->pubsync()（如果有）的调用成功。

Postconditions: 成功时，关联输出为空。

Synchronization: 所有向同一流缓冲区对象传输字符的 emit() 调用似乎按与“happens before”关系 (6.9.2.2) 一致的总顺序执行，其中每个 emit() 调用与该总顺序中的后续 emit() 调用同步。

Remarks: 可能在与 wrapped 唯一关联的锁持有期间调用 wrapped 的成员函数。

```
streambuf_type* get_wrapped() const noexcept;
```

Returns: wrapped。

```
allocator_type get_allocator() const noexcept;
```

Returns: 在构造函数或赋值运算符中设置的分配器的副本。

```
void set_emit_on_sync(bool b) noexcept;
```

Effects: emit_on_sync = b。

