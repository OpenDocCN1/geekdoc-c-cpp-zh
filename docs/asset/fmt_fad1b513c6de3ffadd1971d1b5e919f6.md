
## 27.6.3 类模板 `basic_streambuf<charT,traits>` [streambuf]

`class basic_streambuf<charT,traits>` 作为派生流缓冲区的抽象基类，其对象控制两个字符序列：

- 一个字符输入序列；
- 一个字符输出序列。

## 27.6.3.1 `basic_streambuf` 构造函数 [streambuf.cons]

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

## 27.6.3.2 `basic_streambuf` 公有成员函数 [streambuf.members]

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

返回：如果输入序列读取位置可用，返回 `underflow()`。否则返回 `traits::to_type(*gptr())` 并增加输入序列的指针。

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

## 27.6.3.3 `basic_streambuf` 受保护的成员函数

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

后置条件：`bbeg == eback(), gnext == gptr(), gende == egptr()`。

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

## 27.6.3.4 `basic_streambuf` 虚函数

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
