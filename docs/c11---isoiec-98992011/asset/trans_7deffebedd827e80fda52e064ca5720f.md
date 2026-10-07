

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

errno_t mbstows_s(size_t * restrict retval,
char * restrict dst, size_t dmax,
const char ** restrict src, size_t len,
mbstate_t * restrict ps);
errno_t wcsort_s(size_t * restrict retval,
char * restrict dst, size_t dmax,
const wchar_t ** restrict src, size_t len,
mbstate_t * restrict ps);

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
int ispunct(wint_t wc);
int isspace(wint_t wc);
int isupper(wint_t wc);
int isxdigit(wint_t wc);
int isctype(wint_t wc, wctype_t desc);
wint_t towlower(wint_t wc);
wint_t towupper(wint_t wc);
wint_t towrans(wint_t wc, wctype_t desc);
wint_t towct(wint_t wc, wctype_t desc);
wint_t towct(wint_t wc);

502

§B.29

ISO/IEC 9899:2011 (E)

# Annex C (说明性)

# 序列点

- 标识符与函数调用之间的
- `,` 之前的操作数
- 运算符的第一个操作数与第二个操作数之间的
- `&&`、`||`、`:` 之前的操作数
- `,` 之前的操作数
- `}` 之前的标识符
- `}` 结束的
- 以下内容是序列点：
    - 一个初始化语句
    - `if` 语句的控制表达式
    - `switch` 语句的控制表达式
    - `while` 或 `do` 语句的控制表达式
    - `for` 语句的可选部分
    - `return` 语句
- 之前的
    - 格式化输入之前的
    - 格式化输出之前的
    - 传递给函数的参数
    - 7.22.5.

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 版权所有

# D (规范性)

# 通用字符名称

- 1 本节列出了用于标识符的十六进制值

# D.1 允许的字符范围

- 1 00A8, 00AA, 00AD, 00AF, 00B2–00D2, 00B5–00B7, 00BC–00BE, 00C0–00D6, 00D8–00FF
- 2 0100–167F, 1681–180D, 180F–1FFF
- 3 200B–200D, 202A–202E, 203F–2040, 2054, 2060–206F
- 4 2070–218F, 2460–24FF, 2776–2793, 2C00–2DFF, 2E80–2FFF
- 5 3004–3007, 3021–302F, 3031–303F
- 6 3040–D7FF
- 7 F900–FD3D, FD40–FDCF, FD00–FE44, FE47–FFFD
- 8 10000–1FFD, 20000–2FFD, 30000–3FFD, 40000–4FFD, 50000–5FFD, 60000–6FFD, 70000–7FFD, 80000–8FFD, 90000–9FFD, A0000–AFFD, B0000–BFFF, C0000–CFFD, D0000–DFFD, E0000–EFFF

# D.2 初始不允许的字符范围

- 1 0300–036F, 1DC0–1DFF, 2D00–20FF, FE20–FE2F

