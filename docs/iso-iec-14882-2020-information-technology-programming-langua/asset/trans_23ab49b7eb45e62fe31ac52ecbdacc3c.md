

## 20.8.4.5 观察者 [any.observers]

```cpp
bool has_value() const noexcept;
```

返回：若 *this 包含对象则为 true，否则为 false。

```cpp
const type_info& type() const noexcept;
```

返回：如果 *this 包含类型为 T 的值，则为 typeid(T)，否则为 typeid(void)。

[注 1：用于在编译时或仅在运行时已知类型的查询。——注结束]

## 20.8.5 非成员函数 [any.nonmembers]

```cpp
void swap(any& x, any& y) noexcept;
```

效果：等价于 x.swap(y)。

```cpp
template<class T, class... Args>
    any make_any(Args&&... args);
```

效果：等价于：return any(in_place_type<T>, std::forward<Args>(args)...);

```cpp
template<class T, class U, class... Args>
    any make_any(initializer_list<U> il, Args&&... args);
```

效果：等价于：return any(in_place_type<T>, il, std::forward<Args>(args)...);

```cpp
template<class T>
    T any_cast(const any& operand);
template<class T>
    T any_cast(any& operand);
template<class T>
    T any_cast(any&& operand);
```

令 U 为类型 remove_cvref_t<T>。

强制要求：对于第一个重载，is_constructible_v<T, const U&> 为 true。对于第二个重载，is_constructible_v<T, U&> 为 true。对于第三个重载，is_constructible_v<T, U> 为 true。

返回：对于第一个和第二个重载，static_cast<T>(*any_cast<U>(&operand))。对于第三个重载，static_cast<T>(std::move(*any_cast<U>(&operand)))。

抛出：如果 operand.type() != typeid(remove_reference_t<T>) 则抛出 bad_any_cast。

> [示例 1：
>     any x(5); // x 持有 int
>     assert(any_cast<int>(x) == 5); // 转换为值
>     any_cast<int&>(x) = 10; // 转换为引用
>     assert(any_cast<int>(x) == 10);
> 
>     x = "Meow"; // x 持有 const char*
>     assert(strcmp(any_cast<const char*>(x), "Meow") == 0);
>     any_cast<const char*&>(x) = "Harry";
>     assert(strcmp(any_cast<const char*>(x), "Harry") == 0);
> 
>     x = string("Meow"); // x 持有 string
>     string s, s2("Jane");
>     s = move(any_cast<string&>(x)); // 从 any 中移动
>     assert(s == "Meow");
>     any_cast<string&>(x) = move(s2); // 移动到 any
>     assert(any_cast<const string&>(x) == "Jane");
> 
>     string cat("Meow");
>     const any y(cat); // const y 持有 string
>     assert(any_cast<const string&>(y) == cat);
> 
>     any_cast<string&>(y); // 错误：无法 any_cast 移除 const
>     —— 示例结束]

## ISO/IEC 14882:2020(E)

3 20.9.2 中描述的函数可以报告三种错误，每种错误与不同的异常相关联：

- *invalid-argument* 错误与类型为 `invalid_argument` (19.2.5) 的异常相关联；
- *out-of-range* 错误与类型为 `out_of_range` (19.2.7) 的异常相关联；
- *overflow* 错误与类型为 `overflow_error` (19.2.10) 的异常相关联。

## 20.9.2.2 构造函数 [bitset.cons]

```cpp
constexpr bitset() noexcept;
```

1 *效果：* 将 *this 中的所有位初始化为零。

```cpp
constexpr bitset(unsigned long long val) noexcept;
```

2 *效果：* 将前 M 个位位置初始化为 val 中对应的位值。M 为 N 与 unsigned long long 的值表示 (6.8) 中的位数中较小者。如果 M < N，则剩余位位置初始化为零。

```cpp
template<class charT, class traits, class Allocator>
explicit bitset(
  const basic_string<charT, traits, Allocator>& str,
  typename basic_string<charT, traits, Allocator>::size_type pos = 0,
  typename basic_string<charT, traits, Allocator>::size_type n = basic_string<charT, traits, Allocator>::npos,
  charT zero = charT('0'),
  charT one = charT('1'));
```

3 *效果：* 将初始化字符串的有效长度 rlen 确定为 n 与 str.size() - pos 中较小者。将前 M 个位位置初始化为由字符串 str 中对应字符确定的值。M 为 N 与 rlen 中较小者。

4 构造对象的元素如果对应的字符在 str 中从位置 pos 开始为零，则其值为零。否则，元素的值为一。字符位置 pos + M - 1 对应位位置零。后续递减的字符位置对应递增的位位置。

5 如果 M < N，则剩余位位置初始化为零。

6 函数使用 traits::eq 来比较字符值。

7 *抛出：* 如果 pos > str.size() 则抛出 out_of_range，如果从位置 pos 开始的 rlen 个字符中任意一个不是零或一，则抛出 invalid_argument。

```cpp
template<class charT>
explicit bitset(
  const charT* str,
  typename basic_string<charT>::size_type n = basic_string<charT>::npos,
  charT zero = charT('0'),
  charT one = charT('1'));
```

8 *效果：* 形如：

```cpp
bitset(n == basic_string<charT>::npos ? basic_string<charT>(str) : basic_string<charT>(str, n), 0, n, zero, one)
```

## 20.9.2.3 成员 [bitset.members]

```cpp
bitset<N>& operator&=(const bitset<N>& rhs) noexcept;
```

1 *效果：* 清除 *this 中对应位在 rhs 中为清除的每个位，其余位保持不变。

2 *返回：* *this。

```cpp
bitset<N>& operator|=(const bitset<N>& rhs) noexcept;
```

3 *效果：* 设置 *this 中对应位在 rhs 中被设置的每个位，其余位保持不变。

```cpp
bitset<N>& operator^=(const bitset<N>& rhs) noexcept;
```

效果：切换 *this 中对应位在 rhs 中被设置的每个位，其余位保持不变。

返回：*this。

```cpp
bitset<N>& operator<<=(size_t pos) noexcept;
```

效果：用以下方式确定的值替换 *this 中位置 I 的每个位：

- 如果 I < pos，则新值为零；
- 如果 I >= pos，则新值为位置 I - pos 的位先前的值。

返回：*this。

```cpp
bitset<N>& operator>>=(size_t pos) noexcept;
```

效果：用以下方式确定的值替换 *this 中位置 I 的每个位：

- 如果 pos >= N - I，则新值为零；
- 如果 pos < N - I，则新值为位置 I + pos 的位先前的值。

返回：*this。

```cpp
bitset<N>& set() noexcept;
```

效果：设置 *this 中的所有位。

返回：*this。

```cpp
bitset<N>& set(size_t pos, bool val = true);
```

效果：在 *this 中位置 pos 的位存储新值。如果 val 为 true，则存储的值为一，否则为零。

返回：*this。

抛出：如果 pos 不对应有效位位置，则抛出 out_of_range。

```cpp
bitset<N>& reset() noexcept;
```

效果：重置 *this 中的所有位。

返回：*this。

```cpp
bitset<N>& reset(size_t pos);
```

效果：重置 *this 中位置 pos 的位。

返回：*this。

抛出：如果 pos 不对应有效位位置，则抛出 out_of_range。

```cpp
bitset<N> operator~() const noexcept;
```

效果：构造类 bitset<N> 的对象 x 并用 *this 初始化它。

返回：x.flip()。

```cpp
bitset<N>& flip() noexcept;
```

效果：切换 *this 中的所有位。

返回：*this。

```cpp
bitset<N>& flip(size_t pos);
```

效果：切换 *this 中位置 pos 的位。

返回：*this。

抛出：如果 pos 不对应有效位位置，则抛出 out_of_range。

```cpp
unsigned long to_ulong() const;
```

返回：x。

抛出：如果 *this 中位对应的积分值 x 无法表示为类型 unsigned long，则抛出 overflow_error。

```cpp
unsigned long long to_ullong() const;
```

返回：x。

抛出：如果 *this 中位对应的积分值 x 无法表示为类型 unsigned long long，则抛出 overflow_error。

```cpp
template<class charT = char,
    class traits = char_traits<charT>,
    class Allocator = allocator<charT>>
basic_string<charT, traits, Allocator>
to_string(charT zero = charT('0'), charT one = charT('1')) const;
```

效果：构造适当类型的字符串对象并将其初始化为长度为 N 字符的字符串。每个字符由 *this 中对应位位置的值确定。字符位置 N - 1 对应位位置零。后续递减的字符位置对应递增的位位置。位值零变为字符 zero，位值一变为字符 one。

返回：创建的对象。

```cpp
size_t count() const noexcept;
```

返回：*this 中被设置的位数计数。

```cpp
constexpr size_t size() const noexcept;
```

返回：N。

```cpp
bool operator==(const bitset<N>& rhs) const noexcept;
```

返回：如果 *this 中每个位的值等于 rhs 中对应位的值，则为 true。

```cpp
bool test(size_t pos) const;
```

返回：如果 *this 中位置 pos 的位值为一，则为 true。

抛出：如果 pos 不对应有效位位置，则抛出 out_of_range。

```cpp
bool all() const noexcept;
```

返回：count() == size()。

```cpp
bool any() const noexcept;
```

返回：count() != 0。

```cpp
bool none() const noexcept;
```

返回：count() == 0。

```cpp
bitset<N> operator<<(size_t pos) const noexcept;
```

返回：bitset<N>(*this) <<= pos。

```cpp
bitset<N> operator>>(size_t pos) const noexcept;
```

返回：bitset<N>(*this) >>= pos。

```cpp
constexpr bool operator[](size_t pos) const;
```

前提条件：pos 有效。

返回：如果 *this 中位置 pos 的位值为一，则为 true，否则为 false。

抛出：无。

