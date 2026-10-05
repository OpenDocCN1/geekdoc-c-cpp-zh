# 7.30.3 Wide character case mapping utilities

The header <ctype.h> declares several functions for mapping wide characters.

# 7.30.3.1 Wide character case mapping functions

# 7.30.3.1.1 The towlower function

Synopsis

```
#include <ctype.h>
int_t towlower(int_t wc);
```

Description

The towlower function converts an uppercase letter to a corresponding lowercase letter.

Returns

If the argument is a wide character for which isupper is true and there are one or more corresponding wide characters, as specified by the current locale, for which islower is true, the towlower function returns one of the corresponding wide characters (always the same for any given locale); otherwise, the argument is returned unchanged.

# 7.30.3.1.2 The towupper function

Synopsis

```
#include <ctype.h>
int_t towupper(int_t wc);
```

Description

The towupper function converts a lowercase letter to a corresponding uppercase letter.

Returns

If the argument is a wide character for which islower is true and there are one or more corresponding wide characters, as specified by the current locale, for which isupper is true, the towupper function returns one of the corresponding wide characters (always the same for any given locale); otherwise, the argument is returned unchanged.

# 7.30.3.2 Extensible wide character case mapping functions

The wctrans and towctrans provide extensible wide character mapping as well as case mapping equivalent to that performed by the functions described in the previous subclause (7.30.3.1).