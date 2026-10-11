
`double difftime(time_t time1, time_t time0);`

`time_t mktime(struct tm *timeptr);`

`time_t time(time_t timer);`

`int timespec_get(const struct timespec *ts, int base);`

`char *asctime(const struct tm *timeptr);`

`char *ctime(time_t timer);`

`struct tm *gmtime(time_t timer);`

`struct tm *localtime(time_t timer);`

`size_t maxsize(const restrict s,`

`const char *restrict format,`

`const struct tm *restrict timeptr);`

```
__ __STDC_WANT_LIB_EXT1__
```

```c
errno_t;
rsize_t;
errno_t asctime_s(char *s, rsize_t maxsize,
const struct tm *timeptr);
errno_t ctime_s(char *s, rsize_t maxsize,
const time_t *timer);
struct tm *gmtime_s(const time_t *restrict timer,
struct tm *restrict result);
struct tm *localtime_s(const time_t *restrict timer,
struct tm *restrict result);
```

### B.27 Unicode 工具 <uchar.h>

```c
mbstate_t;size_t;char16_t;char32_t;
size_t _mrtomb(char16_t *restrict pcl6,
const char *restrict s, size_t n,
mbstate_t *restrict ps);
size_t c16rtomb(char * restrict s, char16_t c16,
mbstate_t *restrict ps);
size_t mbrftoc32(char32_t *restrict pc32,
const char *restrict s, size_t n,
mbstate_t *restrict ps);
size_t c32rrtomb(char * restrict s, char32_t c32,
mbstate_t *restrict ps);
```

### B.28 扩展多字节/宽字符工具 <wchar.h>

```c
wchar_t;wint_t;WCHAR_MAX;
size_t;mbstate_t;NULL;WEOF;
int fwprintf(FILE *restrict stream,
const wchar_t *restrict format, ...);
int fwcanf(FILE *restrict stream,
const wchar_t *restrict format, ...);
int fwprintf(wchar_t *restrict s, size_t n,
const wchar_t *restrict format, ...);
int swcsprintf(const wchar_t *restrict s,
const wchar_t *restrict format, ...);
```

B.28 库摘要 497

```c
int vfwprintf(FILE *restrict stream,
const wchar_t *restrict format, va_list);
int vswprintf(wchar_t *restrict s, size_t n,
const wchar_t *restrict format, va_list);
int vfwscanf(const wchar_t *restrict s,
const wchar_t *restrict format, va_list);
int vswprintf(const wchar_t *restrict format,
va_list);
int_t wgetwc(FILE *stream);
wchar_t * wfgetws(wchar_t *restrict s, int n,
FILE *restrict stream);
wint_t wfputwc(wchar_t c, FILE *stream);
int fputwcs(const wchar_t *restrict s,
FILE *restrict stream);
int fwide(FILE *stream, int mode);
wint_t wgetwc(FILE *stream);
wint_t wgetchvar(void);
wint_t wputc(wchar_t c, FILE *stream);
wint_t wputwchar(wchar_t c);
wint_t wungetwc(wint_t c, FILE *stream);
double wscstol(const wchar_t *restrict nptr,
wchar_t **restrict endptr);
float wscstof(const wchar_t *restrict nptr,
wchar_t **restrict endptr);
long double wscstold(const wchar_t *restrict nptr,
wchar_t **restrict endptr);
long int wcstol(const wchar_t *restrict nptr, int base);
wchar_t **restrict endptr, int base);
long int wcstoll(const wchar_t *restrict nptr,
wchar_t **restrict endptr, int base);
unsigned int wcstoul(const wchar_t *restrict nptr,
wchar_t **restrict endptr, int base);
unsigned long int wcstull(
const wchar_t *restrict nptr,
wchar_t **restrict endptr, int base);
```

© ISO/IEC 2011 – 版权所有

ISO/IEC 9899:2011 (E)

```c
wchar_t *wcscpy(wchar_t * restrict s1,
             const wchar_t * restrict s2);
wchar_t *wcscnpy(wchar_t * restrict s1,
              const wchar_t * restrict s2, size_t n);
wchar_t *wcmemcpy(wchar_t * restrict s1,
                  const wchar_t * restrict s2, size_t n);
wchar_t *wmemmove(wchar_t *s1, const wchar_t *s2,
                   size_t n);
wchar_t *wcscat(wchar_t * restrict s1,
                const wchar_t * restrict s2);
wchar_t *wcscat(wchar_t * restrict s1,
              const wchar_t * restrict s2, size_t n);
int wcscmp(const wchar_t *s1, const wchar_t *s2);
int wcscoll(const wchar_t *s1, const wchar_t *s2);
int wcscnmp(const wchar_t *s1, const wchar_t *s2,
             size_t n);
size_t wcsfrm(const wchar_t * restrict s1,
               const wchar_t * restrict s2, size_t n);
int wmemcmp(const wchar_t *s1, const wchar_t *s2,
             size_t n);
wchar_t *wcschr(const wchar_t *s, const wchar_t *c);
size_t wcscspn(const wchar_t *s1, const wchar_t *s2);
wchar_t *wcspbrk(const wchar_t *s1, const wchar_t *s2);
wchar_t *wcschr(const wchar_t *s, const wchar_t *c);
size_t wcsspn(const wchar_t *s1, const wchar_t *s2);
wchar_t *wcststr(const wchar_t *s1, const wchar_t *s2);
wchar_t *wcstok(wchar_t * restrict s1,
                const wchar_t * restrict s2,
                wchar_t ** restrict ptr);
wchar_t *wmemchr(const wchar_t *s, const wchar_t *c, size_t n);
size_t wcslen(const wchar_t *s);
wchar_t *wmemset(const wchar_t *s, const wchar_t *c, size_t n);
size_t wcsftime(const wchar_t * restrict s, size_t maxsize,
                 const wchar_t * restrict format,
                 struct tm * restrict timeptr);
wint_t btowc(int c);
int mbstint(const mbstate_t *ps);
size_t mbrlen(const char * restrict s, size_t n,
mbstate_t * restrict ps);
```

# ISO/IEC 9899:2011 (E)

```c
size_t mbrtowc(wchar_t * restrict pwc,
const char * restrict s, size_t n,
mbstate_t * restrict ps);
size_t wccharomb(wchar_t * restrict s, wchar_t wc,
mbstate_t * restrict ps);
size_t mbrstrtowcs(wchar_t * restrict dst,
const char ** restrict src, size_t len,
mbstate_t * restrict ps);
size_t wcschans(wchar_t * restrict dst,
const wchar_t ** restrict src, size_t len,
mbstate_t * restrict ps);
```

```c
__STDC_WANT_LIB_EXT1__
error_t
int swprintf(FILE * restrict stream,
const wchar_t * restrict format, ...);
int swscanf(FILE * restrict stream,
const wchar_t * restrict format, ...);
int swnprintf_s(wchar_t * restrict s,
size_t n,
const wchar_t * restrict format, ...);
int swprintf_s(wchar_t * restrict s, size_t n,
const wchar_t * restrict format, ...);
int swcanf_s(const wchar_t * restrict s,
const wchar_t * restrict format, ...);
int vprintf_s(FILE * restrict stream,
const wchar_t * restrict format,
va_list arg);
int vscanf_s(FILE * restrict stream,
const wchar_t * restrict format, va_list arg);
int vsnprintf_s(wchar_t * restrict s,
size_t n,
const wchar_t * restrict format,
va_list arg);
int vsprintf_s(wchar_t * restrict s,
size_t n,
const wchar_t * restrict format,
va_list arg);
```

© ISO/IEC 2011 – 版权所有 ISO/IEC 9899:2011 (E)

```c
int vswcanf_s(const wchar_t * restrict s,
const wchar_t * restrict format,
va_list arg);
int vpwprintf_s(const wchar_t * restrict format,
va_list arg);
int vswcanf_s(const wchar_t * restrict format,
va_list arg);
int wprintf_s(const wchar_t * restrict format, ...);
int wcscanf_s(const wchar_t * restrict format, ...);
errno_t wccscpy(wchar_t * restrict s1,
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
size_t slmax,
const wchar_t * restrict s2,
wchar_t ** restrict ptr);
size_t wcsnlen_s(const wchar_t *s, size_t maxsize);
errno_t wcscrt_s(size_t * restrict retval,
char * restrict s, size_t smax,
wchar_t wc, mbstate_t * restrict ps);
```

# §B.28 库摘要

501

国际标准化组织版权
由 IHS 授权提供
授权许可下不允许复制或网络传输

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 版权所有

`errno_t mbstows_s(size_t * restrict retval,`
`char * restrict dst, size_t dmax,`
`const char ** restrict src, size_t len,`
`mbstate_t * restrict ps);`
`errno_t wcsort_s(size_t * restrict retval,`
`char * restrict dst, size_t dmax,`
`const wchar_t ** restrict src, size_t len,`
`mbstate_t * restrict ps);`

# B.29 宽字符分类与映射 <wctype>

```c
wint_t wctype_t EOF
int iswalnum(wint_t wc);
int isalnum(wint_t wc);
int iswblank(wint_t wc);
int iswctrl(wint_t wc);
int isdigit(wint_t wc);
int isgraph(wint_t wc);
int islower(wint_t wc);
int isprint(wint_t wc);
```
