
12 For a string in a non-Unicode encoding, the width of a string is unspecified.

13 A zero (0) character preceding the width field pads the field with leading zeros (following any indication of sign or base) to the field width, except when applied to an infinity or NaN. This option is only valid for arithmetic types other than charT and bool or when an integer presentation type is specified. If the 0 character and an align option both appear, the 0 character is ignored.

[Example 3:

```
char c = 120;
string s1 = format("{:+06d}", c);    // value of s1 is "+00120"
string s2 = format("{:#06x}", 0xa);    // value of s2 is "0x000a"
string s3 = format("{:<06}", -42);    // value of s3 is "-42    " (0 is ignored because of < alignment)
```

— end example]

14 The nonnegative-integer in precision is a decimal integer defining the precision or maximum field size. It can only be used with floating-point and string types. For floating-point types this field specifies the formatting precision. For string types, this field provides an upper bound for the estimated width of the prefix of the input string that is copied into the output. For a string in a Unicode encoding, the formatter copies to the output the longest prefix of whole extended grapheme clusters whose estimated width is no greater than the precision.

15 When the L option is used, the form used for the conversion is called the locale-specific form. The L option is only valid for arithmetic types, and its effect depends upon the type.

- (15.1) — For integral types, the locale-specific form causes the context’s locale to be used to insert the appropriate digit group separator characters.
- (15.2) — For floating-point types, the locale-specific form causes the context’s locale to be used to insert the appropriate digit group and radix separator characters.
- (15.3) — For the textual representation of bool, the locale-specific form causes the context’s locale to be used to insert the appropriate string as if obtained with numpunct::truename or numpunct::falsename.

16 The type determines how the data should be presented.

17 The available string presentation types are specified in Table 61.

### Table 61: Meaning of type options for strings [tab:format.type.string]

| Type | Meaning |
| --- | --- |
| none, s | Copies the string to the output. |

18 The meaning of some non-string presentation types is defined in terms of a call to to_chars. In such cases, let [first, last) be a range large enough to hold the to_chars output and value be the formatting argument value. Formatting is done as if by calling to_chars as specified and copying the output through the output iterator of the format context.

[Note 7: Additional padding and adjustments are performed prior to copying the output through the output iterator as specified by the format specifiers. — end note]

19 The available integer presentation types for integral types other than bool and charT are specified in Table 62.

[Example 4:

```
string s0 = format("{}", 42);    // value of s0 is "42"
string s1 = format("{0:b} {0:d} {0:o} {0:x}", 42);    // value of s1 is "101010 42 52 2a"
string s2 = format("{0:#x} {0:#X}", 42);    // value of s2 is "0x2a 0X2A"
string s3 = format("{:L}", 1234);    // value of s3 can be "1,234"    // (depending on the locale)
```

— end example]

### Table 62: Meaning of type options for integer types [tab:format.type.int]

| Type | Meaning |
| --- | --- |
| b | `to_chars(first, last, value, 2)`; the base prefix is `0b`. |
| B | The same as `b`, except that the base prefix is `0B`. |
| c | Copies the character `static_cast<charT>(value)` to the output. Throws `format_error` if `value` is not in the range of representable values for `charT`. |
| d | `to_chars(first, last, value)`. |
| o | `to_chars(first, last, value, 8)`; the base prefix is `0` if `value` is nonzero and is empty otherwise. |
| x | `to_chars(first, last, value, 16)`; the base prefix is `0x`. |
| X | The same as `x`, except that it uses uppercase letters for digits above 9 and the base prefix is `0X`. |
| none | The same as `d`. [Note 8: If the formatting argument type is `charT` or `bool`, the default is instead `c` or `s`, respectively. — end note] |

20 The available charT presentation types are specified in Table 63.

### Table 63: Meaning of type options for charT [tab:format.type.char]

| Type | Meaning |
| --- | --- |
| none, c | Copies the character to the output. |
| b, B, d, o, x, X | As specified in Table 62. |

21 The available bool presentation types are specified in Table 64.

### Table 64: Meaning of type options for bool [tab:format.type.bool]

| Type | Meaning |
| --- | --- |
| none, s | Copies textual representation, either true or false, to the output. |
| b, B, c, d, o, x, X | As specified in Table 62 for the value `static_cast<unsigned char>(value)`. |

[Note 9: In either case, a sign is included if indicated by the sign option. — end note]

22 The available floating-point presentation types and their meanings for values other than infinity and NaN are specified in Table 65. For lower-case presentation types, infinity and NaN are formatted as `inf` and `nan`, respectively. For upper-case presentation types, infinity and NaN are formatted as `INF` and `NAN`, respectively.

### Table 65: Meaning of type options for floating-point types [tab:format.type.float]

| Type | Meaning |
| --- | --- |
| a | If precision is specified, equivalent to `to_chars(first, last, value, chars_format::hex, precision)` where `precision` is the specified formatting precision; equivalent to `to_chars(first, last, value, chars_format::hex)` otherwise. |
| A | The same as `a`, except that it uses uppercase letters for digits above 9 and `P` to indicate the exponent. |
| e | Equivalent to `to_chars(first, last, value, chars_format::scientific, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| E | The same as `e`, except that it uses `E` to indicate exponent. |
| f, F | Equivalent to `to_chars(first, last, value, chars_format::fixed, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| g | Equivalent to `to_chars(first, last, value, chars_format::general, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| G | The same as `g`, except that it uses `E` to indicate exponent. |
| none | If precision is specified, equivalent to `to_chars(first, last, value, chars_format::general, precision)` where `precision` is the specified formatting precision; equivalent to `to_chars(first, last, value)` otherwise. |

23 The available pointer presentation types and their mapping to to_chars are specified in Table 66.

### Table 66: Meaning of type options for pointer types [tab:format.type.ptr]

| Type | Meaning |
| --- | --- |
| none, p | If `uintptr_t` is defined, `to_chars(first, last, reinterpret_cast<uintptr_t>(value), 16)` with the prefix `0x` added to the output; otherwise, implementation-defined. |

[Note 10: Pointer presentation types also apply to `nullptr_t`. — end note]

## 20.20.3 Error reporting [format.err.report]

1 Formatting functions throw `format_error` if an argument `fmt` is passed that is not a format string for `args`. They propagate exceptions thrown by operations of formatter specializations and iterators. Failure to allocate storage is reported by throwing an exception as described in 16.4.6.13.

## 20.20.4 Formatting functions [format.functions]

1 In the description of the functions, operator + is used for some of the iterator categories for which it does not have to be defined. In these cases the semantics of `a + n` are the same as in 25.2.

```
template<class... Args>
  string format(string_view fmt, const Args&... args);
```

2 Effects: Equivalent to:

```
return vformat(fmt, make_format_args(args...));
```

```
template<class... Args>
  wstring format(wstring_view fmt, const Args&... args);
```

3 Effects: Equivalent to:

```
return vformat(fmt, make_wformat_args(args...));
```

```
template<class... Args>
  string format(const locale& loc, string_view fmt, const Args&... args);
```

4 Effects: Equivalent to:

```
return vformat(loc, fmt, make_format_args(args...));
```

```
template<class... Args>
wstring format(const locale& loc, wstring_view fmt, const Args&... args);
```

Effects: Equivalent to:

```
return vformat(loc, fmt, make_wformat_args(args...));
```

```
string vformat(string_view fmt, format_args args);
wstring vformat(wstring_view fmt, wformat_args args);
string vformat(const locale& loc, string_view fmt, format_args args);
wstring vformat(const locale& loc, wstring_view fmt, wformat_args args);
```

Returns: A string object holding the character representation of formatting arguments provided by `args` formatted according to specifications given in `fmt`. If present, `loc` is used for locale-specific formatting.

Throws: As specified in 20.20.3.

```
template<class Out, class... Args>
Out format_to(Out out, string_view fmt, const Args&... args);
template<class Out, class... Args>
Out format_to(Out out, wstring_view fmt, const Args&... args);
```

Effects: Equivalent to:

```
using context = basic_format_context<Out, decltype(fmt)::value_type>;
return vformat_to(out, fmt, make_format_args<context>(args...));
```
