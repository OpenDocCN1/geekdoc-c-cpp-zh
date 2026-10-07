# Description

2 The isspace function tests for any wide character that corresponds to a locale-specific set of white-space wide characters for which none of *iswalnum, isgraph,* or *iswpunct* is true.

# 7.30.2.1.11 The isupper function

# Synopsis

```
#include <wctype.h>
int isupper(int_t wc);
```

# Description

2 The isupper function tests for any wide character that corresponds to an uppercase letter or is a locale-specific set of wide characters for which none of *iswcntrl, iswdigit, iswpunct,* or *iswspace* is true.

# 7.30.2.1.12 The isxdigit function

# Synopsis

```
#include <wctype.h>
int isxdigit(int_t wc);
```

# Description

2 The isxdigit function tests for any wide character that corresponds to a hexadecimal-digit character (as defined in 6.4.4.1).

# 7.30.2.2 Extensible wide character classification

1 The functions wctype and isctype provide extensible wide character classification as well as testing equivalent to that performed by the functions described in the previous subclause (7.30.2.1).

# 7.30.2.2.1 The iswctype function

# Synopsis

```
#include <wctype.h>
int iswctype(int_t wc, wctype_desc desc);
```

# Description

2 The iswctype function determines whether the wide character has the property described by desc. The current setting of the LC_TYPE category should be the same as the call to wctype that returned the value desc.

3 Each of the following functions has a truth-equivalent to the call to the wide character classification function (7.30.2.1) in the comment that follows