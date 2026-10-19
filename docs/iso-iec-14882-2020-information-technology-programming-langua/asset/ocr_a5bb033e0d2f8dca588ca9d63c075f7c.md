# ISO/IEC 14882:2020(E)

Table 69: Character traits requirements (continued)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|---|---|---|---|
| X::eof() | X::int_type | Returns: a value e such that X::eq_int_type(e,X::to_int_type(c)) is false for all values c. | constant |

2 The class template
template<class charT> struct char_traits;
is provided in the header <string> as a basis for explicit specializations.

# 21.2.3 Traits typedefs [char.traits.typedefs]

```
using int_type = see below;
```

1 Preconditions: int_type shall be able to represent all of the valid characters converted from the corresponding char_type values, as well as an end-of-file value, eof().227

```
using state_type = see below;
```

2 Preconditions: state_type meets the Cpp17Destructible (Table 32), Cpp17CopyAssignable (Table 31), Cpp17CopyConstructible (Table 29), and Cpp17DefaultConstructible (Table 27) requirements.

# 21.2.4 char_traits specializations [char.traits.specializations]

# 21.2.4.1 General [char.traits.specializations.general]

```
namespace std {
    template<> struct char_traits<char>;
    template<> struct char_traits<char8_t>;
    template<> struct char_traits<char16_t>;
    template<> struct char_traits<char32_t>;
    template<> struct char_traits<wchar_t>;
}
```

1 The header <string> defines five specializations of the class template char_traits: char_traits<char>, char_traits<char8_t>, char_traits<char16_t>, char_traits<char32_t>, and char_traits<wchar_t>.

# 21.2.4.2 struct char_traits<char> [char.traits.specializations.char]

```
namespace std {
    template<> struct char_traits<char> {
        using char_type = char;
        using int_type = int;
        using off_type = streamoff;
        using pos_type = streampos;
        using state_type = mbstate_t;
        using comparison_category = strong_ordering;

        static constexpr void assign(char_type& c1, const char_type& c2) noexcept;
        static constexpr bool eq(char_type c1, char_type c2) noexcept;
        static constexpr bool lt(char_type c1, char_type c2) noexcept;

        static constexpr int compare(const char_type* s1, const char_type* s2, size_t n);
        static constexpr size_t length(const char_type* s);
        static constexpr const char_type* find(const char_type* s, size_t n, const char_type& a);

        static constexpr char_type* move(char_type* s1, const char_type* s2, size_t n);
        static constexpr char_type* copy(char_type* s1, const char_type* s2, size_t n);
        static constexpr char_type* assign(char_type* s, size_t n, char_type a);
    }
```

227) If eof() can be held in char_type then some iostreams operations can give surprising results.