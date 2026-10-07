

© ISO/IEC 2011 – 保留所有权利

ISO/IEC 9899:2011 (E)

## 6.4.3Universal字符名称 (Universal character names)

### 语法

```
universal-character-name:
\u hex-quad
\u hex-quad hex-quad

hex-quad:
hexadecimal-digit hexadecimal-digit
hexadecimal-digit hexadecimal-digit
```

## 约束

通用字符名称不应指定标识符小于 00A0 的字符，但 0024 ($)、0040 (@) 或 0060 (') 除；也不可以是 D800 到 DFFF 范围内的字符。⁷³}

## 描述

通用字符名称可用于标识符、字符常量和字符串字面量，用于指定不在基本字符集中的字符。

## 语义

通用字符名称 \unnnnnnn 指定其八位短标识符（如 ISO/IEC 10646 指定）为 nnnnnnn 的字符。⁷⁴

同样，通用字符名称 \unnnn 指定其四位短标识符为 nnnn（且八位短标识符为 0000nnnn）的字符。

> ⁷³) 不允许的字符属于基本字符集以及 ISO/IEC 10646 预留给控制字符、DELETE 字符以及 S 区域（供 UTF-16 使用）的位置。

> ⁷⁴) 短标识符首次指定于 ISO/IEC 10646–1:1993/Amd.9:1997。

## 6.4.4

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

## 6.4.4 常量 (Constants)

### 语法

+ constant:
integer-constant
floating-constant
enumeration-constant
character-constant

## 约束

+ 每个常量应有一个类型，且常量的值应在其类型的可表示值范围内。

## 语义

+ 每个常量都有一个类型，由其形式和值决定，详见后文。

### 6.4.4.1 整数常量 (Integer constants)

### 语法

+ integer-constant:
decimal-constant integer-suffix_{opt}
octal-constant integer-suffix_{opt}
hexadecimal-constant integer-suffix_{opt}

+ decimal-constant:
nonzero-digit
decimal-constant digit

+ octal-constant:
0
octal-constant octal-digit

+ hexadecimal-constant:
hexadecimal-prefix hexadecimal-digit
hexadecimal-constant hexadecimal-digit

+ hexadecimal-prefix: one of
0x 0X

+ nonzero-digit: one of
1 2 3 4 5 6 7 8 9

+ octal-digit: one of
0 1 2 3 4 5 6 7

hexadecimal-digit: one of
0 1 2 3 4 5 6 7 8 9
a b c d e f
A B C D E F

integer-suffix:
unsigned-suffix long-suffix-opt
unsigned-suffix long-long-suffix
long-suffix unsigned-suffix-opt
long-suffix unsigned-suffix-opt

unsigned-suffix: one of
u U

long-suffix: one of
1 L

long-suffix: one of
11 LL

© ISO/IEC 2011 – 保留所有权利 ISO/IEC 9899:2011 (E)

## 描述

+ 2 整数常量以数字开头，但没有点号或指数部分。它可能有一个指定其基数的前缀，以及一个指定其类型的后缀。

+ 3 十进制常量以非零数字开头，由一系列十进制数字组成。八进制常量由前缀 0 可选地跟随一个仅由数字 0 到 7 的序列组成。十六进制常量由前缀 0x 或 0X 开头，由一系列十进制数字和字母 a（或 A）、f（或 F）组成，其值分别为 10 到 15。

## 语义

+ 4 十进制常量的值按基 10 计算；八进制常量的按基 8 计算；十六进制常量的按基 16 计算。词法上的第一个数字是最高位数字。

+ 5 整数常量的类型是其值可以表示的对应列表中第一个。

### §6.4.4.1

ISO/IEC 9899:2011 (E)

| 后缀 | 十进制常量 | 八进制或十六进制常量 |
| --- | --- | --- |
| none | int<br>long int<br>long long int | int<br>unsigned int<br>long int<br>unsigned long int<br>long long int<br>unsigned long int |
| u or U | unsigned int<br>long int<br>long long int | unsigned int<br>long int<br>long long int |
| 1 or L | long int<br>long long int | long int<br>unsigned long int<br>long int<br>unsigned long int |
| Both u or U and 1 or L | unsigned long int<br>long long int | unsigned int<br>unsigned long int |
| Both u or U and 1 or L | long int<br>long long int | long long long int |

如果常量不能由列表中的任何类型表示，则该常量为错误。

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

## 6.4.4.2 浮点常量 (Floating constants)

### 语法

+ floating-constant:
decimal-floating-constant
hexadecimal-floating-constant

+ decimal-floating-constant:
decimal-signand exponent-part<opt>
floating-suffix<opt>

+ hexadecimal-floating-constant:
hexadecimal-prefix hexadecimal-signand exponent-part<opt>
hexadecimal-suffix<opt>

+ decimal-signand:
nonzero-digit
decimal-signand digit

+ hexadecimal-signand:
hexadecimal-prefix hexadecimal-digit
hexadecimal-signand hexadecimal-digit

+ hexadecimal-prefix: one of
0x 0X

+ nonzero-digit: one of
1 2 3 4 5 6 7 8 9

+ hexadecimal-digit: one of
0 1 2 3 4 5 6 7 8 9
a b c d e f
A B C D E F

+ exponent-part:
sign digit-sequence<opt>
sign: one of
+ -

digit-sequence: digit
digit-sequence digit

+ floating-suffix:
unsigned-suffix long-suffix-opt
unsigned-suffix long-long-suffix
long-suffix unsigned-suffix-opt
long-suffix unsigned-suffix-opt

+ unsigned-suffix: one of
u U

long-suffix: one of
1 L

long-suffix: one of
11 LL

## 描述

+ 2 浮点常量有一个尾数部分，后面可以跟一个指数部分，并可能包含一个指定其类型的后缀。

+ 3 十进制浮点常量以非零数字开头，由一系列十进制数字、点号以及另一序列十进制数字组成。十六进制浮点常量由前缀 0x 或 0X 开头，由一系列十六进制数字和值分别为 10 到 15 的字母组成。指数部分由 e、E、p 或 P 后跟带符号的数字序列组成。

## 语义

+ 4 十进制浮点常量的值按基 10 计算；十六进制浮点常量按基 16 计算。尾数解释为（十进制或十六进制）有理数；指数表示尾数要缩放的 10 或 2 的幂次。

+ 5 浮点常量的类型是其值可以表示的对应列表中第一个。

+ 6 带后缀的浮点常量类型为 **double**。如果后缀为 f 或 F，则类型为 **float**。如果后缀为 l 或 L，则类型为 **long double**。

+ 7 浮点常量在翻译时被转换为内部格式。浮点常量的转换在执行期间不会引发异常状态或浮点异常。所有源形式的浮点常量⁷⁷⁵) 应转换为相同的内部格式具有相同的值。

## 建议做法

8 如果常量无法在其评估格式中精确表示，实现应产生诊断信息；然后实现应继续程序的翻译。

9 浮点常量的翻译时转换应与库函数（如 `strtod`）对字符串的执行时转换匹配，前提是两种转换的输入相同、结果格式相同且使用默认执行时舍入⁷⁶)

> ⁷⁷⁵) 库函数建议的转换精度比浮点常量要求的更精确。

