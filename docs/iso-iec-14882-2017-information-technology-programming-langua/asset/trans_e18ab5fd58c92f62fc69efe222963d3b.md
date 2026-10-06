

# ISO/IEC 14882:2017(E)

6 成员 eof() 应当返回 EOF。

```cpp
24.2.3.2 struct char_traits<char16_t>
namespace std {
    template struct char_traits<char16_t> {
        using type = char16_t;
        using int = uint_least16_t;
        using off_type = streamoff;
        using pos_type = u32streamspos;
        using state_type = nstate_t;

        static constexpr void assign(char_type c1, char_type c2) noexcept;
        static constexpr bool eq(char_type c1, char_type c2) noexcept;
        static constexpr bool lt(char_type c1, char_type c2) noexcept;

        static constexpr int compare(const char_type* s1, const char_type* s2, size_t n);
        static constexpr size_t length(const char_type* s, size_t n);
        static constexpr char_type* find(const char_type* s, size_t n, char_type a);

        static char_type* move(char_type* s1, const char_type* s2, size_t n);
        static char_type* copy(const char_type* s1, char_type* s2, size_t n);
        static char_type* find(const char_type* s1, const char_type* s2, size_t n);

        static constexpr int not_eof(const char_type& c) noexcept;
        static constexpr char_type to_char(const int_type& i) noexcept;
        static constexpr int_type to_int(const char_type& c) noexcept;
        static constexpr bool eq(int_type i1, int_type i2) noexcept;
        static constexpr bool not_eof(int_type i) noexcept;
    };
};
```

- 1 u16streamspos 是一个实现定义的类型，满足 30.2 和 30.3 中对 pos_type 的要求。

- 2 两个参数的成员 assign、eq 和 lt 的定义应当与内置运算符 ==、= 分别相同。

- 3 成员 eof() 应当返回一个实现定义的常量，该常量不能是一个有效的 UTF-16 编码单元。

```cpp
24.2.3.3 struct char_traits<char32_t>
namespace std {
    template struct char_traits<char32_t> {
        using type = char32_t;
        using int = uint_least32_t;
        using off_type = streamoff;
        using pos_type = u32streamspos;
        using state_type = nstate_t;

        static constexpr void assign(char_type c1, char_type c2) noexcept;
        static constexpr bool eq(char_type c1, char_type c2) noexcept;
        static constexpr bool lt(char_type c1, char_type c2) noexcept;

        static constexpr int compare(const char_type* s1, const char_type* s2, size_t n);
        static constexpr size_t length(const char_type* s, size_t n);
        static constexpr char_type* find(const char_type* s, size_t n, char_type a);
```

static char_type* move(char_type* s1, const char_type* s2, size_t n);
static char_type* copy(char_type* s1, const char_type* s2, size_t n);
static char_type* assign(char_type* s, size_t n, char_type a);
static constexpr int_type not_eof(int_type c) noexcept;
static constexpr char_type to_char(int_type c) noexcept;
static constexpr int_type to_int(char_type c) noexcept;
static constexpr bool eq(int_type c1, int_type c2) noexcept;
static constexpr int_type eof() noexcept;
```

- 1 类型 u32streams 应当是一个实现定义的类型，满足 30.2 和 30.3 中对 pos_type 的要求。

- 2 两个参数的成员 assign、eq 和 lt 的定义应当与内置运算符 ==、= 分别相同。

- 3 成员 eof() 应当返回一个实现定义的常量，该常量不能出现在有效的 UTF-16 编码单元中。

## 24.2.3.4 char_traits<wchar_t>

```cpp
namespace std {
template<> struct char_traits<wchar_t> {
  using char_type = wchar_t;
  using int_type = wint_t;
  using off_type = streamoff;
  using pos_type = wpos;
  using state_type = mbstate_t;

  static constexpr compare(const char_type& c1, const char_type& c2) noexcept;
  static constexpr bool eq(const char_type c1, const char_type c2) noexcept;
  static constexpr compare(const char_type* s1, const char_type* s2, size_t n);
  static constexpr size_t length(const char_type* s, size_t n);
  static constexpr char_type* find(const char_type* s, size_t n, const char_type a);
  static char_type* move(char_type* s1, const char_type* s2, size_t n);
  static char_type* copy(char_type* s1, const char_type* s2, size_t n);
  static char_type* assign(char_type* s, size_t n, char_type a);

  static constexpr int_type not_eof(int_type c) noexcept;
  static constexpr char_type to_char(int_type c) noexcept;
  static constexpr int_type to_int(char_type c) noexcept;
  static constexpr bool eq_int_type(int_type c1, int_type c2) noexcept;
  static constexpr int_type eof() noexcept;
};
```

- 1 int_type、pos_type 和 state_type 的定义类型应当为 wint_t、wstreams 和 mbstate_t。

- 2 类型 u32streams 应当是一个实现定义的类型，满足 30.2 和 30.3 中对 pos_type 的要求。

- 3 类型 mbstate_t 定义在 <wchar> 中，可以表示任何多字节编码。

- 4 两个参数的成员 assign、eq 和 lt 的定义应当与内置运算符 ==、= 分别相同。

- 5 成员 eof() 应当返回一个实现定义的常量，该常量不能是一个有效的 UTF-16 编码单元。

