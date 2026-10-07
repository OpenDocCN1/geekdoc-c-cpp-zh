© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

```
int vswcanf_s(const wchar_t * restrict s,
const wchar_t * restrict format,
va_list arg);
int vpwprintf_s(const wchar_t * restrict format,
va_list arg);
int vswcanf_s(const wchar_t * restrict format,
va_list arg);
int wprintf_s(const wchar_t * restrict format, ...);
int wcscanf_s(const wchar_t * restrict format, ...);
errno_t wccsscpy(wchar_t * restrict s1,
size_t slmax,
const wchar_t * restrict s2);
errno_t wccsnpy(wchar_t * restrict s1,
size_t slmax,
const wchar_t * restrict s2,
size_t n);
errno_t wmemcmpy(wchar_t * restrict s1,
size_t slmax,
const wchar_t * restrict s2,
size_t n);
errno_t wmmemove_s(wchar_t *s1, size_t slmax,
const wchar_t *s2, size_t n);
errno_t wcscat_s(wchar_t * restrict s1,
size_t slmax,
const wchar_t * restrict s2);
errno_t wcscanf_s(wchar_t * restrict s1,
size_t slmax,
const wchar_t * restrict s2,
size_t n);
char_t *wcstok_s(wchar_t * restrict s1,
size_t * restrict slmax,
const wchar_t * restrict s2,
wchar_t ** restrict ptr);
size_t wcsnlen_s(const wchar_t *s, size_t maxsize);
errno_t wcrtomb_s(size_t * restrict retval,
char * restrict s, size_t smax,
wchar_t wc, mbstate_t * restrict ps);
```

# §B.28

Library summary

501

Copyright International Organization for Standardization
Provided by IHS under license with ISO
No reproduction or networking permitted under license from IHS

Not for Resale