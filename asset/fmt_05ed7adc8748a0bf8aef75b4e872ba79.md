
`void open(const char* s, ios_base::open_mode mode);`

// remainder unchanged

};

这些函数的效果是调用第 27 节中指定的相应成员函数。

## D.7字符流 [depr.str.streams]

头文件 `<iostream>` 定义了三种类型，它们将缓冲区与字符数组关联并辅助读写对象。

### D.7.1 类 streambuf [depr.streambuf]

```cpp
namespace std {
class streambuf : public basic_streambuf<char> {
public:
    explicit streambuf(streamsize alloc_arg = 0);
    streambuf(void* (*palloc_arg)(size_t), void (*pfree_arg)(void*));
    streambuf(char* gnext_arg, streamsize n, char* pbeg_arg = 0);
    streambuf(const char* gnext_arg, streamsize n);
    streambuf(signed char* gnext_arg, streamsize n);
    signed char* pbeg_arg = 0);
    streambuf(const signed char* gnext_arg, size_ n);
    streambuf(unsigned char* gnext_arg, size_ n,
    unsigned char* pbeg_arg = 0);
    streambuf(const unsigned char* gnext_arg, size_ n);
    virtual ~streambuf();
    void freeze(bool freepze = true);
    char* str();
    int count();
protected:
    virtual int_type overflow(int_type c = EOF);
    virtual int_type offsetfail(int_type c);
    virtual int_type underflow();
    virtual pos_type seekpoff(off_type off, ios_base::seek_dir dir,
        ios_base::open_mode which = ios_base::in | ios_base::out);
    virtual pos_type seekppos(pos_type spg,
        ios_base::open_mode which = open);
private:
    size_t n;
};
```

# ISO/IEC 14882:2011(E)

表 157 — `strstreambuf(charT*, streamsize, charT*)` 的影响

| 元素 | 值 |
| --- | --- |
| strmode | 0 |
| alsize | 一个未指定的值 |
| palloc | 空指针 |
| pfree | 空指针 |

如果 `n < 0`，则 `N` 为 `INT_MAX`³³⁷

如果 `pbeg_arg` 为空指针，则函数执行：

```
setg(gnext_arg, gnext_arg, gnext_arg + N);
```

否则，该函数执行：

```
setg(gnext_arg, gnext_arg, pbeg_arg);
setp(pbeg_arg, pbeg_arg + N);
```

```
strstreambuf(const char* gnext_arg, streamsize n);
strstreambuf(const signed char* gnext_arg, streamsize n);
strstreambuf(const unsigned char* gnext_arg, streamsize n);
```

影响：其行为类似于 `strstreambuf(char*)gnext_arg,n)`，不同之处构造函数在 `strmode` 中设置了常量。

```
virtual strstreambuf();
```

影响：销毁 `strstreambuf` 类的对象。只有当 `strmode & allocated != 0` 且 `strmode & frozen == 0` 时，函数才会动态分配数组对象。（D.7.1.3 描述了如何释放动态分配的数组对象）。

# D.7.1.2 成员函数

[depr.strstreambuf.members]

```
void freeze(bool freezezl = true);
```

影响：如果 `strmode & dynamic` 不零，则按以下方式更改动态数组对象的状态：

- 如果 `freezezl` 为 true，则函数在 `strmode` 中设置 `frozen`。
- 否则，它清除 `strmode` 中的 `frozen`。

```
char* str();
```

影响：调用 `freeze()`，然后返回输入序列的起始指针 `gbeg`。

```
int pcount() const;
```

影响：如果输出序列的下一个指针 `pnext` 为空指针，则返回零。否则，返回数组对象的当前有效长度，即下一个指针减去输出序列的起始指针，`pnext - pbeg`。

337)函数签名 `strlen(const char*)` 定义在 `<cstring>` 中。(21.7)。宏 `INT_MAX` 定义在 `<limits>` 中 (18.3)。

# D.7.1.2

# D.7.1.3 strstreambuf 重写的虚函数

```
int_type overflow(int_type c = EOF);
```

影响：如果可能，通过以下两种方式之一将 `c` 指定的字符追加到输出序列：

- 如果 `c != EOF` 且输出序列有可写位置，或者函数提供了一个可写位置（如下文所述），则将 `c` 赋值给 `*pnext++`。
- 返回 `(unsigned char)c`。
- 如果 `c == EOF`，则没有字符需要追加。
- 返回一个非 EOF 的值。
- 返回 EOF 表示失败。

备注：函数可以更改可用写位置的数量。

为了提供一个可写位置，函数会重新分配（初始分配）一个具有足够元素数量 `n`（如果有）的数组对象，加上至少一个额外的写位置。否则，提供多少个额外的写位置未指定.³38。如果 `palloc` 不是空指针，则函数调用 `(*palloc)(n)` 来分配新的动态数组对象。在任何情况下，它都会评估表达式 `new char[n]`。在任何情况下，如果分配失败，函数返回 EOF。否则，它在 `strmode` 中设置 `aligned`。

要释放一个第一个元素为 `p` 的现有动态数组对象：如果 `pfree` 不是空指针，函数调用 `(*free)(p)`。否则，它评估表达式 `delete[p]`。

如果 `strmode & dynamic == 0`，或者 `strmode & frozen != 0`，则函数无法扩展数组（用更大的长度重新分配它）以提供可写位置。

```
int_type pbackfail(int_type c = EOF);
```

如果可能，通过以下三种方式之一将 `c` 指定的字符退回输入序列：

- 如果 `c != EOF`、输入序列有可退回位置，且 `(char)c == gnext[-1]`，则将 `gnext - 1` 赋值给 `gnext`。
- 返回 `c`。
- 如果 `c == EOF`、输入序列有可退回位置且 `strmode & constant` 为 0，则将 `c` 赋值给 `--gnext`。
- 返回 `c`。
- 如果 `c == EOF`、输入序列有可退回位置，则将 `gnext - 1` 赋值给 `gnext`。
- 返回一个非 EOF 的值。
- 返回 EOF 表示失败。

备注：如果函数可以在这些方式中的多种成功，则未指定选择哪种方式。任何调用可能会更改可用退回位置的数量。

```
int_type underflow();
```

影响：如果可能，从输入序列中读取一个字符，而不移动流位置通过它，如下：

> 338 实现在做此决定时应考虑 `alsize`。

# ISO/IEC 14882:2011(E)

- * 如果输入序列有可读位置，函数通过 `(unsigned char)*gnext` 信号成功。
- * 否则，如果下一个指针为空指针，则返回 EOF 表示失败。

备注：任何调用可能会更改可用读位置的数量。

```
pos_type seekpos(pos_type sp, ios_base::opmode which = ios_base::in);
```

影响：如果可能，将流位置更改为控制序列之一中对应 `sp` 存储的位置（如下所示）。

- 如果 `(which & in) != 0`，则定位输入序列。
- 如果 `(which & out) != 0`，则定位输出序列。

如果函数未定位任何序列，则定位操作失败。对于要定位的序列，如果下一个指针为空指针，则定位操作失败。否则，函数通过以下方式确定 `newoff`：

- 如果 `newoff` 是无效流位置、负值或大于 `(seekhigh)`，则定位操作失败。
- 否则，它将 `newoff` 加到起始指针并将结果存储在下一个指针中。

返回：`pos_type(newoff)`，由偏移量（类型为 `off_type`）构造的流位置，如果可能。如果定位失败或构造的对象无法表示流位置，则返回值为 `pos_type(off_type(-1))`。

表 158 seekoff

| 条件 | 结果 |
| --- | --- |
| (which & in) != 0 | 定位输入序列 |
| (which & out) != 0 | 定位输出序列 |
| (which & in) && (which & out) | 同时输入和输出序列 |
| 其他 | 定位操作失败 |

表 159 newoff

| 条件 | newoff |
| --- | --- |
| way == ios::beg | 0 |
| way == ios::cur | 下一个指针减去起始指针 |
| way == ios::end | seekhigh减去起始指针

# ISO/IEC 14882:2011(E)

```
pos_type seekpos(pos_type sp, ios_base::opmode which = ios_base::in);
```

影响：将流位置更改为控制序列之一，如果可能，对应于 `sp` 存储的位置（如下所示）。

- 如果 `(which & in) != 0`，定位输入序列。
- 如果 `(which & out) != 0`，定位输出序列。

如果函数未定位任何序列，则定位操作失败。对于要定位的序列，如果下一个指针为空指针，则定位操作失败。否则，函数通过以下方式确定 `newoff`：

- 如果 `newoff` 是无效流位置、负值或大于 `(seekhigh)`，则定位操作失败。
- 否则，它将 `newoff` 加到起始指针并将结果存储在下一个指针中。

返回：`pos_type(newoff)`，由偏移量（类型为 `off_type`）构造的流位置，如果可能。如果定位失败或构造的对象无法表示流位置，则返回值为 `pos_type(off_type(-1))`。

§ D.7.1.3

```
namespace std {
    class istream : public basic_istream<char> {
    public:
        explicit istream(const char* s);
        explicit istream(char* s);
        istream(const char* s, streamsize n);
        istream(char* s, streamsize n);
        virtual ~istream()();
        streambuf* rdbuf() const;
        char* str();
    private:
        streambuf* sb; // 仅用于说明
    };
}
```

`istream` 类支持读取 `istreambuf` 对象。它提供了一个 `istreamambuf` 对象来控制构造的数组对象。为了示例，这里显示维护的数据：

- `sb`，`strstreambuf` 对象。

# D.7.2.1 istream 构造函数

```
explicit istream(const char* s);
explicit istream(char* s);
```

影响：构造 `istream` 类的对象，使用 `istream(ksb)` 初始化基类，并使用 `strstreambuf(s,0))` 初始化 `sb`。`s` 应指定 NTBS 的第一个元素。

D.7.2.1

# ISO/IEC 14882:2011(E)

```cpp
istream(const char* s, streamsize n);
```

影响：构造一个 `istream` 类对象，通过 `istream(&sb)` 初始化基类，并通过 `streambuf(s,n)` 初始化 `sb`。`s` 应指定长度为 `n` 的数组的第一个元素，且 `n` 应大于零。

## D.7.2.2 成员函数

```cpp
streambuf* rdbuf() const;
```

返回：`const_cast<streambuf*>(&sb)`;

```cpp
char* str();
```

返回：`rdbuf()->str()`。

## D.7.3 ostream 类

```cpp
namespace std {
class ostream : public basic_ostream<char> {
public:
    ostream();
    ostream(char* s, int n, ios_base::openmode mode = ios_base::out);
    virtual ~ostream() =;
    streambuf* rdbuf() const;
    void freeze(bool freezefl = true);
    char* str();
    int count();
private:
    streambuf sb; // 演示模式
};
}
```

`ostream` 类支持向 `streambuf` 类对象写入数据，以控制关联的数组对象。为了演示目的，维护的数据在此处呈现为：

- `sb`，`streambuf` 对象。

## D.7.3.1 ostream 构造函数

```cpp
ostream();
```

影响：构造一个 `ostream` 类对象，通过 `ostream(&sb)` 初始化基类，并通过 `streambuf()` 初始化 `sb`。

```cpp
ostream(char* s, int n, ios_base::openmode mode = ios_base::out);
```

影响：构造一个 `ostream` 类对象，通过 `ostream(&sb)` 初始化基类，并使用两个构造函数之一初始化 `sb`：

- 如果 `(mode & app) == 0`，则 `s` 应指定长度为 `n` 的数组的第一个元素。构造函数为 `strstreambuf(s, n, s)`。

- 如果 `(mode & app) != 0`，则 `s` 指定长度为 `n` 的数组的第一个元素，该数组包含一个空缓冲区，其第一个元素由 `s` 指定。构造函数为 `strstreambuf(s, s, s + std::strlen(s))`。

## D.7.2 成员函数

```cpp
strstreambuf* rdbuf() const;
返回：`(strstreambuf*)&sb`;
void freeze(bool freezefl = true);
影响：调用 `rdbuf()->freeze(freezefl)`;
char* str();
返回：`rdbuf()->str()`;
int pcount() const;
返回：`rdbuf()->pcount()`;
```

## D.7.4 strstream 类

```cpp
namespace std {
class strstream : public basic_iostream<char> {
    // 类型
    typedef char char_type;
    typedef typename char_traits<char>::int_type int_type;
    typedef typename char_traits<char>::pos_type pos_type;
    typedef typename char_traits<char>::off_type off_type;
    // 构造函数/析构函数
    strstream();
    strstream(char* s, int n,
              ios_base::openmode mode = ios_base::in|ios_base::out);
    virtual ~strstream();
    // 成员
    strstreambuf* rdbuf() const;
    void freeze(bool freezefl = true);
    int pcount() const;
    char* str();
    private:
    strstreambuf sb; // 仅异常
};
```
