
```c
#include <wchar.h>

int fprintf(const wchar_t * restrict format, ...);
```

### 描述

`fprintf` 函数等同于 `fwprintf`，不同之处在于参数 `s` 指定了一个用于获取输入的宽字符串，而不是从流中获取。

### 返回值

`fprintf` 函数返回传输的宽字符数量，如果发生输出或编码错误，则返回一个负值。

## 7.29.2.12 `scscanf` 函数

### 语法概要

```c
#include <wchar.h>

int scscanf(const char *s, const char *format, ...);
```

### 描述

`scscanf` 函数等同于 `fscanf`，不同之处在于参数 `s` 指定了一个用于获取输入的字符串，而不是从流中获取。

### 返回值

如果在第一次转换（任何）完成之前发生输入失败，`scscanf` 函数返回宏 `EOF` 的值。否则，`scscanf` 函数返回分配的输入项目数量；在发生早期匹配失败的情况下，该数量可能少于提供的数量，甚至为 0。

## 7.2.3 宽字符输入/输出

### 7.29.3.1 `fgetwc` 函数

### 语法概要

```c
#include <stdio.h>
#include <wchar.h>

wint_t fgetwc(FILE *stream);
```

## 描述

如果指向 `stream` 的输入文件结束标志未设置且存在下一个宽字符，`fgetwc` 函数获取该宽字符，将其转换为 `wint_t` 类型的 `wchar_t`，并移动流的文件位置指示器（如果定义）。

### 返回值

如果流的文件结束标志已设置，或者该流已到达文件结束，则设置流的文件结束标志并 `fgetwc` 返回 `WEOF`。否则，`fgetwc` 函数从输入流中返回下一个字符。如果发生读取错误，则设置流的错误指示器并 `fgetwc` 返回 `WEOF`。如果发生编码错误（包括字节数不足），宏 `EILSEQ` 的值将存储在 `errno` 中，且 `fgetwc` 返回 `WEOF`。341

### 7.29.3.2 `fgetws` 函数

### 语法概要

```c
#include <stdio.h>
#include <wchar.h>

wchar_t *fgetws(wchar_t * restrict s, int n, FILE *restrict stream);
```

### 描述

`fgetws` 函数从指向 `stream` 的流中读取至多比 `n` 少一个的宽字符，并存入指向 `s` 的数组中。在遇到换行宽字符（会被保留）或文件结束后，不再读取额外的宽字符。在数组中读取的最后一个宽字符之后立即写入一个空宽字符。

### 返回值

`fgetws` 函数在成功时返回 `s`。如果遇到文件结束且没有字符读取到数组中，则数组的内容保持不变并返回空指针。如果在操作过程中发生读取或编码错误，数组的内容是不确定的并返回空指针。

### 7.29.3.3 `fputwc` 函数

### 语法概要

```c
#include <stdio.h>
#include <wchar.h>

wint_t fputwc(wchar_t c, FILE *stream);
```

### 描述

`fputwc` 函数将 `c` 指定的宽字符写入指向 `stream` 的输出流中，位于该流关联的文件位置指示器所示的位置（如果定义），并相应地移动指示器。

支持定位请求，或者如果流是用追加模式打开的，则该字符被追加到输出流中。

# 返回

`fputwc` 函数返回写入的宽字符。如果发生写入错误，则设置流的错误指示并 `fputwc` 返回 `EOF`。如果发生编码错误，则宏 `EISEQ` 的值被存储在 `errno` 中，且 `fputwc` 返回 `EOF`。

## 7.29.3.4 `fputws` 函数

### 语法概要

```
#include <stdio.h>
#include <wchar.h>

int fputws(const wchar_t * restrict s, FILE * restrict stream);
```

## 描述

`fputws` 函数将 `s` 指向的宽字符串写入 `stream` 指向的流中。不写入终止的空字符。

### 返回

如果发生写入或编码错误，`fputws` 函数返回 `EOF`；否则，返回一个非负值。

## 7.29.3.5 宽函数 `wide function`

### 语法概要

```
#include <stdio.h>
#include <wchar.h>

int fwide(FILE *stream, int mode);
```

## 描述

宽函数确定 `stream` 指向的流的方向。如果 `mode` 大于零，该函数首先尝试将流设置为宽方向（wide oriented）。如果 `mode` 小于零，函数首先尝试将流设置为字节方向（byte oriented）。否则，`mode` 为零，且函数不改变流的方向。

### 返回

如果调用后流具有宽方向，宽函数返回一个大于零的值；如果流具有字节方向，返回一个小于零的值；如果流没有方向，则返回零。

> 342) 如果流的方向已经确定，`fwide` 不会改变它。

## 7.29.3.6 `getwc` 函数

### 语法概要

```
#include <stdio.h>
#include <wchar.h>

wint_t getwc(FILE *stream);
```

## 描述

`getwc` 函数等同于 `fgetwc`，但如果它实现为宏，则可能会多次评估 `stream`，因此参数不应是具有副作用的表达式。

### 返回

`getwc` 函数返回 `stream` 指向的输入流中的下一个宽字符，或者返回 `WEOF`。

## 7.29.3.7 `getwchar` 函数

### 语法概要

```
#include <wchar.h>

wint_t getwchar(void);
```

## 描述

`getwchar` 函数等同于参数为 `stdin` 的 `getwc`。

### 返回

`getwchar` 函数返回 `stdin` 输入流中的下一个宽字符，或者返回 `WEOF`。

## 7.29.3.8 `putwc` 函数

### 语法概要

```
#include <stdio.h>
#include <wchar.h>

wint_t putwc(wchar_t c, FILE *stream);
```

## 描述

`putwc` 函数等同于 `fputwc`，但如果它实现为宏，则可能会多次评估 `stream`，因此参数不应该是具有副作用的表达式。

### 返回

`putwc` 函数返回写入的宽字符，或者返回 `EOF`。

## 7.29.3.9 `putwchar` 函数

### 语法概要

```
#include <wchar.h>

wint_t putwchar(wchar_t c);
```

## 描述

`putwchar` 函数等同于参数为 `stdout` 的 `putwc`。

### 返回

`putwchar` 函数返回写入的字符，或者返回 `WOEF`。

## 7.29.3.10 `ungetwc`

### 语法概要

```
#include <stdio.h>
#include <wchar.h>

wint_t ungetwc(w_t c, FILE *stream);
```

## 描述

`ungetwc` 函数将 `c` 指定的宽字符推回 `stream` 指向的输入流。被推回的字符将通过该流的后续读取按推回的相反顺序返回。成功调用对 `stream` 指向的文件的定位函数（`fseek`, `fsetpos`, 或 `rewind`）会丢弃任何推回的宽字符。相应的外部流不变。

如果在同一流上没有没有读取或文件定位操作的情况下多次调用 `ungetwc`，操作可能会失败。

如果 `c` 的值等于宏 `WOEF`，操作失败且输入流保持不变。

成功调用 `ungetwc` 会清除流的文件结束指示。在读取或丢弃任何推回的宽字符后，流的位置指示值与推回之前相同。

### 返回

`ungetwc` 函数返回推回的宽字符，如果操作失败则返回 `WEOF`。

## 7.29.4 通用宽字符串工具

头文件 `<wchar.h>` 声明了一些用于宽字符串处理的函数。使用了各种方法来确定数组的长度，但在所有情况下，`wchar_t *` 参数都指向数组的初始（地址最低的）元素。如果在对象边界之外访问数组，行为是未定义的。

声明为 `size_t n` 的参数确定函数的数组长度，在调用该函数时，`n` 可以为零。除非在该子句中特定函数的描述中明确说明，否则此类调用中的指针参数仍应具有 7.1.4 中描述的有效值。在此调用中，定位宽字符的函数会找到位置，比较两个宽字符的函数返回零，拷贝宽字符的函数拷贝零字符。

### 7.29.4.1 宽数值转换函数

#### 7.29.4.1.1 `wstod`, `wcstof`, 和 `wcstold` 函数

### 语法概要

```
#include <wchar.h>

double wstod(const wchar_t * restrict nptr, wchar_t ** restrict endptr);
float wcstof(const wchar_t * restrict nptr, wchar_t ** restrict endptr);
long wcstold(const wchar_t * restrict nptr, wchar_t ** restrict endptr);
```

## 描述

`wstod`, `wcstof`, 和 `wcstold` 函数分别将 `nptr` 指向的宽字符串的初始部分转换为 `double`、`float` 和 `long`。首先，将输入字符串分解为三部分：初始为空的空白字符序列（由 `isspace` 指定）、一个表示无限或 NaN 的序列，以及最后的未识别宽字符序列（包括终止的空字符）。

主体序列的预期格式是一个可选的加号或减号，然后是以下之一：

- 一个非空数字数字序列，可选包含一个小数点宽字符，然后跟一个按照 6.4.2 定义的可选指数部分；
- 0x 或 OX，然后是一个非空十六进制数字序列，可选包含一个小数点宽字符，然后跟一个按照 6.4.2 定义的可选指数部分；
- INF 或 INFINITY，或者除大小写外的任何其他等效字符串
- NAN 或 NAN (n-wchar-sequence_opt)，或者 NAN 部分中除大小写外的任何其他等效字符串，其中：

```
n-wchar-sequence:
digit
nondigit
n-wchar-sequence digit
n-wchar-sequence nondigit
```

主体序列定义为输入字符串中从第一个非空白字符开始符合预期格式的最长子序列。如果输入字符串不符合预期格式，则主体序列不包含宽字符。

如果主体序列符合浮数的预期格式，则从第一个数字或小数点宽字符（任一先出现）开始的宽字符序列按照 6.4.2 的规则解释为浮点常数，用小数点宽字符代替点，且如果在小数点数字中没有出现指数部分或小数点宽字符，则假设在最后一个数字后跟有一个相应类型值为零的指数部分。如果序列以减号开头，则该序列解释为负数³³ 宽字符序列 INF 或 INFINITY 被解释为无限（如果返回类型中可以表示），类似于超出返回类型范围的浮点常数。宽字符序列 NAN 或 NAN (n-wchar-sequence_opt) 被解释为 NaN（如果返回类型中支持），否则类似于不符合预期格式的主体序列部分；³⁴ n-wchar-sequence 的含义由实现定义。实现可以使用 n-wchar-sequence 来确定表示在 NaN 符号位中的额外信息。

最终的宽字符串存储在 `endptr` 指向的对象中，前提是 `endptr` 不是空指针。

如果主体序列为十六进制形式且 `FLT_RADIX` 是 2 的幂，则转换产生的值将经过正确的舍入。

在 "C" 区域设置之外，可能接受额外的、特定区域设置的主体序列形式。

如果主体序列为空或不符合预期格式，则不执行转换；`nptr` 的值存储在 `endptr` 指向的对象中，前提是 `endptr` 不是空指针。

## 推荐实践

如果主体序列为十六进制形式、`FLT_RADIX` 不是 2 的幂且结果无法精确表示，则结果应为适当内部格式中与十六进制浮点源值相邻的两个数字之一，额外要求是误差对于当前的舍入方向应具有正确的符号位。

如果主体序列为十进制格式，且有效位数最多为 `DECIMAL_DIG`（在 `<float.h>` 中定义），则结果应经过正确的舍入。如果主体序列 `D` 为十进制格式且有效位数超过 `DECIMAL_DIG`，请考虑两个边界相邻的十进制字符串 `L` 和 `U`，它们都具有 `DECIMAL_DIG` 个有效数字，且值 `L`、`D` 和 `U` 满足 `L ≤ D ≤ U`。结果应该是根据当前舍入方向正确舍入 `L` 和 `U` 后得到的（相等或相邻）的值之一，额外要求 `D` 的误差对于当前的舍入方向应具有正确的符号位。³⁴⁵)

## 返回

函数返回转换后的值（如果有）。如果无法转换，则返回零。如果正确的值溢出且生效了默认舍入（7.12.1），或者返回了 `HUGE_VAL`、`HUGE_VALF` 或 `HUGE_ALL`（根据返回类型和值的符号），并将宏 `ERANGE` 的值存储在 `errno` 中。如果结果下溢（7.12.1），函数返回一个值大于返回类型中最小归一化正数的数值；`errno` 是否获得值 `ERANGE` 取于实现。

³⁴⁵ `DECIMAL_DIG` 定义在 `<float.h>` 中，应足够大，使得 `L` 和 `U` 通常会舍入到相同的内部浮点值，或者舍入到相邻的值。

## 7.29.4.1.2 `wcstol`, `wcstoll`, `wcstoul` 和 `wcstull` 函数

### 概要

```
#include <wchar.h>

long int wcstol(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
long int wcstoll(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
unsigned long int wcstoul(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
unsigned long int wcstull(const wchar_t * restrict nptr, wchar_t ** restrict endptr, int base);
```
