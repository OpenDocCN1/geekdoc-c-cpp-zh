The isspace function tests for any wide character that corresponds to a locale-specific set of white-space wide characters for which none of iswalnum, iswgraph, or iswpunct is true.

# 7.30.2.1.11 The isupper function

Synopsis

```
#include <ctype.h>
int isupper(wint_t wc);
```

Description

The isupper function tests for any wide character that corresponds to an uppercase letter or is one of a locale-specific set of wide characters for which none of iswcntrl, iswdigit, iswpunct, isspace is true.

# 7.30.2.1.12 The isxdigit function

Synopsis

```
#include <ctype.h>
int isxdigit(wint_t wc);
```

Description

The isxdigit function tests for any wide character that corresponds to a hexadecimal-digit character (as defined in 6.4.4.1).

# 7.30.2.2 Extensible wide character classification functions

The functions wctype and isctype provide extensible wide character classification as well as testing equivalent to that performed by the functions described in the previous subclause (7.30.2.1).

# 7.30.2.2.1 The isctype function

Synopsis

```
#include <ctype.h>
int isctype(wint_t wc, wctype_t desc);
```

Description

The isctype function determines whether the wide character wc has the property described by desc. The current setting of the LC_CTYPE category shall be the same as during the call to wctype that returned the value desc.

Each of the following expressions has a truth-value equivalent to the call to the wide character classification function (7.30.2.1) in the comment that follows the expression: