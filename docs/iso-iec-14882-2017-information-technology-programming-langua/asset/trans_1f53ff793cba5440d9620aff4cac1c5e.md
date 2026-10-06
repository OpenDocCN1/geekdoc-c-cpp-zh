

# ISO/IEC 14882:2017(E)

其中 om 是上一次调用 open() 的打开模式。如果 is_open() 返回 false，则操作失败。

如果 sp 是一个无效流，或者如果定位操作失败，且 sp 尚未通过对同一个文件流的其中一个定位操作（seek 和 seekpos）成功调用过，则效果是未定义的。否则，返回 pos_type(-1)。

```cpp
int sync() override;
```

影响：如果存在输出区域（put area），filebuf 会将字符写入文件，然后通过调用 fflush() 刷新文件。如果存在输入区域（get area），该影响由实现定义。

```cpp
void imbue(const locale& loc) override;
```

要求：如果文件位于某个索引处，且当前 locale 的编码由解码器（25.4.1.4）确定，则它与相应的 locale 相同。

影响：从文件中插入或提取的字符可以一直解码，直到再次调用 imbue。这可能需要实现类重构文件的原始内容。

## 30.9.3 类模板 basic_ifstream

```cpp
namespace std {
    template <class charT, class traits = traits<charT>>
    class basic_ifream : public basic_ifream<charT, traits> {
    public:
        using char_type = charT;
        using int_type = typename traits::int_type;
        using pos_type = typename traits::pos_type;
        using off_type = typename traits::off_type;
        using traits_type = charT;

        // 30.9.3.1, 构造函数
        basic_ifream();
        explicit basic_ifream(const char* s,
                              ios_base::openmode mode = ios_base::in);
        explicit basic_ifream(const filesystem::path::value_type* s,
                             ios_base::openmode mode = ios_base::in); // 仅宽系统；见 30.9.1
        explicit basic_ifream(const string& s,
                              ios_base::openmode mode = ios_base::in);
        explicit basic_ifream(const filesystem::path& s,
                              ios_base::openmode mode = ios_base::in);
        basic_ifream(const basic_ifream& rhs) = delete;
        basic_ifream(basic_ifream&& rhs) = delete;

        // 30.9.3.2, 赋值与交换
        basic_ifream& operator=(const basic_ifream& rhs) = delete;
        basic_ifream& operator=(basic_ifream&& rhs) = delete;
        void swap(basic_ifream& rhs);

        // 30.9.3.3, 成员
        basic_filebuf<charT, traits>* rdbuf() const;
        bool is_open();
        void open(const char* s, ios_base::openmode mode = ios_base::in);
        void open(const filesystem::path::value_type* s,
                  ios_base::openmode mode = ios_base::in); // 仅宽系统；见 30.9.1
        void open(const string& s, ios_base::openmode mode = ios_base::in);
        void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
        void close();
    private:
        basic_filebuf<charT, traits> sb;

    template <class charT, class traits>
    void swap(basic_ifstream<charT, traits>& x,
             basic_ifstream<charT, traits>& y);
};
```

- 1 类 basic_ifstream<charT, traits> 支持从具命名文件读取。它使用 basic_filebuf<charT, traits> 对象来控制关联的序列。为了说明起见，维护的数据在此呈现：
- (1.1) sb，filebuf 对象。

## 30.9.3.1 basic_ifstream 构造函数

```cpp
basic_ifstream();
```

- 1 影响：构造一个 basic_ifstream<charT, traits> 类的对象，使用 basic_ifstream<charT, traits>&(kb) (30.7.4.1) 初始化基类，并使用 basic_filebuf<charT, traits>()(30.9.2.1) 初始化 sb。

```cpp
explicit basic_ifstream(const char* s,
                             ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path::value_type* s,
                        ios_base::openmode mode = ios_base::in); // 仅宽系统；见 30.9.1
```

- 2 影响：构造一个 basic_ifstream<charT, traits> 类的对象，使用 basic_ifstream<charT, traits>&(kb) (30.7.4.1) 初始化基类，并调用 rdbuf()->open(s, mode | ios_base::in)。如果该函数返回空指针，则调用 setfail(failbit)。

```cpp
explicit basic_ifstream(const string& s,
                             ios_base::openmode mode = ios_base::in);
explicit basic_ifstream(const filesystem::path& s,
                        ios_base::openmode mode = ios_base::in);
```

- 3 影响：与 basic_ifstream(s.c_str(), mode)相同。
- 4 影响：从右值 rhs 移动。这通过移动基类和包含的 filebuf 实现。接下来调用 basic_ifstream<charT, traits>::rdbuf(&kb) 来安装包含的 filebuf。

## 30.9.3.2 赋值与交换

```cpp
basic_ifstream& operator=(basic_ifstream& rhs);
```

- 1 影响：将 rhs 的基类和成员赋值给 *this 的成员。
- 2 返回：*this。
- 3 影响：通过调用 basic_istream<charT, traits>::swap(sb) 交换 *this 和 rhs 的状态。
- 4 影响：与 x.swap(y)相同。

```cpp
template <class charT, class traits>
void swap(basic_ifstream<charT, traits>& x,
         basic_ifstream<charT, traits>& y);
```

## 30.9.3.3 成员函数

```cpp
basic_filebuf<charT, traits>* rdbuf();
bool is_open();
void open(const char* s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path::value_type* s,
          ios_base::openmode mode = ios_base::in); // 仅宽系统；见 30.9.1
void open(const string& s, ios_base::openmode mode = ios_base::in);
void open(const filesystem::path& s, ios_base::openmode mode = ios_base::in);
void close();
```

- 1 返回：const_cast<basic_filebuf<charT, traits>*>(&sb)。
- 2 返回：rdbuf()。
- 3 影响：如果 rdbuf() 返回空指针，则调用 rdbuf()->lose；否则调用 setstate(failbit)，可能会抛出 ios_failure。
- 4 影响：与 s.c_str()相同。
- 5 影响：调用 rdbuf()，如果该函数返回空指针，调用 setstate(failbit)，可能会抛出 ios_failure。

## 30.9.4 类模板 basic_ofstream

```cpp
namespace std {
template <class charT, class traits = traits<charT>>
class basic_ofstream : public basic_ostream<charT, traits> {
public:
    using char_type = charT;
    using int_type = typename traits::int_type;
    using pos_type = typename traits::pos_type;
    using off_type = typename traits::off_type;
    using traits_type = traits;

    // 30.9.1, 构造函数
    basic_ofstream();
    explicit basic_ofstream(const char* s,
        ios_base::openmode mode = ios_base::in);
    explicit basic_ofstream(const filesystem::path& s, value_type s,
        ios_base::openmode mode = ios_base::out); // 仅宽系统；见 30.9.1
    explicit basic_ofstream(const string& s,
        ios_base::openmode mode = ios_base::out);

    explicit basic_ofstream(const filesystem::path& s, ios_base::openmode mode = ios_base::out);
    basic_ofstream(const basic_ofstream& rhs) = delete;
    basic_ofstream(basic_ofstream& rhs);

    // 30.9.4.2. 赋值与交换
    basic_ofstream& operator=(const basic_ofstream& rhs) = delete;
    basic_ofstream& operator=(basic_ofstream& rhs) = delete;
    void swap(basic_ofstream& rhs);

    // 30.9.4.3. 成员
    basic_filebuf<charT, traits> rdbuf();
    bool is_open();
    void open(const char* s, ios_base::openmode mode = ios_base::out);
    void open(filesystem::path::value_type s, ios_base::openmode mode = ios_base::out); // 仅宽系统；见 30.9.1
    void open(const string& s, ios_base::openmode mode = ios_base::out);
    void open(const filesystem::path& s, ios_base::openmode mode = ios_base::out);
    void close();

private:
    basic_filebuf<charT, traits> sb; // 仅用于说明
};

template <class charT, class traits>
void swap(basic_ofstream<charT, traits>& x, 
         basic_ofstream<charT, traits>& y);
```

类 basic_ofstream<charT, traits> 支持向具命名文件写入。它使用 basic_filebuf<charT, traits> 来控制关联的序列。为了说明起见，维护的数据在此呈现：

- (1.1) sb，filebuf 对象。

## 30.9.4.1 basic_ofstream 构造函数

```cpp
basic_ofstream();
```

- 1 影响：构造一个 basic_ofstream<charT, traits> 类的对象，使用 basic_ofstream<charT, traits>&(rhs) (30.7.4.1) 初始化基类，并使用 basic_filebuf<charT, traits>()(30.9.2.1) 初始化 sb。

```cpp
explicit basic_ofstream(const char* s,
                             ios_base::openmode mode = ios_base::out);
explicit basic_ofstream(const filesystem::path::value_type s,
                        ios_base::openmode mode = ios_base::out); // 仅宽系统；见 30.9.1
```

- 2 影响：构造一个 basic_ofstream<charT, traits> 类的对象，使用 basic_ofstream<charT, traits>&(rhs) (30.7.4.1) 初始化基类，并调用 rdbuf()->open(s, mode | ios_base::out)。如果该函数返回空指针，则调用 setstate(failbit)。

