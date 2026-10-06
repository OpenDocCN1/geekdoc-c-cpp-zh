# ISO/IEC 14882:2017(E)

5 Returns: lhs.compare(rhs) > 0.

```
template<class charT, class traits>
constexpr bool operator<=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

6 Returns: lhs.compare(rhs) < 0.

```
template<class charT, class traits>
constexpr bool operator>=(basic_string_view<charT, traits> lhs,
    basic_string_view<charT, traits> rhs) noexcept;
```

7 Returns: lhs.compare(rhs) >= 0.

# 24.4.4 Inserters and extractors

```
template<class charT, class traits>
basic_ostream<charT, traits>& os,
operator<<(basic_string_view<charT, traits> const&);
```

+   * Effects: Behaves as a formatted output (30.7.5.2.1) of os. A character sequence initializes of the elements defined by the range [str.begin(), str.end()). Determines padding for seq as in 30.7.5.2.1). Inserts seq as if calling os.dbuf()->sput(seq, n), where n is the larger of str.length() and str.size()); then calls os.width(n).

2 Returns: os

# 24.4.5 Hash

```
template<> struct hash<string_view>;ntemplate<> struct hash<u16_string_view>;ntemplate<> struct hash<u32_string_view>;ntemplate<> struct hash<wstring_view>;
```

The specialization is defined (23.14.15). [Note: The hash value of a string view object is equal to the hash value of the corresponding string object (24.3.5). end note]

# 24.4.6 Suffix for basic_string_view literals

1 Returns: string_view(str, len).

2 Returns: u16_string_view(str, len).

3 Returns: u32_string_view(str, len).

4 Returns: wstring_view(str, len).

# 24.5 Null-terminated sequence utilities

# 24.5.1 Header <cctype> synopsis

```
namespace std {
 intalnum(int c);
 isalpha(int c);
 isblankspace(int c);
```

©ISO/IEC - 2017 - All rights reserved

772