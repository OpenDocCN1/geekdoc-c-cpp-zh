
`char_type* pptr() const;`

`void pbuf(int n);`

`void setp(char_type* pbeg, char_type* pend);`

### 27.6.3.4 虚函数:

### 27.6.3.4.1 无长度限制:

`virtual void imbue(const locale& loc);`

### 27.6.3.4.2 缓冲区管理与定位:

`virtual basic_streambuf<char_type,traits*>`

`setbuf(char_type* s, streamsize n);`

`virtual pos_type seekoff(off_type off, off_type ios, ios_base::seekdir dir, ios_base::openmode mode = ios_base::in | ios_base::out);`

`virtual pos_type seekpos(pos_type sp, ios_base::openmode mode = ios_base::in | ios_base::out);`

`virtual int sync() = 0;`

### 27.6.3.4.3 获取区域:

`virtual streamsize showmanc();`

`virtual streamsize getxtget(const char_type* s, streamsize n);`

`virtual int_type underflow();`

`virtual int_type uflow();`

### 27.6.3.4.4 回退:

`virtual int_type pbackfail(int_type c = traits::eof());`

### 27.6.3.4.5 写入区域:

`virtual streamsize xputf(const char_type* s, streamsize n);`

`virtual int_type overflow(int_type c = traits::eof());`

}

`class basic_streambuf<charT,traits>` 作为派生流缓冲区的抽象基类，其对象控制两个字符序列：

- 一个字符输入序列；
- 一个字符输出序列。

## 27.6.3.1 basic_streambuf 构造函数 [streambuf.cons]

```cpp
basic_streambuf();
```

1 效果：构造一个 `basic_streambuf<charT,traits>` 类的对象并初始化：
   - 将其所有指针对象置为空指针，

2 备注：`getloc()` 成员已初始化，其结果为调用 `locale` 成员函数以及构造时的结果。`locale()` 以及由此获得的成员面（facets）可以缓存到下一次调用成员函数 `imbue` 为止。

```cpp
basic_streambuf(const basic_streambuf& rhs);
```

3 效果：构造 `rhs` 的拷贝。

4 后置条件：
- `eback() == rhs.eback()`
- `gptr() == rhs.gptr()`
- `egptr() == rhs.egptr()`
- `pbase() == rhs.pbase()`
- `pptr() == rhs.pptr()`
- `eptr() == rhs.eptr()`
- `getloc() == rhs.getloc`

```cpp
"basic_streambuf();
```

5 效果：无。

## 27.6.3.2 basic_streambuf 公有成员函数 [streambuf.members]

### 27.6.3.2.1 区域 [streambuf.locales]

```cpp
locale pubimbue(const locale& loc);
```

1 后置条件：`loc == getloc()`

2 效果：调用 `imbue(loc)`。

3 返回：`getloc()` 的旧值。

4 返回：如果 `imbue()` 已调用，则返回提供的 `loc` 的值，即构造时的全局 `locale`；如果在 `imbue()` 返回之前已调用（即在 `imbue()` 调用内部），则返回之前的值。默认构造函数是受保护的，以确保只有派自此类的对象可以被构造。

### 27.6.3.2.2 缓冲区管理与定位

```cpp
basic_streambuf<char_traits, char*> putbuf(char_type* s, size_type n);
```

返回：`setbuf(sp, n)`。

```cpp
pos_type puboff(off_type off_type, ios_base::seekdir way, ios_base::openmode mode = ios_base::in | ios_base::out);
```

返回：`seekoff(sp, off)`。

```cpp
pos_type pubseek(pos_type sp, ios_base::openmode mode = ios_base::in | ios_base::out);
```

返回：`seekpos(sp, which)`。

```cpp
int pubsync();
```

返回：`sync()`

### 27.6.3.2.3 获取区域

```cpp
streamsize in_avail();
```

返回：如果读取位置可用，返回 `egptr() - gptr()`。否则返回 `showc()`。

```cpp
int_type nextc();
```

效果：调用 `sbump()`。返回：`traits::eof()`。

```cpp
int_type sumpbc();
```

返回：：：：：如果序列序列位置位置位置，，

`underflow()`。，，返回 `traits::to_type(*gptr())` 增加输入序列的指针。

```cpp
int_type getsec();
```

返回：如果输入序列读取位置可用，返回 `underflow()`。否则返回 `traits::to_type(*gptr())`。

```cpp
streamsize getn(char_type* s, size_type n);
```

返回：`xsget(s, n)`。

### 27.6.3.2.4 回退

```cpp
int_type putback(char_type c);
```

返回：如果输入序列回退位置可用，或者 `traits::eq(c, gptr())` 为假，则返回 `pback(traits::to_type(c))`。否则，减少输入序列的指针并返回 `traits::to_type(*gptr())`。

```cpp
int_type sungetc();
```

返回：如果输入序列回退位置可用，返回 `pbackfail()`。否则，减少输入序列的指针并返回 `traits::to_type(*gptr())`。

### 27.6.3.2.5 写入区域

```cpp
int_type sputc(char_type c);
```

返回：如果输出序列写入位置可用，返回 `overflow(traits::to_type(c))`。否则，将 `c` 存储在输出序列的下一个指针处，增加指针，并返回 `traits::to_type(c)`。

```cpp
streamsize sputn(const char_type* s, streamsize n);
```

返回：`xsputn(s, n)`。

## 27.6.3.3 basic_streambuf 受保护的成员函数

### 27.6.3.3.1 赋值

```cpp
basic_streambuf& operator=(const basic_streambuf& rhs);
```

效果：将 `rhs` 的成员变量赋值给 `*this`。

后置条件：
```cpp
eback() == rhs.eback()
gptr() == rhs.gptr()
egptr() == rhs.egptr()
pbase() == rhs.base()
pptr() == rhs.pptr()
epptr() == rhs.epptr()
getloc() == rhs.getloc()
```

```cpp
void swap(basic_streambuf& rhs);
```

效果：交换 `rhs` 和 `*this` 的成员变量。

### 27.6.3.3.2 获取区域访问

```cpp
char_type* eback() const;
```

返回：输入序列的起始指针。

```cpp
char_type* gptr() const;
```

返回：输入序列的下一个指针。

```cpp
char_type* egptr() const;
```

返回：输入序列的结束指针。

```cpp
void gumpb(int n);
```

效果：在输入序列的下一个指针上增加 `n`。

```cpp
void setg(char_type* gbeg, char_type* gnext, char_type* gend);
```

后置条件：`bbeg == eback(), gnext == gptr(), 和 gende == egptr()`。

### 27.6.3.3 写入区域访问

```cpp
char_type* pbase() const;
```

1 返回：输出序列的起始指针。

```cpp
char_type* pptr() const;
```

2 返回：输出序列的下一个指针。

```cpp
char_type* epptr() const;
```

3 返回：输出序列的结束指针。

```cpp
void pump(int n);
```

4

```cpp
void setp(char_type* pbeg, char_type* pend);
```

5 后置条件：`bbeg == pbase(), pbeg == pptr(), 和 pend == epptr()`。

## 27.6.3.4 basic_streambuf 虚函数

### 27.6.3.4.1 区域

```cpp
void inue(int locale);
```

1 效果：更改基于区域的任何转换。

2 备注：派生类将在区域变化时获得通知。派生自 `basic_streambuf` 的类在调用之间可以安全地调用 `locale` 函数和成员。

3 默认行为：什么都不做。

### 27.6.3.4.2 缓冲区管理与定位

```cpp
basic_streambuf* setbuf(char_type* s, size_type n);
```

1 效果：以本节中派生自 `basic_streambuf` 的每个类单独定义的方式影响缓冲（27.8.2.4, 27.9.1.5）。

2 默认行为：返回空。

3 改变：以本节中派生自 `basic_streambuf` 的每个类单独定义的方式改变流的一个或多个控制序列（27.8.2.4, 27.9.1.5）。

4 默认行为：返回 `pos_type(off_type(-1))`。

# ISO/IEC 14882:2011(E)

5 影响：更改一个或多个受控序列中的流位置，其方式在本节中针对派生自 `basic_streambuf` 的每个类另行定义（27.8.2, 27.9.1.1）。

6 默认行为：返回 `pos_type(off_type(-1))`。

```
int sync();
```

7 影响：将受控序列与数组同步。也就是说，如果 `pbase()` 不为空，则将 `pbase()` 和 `pptr()` 之间的字符写入受控序列中。然后可以根据需要重置指针。

8  失败时返回 -1。什么构成失败由每个派生类决定（27.9.1.5）。

9 默认行为：返回零。

# 27.6.3.4.3 Get area

[streambuf.virt:get] 306

- 1 返回：序列中可用字符数量的估计值，或为 -1。如果返回正值，则连续调用 `underflow()` 将在至少从流中提取出相应数量字符之前不会返回 `traits::eof()`。如果 `showmanyc()` 返回 -1，则 `underflow()` 或 `overflow()` 将失败.³307

- 2 默认行为：返回 `traits::eof()`。

- 3 使用 `traits::eof()`。\308

```
streamsize getn(char* s, streamsize n);
```

- 4 影响：将最多 `n` 个字符分配给数组的连续元素，其第一个元素由 `s` 指定。字符从输入序列中读取，直到重复调用 `spmbpc()` 返回为止。当分配了 `n` 个字符或 `spmbpc()` 返回 `traits::eof()` 时，分配停止。

- 5 返回：已分配的字符数.³308

- 6 使用 `traits::underflow()`。

```
int_type underflow();
```

- 7 返回：`basic_streambuf` 的公共成员，此虚函数函数仅在 `gptr()` 为空或 `gptr() == egptr` 时才会失败；

- 8 返回：`to_int_type(c)`，其中 `c` 是待处理序列的第一个字符，且不移动输入序列的位置。如果待处理序列为空，则函数返回 `traits::eof()` 以表示失败。

9 待处理字符序列定义为以下内容的拼接：

- a) 如果 `gptr()` 不为 NULL，则从 `gptr()` 开始的 `egptr()` 个字符，否则为空序列。

- b) 来自输入序列的某些（可能为空）字符序列。

> 300: `showmany` 的名称是 "cs-how-many-sec"，而不是 "show-manic。（注意：OCR 文本此处似乎也有错误）
> 307) `underflow` 或 `overflow` 可能会通过过早抛出异常而失败。意图不仅是调用不返回 `eof()`，而是让它们“立即”返回。
> 308) 派生自 `basic_streambuf` 的类可以通过重写基类中的这些定义，提供更高效的方法来实现 `xsgetn()` 和 `xsputn()`。

# § 27.6.3.4.3

ISO/IEC 2011 – 版权所有

1020

结果字符是：

- a) 如果待处理序列不空，则为序列的第一个字符。
- b) 如果待处理序列为空，则为从输入序列中读取的下一个字符。

备份序列定义为以下内容的拼接：

- a) 如果 `eback()` 为空，则为空，
- b) 否则，从 `eback()` 开始的 `traits() - eback()` 个字符。

影响：该函数设置 `gptr()` 和 `egptr()` 以满足以下条件之一：

- a) 如果待处理序列不空，`egptr()` 为空且从 `gptr()` 开始的 `egptr() - gptr()` 个字符是待处理序列中的字符
- b) 如果待处理序列为空，`egptr()` 为空

如果 `eback()` 和 `gptr()` 不为空，则待处理序列将满足以下条件：

- a) 如果待处理序列包含至少 `gptr() - eback()` 个字符，则从 `gptr()` 开始的 `gptr() - eback()` 个字符是备份序列的字符
- b) 如果待处理序列为空，`gptr()` 和 `egptr()` 将被设置为相同的非空值

待处理序列定义为 `underflow()` 满足以下条件：

- a) 如果待处理序列包含 `gptr() - eback()` 个字符，则备份序列为 `gptr() - eback()` 个字符
- b) 如果待处理序列为空，则为空

默认行为：返回 `traits::eof()`。

```
int_type uflow();
```

要求：`uflow()` 返回 `int_type(c)`，除非 `traits::eof()` 失败。

待处理序列定义为 `underflow()`，并具有以下修改：

- a) 如果 `traits::eq_type(c,traits::eof())` 为 true，则输入序列被回溯
- b) 如果 `traits::eq_type(c,traits::eof())` 为 false，则 `c` 被插入。

# ISO/IEC 14882:2011(E)

后置条件：返回时，`gptr()`、`eback()` 和 `pptr()` 的状态相同。

3 返回：`traits::eof()` 表示失败。失败可能是因为输入序列无法回溯或其他原因。

4 返回：非 `traits::eof()` 的值表示成功。

5 默认行为：返回 `traits::eof()`。

# 27.6.3.4.5 Put area

[streambuf.virt:put]

```
streamsize xsputn(const char* s, streamsize n);
```

- 1 影响：将 `n` 个字符写入数组的连续元素，其第一个元素由 `s` 指定。字符从输入序列获取，如同重复调用 `sput(c)` 返回一样。`pptr() == eptr()` 情况未定义。

- 2 返回：写入的字符数。

```
int_type overflow(int_type c = traits::eof());
```
