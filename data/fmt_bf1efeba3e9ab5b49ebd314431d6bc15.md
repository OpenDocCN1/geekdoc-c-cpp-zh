
```cpp
namespace std {
    template<>struct char_traits<char32_t> {
        typedef char32_t char_type;
        typedef uint_least32_t int_type;
        typedef streamoff off_type;
        typedef u32streampos pos_type;
        typedef mbstate_t state_type;
        static void assign(char_type& c1, const char_type& c2) noexcept;
        static constexpr bool eq(char_type c1, const char_type c2) noexcept;
        static constexpr bool neq(char_type c1, const char_type c2) noexcept;

        static int compare(const char_type* s1, const char_type* s2, size_t n);
        static size_t length(const char_type* s);
        static char_type find(const char_type* s, size_t n, const char_type& a);
        static char_type move(const char_type* s1, const char_type* s2, size_t n);
        static char_type copy(const char_type* s1, const char_type* s2, size_t n);
        static char_type assign(const char_type* s1, size_t n);

        static constexpr int_type not_of(int_type c) noexcept;
        static constexpr char_type to_char(const char_type c) noexcept;
        static constexpr bool eq_int(int_type c1, int_type c2) noexcept;
        static constexpr int_type neof(int_type c) noexcept;
    };
}
```

# ISO/IEC

```cpp
const char_type& a;
static char_type* move(char_type* s1, const char_type* s2, size_t n);
static char_type* copy(char_type* s1, const char_type* s2, size_t n);
static char_type* assign(char_type* s, size_t n, char_type a);
static constexpr int_type not_of(int_type c) noexcept;
static constexpr char_type_to_char_type(int_type c) noexcept;
static constexpr int_type_to_int_type(char_type c) noexcept;
static constexpr bool b_eq(int_type c1, int_type c2) noexcept;
static constexpr int_type eof(void) noexcept;
}
```

1. `u32wstreams` 应当是一个实现定义的类型，满足 27.2.2 和 27.3 中对 `pos_type` 的要求。
2. 两个参数的 `assign`、`eq` 和 `lt` 的定义应当分别与内置运算符 `=`、`<` 和 `<` 相同。
3. 成员 `eof()` 应当返回一个不能作为代码单元的实现定义的常量。

## 21.2.3.4 struct char_traits<wchar_t>

```cpp
namespace std {
template<typename T> struct char_traits<T> {
    typedef T char_type;
    typedef wint_t int_type;
    typedef streamoff off_type;
    typedef wstreampos pos_type pos_type;
    typedef mbstate_t state_type;
};
[char.traits.specializations.wchar_t]

    static void assign(char_type& c1, const char_type& c2) noexcept;
    static constexpr bool b_eq(char_type c1, char_type c2) noexcept;
    static constexpr bool b_lt(char_type c1, char_type c2) noexcept;

    static int compare(const char_type* s1, const char_type* s2, size_t n);
    static size_t length(const char_type* s);
    static const char_type* find(const char_type* s, size_t n, char_type a);
    static char_type* move(const char_type* s1, const char_type* s2, size_t n);
    static char_type* copy(const char_type* s1, const char_type* s2, size_t n);
    static char_type* assign(char_type* s, size_t n, char_type a);

    static constexpr int_type not_of(int_type c) noexcept;
    static constexpr char_type_to_char_type(int_type c) noexcept;
    static constexpr int_type_to_int_type(char_type c) noexcept;
    static constexpr bool b_eq(int_type c1, int_type c2) noexcept;
}
```

1. `int_type`、`pos_type` 和 `state_type` 的定义类型应当分别为 `wint_t`、`wstreams` 和 `mbstate_t`。
2. `wstreams` 应当是一个实现定义的类型，满足 27.2.2 和 27.3 中对 `pos_type` 的要求。

## § 21.2.3.4

## N4296

类型 `mbstate_t` 定义在 `<char>` 中，可以表示实现支持的多字节字符编码规则集中可能发生的任何转换状态。

两个参数的方法 `assign`、`eq` 和 `lt` 的定义应当分别与内置运算符 `=`、`==` 和 `<` 相同。

成员 `eof()` 应当返回 `EOF`。

## 21.3 String类 [string.classes]

头文件 `<string>` 定义了用于处理类字符对象长度序列的 `basic_string` 模板以及四种类型 `u16string`、`u32string` 和 `wstring`，分别命名为 `basic_string<char>`、`basic_string<char16_t>`、`basic_string<char32_t>` 和 `basic_string<wchar_t>`。

## 头文件 <initializer_list> 概要

namespace std {

```cpp
// 21.2. char 特性
template<class charT> struct char_traits;
template<> struct char_traits<char>;
template<> struct char_traits<char16_t>;
template<> struct char_traits<char32_t>;
template<> struct char_traits<wchar_t>;
```

```cpp
// 21.4. basic_string
template<class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT>
basic_string;
```

```cpp
template<class charT, class traits, class Allocator>
operator+(const basic_string<charT,traits,Allocator>& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+=(const basic_string<charT,traits,Allocator>& lhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+=(const basic_string<charT,traits,Allocator>& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+=(const basic_string<charT,traits,Allocator>& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator(const charT& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator(const charT& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+=(const charT& lhs,
       const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+(const basic_string<charT,traits,Allocator>&&
```

```cpp
template<class charT, class traits, class Allocator>
operator+(charT lhs, const basic__<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+(charT lhs, basic_string<charT,traits,Allocator>&& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator+(const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& lhs) noexcept;
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator!=(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator!=(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator!=(const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& lhs) noexcept;
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
operator!=(const basic_string<charT,traits,Allocator>&& lhs) noexcept;
```

```cpp
template<class charT, class traits, class Allocator>
operator=(const basic_string<charT,traits,Allocator>&& lhs,
           const charT& rhs);
```

```cpp
bool operator>(const charT* lhs,
    const basic_string<charT,traits,Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
bool operator<<=(const basic_string<charT,traits,Allocator>&& lhs) noexcept;
```
