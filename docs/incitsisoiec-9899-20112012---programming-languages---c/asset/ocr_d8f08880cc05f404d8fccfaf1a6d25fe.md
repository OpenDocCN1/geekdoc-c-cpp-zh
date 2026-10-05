pointed to by s2.

# 7.24.4.3 The strlen function

Synopsis

```
#include <string.h>
int strlen(const char *s1, const char *s2);
```

Description
strlen function compares the string pointed to by s1 to the string pointed to by s2, both interpreted as appropriate to the LC_COLLATE category of the current locale.

Returns

The strlen function returns an integer greater than, equal to, or less than zero, as the string pointed to by s1 is greater than, equal to, or less the string pointed to by s2 when both are interpreted as appropriate to the current locale.

# 7.24.4.4 The strcmp function

Synopsis

```
#include <string.h>
int strcmp(const char *s1, const char *s2, size_t n);
```

Description
strcmp function compares not than n characters (characters that follow a null character are not compared) from the array pointed to by s1 to the array pointed to by s2.

Returns

The strcmp function returns an integer greater than, equal to, or less than zero, as the possibly null-terminated array pointed to by s1 is greater than, equal to, or less the possibly null-terminated array pointed to by s2.

# 7.24.4.5 The strxfrm function

Synopsis

```
#include <string.h>
size_t strxfrm(char * restrict s1, const char * restrict s2, size_t n);
```

Description

strxfrm function transforms the string pointed to by s2 and places the resulting string into the array pointed to by s1. The transformation is that if the strcmp function is applied to two transformed strings, it returns a value greater than, equal to, or