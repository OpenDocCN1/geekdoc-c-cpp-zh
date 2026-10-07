# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.29.4.2.4 The wmemmove function

# Synopsis

```
#include <wchar.h>
wchar_t *wmemmove(wchar_t *s1, const wchar_t *s2,
size_t n);
```

# Description

The wmemmove function copies n wide characters from the object pointed to by s2 to the object pointed to by s1. Copying takes place if the n wide characters from the object pointed to by s2 are first copied into a temporary array of n wide characters that does not overlap the objects pointed to by s1 or s2, and the n wide characters from the temporary array are copied into the object pointed to by s1.

# Returns

The wmemmove function returns the value of s1.

# 7.29.4.3 Wide string concatenation functions

# 7.29.4.3.1 The wscat function

# Synopsis

```
#include <wchar.h>
wchar_t *wscat(wchar_t * restrict s1,
wchar_t * restrict s2);
```

# Description

The wscat function appends a copy of the wide string pointed to by s2 (including the terminating null character) to the end of the wide string pointed to by s1. The initial wide character of s2 overwrites the null character at the end of s1.

# Returns

The wscat function returns the value of s1.

# 7.29.4.3.2 The wscncat function

# Synopsis

```
#include <wchar.h>
wchar_t *wscncat(wchar_t * restrict s1,
wchar_t * restrict s2,
size_t n);
```

# Description

The wscncat function appends more than n wide characters (a null wide character and those that follow are not appended) from the array pointed to by s2 to the end of