

| 原型 | 描述 |
|---|---|
| `char *getenv(const char *name);` | 返回一个指针，指向表示由 name 指向的环境变量值的字符串；如果无法匹配指定名称，则返回 NULL。 |
| `_Noreturn void quick_exit(int status);` | 导致正常程序终止发生。不会调用由 atexit() 注册的函数以及由 signal() 注册的信号处理函数。由 at_quick_exit() 注册的函数将按注册顺序的逆序被调用。如果程序多次调用 quick_exit()，或者同时调用 quick_exit() 和 exit()，则行为未定义。通过调用 _Exit(status) 将控制权返回给宿主环境。(C11) |
| `int system(const char *str);` | 将 str 指向的字符串传递给宿主环境，由命令处理器（如 DOS 或 UNIX）执行。如果 str 是 NULL 指针，则当存在可用的命令处理器时函数返回非零值，否则返回零；如果 str 不为 NULL，则返回值由实现定义。 |
| `void *bsearch(const void *key, const void *base, size_t nmem, size_t size, int (*comp)(const void *, const void *));` | 在 base 指向的、具有 nmem 个大小为 size 的元素的数组中，搜索与 key 指向的对象匹配的元素；元素由 comp 指向的函数进行比较；如果 key 对象小于某个数组元素，比较函数返回小于零的值；如果两者等价，返回零；如果 key 对象大于该数组元素，返回大于零的值。该函数返回指向匹配元素的指针，如果没有元素匹配则返回 NULL；如果两个或更多元素与 key 匹配，将选择其中哪一个匹配元素是未指定的。 |
| `void qsort(void *base, size_t nmem, size_t size, int (*comp)(const void *, const void *));` | 按照 comp 指向的函数所提供的顺序，对 base 指向的数组进行排序；该数组有 nmem 个元素，每个元素的大小为 size 字节；如果第一个实参指向的对象小于第二个实参指向的对象，比较函数返回小于零的值；如果对象等价，返回零；如果第一个对象大于第二个对象，返回大于零的值。 |
| `int abs(int n);` | 返回 n 的绝对值；如果 n 是一个没有对应正值的负数（在二进制补码表示中，当 n 为 INT_MIN 时可能发生），则返回值可能是未定义的。 |
| `div_t div(int numer, int denom);` | 计算 numer 除以 denom 的商和余数，将商放入 div_t 结构的 quot 成员，余数放入 rem 成员；对于不精确的除法，商是大小最接近代数商且幅值较小的整数（即向零截断）。 |
| `long labs(long n);` | 返回 n 的绝对值；如果 n 是一个没有对应正值的负数（在二进制补码表示中，当 n 为 LONG_MIN 时可能发生），则返回值可能是未定义的。 |
| `ldiv_t ldiv(long numer, long denom);` | 计算 numer 除以 denom 的商和余数，将商放入 ldiv_t 结构的 quot 成员，余数放入 rem 成员；对于不精确的除法，商是大小最接近代数商且幅值较小的整数（即向零截断）。 |
| `long long llabs(long long n);` | 返回 n 的绝对值；如果 n 是一个没有对应正值的负数（在二进制补码表示中，当 n 为 LONG_LONG_MIN 时可能发生），则返回值可能是未定义的（C99）。 |
| `lldiv_t lldiv(long long numer, long long denom);` | 计算 numer 除以 denom 的商和余数，将商放入 lldiv_t 结构的 quot 成员，余数放入 rem 成员；对于不精确的除法，商是大小最接近代数商且幅值较小的整数——即向零截断（C99）。 |
| `int mblen(const char *s, size_t n);` | 返回构成 s 所指向的多字节字符的字节数（最多 n 个）；如果 s 指向空字符，则返回 0；如果 s 不指向有效的多字节字符，则返回 -1；如果 s 为 NULL，则当多字节字符具有依赖状态的编码时返回非零值，否则返回零。 |
| `int mbtowc(wchar_t *pw, const char *s, size_t n);` | 如果 s 不为 NULL，则确定构成 s 所指向的多字节字符的字节数（最多 n 个），并确定该字符的 wchar_t 代码；如果 pw 不为 NULL，则将该代码赋给 pw 所指向的位置；返回与 mblen(s, n) 相同的值。 |
| `int wctomb(char *s, wchar_t wc);` | 将 wc 中的字符代码转换为对应的多字节字符表示，并存储到 s 指向的数组中（除非 s 为 NULL）；如果 s 不为 NULL，当 wc 不是有效的多字节字符时返回 -1。如果 wc 有效，则返回构成该多字节字符的字节数。如果 s 为 NULL，则当多字节字符具有依赖状态的编码时返回非零值，否则返回零。 |
| `size_t mbstowcs(wchar_t * restrict pwcs, const char * restrict s, size_t n);` | 将 s 指向的多字节字符数组转换为宽字符代码数组，存储在以 pwcs 开头的位置；转换进行到 pwcs 数组中的 n 个元素或 s 数组中的空字节（以先到者为准）。如果遇到无效的多字节字符，则返回 (size_t) (-1)；否则，返回填充的数组元素个数（不包括空字符，如果有的话）。 |
| `size_t wcstombs(char * restrict s, const wchar_t * restrict pwcs, size_t n);` | 将存储在 pwcs 指向的数组中的宽字符代码序列转换为多字节字符序列，并复制到 s 指向的位置，在存储了 n 个字节或一个空字符后停止，以先到者为准。如果遇到无效的宽字符代码，则返回 (size_t) (-1)；否则，返回填充的数组字节数（不包括空字符，如果有的话）。 |

## _Noreturn：stdnoreturn.h

这里定义了宏 noreturn，它展开为 _Noreturn。

## 字符串处理：string.h

string.h 库定义了 size_t 类型和用于空指针的 NULL 宏。它提供了几个用于分析和处理字符串的函数，以及一些更一般地处理内存的函数。表 RS.V.37 列出了这些函数。

### 表 RS.V.37 字符串函数

| 原型 | 描述 |
|---|---|
| `void *memchr(const void *s, int c, size_t n);` | 在 s 指向的对象的前 n 个字符中查找 c（转换为 unsigned char）的第一次出现；返回指向第一次出现位置的指针，如果未找到则返回 NULL。 |
| `int memcmp(const void *s1, const void *s2, size_t n);` | 比较 s1 指向的对象的前 n 个字符与 s2 指向的对象的前 n 个字符，将每个值解释为 unsigned char。如果所有 n 对都匹配，则两个对象相同；否则，按第一对不匹配的值进行比较。如果两个对象相同，返回零；如果第一个对象在数值上小于第二个对象，返回小于零的值；如果第一个对象大于第二个对象，返回大于零的值。 |
| `void *memcpy(void * restrict s1, const void * restrict s2, size_t n);` | 将 n 个字节从 s2 指向的位置复制到 s1 指向的位置；如果两个位置重叠，则行为未定义；返回 s1 的值。 |
| `void *memmove(void *s1, const void *s2, size_t n);` | 将 n 个字节从 s2 指向的位置复制到 s1 指向的位置；其行为如同先复制到临时位置，因此可以复制到重叠的位置；返回 s1 的值。 |
| `void *memset(void *s, int v, size_t n);` | 将值 v（转换为 unsigned char 类型）复制到 s 指向的前 n 个字节；返回 s。 |

