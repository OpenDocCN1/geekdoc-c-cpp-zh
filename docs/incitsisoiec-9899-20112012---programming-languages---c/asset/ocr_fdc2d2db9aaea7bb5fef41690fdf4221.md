# 7.29.6.1 Single-byte/wide character conversion functions

# 7.29.6.1.1 The btowc function

Synopsis

```
#include <wchar.h>
wint_t btowc(int c);
```

Description

The btowc function determines whether c constitutes a valid single-byte character in the initial shift state.

Returns

The btowc function returns EOF if c has the value EOF or if (unsigned char) c does not constitute a valid single-byte character in the initial shift state. Otherwise, it returns the wide character representation of that character.

# 7.29.6.1.2 The wctob function

Synopsis

```
#include <wchar.h>
wctob(wint_t c);
```

Description

The wctob function determines whether c corresponds to a member of the extended character set whose multibyte character representation is a single byte when in the initial shift state.

Returns

The wctob function returns EOF if c does not correspond to a multibyte character with length one in the initial shift state. Otherwise, it returns the single-byte representation of that as an unsigned char converted to an int.

# 7.29.6.2 Conversion state functions

# 7.29.6.2.1 The mbsisinit function

Synopsis

```
#include <wchar.h>
mbsisinit(const mstate_t *ps);
```

Description

If ps is not a null pointer, the mbsisinit function determines whether the referenced mstate_t object describes an initial conversion state.