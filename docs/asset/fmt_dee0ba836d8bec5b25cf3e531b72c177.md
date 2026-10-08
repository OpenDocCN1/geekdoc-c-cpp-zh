
## 5 让 `En` = 去除限定符的 `Type` 的 `tuple_element<I, T>`。这三个模板中的每一个都应满足转换特质（TransformationTrait）要求（20.10.1），其成员类型命名为如下：

### (5.1) 对于第一个特化，`add_const<typename T::type>::type`；

### (5.2) 对于第二个特化，`add_volatile<typename T::type>::type`；

### (5.3) 对于第三个特化，`add_cv<typename T::type>::type`。

## 6 除了通过包含 `<tuple>` 头文件可用外，这三个模板在包含 `<array>` 或 `<utility>` 任意一个头运行时也是可用的。

## 20.4.2.6 元素访问 [tuple_elem]

```cpp
template <size_t I, class... Types>
const typename tuple_element<I, tuple<...>>::type& get(tuple<...>& t) noexcept;
```

- 1 要求：`I < sizeof...(Types)`。如果 `I` 越界，则程序是违形式的。

- 2 返回：指向 `T` 中第 `I` 个元素的引用，其中索引从 0 开始。

```cpp
template <size_t I, class... Types>
const typename tuple_element<I, tuple<...>>::type& get(tuple<...>& t) noexcept;
```

- 3 效果：等价于 `return std::forward<typename tuple_element<I, tuple<...>>::type&>(t);`；

- 4 注意：如果 `Types` 中的 `T` 是某种引用类型 `X`，则该类型为 `X` 而不是 `X&`。然而，如果元素是非引用类型 `T`，则返回类型为 `T`。

```cpp
template <size_t I, class... Types>
const typename tuple_element<I, tuple<...>>::type& get(tuple<...>& t) noexcept;
```

- 5 要求：`I < sizeof...(Types)`。如果 `I` 越界，则程序是违形式的。

- 6 返回：指向 `t` 中元素的 `const` 引用，其中索引从 0 开始。

- 7 注意：如果 `Types` 中的 `T` 是某种引用类型 `X`，则返回类型为 `const X` 而不是 `const&`。然而，如果元素是非引用类型 `T`，则返回类型为 `const T`。这与定义用于成员变量的 `const` 是一致的。

- 8 类型 `T` 在 `T...` 中恰好出现一次。否则，对应于 `T` 中类型的 `t` 是违形式的。

- 9 返回：指向 `t` 中对应于 `T` 中类型的元素的引用。

[示例]:

```cpp
tuple<int, int, double, double> t(1, 2, 3, 4, 5, 6);
const int& i1 = get<0>(t); // 无歧义
const int& i2 = get<1>(t); // 无歧义
const double& d = get<2>(t); // 违形式
```

- 11 注意：如果此功能是作为成员函数提供的，则返回的是非成员函数，其中依赖模板参数的类型将需要 `template` 关键字。

## 20.4.2.7 关系运算符 [tuple.rel]

```cpp
template<class Types, class... Utypes>
const bool operator=(const tuple<...>& t, const tuple<...>& u);
```

- 1 返回：对于所有 `i`，`0 <= i < sizeof...(Types)`，`get<i>(t) == get<i>(u)` 是一个有效的表达式，返回一个可转换为 `bool` 的类型。

- 2 返回：如果对于所有 `i` `get<i>(t) == get<i>(u)` 则返回 `true`，否则返回 `false`。任何零长度元组均返回 `false`。

- 3 效果：基础比较按索引顺序进行。比较或元素访问在第一个求值为 `false` 的比较后执行。

```cpp
template<class Types, class... Utypes>
const bool operator==(const tuple<...>& t, const tuple<...>& u);
```

- 4 返回：对于所有 `i`，`0 <= i < sizeof...(Types)`，`get<i>(t) < get<i>(u)` 且 `get<i>(t) > get<i>(u)` 是有效的（注：此处应为：对于所有 `i`，`0 <= i < sizeof...(Types)`，`get<i>(t) < get<i>(u)` 且 `get<i>(t) > get<i>(u)` 是返回一个可转换为 `bool` 的类型）。

- 5 返回：`t` 和 `u` 的字典序比较结果。定义为：`(bool)(get<i>(t) < get<i>(u)) || !(get<i>(t) < get<i>(u))`，对于任何零长度元组返回 `false`。

```cpp
template<class Types, class... Utypes>
const bool operator==(const tuple<...>& t, const tuple<...>& u);
```

- 6 返回：`t == u`。

```cpp
template<class TTypes, class... Utypes>
constexpr bool operator>(const tuple<...>& t, const tuple<...>& u) noexcept;
```

- 7 返回：`u < t`。

```cpp
template<class TTypes, class... Utypes>
constexpr bool operator<(const tuple<...>& t, const tuple<...>& u) noexcept;
```

- 8 返回：`t > u`。

- 9 注意：上述比较运算符的定义不需要 `t` 或 `u` 是可构造的。此外，比较运算符是短路的；它们不会执行确定结果所需的元素访问。

## 20.4.2 Triple traits [tuple.traits]

```cpp
template<class allocator, template<typename> class Alloc : true_type { };
```

- 要求：`Alloc` 应是 `Allocator` (17.6.3)。

- 1 该特化告知其他组件 `allocator` 有 `size_type`。

```cpp
template<class Types, class... Utypes>
const bool operator=(const tuple<...>& t, const tuple<...>& u);
```

- `T` 是整数类型。

```cpp
namespace std {
    template<class T, T...>
    struct integer_sequence {
        typedef T value_type;
        static constexpr size_t size() noexcept { return sizeof...(I); };
    }
}
```

- `T` 应为整数类型。

```cpp
template<class T, TN...>
using make_integer_sequence = integer_sequence<T, TN>;
```

- 如果 `N` 是正值，别名模板 `make_integer_sequence` 表示具有 `N` 个非类型参数的 `integer_sequence`。类型 `make_integer_sequence<T, N>` 表示类型 `integer_sequence<T, 0, 1, ..., N-1>`。

## 20.6 类模板 bitset [template.bitset]

Header `<bitset>` synopsis

```cpp
#include <string>
#include <iostream> // 用于 istream, ostream
namespace std {
    template<size_t N> bitset {

        // 20.6.4 bitset 运算符
        template<size_t N>
        const operator<(const bitset<N>&, const bitset<N>&) noexcept;
        template<size_t N>
        const bool operator>(const bitset<N>&, const bitset<N>&) noexcept;
        template<size_t N>
        bitset& operator=(const bitset<N>&, const bitset<N>&) noexcept;
        template<class charT, class traits, size_t N>
        basic_ostream&operator<<(basic_ostream<charT, traits>& os, bitset<N>& x);
        template<class charT, class traits, size_t N>
        basic_ostream<charT, traits>operator<<(basic_ostream<charT, traits>& os, const bitset<N>& x);
    }
}
```

- 1 头 `<bitset>` 定义了一个类模板和若干相关函数，用于表示和操作固定大小的位序列。

# ISO/IEC 4296

```cpp
reference() noexcept;

public:
-reference() noexcept;
reference& operator=(bool x) noexcept;
reference& operator=(const reference&) noexcept;
bool operator() const noexcept;
operator bool() const noexcept;
reference flip() noexcept;
// for b[i] = x;
// for b[i] = b[j];
// flips the bit
// for x = b[i];
// for b[i].flip();

// 20.6.1构造函数:
constexpr bitset() noexcept;
constexpr bitset(unsigned long val) noexcept;
template<class Char, class traits, class Allocator>
explicit bitset(
const basic_string<Char, traits, Allocator>& str,
type = basic_string<Char, traits, Allocator>::size_type n = 0,
char zero = basic_string<Char, traits, Allocator>::npos,
char zero = Char('0'), char one = Char('1'));

template<class Char>
explicit bitset(
const char* str,
type = basic_string<Char, traits, Allocator>::size_type n = npos,
char zero = char('0'), char one = char('1'));

// 20.6.2操作:
bitset& operator=(const bitset<N>& rhs) noexcept;
bitset& operator|=(const bitset<N>& rhs) noexcept;
bitset& operator&=(const bitset<N>& rhs) noexcept;
bitset& operator>>=(size_t pos) noexcept;
bitset& set() noexcept;
bitset& set(size_t pos, bool val = true);
bitset& reset() noexcept;
bitset& reset(size_t pos);
bitset& operator() const noexcept;
bitset& flip() noexcept;
bitset& flip(size_t pos);

// 访问:
constexpr operator()(size_t pos) const // for b[i];
reference operator[](size_t pos) const // for b[i];

unsigned long to_unsigned() const;
unsigned long to_unsigned() const {
class Char = char;
template<class Char>
class traits = traits<Char>
class Allocator = allocator<Char> 
basic_string<Char, traits, Allocator>
to_string(char zero = char('0'), char one = char('1')) const noexcept;
size_t count() const noexcept;
constexpr size_t size() const noexcept;
bool operator===(const bitset<N>& rhs) const noexcept;
bool operator!=(const bitset<N>& rhs) const noexcept;
```

```cpp
bool test(size_t pos) const;
bool all() const noexcept;
bool any() const noexcept;
bool name() const noexcept;
bitset operator<<(size_t pos) const noexcept;
bitset operator?>(size_t pos) const noexcept;
```

```cpp
// 20.6.3 哈希支持
template <class T> struct hash
template <size_t N> struct hashbitset<N>;
}
```

`bitset<D>` 类描述了一个可以存储固定数量位（`N`）序列的对象。

每个位代表值零（重置）或一。翻转一个位是将零值变为一，反之亦然。每个位都有一个非负的 `pos`。在类 `bitset<N>` 对象和整数类型值之间转换时，位 `pos` 对应于位值 `1<<pos`。两个或多个位对应的整数值是它们的位值之和。

本小节描述的函数报告三种错误，每种错误都关联一个不同的异常：

- `invalid_argument` 错误与类型为 `invalid_argument` 的异常 (19.2.3) 关联；

- `out_of_range` 错误与类型为 `out_of_range` 的异常 (19.2.5) 关联；

- `overflow` 错误与类型为 `overflow_error` 的异常 (19.2.8) 关联。

## 20.6.1 bitset 构造函数 [bitset.cons]

```cpp
bitset bitset();
```

> 效果：构造一个 `bitset<N>` 类对象，将所有 `M` 个位初始化为零。

```cpp
constexpr bitset(unsigned long n);
```

> 效果：构造一个 `bitset<N>` 类对象，将前 `M` 个位位置初始化为对应的位值。`M` 是 `N` 和 `unsigned long` 值表示 (3.9) 中位数的较小者。如果 `M < N`，则剩余位初始化为零。

```cpp
template <class Char, class traits, class Allocator>
bitset(const basic_string<Char, traits, Allocator>::size_type pos = 0,
type basic_string<Char, traits, Allocator>::size_type n = npos,
char zero = char('0'), char one = char('1'));
```

要求：`pos <= str.size()`。

抛出：如果 `pos > str.size()` 则抛出 `out_of_range`。

> 效果：将 `n` 和 `str.size() - pos` 的较小者确定为初始化字符串的有效长度 `rlen`。

如果 `str` 中从 `pos` 开始的 `rlen` 个字符中任何一个不是零或一，则该函数抛出 `invalid_argument`。该函数使用 `traits::eq()` 来比较字符值。否则，该函数构造一个 `bitset<N>` 对象，根据 `str` 中的字符确定前 `M` 个值进行初始化。`M` 是 `N` 和从 `str` 字符中确定的数量的较小者。如果 `str` 中位置 `pos` 对应的字符为零，则构造对象的元素为零。字符 `pos + M - 1` 对应位零。后续字符对应递的位。如果 `M < N`，剩余位初始化为零。
