
### `basic_istream` 成员声明

```cpp
using pos_type = typename traits::pos_type;

using off_type = typename traits::off_type;

using traits_type = traits;

// 30.7.4.1. 构造函数/析构函数

explicit basic_istream(basic_streambuf<charT, traits>* sb);

virtual ~basic_istream();

// 30.7.4.2. 前缀/后缀

charT& operator()();

operator&(basic_istream<charT, traits>& i) operator&(&(basic_istream<charT, traits>& i);

basic_istream<charT, traits>& operator()();

operator>>(basic_istream<charT, traits>& i) operator&(&(basic_istream<charT, traits>& i);

basic_istream<charT, traits>& operator()();

basic_istream<charT, traits>& operator>>(short& n);

basic_istream<charT, traits>& operator>>(unsigned short& n);

basic_istream<charT, traits>& operator>>(int& n);

basic_istream<charT, traits>& operator>>(unsigned int& n);

basic_istream<charT, traits>& operator>>(long& n);

basic_istream<charT, traits>& operator>>(unsigned long& n);

basic_istream<charT, traits>& operator>>(long long& n);

basic_istream<charT, traits>& operator>>(long long& n);

basic_istream<charT, traits>& operator>>(float& f);

basic_istream<charT, traits>& operator>>(double& f);

basic_istream<charT, traits>& operator>>(long& f);

basic_istream<charT, traits>& operator=(void* p);

basic_istream<charT, traits> operator=(void* p);

basic_istream<charT, traits> operator=(basic_streambuf<charT, traits>* sb);

// 30.7.4.3. 非格式化输入

streamsize gcount() const;

int_type get() const;

basic_istream<charT, traits>& get(char_type& c);

basic_istream<charT, traits>& get(char_type* s, streamsize n);

basic_istream<charT, traits>& get(char_type* s, streamsize n, char_type delim);

basic_istream<charT, traits>& get(basic_streambuf<charT, traits>& sb);

basic_istream<charT, traits>& get(basic_streambuf<charT, traits>& sb, char_type delim);

basic_istream<charT, traits>& getline(char_type* s, streamsize n);

basic_istream<charT, traits>& getline(char_type* s, streamsize n, char_type delim);

basic_istream<charT, traits>& ignore(streamsize n = 1, int_type e = traits::eof());

int_type peek();

basic_istream<charT, traits>& read(char_type* s, streamsize n);

streamsize read(char_type* s, streamsize n);

basic_istream<charT, traits>& putchar(char_type c);

basic_istream<charT, traits>& unget();

sync();

pos_type tellg();

basic_istream<charT, traits>& seekg(pos_type);

basic_istream<charT, traits>& seekg(off_type off, ios_base::seekdir dir);

protected:

// 30.7.4.1.1, 移动构造函数

basic_istream(basic_istream&& rhs) = delete;

basic_istream(basic_istream&& rhs);

// 30.7.4.1.2, 赋值和交换

basic_istream& operator=(const basic_istream& rhs) = delete;

basic_istream& operator=(basic_istream& rhs);

void swap(basic_istream& rhs);

// 30.7.4.2, 提取模板

template<class charT, class traits>

basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>&, char_type&);

template<class charT, class traits>

basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>&, unsigned char_type&);

template<class charT, class traits>

basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>&, signed char_type&);

template<class charT, class traits>

basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>&, char_type&);

template<class charT, class traits>

basic_istream<charT, traits>& operator>>(basic_istream<charT, traits>&, unsigned char_type, signed char_type&);

};
```

`basic_istream` 类定义了一些成员函数签名，用于协助从由流缓冲区读取和解释输入。
两组成员函数签名共享共同属性：格式化输入函数（或提取器）和非格式化输入函数。这两组函数的描述都是通过调用 `rdbuf()->sgetc()` 或 `rdbuf()->getc()` 获取（或提取）输入字符。它们可以使用 `istream` 的其他公共成员。

如果调用的函数之一抛出异常，除非另有说明，否则输入函数设置 `badbit`。如果 `badbit` 不在 `exceptions()` 中，输入函数将在不完成操作的情况下抛出异常，或者不抛出任何异常并按照函数返回失败指示的方式继续。

### 30.7.4.1.1 basic_stream 构造函数 [stream.cons]

`explicit basic_stream(basic_streambuf<charT,traits>* sb);`

1. 影响：构造一个 `basic_stream` 类对象，使用 `basic_ios::init(sb)` (30.5.5,2) 初始化基类。
2. 后置条件：`gcount() == 0`。
`basic_stream(const basic_stream& rhs);`
3. 影响：从 `rhs` 值移动构造。这是通过默认构造该类、从 `rhs` 拷贝 `gcount()`、调用 `basic_ios<charT,traits>::move(rhs)` 初始化基类并将 `rhs` 的 `gcount()` 设置为 0 来的。
`virtual ~basic_stream();`
4. 影响：销毁一个 `basic_stream` 类对象。
5. 备注：不对 `rdbuf()` 执行任何操作。

### 30.7.4.2 类 basic_stream 赋值和交换 [stream.assign]

`basic_stream&operator=(basic_stream& rhs);`

1. 影响：通过 `swap(rhs)` 实现。
2. 返回：`*this`。

`void swap(basic_stream& rhs);`
3. 影响：调用 `basic_ios<charT,traits>::swap(rhs)`。交换由 `gcount()` 和 `rhs.gcount()` 返回的值。

### 30.7.4.1.3 类 basic_stream::sentry [stream.sentry]

```cpp
namespace std {

template <class charT, class traits = char_traits<charT>>

class basic_stream<charT,traits>::sentry {

  using traits = traits;

  bool ok; // 仅异常

```
```cpp
public:

  explicit sentry(basic_stream<charT,traits>& is, bool noskipw = false);

  -sentry();

  sentry(const sentry&) = delete;

  sentry& operator=(const sentry&) = delete;

  explicit operator bool() const { return ok; }

};
```

`sentry` 定义了一个负责执行异常安全的前缀和后缀操作的类。

# ISO/14882:2017(E)

`explicit sentry(basic_istream<CharT>& is, bool noskipw = false);`

影响：如果 `is.good()` 为 false，则调用 `is.setstate(failbit)`。否则，为未格式化输入做好准备。如果 `is.tie()` 不是空指针，则调用 `is.flush()` 以使输出序列与任何外部 C 流同步。但如果 `is.tie()` 的输入为空，则此操作可以被抑制。实现允许推迟该调用，直到发生对 `is.rdbuf()->underflow()` 的调用。如果在 `sentry` 对象销毁之前没有发生此类调用，则 `flush` 的调用可能会延迟。如果 `noskipw` 为 true 且 `is.flags()` 为真，只要下一个输入字符 `c` 是空白字符，就会丢弃每个字符。如果 `is.rdbuf()->sbumpc()` 返回 `traits::eof()` 则调用 `setstate(eofbit)`（该函数可能会抛出 `ios_base::failure`）。

- 备注：构造函数 `sentry(basic_istream<CharT>&, bool noskipw = false)` 使用 `is` 的浸入区域（imbued locale），来确定下一个输入字符是否为空白字符。

- 为了判断 `c` 是否为空白字符，构造函数执行的操作如同执行了以下代码：
```cpp
typeype<char> ctype = use_facet<ctype<char>>(is.getloc());

if (ctype.space(c) != 0) ok_ = true; else ok_ = false;

// c 是空白字符。
```
- 如果在准备完成后，`is.good()` 为真。在准备期间，构造函数可能会调用 `setstate(failbit)`（该函数可能会抛出 `ios_base::failure(30.5.5.4)`）。

- `-sentry();`
影响：无。

- `explicit operator bool();`
影响：返回 `ok_`

## 30.7.4.2 格式化输入函数

### 30.7.4.2.1 通用要求

每个格式化输入都通过构造一个 `noskipw`（第二个）参数为 false 的 `sentry` 类对象来开始执行。如果 `sentry` 对象返回 true，在转换为 bool 类型的值时，该函数获取了所请求的输入。如果在输入过程中抛出异常，则该函数的错误状态中将开启 `ios::badbit`。如果 `exceptions::badbit != 0`，则抛出该异常。在任何情况下，格式化输入函数都会销毁 `sentry` 对象。如果没有抛出异常，它返回自身。

## 30.7.4.2.2 算术提取器

```cpp
operator>>(unsigned short& val);

operator>>(unsigned int& val);

operator>>(long& val);

operator>>(unsigned long& val);
```

305 这只有在库的一部分函数中可能的。用户代码中使用的构造函数的语义如指定所示。

306 `sentry` 构造函数和析构函数还可以执行额外的依赖于实现的操作。

307 这不会导致抛出 `ios::failure`。
`operator>>(long long& val);`
`operator>>(unsigned long long& val);`
`operator>>(float& val);`
`operator>>(double& val);`
`operator>>(long double& val);`
`operator>>(bool& val);`
`operator>>(void& val);`

- 在插入器的情况下，这些提取器提取 `locale` 的 `num_get<>` (25.4.2.1) 对象的私有成员，以执行输入流数据的数据。这些提取器的行为类似于格式化输入函数（如 30.7.4.2 所示）。在 `sentry` 对象构造后，转换如同通过以下代码执行：

```cpp
using num_get_char<char, istream_iterator<char, traits>>;

iostate err = iostate::goodbit;

use_get<numeric>(loc).get(*this, 0, *this, err, lval);

setstate(err);
```

在上述片段中，`loc` 代表 `basic_ios` 类。[注意：第一个参数提供了一个指向输入流的 `istream_iterator` 类对象作为迭代器。它跳过了 `istream` 并使用 `streambufs`，因此它不直接依赖于 `istream`]。

`operator>>(int& val);`
转换如同通过以下代码执行（使用与前面的代码相同的符号）：

```cpp
using num_get_char<char, istream_iterator<char, traits>>;

iostate err = ios_base::goodbit;

long lval;

use_get<numeric>(loc).get(*this, 0, *this, err, lval);

if (lval < numeric_limits<int>::min())

 err = ios_base::failbit;

val = numeric_limits<int>::min();

else if (lval > numeric_limits<int>::max())

 err = ios_base::failbit;

val = numeric_limits<int>::max();

else

val = static_cast<short>(lval);

setstate(err);
```
```cpp
val = static_cast<int>(lval);

setstate(basic_istream::err);
```

## 30.7.4.2.3 basic_istream::operator>

```cpp
basic_charT, traits&*operator=(basic_istream<charT, traits> (*pf)(basic_istream<charT, traits&));
```

影响：无。此提取器的行为类似于格式化输入函数（如 30.7.4.2.1 所示）。

返回：`pf(*this)`.
```cpp
