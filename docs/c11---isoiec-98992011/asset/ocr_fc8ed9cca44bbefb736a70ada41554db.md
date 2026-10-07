ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

```
errno_t mbscortows_s(size_t * restrict retval,
char_t * restrict dst, rsize_t dmaxsize,
const char ** restrict src, rsize_t len,
mbstate_t * restrict ps);
erno_t wcsortumbs_s(size_t * restrict retval,
char * restrict dst, rsize_t dmaxsize,
const wchar_t ** restrict src, rsize_t len,
mbstate_t * restrict ps);
```

# B.29 Wide character classification and mapping utilities <wctype.h>

```
wint_t wctrans_t wctype_t WEOF

int iswalnum(wint_t wc);
int isalnum(wint_t wc);
int iswblank(wint_t wc);
int iswctrl(wint_t wc);
int isdigit(wint_t wc);
int isgraph(wint_t wc);
int islower(wint_t wc);
int isprint(wint_t wc);
int ispunct(wint_t wc);
int isspace(wint_t wc);
int isupper(wint_t wc);
int isxdigit(wint_t wc);
int isctype(wint_t wc, wctype_t desc);
wctype_t wctype(const char *property);
wint_t towlower(wint_t wc);
wint_t towupper(wint_t wc);
wint_t towctrans(wint_t wc, wctrans_t desc);
wctrans_t wctrans(wctrans(const char *property));
```

502

Library summary

§B.29

Copyright International Organization for Standardization
Provided by IHS under license with ISO
No reproduction or networking permitted without license from IHS

Not for Resale