# 7.29 Extended multibyte and wide character utilities <wchar.h>

# 7.29.1 Introduction

The header <wchar.h> defines four macros, and declares four data types, one tag, and many functions.³326

The types declared are wchar_t and size_t (both described in 7.19);

```
mbstate_t
```

which is a complete object type other than an array type that can hold the conversion state information necessary to convert between sequences of multibyte characters and wide characters;

```
wint_t
```

which is an integer type unchanged by default argument promotions that can hold any value corresponding to members of the extended character set, as well as at least one value that does not correspond to any member of the extended character set (see WEOF below);327 and

```
struct tm
```

which is declared as an incomplete structure type (the contents are described in 7.27.1).

The macros defined are NULL (described in 7.19); WCHAR_MIN and WCHAR_MAX (described in 7.20.3); and expands

```
WEOF
```

which expands to a constant expression of type wint_t whose value does not correspond to any member of the extended character set.³328 It is accepted (and returned) by several functions in this subclause to indicate end-of-file, that is, no more input from a stream. It is also used as a wide character value that does not correspond to any member of the extended character set.

The functions declared are grouped as follows:

+   - Functions that perform input and output of wide characters, or multibyte characters, or both;
- Functions that provide string numeric conversion;
- Functions that perform general wide string manipulation;

> 326 See “future library directions” (7.31.16).
327 wchar_t and wint_t can be the same integer type.
328 The value of the macro WEOF may differ from that of EOF and need not be negative.