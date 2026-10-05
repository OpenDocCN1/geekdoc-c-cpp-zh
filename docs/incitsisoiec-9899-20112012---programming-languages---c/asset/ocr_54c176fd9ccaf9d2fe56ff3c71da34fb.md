# 7.20.2.5 Limits of greatest-width integer types

+   - minimum value of greatest-width signed integer type

```
INTMAX_MIN -(2^63 - 1)
```

+   - maximum value of greatest-width signed integer type

```
INTMAX_MAX 2^63 - 1
```

+   - maximum value of greatest-width unsigned integer type

```
UINTMAX_MAX 2^64 - 1
```

# 7.20.3 Limits of other integer types

1 The following object-like macros specify the minimum and maximum limits of integer types corresponding to those defined in other standard headers.

2 Each instance of these macros shall be replaced by a constant expression suitable for use in #if preprocessing directives, and this expression shall have the same type as an expression that is an object of the corresponding type converted according to the integer promotions. Its implementation-defined value shall be equal or greater in magnitude (absolute value) than the value given below, with the same sign. An implementation shall define only the macros corresponding to those typedef names it actually provides.263

+   - limits of ptrdiff_t

```
PTRDIFF_MIN -65535
PTRDIFF_MAX +65535
```

+   - limits of sig_atomic_t

```
SIG_ATOMIC_MIN see below
SIG_ATOMIC_MAX see below
```

+   - limit of size_t

```
SIZE_MAX 65535
```

+   - limits of wchar_t

```
WCHAR_MIN see below
WCHAR_MAX see below
```

+   - limits of wint_t

> 263) A freestanding implementation need not provide all of these types.