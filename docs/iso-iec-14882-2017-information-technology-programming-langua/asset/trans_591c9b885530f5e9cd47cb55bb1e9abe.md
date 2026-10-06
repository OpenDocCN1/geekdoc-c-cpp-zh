

# ISO/IEC 14882:2017(E)

```cpp
int compare(size_type pos, size_type n1, charT* s, size_type n2);
```

返回：`basic_string(*this).compare(n1, s, n2)`。

## 24.3.3 basic_string 非成员函数

### 24.3.3.1 operator+
```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(lhs).append(rhs)`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(lhs).append(rhs)`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(rhs.insert(0, lhs))`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(rhs.insert(0, lhs))`。注意：等价于 `rhs.insert(0, lhs)`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>& lhs,
          const basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(lhs) + rhs`。备注：使用了 `length()`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const charT& lhs, basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(lhs) + rhs`。使用了：`length()`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const charT& lhs, basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(1, lhs) + rhs`。

```cpp
template<class charT, class traits, class Allocator>
basic_string<charT, traits, Allocator>
operator+(const charT& lhs, basic_string<charT, traits, Allocator>& rhs);
```

返回：`basic_string<charT, traits, Allocator>(std::move(rhs.insert(0, 1, lhs)))`。

## 24.3.3.2 operator==
```cpp
template<class charT, class traits, class Allocator>
bool operator==(const basic_string<charT, traits, Allocator>& lhs,
               const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`rhs == lhs`。

```cpp
template<class charT, class traits, class Allocator>
bool operator==(const charT* lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`rhs == lhs`。

```cpp
template<class charT, class traits, class Allocator>
bool operator==(const basic_string<charT, traits, Allocator>& lhs, const charT* rhs);
```

要求：rhs 指向一个至少包含 `traits::length(rhs) + 1` 个 charT 元素的数组。

返回：`lhs.compare(rhs) == 0`。

## 24.3.3.3 operator!=
```cpp
template<class charT, class traits, class Allocator>
bool operator!=(const basic_string<charT, traits, Allocator>& lhs,
               const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`lhs != rhs`。

```cpp
template<class charT, class traits, class Allocator>
bool operator!=(const charT* lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`rhs != lhs`。

```cpp
template<class charT, class traits, class Allocator>
bool operator!=(const basic_string<charT, traits, Allocator>& lhs, const charT* rhs);
```

要求：rhs 指向一个至少包含 `traits::length(rhs) + 1` 个 charT 元素的数组。

返回：`lhs.compare(rhs) != 0`。

## 24.3.3.4 operator<
```cpp
template<class charT, class traits, class Allocator>
bool operator<(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`lhs.compare(rhs) < 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator<(const charT* lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`lhs.compare(rhs) < 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator<(const basic_string<charT, traits, Allocator>&& lhs, const charT& rhs);
```

返回：`lhs.compare(rhs) < 0`。

## 24.3.3.5 operator>
```cpp
template<class charT, class traits, class Allocator>
bool operator>(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`lhs.compare(rhs) > 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator>(const charT* lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`lhs.compare(rhs) > 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator>(const basic_string<charT, traits, Allocator>&& lhs, const charT& rhs);
```

返回：`lhs.compare(rhs) > 0`。

## 24.3.3.6 operator<=
```cpp
template<class charT, class traits, class Allocator>
bool operator<=(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`lhs.compare(rhs) <= 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator<=(const charT* lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`rhs.compare(lhs) <= 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator<=(const basic_string<charT, traits, Allocator>& lhs, const charT* rhs);
```

返回：`lhs.compare(rhs) <= 0`。

## 24.3.3.7 operator=>
```cpp
template<class charT, class traits, class Allocator>
bool operator>>(const basic_string<charT, traits, Allocator>&& lhs,
          const basic_string<charT, traits, Allocator>& rhs) noexcept;
```

返回：`lhs.compare(rhs) >= 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator>>(const charT& lhs, const basic_string<charT, traits, Allocator>& rhs);
```

返回：`rhs.compare(lhs) <= 0`。

```cpp
template<class charT, class traits, class Allocator>
bool operator>>(const basic_string<charT, traits, Allocator>&& lhs, const charT& rhs);
```

返回：`lhs.compare(rhs) >= 0`。

## 24.3.3.8 swap
```cpp
template<class charT, class traits, class Allocator>
void swap(basic_string<charT, traits, Allocator>&& lhs,
          basic_string<charT, traits, Allocator>&& rhs)
noexcept(noexcept(lhs.swap(rhs)));
```

影响：等于 `lhs.swap(rhs)`。

## 24.3.3.9 插入符和提取器
```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&
operator>>(basic_istream<charT, traits>&& is, basic_string& str);
```

作为格式化输入函数 (3.4.2.1) 执行。在构造 sentry 对象后，如果 sentry 转换为 true，则调用 sentry.erase() 并从 is 提取字符并追加到其中，类似于调用 sentry.append(i)。如果 is.width() 大于 0，则追加最多 n 个字符直到 str.max_size()。提取并追加字符直到发生以下情况之一：

- 存储了 n 个字符；
- 输入序列结束；
- 对于下一个可用输入字符 c，isspace(c, is.geteof()) 为真。

在提取最后一个字符（如果有）后，is.width() 零并销毁 sentry 对象。

函数未提取任何字符，将调用 is.setstate(ios::failbit)，这可能会抛出 ios_failure(30.5.5.4)。

返回：is。

```cpp
template<class charT, class traits, class Allocator>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>&& os, const basic_string& str);
```

影响：等于 `return os << basic_string_view<charT, traits>(str);`。

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&
getline(basic_istream<charT, traits>&& is, basic_string& str);
```

