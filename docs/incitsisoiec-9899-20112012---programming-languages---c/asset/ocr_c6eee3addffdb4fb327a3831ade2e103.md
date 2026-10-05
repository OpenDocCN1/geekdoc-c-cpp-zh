# 7.29.4.6 Miscellaneous functions

# 7.29.4.6.1 The wcslen function

Synopsis

```
#include <wchar.h>
size_t wcslen(const wchar_t *s);
```

Description
The wcslen function computes the length of the wide string pointed to by s.

Returns

The wcslen function returns the number of wide characters that precede the terminating
ull wide character.

# 7.29.4.6.2 The wmemset function

Synopsis

```
#include <wchar.h>
wchar_t *wmemset(wchar_t *s, wchar_t c, size_t n);
```

Description
The wmemset function copies the value of c into each of the first n wide characters of
the object pointed to by s.

Returns

The wmemset function returns the value of s.

# 7.29.5 Wide character conversion functions

# 7.29.5.1 The wcsftime function

Synopsis

```
#include <time.h>
#include <wchar.h>
size_t wcsftime(wchar_t * restrict s,
size_t maxsize,
const wchar_t * restrict format,
const struct tm * restrict timeptr);
```

Description
The wcsftime function is equivalent to the strftime function, except that:

+   - The argument s points to the initial element of an array of wide characters into which
the generated output is to be placed.