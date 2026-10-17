
- 影响: 等价于返回 `substr(pos1, n1).compare(str)`;

`constexpr compare(size_type pos1, size_type n1, basic_string_view str, size_type pos2, size_type n2) const;`

- 影响: 等价于返回 `substr(pos1, n1).compare(str.substr(pos2, n2))`;

# ISO/IEC 14882:2017(E)

| 表 66 — compare() 结果 |
| 条件 | 返回值 |
| :--- | :--- |
| `size()` < `str.size()` | < 0 |
| `size()` == `str.size()` | 0 |
| `size()` > `str.size()` | > 0 |

```
constexpr int compare(const char* s) const;
```

*影响: 等价于返回 compare(basic_string_view(s));*

```
constexpr int compare(size_type pos, size_type n1, const char* s) const;
```

*影响: 等价于返回 substr(pos, n1), compare(basic_string_view(s));*

```
constexpr int compare(size_type pos1, size_type n1, basic_string_view str) const;
```

*影响: 等价于返回 substr(pos1, n1), compare(string_view(s));*

## 24.4.2.7 查找 [string_view]

1. 本节描述了 `basic_string_view` 的成员 `find`, `rfind`, `first_of_`, `last_of_`, `find_not_of_`, 和 `last_not_of_`.

2. 这些函数的复杂度最坏为 `O(size())`，但实现可以更好。

3. 形式为 `constexpr return_type F(const char* s)` 的成员函数等价于 `basic_string_view(s)`。

4. 形式为 `constexpr return_type F(const char* s)` 的成员函数等价于 `substr(pos1, n1)`。

5. 形式为 `constexpr return_type F(const char* s)` 的成员函数等价于 `substr(pos1, n1).compare(str)`。

6. 形式为 `constexpr return_type F(const char* s)` 的成员函数等价于 `substr(pos1, n1).compare(str.substr(pos2, n2))`。

# ISO/IEC 14882:2017(E)

表 67 — 额外的 `basic_string_view` 比较重载

| 表达式 | 等价于 |
| --- | --- |
| `t == sv` | `S(t) == sv` |
| `sv == t` | `sv == S(t)` |
| `t != sv` | `S(t) != sv` |
| `sv != t` | `sv != S(t)` |
| `t < sv` | `S(t) < sv` |
| `sv < t` | `sv < S(t)` |
| `t > sv` | `S(t) > S(t)` |
| `sv > t` | `sv > S(t)` |
| `t <= sv` | `S(t) <= sv` |
| `sv <= t` | `sv <= S(t)` |
| `t >= sv` | `S(t) >= S(t)` |
| `sv >= t` | `sv >= S(t)` |

```cpp
template<class charT, class traits>
constexpr bool operator===(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept {
    return lhs.compare(rhs) == 0;
}
```

```cpp
template<class charT, class traits>
constexpr bool operator===(basic_string_view<charT, traits> lhs,
    _identitybasic_string_view<charT, traits> rhs) noexcept {
    return lhs.compare(rhs) == 0;
}
```

```cpp
template<class charT, class traits>
constexpr bool operator<=(basic_string_view<charT, traits> lhs,
    _identitybasic_string_view<charT, traits> rhs) noexcept {
    return lhs.compare(rhs) == 0;
}
```

-- 示例

```cpp
template<class charT, class traits>
constexpr bool operator!=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept {
    return lhs.compare(rhs) == 0;
}
```

2 返回：`lhs.compare(rhs) == 0`。

```cpp
template<class charT, class traits>
constexpr bool operator*=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

3 返回：`lhs.compare(rhs) != 0`。

```cpp
template<class charT, class traits>
constexpr bool operator<(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

4 返回：`lhs.compare(rhs) < 0`。

```cpp
template<class charT, class traits>
constexpr bool operator>(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

5 返回：`lhs.compare(rhs) > 0`。

```cpp
template<class charT, class traits>
constexpr bool operator<=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

6 返回：`lhs.compare(rhs) < 0`。

```cpp
template<class charT, class traits>
constexpr bool operator>=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

7 返回：`lhs.compare(rhs) >= 0`。

## 24.4.4 插入器与提取器

```cpp
template<class charT, class traits>
basic_ostream<charT, traits>& os,
operator<<(basic_string_view<charT, traits> const&);
```

- *影响*：表现为 `os` 的格式化输出 (30.7.5.2.1)。由范围 `[str.begin(), str.end())` 定义的元素初始化一个字符序列。如 30.7.5.2.1) 所示确定 `seq` 的填充。插入 `seq` 相当于调用 `os.dbuf()->sput(seq, n)`，其中 `n` 是 `str.length()` 和 `str.size()` 之间的较大值；然后调用 `os.width(n)`。

2 返回：`os`

## 24.4.5 哈希值

```cpp
template<> struct hash<string_view>;
template<> struct hash<u16_string_view>;
template<> struct hash<u32_string_view>;
template<> struct hash<wstring_view>;
```

该特化已定义 (23.14.15)。[注：`string_view` 对象的哈希值等于对应字符串对象的哈希值 (24.3.5)。结注]

## 24.4.6 basic_string_view 字面量的后缀

1 返回：`string_view(str, len)`。

2 返回：`u16_string_view(str, len)`。

3 返回：`u32_string_view(str, len)`。

4 返回：`wstring_view(str, len)`。

## 24.5 空终止序列实用程序

### 24.5.1 头文件 <cctype> 概要

```cpp
namespace std {
    intalnum(int c);
    int isalpha(int c);
    int isspace(int c);
    int iscntrl(int c);
    int isdigit(int c);
    int isgraph(int c);
    int islower(int c);
    int isprint(int c);
    intispunct(int c);
    int isspace(int c);
    int ispper(int c);
    int isxdigit(int c);
    int tolower(int c);
    int toupper(int c);
}
```

1 `<cctype>` 的内容和含义与 C 标准库 `<ctype.h>` 相同。另见 C 7.4

### 24.5.2 头文件 <cwctype> 概要

```cpp
namespace std {
    using wint_t = 见下;
    using wctrans_t = 见下;
    using vctype_t = 见下;

    int iswalnum(wint_t wc);
    int iswalpha(wint_t wc);
    int iswspace(wint_t wc);
    int iswcnt(wint_t wc);
    int iswidigit(wint_t wc);
    int iswgraph(wint_t wc);
    int iswlower(wint_t wc);
    int iswprint(wint_t wc);
    int isispunct(wint_t wc);
    int iswspace(wint_t wc);
    int isisupper(wint_t wc);
    int iswidigit(wint_t wc);
    int isctype(wint_t wc, wctrans_t desc);
    vctype_t cwctype(wint_t wc);
    int towlower(wint_t wc);
    int toupper(wint_t wc);
    int towctrans(wint_t wc, wctrans_t desc);
    wctrans_t isctype(const char* property);
}
#define WEOF
```

1 `<cwctype>` 的内容和含义与 C 标准库 `<ctype.h>` 相同。另见 C 7.3

### 24.5.3 头文件 <cwstring> 概要

```cpp
namespace std {
    using size_t = 21.2;

    void* copy(void* s1, void* s2, size_t n);
    void* memmove(void* s1, void* s2, size_t n);
    char* strcpy(char* s1, char* s2);
    char* strncpy(char* s1, char* s2, size_t n);
    char* strcat(char* s1, char* s2, size_t n);
    char* ncat(char* s1, char* s2, size_t n);
    void* memcmp(void* s1, void* s2, size_t n);
    int strcmp(char* s1, char* s2, size_t n);
    void memset(void* s, int c, size_t n);
    char* strerr(int err);
    size_t strstr(const char* s);
}
#define NULL 21.3
```

1 `<cstring>` 的内容和含义与 C 标准库 `<string.h>` 相同。

2 `strchr` 和 `strtok` 不要求避免数据竞态 (20.5.5.9)。

3 `memcmp` 和 `memmove` 是安全的 (21.10.4)。

注：`strspn`, `strbrk`, `strstr` 和 `memcmp` 有不同的签名，但它们在 C 标准库中的行为相同 (20.2)。注

另见 C 7.24

### 24.5.4 头文件 <cwchar> 概要

```cpp
namespace std {
    using size_t = 21.2;
    using mbtopt_t = 见下文;
    using wint_t = 见下文;

    struct {
        int fwprintf(FILE* stream, const wchar_t* format, ...);
        int vswprintf(FILE* stream, const wchar_t* format, ...);
        int vswprintf(const wchar_t* s, size_t n, const wchar_t* format, ...);
        int vscanf(const wchar_t* s, const wchar_t* format, ...);
        int vsprintf(const wchar_t* s, const wchar_t* format, va_list arg);
        int vwcemprintf(FILE* stream, const wchar_t* format, va_list arg);
        int vswmemprintf(const wchar_t* s, size_t n, const wchar_t* format, va_list arg);
        int vswcscan(const wchar_t* s, const wchar_t* format, va_list arg);
        int vsmemcmp(const wchar_t* s, size_t n, const wchar_t* format, va_list arg);
        int vsprintf(const wchar_t* format, va_list arg);
        int wprintf(const wchar_t* format, ...);
        int wscanf(const wchar_t* format, ...);
    };
};
```

[cwchar.syn]
