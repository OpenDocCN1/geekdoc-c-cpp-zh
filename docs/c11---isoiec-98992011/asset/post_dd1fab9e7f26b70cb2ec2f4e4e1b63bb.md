
# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

## 7.30.3.2.1 The wctrans function

Synopsis

```
#include <ctype.h>
wint_t wctrans(wint_t wc, wctrans_t desc);
```

Description

The wctrans function maps the wide character wc using the mapping described by desc. The current setting of the LC_TYPE category shall be the same as during the call to wctrans that returned the value desc.

Each of the expressions behaves the same as the call to the wide character case mapping function (7.30.3.1) in the comment that follows the expression:

```
wctrans(wc
```

Returns

The wctrans function returns the mapped value of wc using the mapping described by desc. If desc is zero, the wctrans function returns the value of wc.

## 7.30.3.2.2 The wctrans function

Synopsis

```
#include <ctype.h>
wctrans_t wctrans(const char *pointer);
```

Description

The wctrans function constructs a value with wctrans_t that describes a mapping between wide characters identified by the string argument property.

The strings listed in the description of the wctrans function shall be valid in all locales as property arguments to the wctrans function.

Returns

If property identifies a valid mapping of wide characters according to the LC_TYPE category of the current locale, the wctrans function returns a nonzero value that is valid as the second argument to the wctrans function; otherwise, it returns zero.

## 7.31 Future library directions

The following names are grouped under individual headers for convenience. All external names described below are reserved no matter what headers are included by the program.

### 7.31.1 Complex arithmetic <complex.h>

The function names

| cexpml | clog2 |
| cerfc | clog10 |
| cexp2 | clog1p |
| clgamma | ctgamma |

and the .h names suffixed with **f** or 1 may be added to the declarations in the <complex.h> header.

### 7.31.2 Character handling <ctype.h>

Function names begin with either **is** or **to**, and a lowercase letter may be added to the declarations in the <ctype.h> header.

### 7.31.3 Errors <errno.h>

Macros begin with **E** and a digit or **E** and an uppercase letter may be added to the macros defined in the <errno.h> header.

### 7.31.4 Floating-point environment <fenv.h>

Macros begin with **FE_** and an uppercase letter may be added to the macros defined in the <fenv.h> header.

### 7.31.5 Format conversion of integer types <inttypes.h>

Macros begin with either **PRI** or **SCN**, and a lowercase letter or **X** may be added to the macros defined in the <inttypes.h> header.

### 7.31.6 Localization <locale.h>

Macros begin with **LC_** and an uppercase letter may be added to the macros defined in the <locale.h> header.

### 7.31.7 Signal handling <signal.h>

Macros begin with either **SIG** and an uppercase letter or **SIG_** and an uppercase letter may be added to the macros defined in the <signal.h> header.

### 7.31.8 Atomics <stdatomic.h>

Macros begin with **ATOMIC_** and an uppercase letter may be added to the macros defined in the <stdatomic.h> header. Typedef names that begin with **atomic_** or **memory_** and a lowercase letter may be added to the declarations in the <stdatomic.h> header. Enumeration constants that begin with **memory_order_** and a lowercase letter may be added to the definition of the memory_order type in the <stdatomic.h> header. Function names begin with atomic_ and a lowercase letter may be added to the declarations in the <stdatomic.h> header.

### 7.31.9 Boolean type and values <stdbool.h>

The ability to define and perhaps then redefine the macros bool, true, and false is an obsolete feature.

### 7.31.10 Integer types <stdint.h>

Typedef names with int or uint ending with _t may be added to the types defined in the <stdint.h> header. Macro names begin with INT and UINT ending with _MAX, _MIN, or _C may be added to the macros defined in the <stdint.h> header.

### 7.31.11 Input/output <stdio.h>

Lowercase letters may be added to the conversion specifiers and length modifiers in fprintf and fscanf. Other characters may be used in extensions.

The use of unget on a binary stream where the position index is zero prior to the call is an obsolete feature.

### 7.31.12 General utilities <stdlib.h>

Function names begin with str and a lowercase letter may be added to the declarations in the <stdlib.h> header.

### 7.31.13 String handling <string.h>

Function names begin with str, mem, or wcs and a lowercase letter may be added to the declarations in the <string.h> header.

### 7.31.14 Date and time <time.h>

Macros beginning with TIME_ and an uppercase letter may be added to the macros in the <time.h> header.

### 7.31.15 Threads <threads.h>

Function names, enumerations and constants that begin with either end_mtx_thrd_ or tss_ and a lowercase letter may be added to the declarations in the <threads.h>.

### 7.31.16 Extended multibyte and wide character utilities <wchar.h>

Function names begin with wcs and a lowercase letter may be added to the declarations in the <wchar.h> header.

Lowercase letters may be added to the conversion specifiers and length modifiers in fprintf and fscanf. Other characters may be used in extensions.

### 7.31.17 Wide character classification and mapping utilities <wctype.h>

Function names that begin with is or to and a lowercase letter may be added to the declarations in the <wctype.h> header.

## Annex A

### §A.1 Lexical

Lexical elements

- token
- constant
- punctuator
- whitespace
- identifier

### §A.1.2 Keywords

- auto
- break
- case
- const
- continue
- default
- do
- double
- else
- for
- enum
- extern
- float
- for
- goto
- if
- inline
- int
- register
- return
- return
- short
- sizeof
- signed
- static
- struct
- switch
- typedef
- unsigned
- union
- void
- volatile
- while
- _Atomic (implementation)

### §A.1.3 Identifiers

- identifier
- nondigit
- other characters

### §A.1.4 Universal character names

- \u hexquad

### §A.1.5 Constants

- integer-constant
- floating-constant
- enumeration-constant
- decimal-constant
- octal-constant
- hexadecimal-constant
