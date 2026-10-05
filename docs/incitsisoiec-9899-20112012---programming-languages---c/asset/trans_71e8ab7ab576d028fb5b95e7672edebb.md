

```c
size_t mbrtowchar(wchar_t restrict pwc,
const char * restrict s,
mbstate_t * restrict ps);
size_t wctowchar(char * restrict s, wchar_t wc,
mbstate_t * restrict ps);
size_t mbstows(wchar_t * restrict dst,
const char ** restrict src, size_t len,
mbstate_t * restrict ps);
size_t wcsstombs(char * restrict dst,
const wchar_t ** restrict src, size_t len,
mbstate_t * restrict ps);
```

```c
__STDC_WANT_LIB_EXT1__
errno_t
rsize_t
int fwprintf_f_s(FILE * restrict stream,
const wchar_t * restrict format, ...);
int fwscanf_f_s(FILE * restrict stream,
const wchar_t * restrict format, ...);
int swnprintf_f_s(wchar_t * restrict s, rsize_t n,
const wchar_t * restrict format, ...);
int swprintf_f_s(wchar_t * restrict s, rsize_t n,
const wchar_t * restrict format, ...);
int swcanf_f_s(const wchar_t * restrict s,
const wchar_t * restrict format, ...);
int vprintf_f_s(FILE * restrict stream,
const wchar_t * restrict format,
va_list arg);
int vfscanf_f_s(FILE * restrict stream,
const wchar_t * restrict format, va_list arg);
int vsnprintf_f_s(wchar_t * restrict s,
rsize_t n,
const wchar_t * restrict format,
va_list arg);
int vsprintf_f_s(wchar_t * restrict s,
rsize_t n,
const wchar_t * restrict format,
va_list arg);
```

```c
int vswcanf_s(const wchar_t * restrict s,
   const wchar_t * restrict format,
   va_list arg);
int wprintf_s(const wchar_t * restrict format,
   va_list arg);
int vswcanf_s(const wchar_t * restrict format,
   va_list arg);
int wprintf_s(const wchar_t * restrict format, ...);
int wswcanf_s(const wchar_t * restrict format, ...);
errno_t wcscpy_s(wchar_t restrict s1,
   rsize_t slmax,
   const wchar_t * restrict s2);
errno_t wcscncpy_s(wchar_t * restrict s1,
   rsize_t slmax,
   const wchar_t * restrict s2,
   rsize_t n);
errno_t wmemcpy_s(wchar_t * restrict s2,
   rsize_t n);
errno_t wmemmove_s(wchar_t *s1, rsize_t slmax,
   const wchar_t *s2, rsize_t n);
errno_t wcscat_s(wchar_t * restrict s1,
   rsize_t slmax,
   const wchar_t * restrict s2);
errno_t wcsncat_s(wchar_t * restrict s1,
   rsize_t slmax,
   const wchar_t * restrict s2,
   rsize_t n);
wchar_t *wcstok_s(wchar_t * restrict s1,
   rsize_t * restrict slmax,
   const wchar_t * restrict s2,
   wchar_t ** restrict ptr);
size_t _wcslen_s(const wchar_t *s, size_t maxsize);
errno_t _wcrtomb_s(size_t * restrict retval,
   char * restrict s, rsize_t smax,
   wchar_t wc, mbstate_t * restrict ps);
```

errno_t mbrstowcs_s(size_t * restrict retval,
wchar_t * restrict dst, rsize_t dstmax,
const char ** restrict src, rsize_t len,
mbstate_t * restrict ps);
errno_t wcsrtombs_s(size_t * restrict retval,
char_t * restrict dst, rsize_t dstmax,
const wchar_t ** restrict src, rsize_t len,
mbstate_t * restrict ps);

## B.29 宽字符分类与映射实用 <wctype.h>

```c
wint_t wctrans_t wctype_t WEOF

int iswalnum(wint_t wc);
int isalpha(wint_t wc);
int iswblank(wint_t wc);
int iswcntrl(wint_t wc);
int isdigit(wint_t wc);
int isgraph(wint_t wc);
int islower(wint_t wc);
int isprint(wint_t wc);
int isispunct(wint_t wc);
int isspace(wint_t wc);
int isupper(wint_t wc);
int isxdigit(wint_t wc);
int iswtype(wint_t wc, wctype_t desc);
wctype_t wctype(const char *property);
wint_t towlower(wint_t wc);
wint_t toupper(wint_t wc);
wint_t towctrans(wint_t wc, wctype_t desc);
wint_t wctrans(const char *property);

## 附录 C
序列点

以下是 5.1.2 中描述的序列点：

- 函数声明符与实际参数之间 (6.5.2)。
- 以下运算符第一个和第二个操作数之间：逻辑与 `&&` (6.5.13)，逻辑或 `||` (6.5.14)，逗号 (6.5.17)。
- 条件运算符 `?` 的第一个操作数与第二个、第三个操作数之间 (6.5.15)。
- 完整表达式的结束 (6.7.6)。
- 与下一个完整表达式之间。以下为完整表达式：复合字面量的一部分 (6.7.9)；语句 (6.8.3)；选择语句 (if 或 switch) 的控制表达式 (6.8.4)；for 语句的（可选）表达式 (6.8.5)；返回语句的（可选）表达式 (6.8.6)。
库函数之前 (7.1.4)。
格式化输出操作之后 (7.2.6, 7.2.9)。
每次调用调用之前和之后，以及传递给该函数的对象的移动之间 (7.2.5)。

## 附录 D
通用名称

此节列出了在标识符中有效的十六进制值。

## D.1 允许的字符范围

- 00A8, 00AA, 00AD, 00AF, 00B2–00B5, 00B7–00BA, 00BC–00BE, 00C0–00D6, 00D8–00F6, 00F8–00FF
- 0100–167F, 1681–180D, 180F
- 200B–200D, 202A–202E, 203F–2040, 2054, 2060–206F
- 2070–218F, 2460–24FF, 2776–2793, 2C00–2DFF, 2E80–FFF
- 3004–3007, 3021–302F, 3031–303F
- 3040–D7FF
- F900–FD3D, FD40–FDCF, FDF0–FE44, FE47–FFFD
- 10000–1FFD, 20000–2FFD, 30000–3FFD, 40000–4FFD, 50000–5FFD, 60000–6FFD, 70000–7FFD, 80000–8FFD, 90000–9FFD, A0000–AFFD, B0000–BFFD, C0000–CFFD, D0000–DFFD, E0000–EFFF

## D.2 不允许的字符范围

- 0300–036F, 1DC0–1FFD, 20D0–2FF, FE20–FE2F

## 附录 E
实现限制

`<limits.h>` 头文件的内容所示，按字母顺序排列。所示的最小值应由相同符号的实现定义值替换。这些值应为用于 `#if` 预处理指令的常量表达式。相关组件在 5.2.4.2.1 中进一步描述。

```c
#define CHAR_BIT 8
#define CHAR_MAX UCHAR_MAX or SCHAR_MAX
#define CHAR_MIN 0 or SCHAR_MIN
#define INT_MAX +32767
#define INT_MIN -32767
#define LONG_MAX +2147483647
#define LONG_MIN -2147483647
#define LLONG_MAX +9223372036854775807
#define LLONG_MIN -9223372036854775807
#define MB_LEN_MAX 1
#define SCHAR_MAX +127
#define SCHAR_MIN -128
#define SHRT_MAX 32767
#define SHRT_MIN -32768
#define USCHAR_MAX 255
#define USCHAR_MIN 0
#define UINT_MAX 4294967295
#define ULONG_MAX 4294967295
#define ULLONG_MAX 18446744073709551615
```

`<float.h>` 头文件的内容所示。

```c
#define DECIMAL_DIG 10
#define FLT_DECIMAL_DIG 6
#define FLT_DIG 6
#define FLT_MANT_DIG
#define FLT_MAX_10_EXP +37
#define FLT_MAX_EXP
#define FLT_MIN_10_EXP -37
#define FLT_MIN_EXP
#define FLT_RADIX 2
#define LDLB_DECIMAL_DIG 10
#define LDLB_DIG 10
#define LDLB_MANT_DIG
#define LDLB_MAX_10_EXP +37
#define LDLB_MAX_EXP
#define LDLB_MIN_10_EXP -37
#define LDLB_MIN_EXP
```

