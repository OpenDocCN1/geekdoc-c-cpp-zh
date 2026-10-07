
ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

+   3 The macros defined are NULL (described in 7.19); and

```
LC_ALL
LC_COLLATE
LC_CTYPE
LC_MONETARY
LC_NUMERIC
LC_TIME
```

which expand to integer expressions with distinct values, suitable for use as the first argument to the setlocale function^{222} Additional macro definitions, beginning with the characters LC_ and an uppercase letter,^{223} may also be specified by the implementation.

## 7.11.1 Local control

### 7.11.1.1 The setlocale function

Synopsis

```c
 #include <locale.h>
char *setlocale(int category, const char *locale);
```

Description

+   2 The setlocale function selects the appropriate portion of the program's locale as specified by the category and locale arguments. The setlocale function may be used to change or query the program's current locale or portions thereof. The value LC_ALL for category names only a portion of the program's locale. LC_COLLATE affects the behavior of the strcoll and strftime functions. LC_CTYPE affects the behavior of the character handling functions^{224} and the multibyte wide character functions. LC_MONETARY affects the formatting information returned by the localconv function. LC_NUMERIC affects the decimal-point character for the formatted/output functions and the string conversions, as well as the nonetary formatting information returned by the localconv function. LC_TIME affects the behavior of the strftime and wcsftime functions.

+   3 A value of "C" for locale specifies the minimum environment for C translation; a value of "" for locale specifies the locale-specific native environment. Other implementation-defined strings may be passed as the second argument to setlocale.

222) ISO/IEC 9945-2 specifies locale and character formats that may be used to specify locales for C.

223) See "future library directions" (7.31.6).
224 The only functions in C whose behavior is not affected by the current locale is isdigit and isdigit.

224

Library

§7.11.1

© ISO/IEC 2011 – All rights reserved
ISO/IEC 9899:2011 (E)

+   4 At program startup, the equivalent of
`setlocale(LC_ALL, "C")`
is executed.

+   5 A call to the **setlocale** function may introduce a data race with other calls to the **setlocale** function or with functions that are affected by the current locale.
The implementation shall behave as if no library function calls the **setlocale** function.

# Returns

6 If a pointer to a string is given for **locale** and the selection can be honored, the **setlocale** function returns a pointer to the string associated with the specified **category** for the new locale. If the selection cannot be honored, the **setlocale** function returns a null pointer and the program's locale is not changed.

7 A null pointer for **locale** causes the **setlocale** function to return a pointer to the string associated with the **category** for the program's current locale; the program's locale is not changed^{225}

8 The pointer returned by the **setlocale** function is such that a subsequent call with that value and its associated category will restore that part of the program's locale. The string should not be modified by the program, but may be overwritten by a subsequent call to the **setlocale** function.

**References**: formatted input/output functions (7.21.6), multibyte/wide character conversion functions (7.22.7), multibyte string conversion functions (7.22.8), numeric conversion functions (7.22.1), the **strcoll** function (7.24.4.3), the **strptime** function (7.27.3.5), the **strxfrm** function (7.24.4.5).

## 7.11.2 Numeric formatting convention inquiry

### 7.11.2.1 The localeconv function

# Synopsis

```c
#include <locale.h>
struct lconv *localeconv(void);
```

# Description

2 The **localeconv** function sets the components of an object with type **struct lconv** with values appropriate for the formatting of numeric quantities (monetary and otherwise) according to the rules of the current locale.

> 225) The implementation shall arrange to encode a string in the various categories due to a heterogeneous locale when **category** has the value **LC_ALL**.

§7.11.2.1 Library 225

ISO/IEC 9899:2011 (E)

# © ISO/IEC 2011 – All rights reserved

3 The members of the structure with type char * are pointers to strings, any of which (except decimal_point) can point to "", to indicate that the value is not available in the current locale or is of zero length. Apart from grouping and mon_grouping, the strings shall start and end in the initial shift state. The members with type char are nonnegative numbers, any of which can be CHAR_MAX to indicate that the value is not available in the current locale. The members include the following:

```c
char *decimal_point
```

The decimal-point character used to format nonmonetary quantities.

```c
char *thousands_sep
```

The character used to separate groups of digits before the decimal-point character in formatted nonmonetary quantities.

```c
char *grouping
```

A string whose elements indicate the size of each group of digits in formatted monetary quantities.

```c
char *mon_decimal_point
```

The decimal-point used to format monetary quantities.

```c
char *mon_thousands_sep
```

The separator for groups of digits before the decimal-point in formatted monetary quantities.

```c
char *mon_grouping
```

A string whose elements indicate the size of each group of digits in formatted monetary quantities.

```c
char *positive_sign
```

The string used to indicate a nonnegative-valued formatted monetary quantity.

```c
char *negative_sign
```

The string used to indicate a negative-valued formatted monetary quantity.

```c
char *currency_symbol
```

The local currency symbol applicable to the current locale.

```c
char *frac_digits
```

The number of fractional digits (after the decimal-point) to be displayed in a locally formatted monetary quantity.

```c
char *p_s_precedes
```

Set to 1 or 0 if the currency_symbol respectively precedes or precedes the value.

char *cs_precedes

Set to 1 or 0 if the currency_symbol respectively precedes or succeeds the value.

char *sep_by_space

Set to a value indicating the separation of the currency_symbol, the sign string, and the value.

char *n_by_space

Set to a value indicating the separation of the currency_symbol, the sign string, and the value.

char *p_sign_posn

Set to a value indicating the positioning of the positive_sign.

char *n_sign_posn

Set to a value indicating the positioning of the negative_sign.

char *int_curr_symbol

The international currency symbol applicable to the current locale.

int_frac_digits

The number of fractional digits (after the decimal-point) to be displayed in an internationally formatted monetary quantity.

int_p_precedes

Set to 1 or 0 if the int_curr_symbol respectively precedes or succeeds the value.

int_n_precedes

Set to 1 or 0 if the int_curr_symbol respectively precedes or succeeds the value.

int_p_by_space

Set to a value indicating the separation of the int_curr_symbol, the sign string, and the value.

int_n_by_space

Set to a value indicating the separation of the int_curr_symbol, the sign string, and the value.

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved
