# ISO/IEC 14882:2017(E)

25.4.1.3.2 ctype<char> members
In the following member descriptions, for unsigned char values v where >= table_size, table() {} is assumed to have an implementation-specific value (possibly different for each such value v) without performing the array lookup.

```
explicit ctype(unsigned char* mask = nullptr, bool del = false, size_t refs = 0);
```

Requires: either 0 or an array of at least table_size elements.
Effects: Passes its refs to its base constructor.

```
bool is(mask m, const char c);
const* is(const char low, const char high, mask vec, const vec c);
```

Effects: The second return, for all *p in the range [low, high], assigns to vec[p - low] the value table((unsigned char*)p).
Returns: The first form returns table((unsigned char)c) & m; the second form returns high.

```
const char* scan(mask m, const char low, const char high);
```

Returns: The smallest p in the range [low, high] such that table((unsigned char*)p) & m is true.

```
const char* scan_not(mask m, const char low, const char high, const char high);
```

Returns: The smallest p in the range [low, high] such that table((unsigned char*)p) & m is false.

```
char toupper(const char c);
const* toupper(char low, const char high);
```

Returns: do_tolower(const c) or do_tolower(low, high), respectively.

```
char tolower(const char c);
const* tolower(char low, const char high);
```

Returns: do_tolower(const c) or do_wider(low, high), respectively.

```
char wider(const char c);
const* wider(const char low, const char high, char* to);
```

Returns: do_narrow(char c, char dfault);
const* do_narrow(const char low, const char high, char dfault, char* to);

Returns: do_narrow(const c, dfault) or do_wider(low, high, dfault, to), respectively.

```
const mask* table() noexcept;
```

Returns: The first constructor argument, if it was nonzero, otherwise classic_table().

# 25.4.1.3.3 ctype<char> static members

```
static const mask* classic_table() noexcept;
```

Returns: A pointer to the initial element of an array of size table_size which represents the characters of the "C" locale.