```
long double stold(constwstring& str, size_t* idx = nullptr);
wstring to_wstring(int val);
wstring to_wstring(unsigned val);
wstring to_wstring(long val);
wstring to_wstring(unsigned long val);
wstring to_wstring(long long val);
wstring to_wstring(unsigned long long val);
wstring to_wstring(float val);
wstring to_wstring(double val);
wstring to_wstring(long double val);

namespace pmr {
    template<class charT, class traits = char_traits<charT>>
        using basic_string = std::basic_string<charT, traits, polymorphic_allocator<charT>>;

    using string      = basic_string<char>;
    using u8string    = basic_string<char8_t>;
    using u16string   = basic_string<char16_t>;
    using u32string   = basic_string<char32_t>;
    usingwstring      = basic_string<wchar_t>;
}

// 21.3.6, hash support
template<class T> struct hash;
template<> struct hash<string>;
template<> struct hash<u8string>;
template<> struct hash<u16string>;
template<> struct hash<u32string>;
template<> struct hash<wstring>;
template<> struct hash<pmr::string>;
template<> struct hash<pmr::u8string>;
template<> struct hash<pmr::u16string>;
template<> struct hash<pmr::u32string>;
template<> struct hash<pmr::wstring>;

inline namespace literals {
inline namespace string_literals {
    // 21.3.7, suffix for basic_string literals
    constexpr string      operator""s(const char* str, size_t len);
    constexpr u8string    operator""s(const char8_t* str, size_t len);
    constexpr u16string   operator""s(const char16_t* str, size_t len);
    constexpr u32string   operator""s(const char32_t* str, size_t len);
    constexprwstring      operator""s(const wchar_t* str, size_t len);
}
}
```

# 21.3.3 Class template basic_string [basic.string]

# 21.3.3.1 General [basic.string.general]

1 The class template basic_string describes objects that can store a sequence consisting of a varying number of arbitrary char-like objects with the first element of the sequence at position zero. Such a sequence is also called a “string” if the type of the char-like objects that it holds is clear from context. In the rest of 21.3.3, the type of the char-like objects held in a basic_string object is designated by charT.

2 A specialization of basic_string is a contiguous container (22.2.1).

3 In all cases, [data(), data() + size()] is a valid range, data() + size() points at an object with value charT() (a “null terminator”), and size() <= capacity() is true.

```
namespace std {
    template<class charT, class traits = char_traits<charT>,
             class Allocator = allocator<charT>>
    class basic_string {
```