

# ISO/14882:2017(E)

explicit sentry(basic_istream<CharT>& is, bool noskipw = false);

影响：如果 is.good() 为 false，则调用 is.setstate(failbit)。否则，为未格式化输入做好准备。如果 is.tie() 不是空指针，则调用 is.flush() 以使输出序列与任何外部 C 流同步。但如果 is.tie() 的输入为空，则此操作可以被抑制。实现允许推迟该调用，直到发生对 is.rdbuf()->underflow() 的调用。如果在 sentry 对象销毁之前没有发生此类调用，则 flush 的调用可能会延迟。如果 noskipw 为 true 且 is.flags() 为真，只要下一个输入字符 c 是空白字符，就会丢弃每个字符。如果 is.rdbuf()->sbumpc() 返回 traits::eof()则调用 setstate(eofbit)（该函数可能会抛出 ios_base::failure）。

- 备注：构造函数 sentry(basic_istream<CharT>&, bool noskipw = false) 使用 is 的浸入区域（imbued locale），来确定下一个输入字符是否为空白字符。

- 为了判断 c 是否为空白字符，构造函数执行的操作如同执行了以下代码：
```cpp
typeype<char> ctype = use_facet<ctype<char>>(is.getloc());
if (ctype.space(c) != 0) ok_ = true; else ok_ = false;
// c 是空白字符。
```

- 如果在准备完成后，is.good() 为真。在准备期间，构造函数可能会调用 setstate(failbit)（该函数可能会抛出 ios_base::failure(30.5.5.4)）。

- -sentry();

影响：无。

- explicit operator bool();

影响：返回 ok_

## 30.7.4.2 格式化输入函数

### 30.7.4.2.1 通用要求

每个格式化输入都通过构造一个 noskipw（第二个）参数为 false 的 sentry 类对象来开始执行。如果 sentry 对象返回 true，在转换为 bool 类型的值时，该函数获取了所请求的输入。如果在输入过程中抛出异常，则该函数的错误状态中将开启 ios::badbit。如果 exceptions::badbit != 0，则抛出该异常。在任何情况下，格式化输入函数都会销毁 sentry 对象。如果没有抛出异常，它返回自身。

## 30.7.4.2.2 算术提取器

```cpp
operator>>(unsigned short& val);
operator>>(unsigned int& val);
operator>>(long& val);
operator>>(unsigned long& val);
```

305 这只有在库的一部分函数中可能的。用户代码中使用的构造函数的语义如指定所示。

306 sentry 构造函数和析构函数还可以执行额外的依赖于实现的操作。

307 这不会导致抛出 ios::failure。

operator>>(long long& val);
operator>>(unsigned long long& val);
operator>>(float& val);
operator>>(double& val);
operator>>(long double& val);
operator>>(bool& val);
operator>>(void& val);

- 在插入器的情况下，这些提取器提取 locale 的 num_get<> (25.4.2.1) 对象的私有成员，以执行输入流数据的数据。这些提取器的行为类似于格式化输入函数（如 30.7.4.2 所示）。在 sentry 对象构造后，转换如同通过以下代码执行：

```cpp
using num_get_char<char, istream_iterator<char, traits>>;
iostate err = iostate::goodbit;
use_get<numeric>(loc).get(*this, 0, *this, err, lval);
setstate(err);
```

在上述片段中，loc 代表 basic_ios 类。[注意：第一个参数提供了一个指向输入流的 istream_iterator 类对象作为迭代器。它跳过了 istream 并使用 streambufs，因此它不直接依赖于 istream]。

operator>>(int& val);
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

返回：pf(*this)。

```cpp
basic_charT, traits&*operator=(basic_ios<charT, traits> (*pf)(basic_ios<charT, traits&));
```

影响：pf(*this)。此提取器的行为类似于格式化输入函数（如 30.7.4.2.1 所示）。

返回：*this。

```cpp
basic_charT, traits&*operator=(ios_base& (*pf)(ios_base&));
```

影响：pf(*this)。此提取器的行为类似于格式化输入函数（如 30.7.4.2.1 所示）。

返回：*this。

```cpp
template<class charT>
basic_istream<charT, traits>&operator>(in, charT& s);
template<class charT>
basic_istream<charT, traits>&operator>(in, unsigned charT& s);
template<class charT>
basic_istream<charT, traits>&operator>(in, signed charT& s);
```（等待，原文此处有一些重叠）

影响：行为类似于格式化输入函数（如 30.7.4.2.1 所示）。在 sentry 对象构造后，它提取字符并将它们存储到由 s 指定的数组连续位置。如果 width() 大于零，n 为 width()。否则 n 是存储的最大字符数。n 是可以存储终止符() 的 char_type 最大数量。提取并存储字符直到满足任一情况：

- 存储了 n-1 个字符；
- 输入序列结束；
- 让 ce 在下一个 (in.get()) 中存储空字节；is 为 true。
- operator 然后设置 width(0)

如果提取失败，它调用 setstate(failbit)，这可能会触发 ios_base::failure(30.5.5.4)。

返回：in。

```cpp
template<class charT, traits&>&operator=(basic_istream<charT, traits&>& in, charT& c);
```

308 例如，函数 ws(30.7.4.4)。
309 例如，函数 dec(ios_base)(30.5.6.3)。

- 12 影响：作为 in 的格式化输入成员（如 30.7.4.2.1 所示）。如果从它构造 sentry 对象，如果 in 有值并且存储在 c 中。否则，函数调用 setstate(failbit)。
- 13 返回：in。
- 14 影响：作为未格式化输入函数 (30.7.4.3)。如果 sb 为空，调用 setstate(failbit)，这可能会抛出 ios_base::failure(30.5.5.4)。在 sentry 对象构造后，从 sb 控制的输出序列提取并插入字符。提取并插入字符直到输入结束：

- (14.1) 文件结束序列
- (14.2) 插入输出序列失败（如果要插入的字符未被提取）
- (14.3) 发生异常（如果异常被捕获）。

如果函数不能，它调用 setstate(failbit)，如果是因为在从*this 抛出字符时捕获异常且*this 错误状态中开启了 failbit，则抛出 ios_base::failure (30.5.5.4)。（basic_ios::clear() 的异常未被捕获或重新抛出）。如果 exceptions()&badbit != 0，则抛抛异常。计算提取的数量。如果没有抛出异常，通过将计数存储在对象中并返回值来结束。在任何情况下，sentry 在离开未格式化输入函数之前会被销毁。

- 16 返回：this。

## 30.7.4 未格式化输入函数

1 每个未格式化输入都通过构造一个返回为 bool 的 sentry 对象来开始执行，当转换为 bool 时，构造函数继续获取所请求的输入。如果 sentry 对象返回 true，当转换。否则，如果 sentry 构造通过抛出异常失败，转换为 bool 值时函数返回无效输入。在任何情况下，提取的字符数设置为以最大值作为参数的输入函数的值。如果它在 or 的第一个位置读取一个字符 (char*)。（basic_ios::clear() 的异常未被捕获或重新抛出）。如果 (exceptions()&badbit != 0) 则重新抛出异常。计算提取的数量。如果没有抛出异常，通过将计数存储在对象中并返回值来结束。

- 2 影响：无。此成员函数的行为类似于未格式化输入函数。
- 3 返回：由最后调用的未格式化输入成员函数对象提取的字符数。

```cpp
int_type get();
```

- 4 影响：作为未格式化输入函数（如上）。在构造 sentry 对象后，如果可用则提取字符 c。否则，函数调用 setstate(failbit)，这可能会抛出 ios_base::failure(30.5.5.4)。

