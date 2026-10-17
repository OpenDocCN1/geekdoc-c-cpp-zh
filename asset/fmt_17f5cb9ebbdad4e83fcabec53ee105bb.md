
- 1. 每个成员函数都通过构造一个 `sentry` 类对象开始执行。通过销毁 `sentry` 返回。

- 2. 如果 `fail() != false`，则返回 `pos_type(-1)` 表示失败。否则，返回 `rdbuf()->pubseek(0, cur)`。

```cpp
pos_type basic_ostream<charT,traits>& seek(pos_type pos);
```

- 3 效果：如果 `fail() != true`，则执行 `rdbuf()->pubseek(pos, ios_base::out)`。在失败情况下，函数调用 `setstate(failbit)`（可能会抛出 `ios_base::failure`）。

- 4 返回：`*this*`。如果函数确定没有必要同步，则 `os.tie()->flush` 不一定会发生。`sentry` 的构造函数和析构函数还可以执行依赖于实现的操作。

```cpp
basic_ostream<charT,traits> seekp(off_type off, ios_base::seekdir dir);
```

- 5 效果：如果 `fail() != true`，则执行 `rdbuf()->pubseek(off, dir, ios_base::out)`。

- 6 返回：`*this*`。

### 27.7.3.6 格式化输出函数 [ostream.formatted]

- 1 共同要求：每个输出函数都通过构造一个 `sentry` 类对象开始。如果该对象在转换为 `bool` 值时返回真，则函数尝试生成请求的输出。如果生成失败，格式化输出函数会设置 `setstate(ios_base::failbit)`，这可能会抛出异常。如果在输出期间抛出异常，则 `ios::badbit` 在错误状态中被开启。如果 `(exceptions()&bad) != 0` 则抛出异常。无论是否抛出异常，`sentry` 都会在离开格式化输出函数之前被销毁。如果没有抛出异常，格式化输出的结果为 `*this*`。

- 2 单个格式化输出操作的描述说明了它们是如何执行的，并且没有提到 `sentry` 对象。

#### 27.7.3.6.2 算术插入 [ostream.Inserters]

```cpp
operator<<(bool val);
operator<<(short val);
operator<<(unsigned short val);
operator<<(int val);
operator<<(unsigned int val);
operator<<(long val);
operator<<(unsigned val);
operator<<(long long val);
operator<<(unsigned long val);
operator<<(float val);
operator<<(double val);
operator<<(long double);
operator<<(const void*)
```

- 1 效果：`num_get` 和 `num_put` 类处理数值格式化。当 `val` 类型为 `bool`、`long`、`long long`、`double` 或 `const void*` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

当 `val` 类型为 `long` 且 `ios_base::oct || ios_base::hex` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

- 2 效果：`base` 格式化。当 `val` 类型为 `unsigned short` 或 `unsigned int` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

- 3 不抛出异常：当 `val` 类型为 `unsigned long` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

- 4 效果：当 `val` 类型为 `float` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

- 5 效果：当 `val` 类型为 `double` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

- 6 效果：当 `val` 类型为 `long double` 时，格式转换执行了以下代码片段：

```cpp
bool failed = use_facet<num_put<charT,ostream_iterator<charT,traits>>(get_loc()).put(this, "", fill);
```

### 27.7.6.3 basic_ostream::operator<< [ostream.inserters]

`basic_ostream<charT,traits>& operator<< (ios_base& *(pf)(ios_base&))`

影响：调用 `pf(*this)`。此插入符的行为不类似于格式化输出函数（如 27.7.3.6.1 所示）。

返回：`*this*`。

`basic_ostream<charT,traits>& operator<< (basic_streambuf<charT,traits> sb);`

影响：表现为非格式化输出函数（如 27.7.3.7，第 1 段所示）。在哨兵对象构造后，如果 `sb` 没有调用 `setstate(badbit)`（这可能会抛出 `base::failure`）。

从 `sb` 获取字符并将其插入到 `*this*` 中。从 `sb` 读取并插入字符到 `*this*`，直到发生输入序列的任何一种情况：

- 发生文件结束（end-of-file）

- 在输出序列中插入失败（在这种情况下，要插入的字符将不会提取）

- 从 `sb` 获取字符时发生异常。

如果函数没有获取到任何字符，它将调用 `setstate(failbit)`（这可能会抛出 `ios_base::failure(27.7.5.4)`）。如果在提取字符时抛出异常，函数会在错误状态中设置 `failbit`，且如果 `(exceptions() & badbit) != 0` 则捕获的异常将被重新抛出。

返回：`*this*`。

### 27.7.3.4 字符插入器模板 [ostream.inserters.character]

```cpp
template<charT, traits>
basic_ostream<charT,traits>& operator<<<(basic_ostream<charT,traits>& out,
charT c);
template<charT, traits>
basic_ostream<charT,traits>& operator<<<(basic_ostream<charT,traits>& out,
char c);
// 序列化
template<charT, traits>
basic_ostream<charT,traits>& operator<<<(basic_ostream<charT,traits>& out,
char c);
// 有符号和无符号
template<charT, traits>
basic_ostream<charT,traits>& operator<<<(basic_ostream<charT,traits>& out,
signed char c);
template<charT, traits>
basic_ostream<charT,traits>& operator<<<(basic_ostream<charT,traits>& out,
unsigned char c);
```

影响：行为类似于对 `out` 进行格式化插入（如 27.7.3.6.1 所示）。构造哨兵对象后会插入字符。如果 `c` 的类型为 `char` 且流的字符不是 `char`，则要插入的字符为 `out.width(c)`；否则字符为 `c`。填充按照 22.4.2.2.2 所示的方式确定。调用了 `width(0)`。插入字符和任何所需的填充被插入到 `out` 中。

返回：`*this*`。

# ISO/IEC 14882:2011(E)

```cpp
template<class charT, class traitsT>
basic_ostream<charT,traits>&& operator<<((basic_ostream<charT,traits>&& out,
                               const charT* s);
```

```cpp
template<class charT, class traitsT>
basic_ostream<charT,traits>&& operator<<((basic_ostream<charT,traits>&& out,
                               const charT* s);
```

```cpp
template<class traitsT>
basic_ostream<charT,traits>&& operator<<((basic_ostream<charT,traits>&& out,
                               const charT* s);
```

```cpp
template<class traitsT>
basic_ostream<charT,traits>&& operator<<((basic_ostream<charT,traits>&& out,
                               const signed char* s);
```

```cpp
template<class traitsT>
basic_ostream<charT,traits>&& operator<<((basic_ostream<charT,traits>&& out,
                               const unsigned char* s);
```

3 `s` 不应为空指针。

4 影响：行为类似于对 `out` 的格式化插入器（如 27.7.3.6.1 所示）。插入哨兵对象（`sentry`）后，从 `s` 开始插入 `n` 个字符，其中 `n` 是通过以下方式计算出的：

```
traits::length(s) 对于第一个参数类型为 charT,
traits& 且第二个类型为 const char* 的重载，同时也适用于第一个参数
类型为 basic_ostream<charT,traits>& 且第二个类型为 const char* 的重载
```

```
std::char<char>::length(s) 对于第一个参数类型为
char* 且第二个类型为 const char* 的重载，
```

```
traits::length(reinterpret_cast<const char*>(s)) 对于另外两个重载。
```

5 填充按照 22.4.2.2.2 所示的方式确定。从 `s` 开始的 `n` 个字符使用 `out(27.5.5.3)` 扩展。宽后的字符和任何所需的填充被插入到 `out` 中。调用 `width(0)`。

6 返回：`out`。

### 27.7.3.7 非格式化输出函数 [ostream,unformatted]

1 每个非格式化输出函数通过构造 `sentry` 类对象开始执行。如果该对象转换为 `bool` 值时返回 `true`，则函数调用生成所需的 `out` 输出。如果在 `out` 期间抛出异常，则在 `*this error state*` 中开启 `ios::badbit`。

如果 `(exceptions() & badbit) != 0` 则抛出异常。在这种情况下，非格式化输出函数由临时对象销毁；如果没有抛出异常，则返回非格式化输出的值。

```cpp
basic_ostream<charT,traits>&& out(charT* c);
```

2 影响：表现为非格式化输出函数（如 27.7.3.7，第 1 段所示）。在构造哨兵对象后，可能的插入字符 `c`。否则，调用 `setstate(badbit)`（这可能会抛出 `ios_base::failure (27.7.5.4)`）。

3 返回：`*this*`。注意此函数未对 `signed char` 和 `unsigned char` 进行重载。

27.7.3.7

```cpp
basic_ostream& write(const char* s, streamsize n);
```

5 影响：表现为非格式化输出（如 27.7.3.7，第 1 段所示）。在构造哨兵对象后，从数组的连续位置插入边界，其第一个元素由 `s` 指定。插入字符，直到满足以下情况之一：

- 插入了 `n` 个字符；

- 插入到输出序列失败（在这种情况下函数调用 `setstate(badbit)`，这可能会抛出异常）。

6 影响：表现为非格式化输出（如 27.7.3.7，第 1 段所示）。构造哨兵对象后，如果该对象转换为 `bool` 值时返回 `true`，则函数调用生成所需的 `out` 输出。如果在 `out` 期间抛出异常，则在 `*this error state*` 中开启 `ios::badbit`。

如果 `(exceptions() & badbit) != 0` 则抛出异常。在这种情况下，非格式化输出函数由临时对象销毁；如果没有抛出异常，则返回非格式化输出的值。

```cpp
basic_ostream& flush();
```

### 27.7.3.8 标准 basic_ostream 操纵符 [ostream.manip]

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& endl(basic_ostream<charT,traits>& out);
}
```

1 影响：在 `out` 中插入 `'\n'` 符。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& ends(basic_ostream<charT,traits>& out);
}
```

1 影响：在 `out` 中插入文件结束。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& flush(basic_ostream<charT,traits>& out);
}
```

1 影响：调用 `out.flush()`。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setw(basic_ostream<charT,traits>& out, int n);
}
```

1 影响：调用 `out.width(n)`。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setfill(basic_ostream<charT,traits>& out, char c);
}
```

1 影响：调用 `out.setfill(c)`。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setbase(basic_ostream<charT,traits>& out, int base);
}
```

1 影响：调用 `out.setbase(base)`。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& setf(basic_ostream<charT,traits>& out, ios_base::fmtflag flags);
}
```

1 影响：调用 `out.setf(flags)`。

2 返回：`*this*`。

```cpp
namespace std {
template<class charT, traits>
basic_ostream<charT,traits>& unsetf(basic_ostream<charT,traits>& out, ios_base::fmtflag flags);
}
```

1 影响：调用 `out.unsetf(flags)`。

2 返回：`*this*`。
