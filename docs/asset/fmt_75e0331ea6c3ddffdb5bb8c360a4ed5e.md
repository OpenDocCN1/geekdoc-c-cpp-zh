
> ⁷³) 不允许的字符属于基本字符集以及 ISO/IEC 10646 预留给控制字符、DELETE 字符以及 S 区域（供 UTF-16 使用）的位置。

> ⁷⁴) 短标识符首次指定于 ISO/IEC 10646–1:1993/Amd.9:1997。

## 6.4.4

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

## 6.4.4 常量 (Constants)

### 语法

+ `constant`:
`integer-constant`
`floating-constant`
`enumeration-constant`
`character-constant`

### 约束

+ 每个常量应有一个类型，且常量的值应在其类型的可表示值范围内。

### 语义

+ 每个常量都有一个类型，由其形式和值决定，详见后文。

### 6.4.4.1 整数常量 (Integer constants)

### 语法

+ `integer-constant`:
`decimal-constant` `integer-suffix`_{opt}
`octal-constant` `integer-suffix`_{opt}
`hexadecimal-constant` `integer-suffix`_{opt}

+ `decimal-constant`:
`nonzero-digit`
`decimal-constant` `digit`

+ `octal-constant`:
`0`
`octal-constant` `octal-digit`

+ `hexadecimal-constant`:
`hexadecimal-prefix` `hexadecimal-digit`
`hexadecimal-constant` `hexadecimal-digit`

+ `hexadecimal-prefix`: one of
`0x` `0X`

+ `nonzero-digit`: one of
`1` `2` `3` `4` `5` `6` `7` `8` `9`

+ `octal-digit`: one of
`0` `1` `2` `3` `4` `5` `6` `7`
`hexadecimal-digit`: one of
`0` `1` `2` `3` `4` `5` `6` `7` `8` `9`
`a` `b` `c` `d` `e` `f`
`A` `B` `C` `D` `E` `F`

`integer-suffix`:
`unsigned-suffix` `long-suffix-opt`
`unsigned-suffix` `long-long-suffix`
`long-suffix` `unsigned-suffix-opt`
`long-suffix` `unsigned-suffix-opt`

`unsigned-suffix`: one of
`u` `U`

`long-suffix`: one of
`1` `L`

`long-suffix`: one of
`11` `LL`

© ISO/IEC 2011 – 保留所有权利 ISO/IEC 9899:2011 (E)

### 描述

+ 2 整数常量以数字开头，但没有点号或指数部分。它可能有一个指定其基数的前缀，以及一个指定其类型的后缀。

+ 3 十进制常量以非零数字开头，由一系列十进制数字组成。八进制常量由前缀 `0` 可选地跟随一个仅由数字 0 到 7 的序列组成。十六进制常量由前缀 `0x` 或 `0X` 开头，由一系列十进制数字和字母 `a`（或 `A`）、`f`（或 `F`）组成，其值分别为 10 到 15。

### 语义

+ 4 十进制常量的值按基 10 计算；八进制常量的按基 8 计算；十六进制常量的按基 16 计算。词法上的第一个数字是最高位数字。

+ 5 整数常量的类型是其值可以表示的对应列表中第一个。

### §6.4.4.1

ISO/IEC 9899:2011 (E)

| 后缀 | 十进制常量 | 八进制或十六进制常量 |
| --- | --- | --- |
| none | `int`<br>`long int`<br>`long long int` | `int`<br>`unsigned int`<br>`long int`<br>`unsigned long int`<br>`long long int`<br>`unsigned long int` |
| `u` or `U` | `unsigned int`<br>`long int`<br>`long long int` | `unsigned int`<br>`long int`<br>`long long int` |
| `1` or `L` | `long int`<br>`long long int` | `long int`<br>`unsigned long int`<br>`long int`<br>`unsigned long int` |
| Both `u` or `U` and `1` or `L` | `unsigned long int`<br>`long long int` | `unsigned int`<br>`unsigned long int` |
| Both `u` or `U` and `1` or `L` | `long int`<br>`long long int` | `long long long int` |

如果常量不能由列表中的任何类型表示，则该常量为错误。

ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 保留所有权利

## 6.4.4.2 浮点常量 (Floating constants)

### 语法

+ `floating-constant`:
`decimal-floating-constant`
`hexadecimal-floating-constant`

+ `decimal-floating-constant`:
`decimal-signand` `exponent-part`<opt>
`floating-suffix`<opt>

+ `hexadecimal-floating-constant`:
`hexadecimal-prefix` `hexadecimal-signand` `exponent-part`<opt>
`hexadecimal-suffix`<opt>

+ `decimal-signand`:
`nonzero-digit`
`decimal-signand` `digit`

+ `hexadecimal-signand`:
`hexadecimal-prefix` `hexadecimal-digit`
`hexadecimal-signand` `hexadecimal-digit`

+ `hexadecimal-prefix`: one of
`0x` `0X`

+ `nonzero-digit`: one of
`1` `2` `3` `4` `5` `6` `7` `8` `9`

+ `hexadecimal-digit`: one of
`0` `1` `2` `3` `4` `5` `6` `7` `8` `9`
`a` `b` `c` `d` `e` `f`
`A` `B` `C` `D` `E` `F`

+ `exponent-part`:
`sign` `digit-sequence`<opt>
`sign`: one of
`+` `-`
`digit-sequence`: `digit`
`digit-sequence` `digit`

+ `floating-suffix`:
`unsigned-suffix` `long-suffix-opt`
`unsigned-suffix` `long-long-suffix`
`long-suffix` `unsigned-suffix-opt`
`long-suffix` `unsigned-suffix-opt`

+ `unsigned-suffix`: one of
`u` `U`

`long-suffix`: one of
`1` `L`

`long-suffix`: one of
`11` `LL`

### 描述

+ 2 浮点常量有一个尾数部分，后面可以跟一个指数部分，并可能包含一个指定其类型的后缀。

+ 3 十进制浮点常量以非零数字开头，由一系列十进制数字、点号以及另一序列十进制数字组成。十六进制浮点常量由前缀 `0x` 或 `0X` 开头，由一系列十六进制数字和值分别为 10 到 15 的字母组成。指数部分由 `e`、`E`、`p` 或 `P` 后跟带符号的数字序列组成。

### 语义

+ 4 十进制浮点常量的值按基 10 计算；十六进制浮点常量按基 16 计算。尾数解释为（十进制或十六进制）有理数；指数表示尾数要缩放的 10 或 2 的幂次。

+ 5 浮点常量的类型是其值可以表示的对应列表中第一个。

+ 6 带后缀的浮点常量类型为 `double`。如果后缀为 `f` 或 `F`，则类型为 `float`。如果后缀为 `l` 或 `L`，则类型为 `long double`。

+ 7 浮点常量在翻译时被转换为内部格式。浮点常量的转换在执行期间不会引发异常状态或浮点异常。所有源形式的浮点常量⁷⁷⁵) 应转换为相同的内部格式具有相同的值。

### 建议做法

8 如果常量无法在其评估格式中精确表示，实现应产生诊断信息；然后实现应继续程序的翻译。

9 浮点常量的翻译时转换应与库函数（如 `strtod`）对字符串的执行时转换匹配，前提是两种转换的输入相同、结果格式相同且使用默认执行时舍入⁷⁶)

> ⁷⁷⁵) 库函数建议的转换精度比浮点常量要求的更精确。

## 6.4.4.3 枚举常变量

语法

```
enumeration-constant:
  identifier
```

声明为枚举常量的标识符其类型为 `int`。

前向引用：枚举说明符 (`6.7.2.2`)。

## 6.4.4.4 字符常量

语法

```
' c-char-sequence ' 
L' c-char-sequence ' 
u' c-char-sequence ' 
U' c-char-sequence ' 
c-char-sequence:
  c-char
  c-char-sequence c-char
c-char:
  源字符集中的任意成员，但
  单引号 '、反斜杠 \ 或换行字符
  转义序列
escape-sequence:
  simple-escape-sequence
  octal-escape-sequence
  hexadecimal-escape-sequence
  universal-character-name
simple-escape-sequence: 
  \' ' \ \
  a \b \f \n \t \v
octal-escape-sequence:
  \octal-digit
  \octal-digit octal-digit
  \octal-digit octal-digit octal-digit
```

`hexadecimal-escape-sequence`:

`\x` `hexadecimal-digit`

`hexadecimal-escape-sequence` `hexadecimal-digit`

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 版权所有

### 描述

- 2 整数字符常量是用单引号括起来的一个或多个多字节字符的序列，例如 `'x'`。宽字符常量与之相同，但额外带有字母 `L`、`u` 或 `U` 作为前缀。在详细说明的少数例外之外，序列中的元素是源字符集的成员；它们以一种实现定义的方式映射到执行字符集的成员。

- 3 单引号 `'`、双引号 `"`、问号 `?`、反斜杠 `\` 以及任意整数均可根据下面的转义序列表进行表示：

| 单引号 `'` | `\'` |
| 双引号 `"` | `\"` |
| 问号 `?` | `\?` |
| 反斜杠 `\` | `\\` |
| 八进制字符 | `\octal digits` |
| 十进制字符 | `\x hexadecimal-digit` |

- 4 双引号 `"` 和问号 `?` 既可以通过自身表示，也可以分别通过转义序列 `\"` 和 `\?` 表示；而单引号 `'` 和反斜杠 `\` 则应通过转义序列 `\'` 和 `\\` 表示。

- 5 转义序列中反斜杠后面的数字被视为整数字符常量的单个字符构建或宽字符常量的单个字符构建的一部分。该八进制整数的数值据此构成了所需字符或宽字符的值。

- 6 十进制转义序列中反斜杠和字母 `\x` 之后的十六进制数字被视为整数字符常量的单个字符构建或宽字符常量的单个字符构建的一部分。该十六进制整数的数值据此构成了所需字符或宽字符的值。

- 7 每个八进制或十六进制转义序列都是构成该转义序列的最长字符序列。

- 8 此外，不在基本字符集中的字符可以通过通用字符名称表示，以及某些由反斜杠 `\` 后跟小写字母组成的非图形字符表示：`\a`, `\b`, `\f`, `\n`, `\r`, `\t`, 和 `\v`(77)。

语言

§6.4.4.4

八进制或十六进制转义序列的值应在对应类型的可表示值范围内：

| 前缀 | 对应类型 |
| --- | --- |
| 无 | `unsigned char` |
| `L` | `wchar_` |
| `u` | `char16_t` |
| `U` | `char32_t` |

### 语义

整数字符的类型为 `int`。包含映射到单字节执行字符的单个字符的整数常量的值为该字符的表示值。包含多个字符（例如 `'ab'`）或包含不映射到单字节执行字符的转义序列的整数常量的值取决于实现。如果整数常量包含单个字符或转义序列，其值为带有字母 `L` 前缀的宽字符（在 `<stddef.h>` 中定义的 `wchar_`）；带有字母 `u` 或 `U` 前缀的宽字符分别为 `char16_t` 或 `char32_t`（分别在 `<uchar.h>` 中定义）。包含对应执行字符集的单个多字节字符的宽字符的值，由 `mbtowc`、`mbrtoc6` 或 `mbrtoc32`（取决于其类型而定）定义。

示例 1 构造 `'\0'` 常用于表示空字符。

示例 2 使用补码表示整数并对类型为 `char` 的对象使用八位的情况：在 `char` 范围与 `unsigned char` 相同的实现中，整数常量 `'\xff'` 的值为 `-1`；如果 `char` 范围与 `unsigned char` 相同，字符常量 `'\xff'` 的值为 `+255`。(77)字符的语义在 5.2 中讨论过。如果反斜杠后跟随任何其他字符，则结果无效并需要诊断。参见“未来方向”(`6.1.4`)。

示例 3 即使对类型为 `char` 的对象使用八位，构造 `'\123'` 指定了一个仅包含一个字符的整数常量，由十六进制转义序列结束。为了指定包含值为 `\x12` 和 `'3'` 的双字符常量，可以使用构造 `'\023'`，以三个八进制数字结束。（该双字符整数常量的值取决于实现。）

示例 4 即使对类型为 `wchar_t` 的对象使用更多位，构造 `L'\1234'` 指定了由值 0 和 `'4'` 组合得到的实现的值。

前向引用：常见定义 `<stddef.h>` (7.19)，`mbtowc` 函数 (7.2)，Unicode 字面量 `<uchar.h>` (7.28)。

## 6.4.5 字面量

语法

```
string-literal:
  encoding-prefix_opt s-char-sequence_opt
  encoding-prefix:
    u8
    u
    U
    L
  s-char-sequence:
    s-char
    s-char-sequence s-char
  源字符集中的任意成员，但
  双引号 ", 反斜杠 \ 或换行字符
  escape-sequence
```

### 约束

- 2 相邻字面量标记序列不应同时包含宽字面量和 UTF-8 字面量。

### 描述

- 3 字符串常量是用双引号括起来的零或多个多字节字符的序列，例如 `"xyz"`。UTF-8 字面量与之相同，但带有 `u8` 前缀。宽字面量与之相同，但带有字母 `L`、`u` 或 `U` 前缀。

- 4 相同的考虑适用于字符串的每个元素，如同它是整数常量（对于字符或 UTF-8 字面量）或宽字符（对于宽字面量），可以通过自身或转义序列 `\'` 表示，但双引号 `"` 应由转义序列 `\"` 表示。

### 语义

- 5 在翻译阶段 6 中，任何相邻字符和相同前缀字面量标记序列指定的多字节序列被合并成单个多字节序列。如果标记中的任一个具有编码前缀，则生成的多字节序列被视为具有相同的前缀；否则，被视为字符串常量。不同前缀的字面量标记是否可以合并，如果是，则生成的多字节序列的结果取决于实现。

- 6 在翻译阶段 7 中，零的字节或代码值被编码到由字符串或字面量生成的每个多字节序列中。然后使用该多字节序列来初始化具有静态存储期且足够包含该序列的数组。对于字符常量，数组元素类型为 `char`，并用多字节序列的各个字符初始化。对于 UTF-8 字面量，数组元素类型为 `char`，并用 UTF-8 编码的多字节序列的字符初始化。对于带有字母 `l` 前缀的宽字面量，数组元素类型为 `char_t`，并根据实现定义的当前区域由 `mbstows` 函数定义与多字节序列对应的宽字符序列初始化。带有字母 `u` 或 `O` 前缀的宽字面量，数组元素类型分别为 `char16_t` 或 `char32_t`，并根据其类型通过适连续调用 `mbrtoc6` 或 `mbrtoc32` 定义与多字节序列对应的宽字符序列初始化。包含在执行字符集中未表示的多字节字符或转义序列的字符串常量的值取决于实现。

- 7 不确定这些数组的各个元素是否具有适当的值。如果程序尝试修改数组，行为是未定义的。

示例 1 这对相邻的字符字面量

```
"\x12" "3"
```

产生一个包含两个值为 `\x12` 和 `'3'` 的字符的单个字符串常量，因为转义序列在相邻字符串字面量合并之前会被转换为执行字符集中的单个成员。

- 9 示例 2 每个相邻字面量标记序列的每个

78) 字符串常量不需要是字符串（参见 7.1.1），因为可以通过 `\0` 转义序列在其中嵌入空字符。

# ISO/IEC 9899:2011 (E)

"a" "b" "L"c"

"a" "L"b" "c"

L"a" "b" "L"c"

L"a" "L"b" "L"c"

同样，每一个序列

"a" "b" "u"c"

"a" "u"b" "c"

u"a" "b" "u"c"

"u" "u"b" "u"c"

均等于

uuabcabc

**前向引用：**常用定义 `<stddef.h>` (7.19)，**mbstowcs** 函数 (72.2.8.1)，`<uchar.h>` 中的 Unicode 单元 (7.28)。

## 6.4.6 标点符号

### 语法

- 标点符号：以下之一

[ ] ( ) { } . ->

++ / & * + ~ !

/ % << >> > <= == != ^ && ||

? ;

* = / % += - <= >= &= = | |

# ##

< : > % % % : % ::

### 语义
