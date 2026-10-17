
```cpp
basic_ostream<Char, traits>& operator<<((double d));

basic_ostream<Char, traits>& operator<<((long double d));

basic_ostream<Char, traits>& operator<<((const void* p));

basic_ostream<Char, traits>& operator<<((nullptr));

basic_ostream<Char, traits>& operator<<((streambuf<Char, traits>* sb));

// 29.7.5.4 非格式化输出

basic_ostream<Char, traits>& put(char_type c);

basic_ostream<Char, traits>& write(const char_type* s, streamsize n);

basic_ostream<Char, traits>& flush();

// 29.7.5.2.5 Seek

pos_type tellp();

basic_ostream<Char, traits>& seekp(pos_type off, ios_base::dir dir);

basic_ostream<Char, traits>& seekp(pos_type off, ios_base::dir dir);

protected:

// 29.7.5.2.2 移动构造函数

basic_ostream(const basic_ostream&) = delete;

basic_ostream(basic_ostream&& rhs) = delete;

// 29.7.5.2.3 拷贝与交换

basic_ostream& operator=(const basic_ostream&) = delete;

basic_ostream& operator=(basic_ostream&& rhs) = delete;

void swap(basic_ostream&);

// 29.7.5.3.4 插入符

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, const charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, const charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, signed charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, unsigned charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, char& t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, char8_t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, char16_t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, char32_t) = delete;

template<class charT, class traits>
operator<<((basic_ostream<charT, traits>&, char& t) = delete;

template<class charT, class traits>
operator<<((basic_ostream<charT, traits>&, char16_t) = delete;

template<class charT, class traits>
operator<<((basic_ostream<charT, traits>&, char32_t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, const charT*);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((basic_ostream<charT, traits>&, const char*);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, const char*)

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, signed charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, unsigned charT);

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, char*) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, char8_t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, char16_t) = delete;

template<class charT, class traits>
basic_ostream<charT, traits>& operator<<((const basic_ostream<charT, traits>&, char32_t) = delete;

template<class traits>
basic_ostream<char, traits>&
operator<<((basic_ostream<char, traits>&, const char32_t*) = delete;

template<class traits>
basic_ostream<char, traits>&
operator<<((basic_ostream<char, traits>&, const char8_t*) = delete;

template<class traits>
basic_ostream<char, traits>&
operator<<((basic_ostream<char, traits>&, const char16_t*) = delete;

}
```

- 1 头文件 `<ostream>` 定义了一个类型和若干个函数签名，用于控制向流缓冲区的输出，以及一个插入到流右值的模板。
- 2 两个组函数共享共同的属性：格式化输出函数（插入）和非格式化输出函数。
- 3 如果这些函数任一个抛出异常，除非另有说明，否则函数会在错误状态中设置 `bad`。如果 `exceptions()` 中设置了 `bad`，则函数将返回异常而不完成其操作；否则，它将不会抛出异常，并像函数返回失败指示一样继续执行。
- 4 注意：删除的 `operator<<` 重载防止了将字符格式化为整数和指针。

# ISO/IEC 14882:2020(E)

```cpp
sentry(const sentry&) = delete;
sentry& operator=(const sentry&) = delete;
};
```

`sentry_base` 定义了一个类，负责执行异常安全的前置和后置操作。

```cpp
explicit sentry_base(basic_ostream<charT, traits>& os);
```

如果 `os.good()` 为真，则为格式化或非格式化输出做准备。如果 `os.tie()` 不是指针，则调用 `os.tie(flush)`。

如果在准备工作完成后，`os.good()` 为真，则 `ok == true`，否则 `ok == false`。

在准备期间，构造函数可能会调用 `setstate(failbit)`，如果结果为真，则 `ok == true`，否则 `ok == false`。

在准备期间，构造函数可能会调用 `setstate(failbit)`（这可能会抛出 `ios_base::nfailure(29.5.5.4)`）。

```cpp
-sentry();
```

如果 `os.flags() && ios_base::unitbuf() && !uncaught_exceptions() && os.good()` 为真，则调用 `os.dbuf() ->pubsync(os)`。如果返回 `-1`，则在 `os.state()` 中设置 `badbit` 而不传播异常。

```cpp
explicit operator bool() const;
```

影响：返回 `ok`。

## 29.7.5.2 位操作成员 [ostream.seeks]

- 1 每个成员函数都通过构造一个 `sentry` 类的对象开始执行。它通过 `sentry` 对象返回。

```cpp
pos_type tie();
```

返回：如果 `cur()` != false，则返回 `pos_type(-1)` 以指示失败。否则，返回 `rdbuf() ->puboff(0, 2)`，

```cpp
basic_ostream<charT, traits>& seek(pos_type pos, ios_base::seekdir dir);
```

影响：如果 `fail() != true`，则执行。如果 `fail() != true`，则执行 `rdbuf() ->pubseekoff(off, dir, ios_base::out)`。在函数调用 `setstate(failbit)` 时（这可能会抛出 `ios_base::failure`）。

- 4 *this*。

## 29.7.5.3 格式化输出函数 [ostream.formatted]

### 29.7.5.3.1 通用要求

- 1 每个输出函数都通过构造一个 `sentry` 对象开始执行。如果此对象转换为 `bool` 类型值时返回真，则函数执行以生成所需的输出。如果生成失败，格式化输出会设置 `state(ios_base::failbit)`，这可能会抛出异常。如果抛出异常，则错误状态中会开启 `ios_base::badbit`。如果没有抛出异常，`sentry` 对象将在允许格式化输出之前销毁。无论是否抛出异常，格式化输出函数的结果都是 *this*。
- 2 个格式化输出函数的描述显示了它们如何执行输出，且没有提到 `sentry`。
- 3 格式化输出函数的描述显示了它们如何执行输出。如果 `sentry` 对象在转换为 `bool` 类型时返回真，则函数执行以生成所需的输出。如果生成失败，格式化输出会设置。

## 29.7.5.3.2 算术插入符 [ostream.inserters]

```cpp
operator<<(bool)
operator<<(short)
operator<<(unsigned short)
operator<<(int)
operator<<(unsigned int)
operator<<(long)
operator<<(unsigned long)
operator<<(long long)
operator<<(unsigned long long)
operator<<(float)
operator<<(double)
```

- 影响：`num_get<>` 和 `num_put` 类处理数值格式化和解析。这些插入符使用区域化格式化。当类型为 `bool`、`long`、`unsigned long`、`long long`、`double` 或 `const void` 时，格式化转换发生如下代码片段：

```cpp
bool failed = use_facet(
num_put<charT, ostream_iterator<charT, traits>>(
(get).put(*this, +this, fill(0)),
```

当类型为 `short` 时，格式化转换发生如下代码片段：

```cpp
ios_base::basefield = ios_base::flags() & ios_base::basefield;
bool failed = use_facet(
num_put<charT, ostream_iterator<charT, traits>>(
(get).put(*this, +this, fill(0)), basefield = ios_base::oct || ios_base::hex
: static_cast<long>(static_cast<unsigned short>(val))
: static_cast<long>(val).failed());
```

当类型为 `int` 时，格式化转换发生如下代码片段：

```cpp
ios_base::basefield = ios_base::flags() & ios_base::basefield;
bool failed = use_facet(
num_put<charT, ostream_iterator<charT, traits>>(
(get).put(*this, +this, fill(0)), basefield = ios_base::oct || ios_base::hex
: static_cast<long>(static_cast<unsigned short>(val))
: static_cast<long>(val).failed());
```
（注：原文中算术插入符部分存在大量重叠和逻辑损坏，上述内容是基于可见片段的尝试重构。）

# ISO/IEC 14882:2020

```cpp
template<class trait>
basic_ostream<char, traits>& operator<<(basic_ostream<char, traits>& out, unsigned char c);
```

- 1 效果：行为类似于格式化输出函数（29.7.5.3.1）。如果 `c` 具有 `char` 类型且流的类型不是 `char`，则构造字符序列 `seq`，并根据 `out.w(c)` 填充 `const seq`；否则 `seq` 由 `c` 组成。按照 29.7.5.3.1 的描述确定 `seq` 的填充。将 `seq` 插入 `out` 中。调用 `out.width(0)`。
- 2 返回值：`out`.

```cpp
template<class charT, class traits>
basic_ostream<charT, traits>& operator<<(basic_ostream<charT, traits>& out, const charT* s);
template<class charT, class traits>
```
