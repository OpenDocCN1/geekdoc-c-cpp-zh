
```a b c d e f g h i j k l m n o p q r s t u v w x y
A B C D E F G H I J K L M N O P Q S T U V W X Z
0 1 2 3 4 5 6 7 8 9
- { } [ ] < > = % $ ^ _ . , ; ? ~ * - & | |```
2通用字符名构造了一种命名其他字符的方法。

```十六进制对:
十六进制数字-十六进制
```

```通用字符名:
uu十六进制对十六进制对
```

通用字符名表示 ISO/IEC 10646 中的字符，其代码点是由通用字符名中的十六进制数字表示的十六进制数。非字符点和预留代码点被视为指定任何 ISO/IEC 10646 字符。*通用字符名* c-序列、s-序列或 r-序列，字符字面量*或字符串（在任何情况下；*定义列表*内）对应于控制字符或源字符集，程序将是非法的¹³¹² 源字符集的成员旨在标识来自 ISO/IEC 10646 子集的 ASCII 字符。然而，从源文件到字符集（在翻译阶段 1 中定义）的映射是由实现定义的，因此必须记录源字符如何在源文件中表示。

¹³ r-序列 (5.13.5) 中类似于通用字符名的字符序列不形成通用字符。

# ISO/IEC 14882:2020(E)

> [注意 1：ISO/IEC 10646 代码点在 [0,FFFFFFFF]（十六进制）范围内。代理点是范围 [D800,DFFF]（十六进制）内的值。控制字符是代码点位于 [0,1F] 或 [7F,9F]（十六进制）范围内的字符。—— 笔记结束

基础执行集和基础宽字符集应包含源字符集的所有成员，加上表示警告和回车的字符，以及一个空字符（代表空字符），其值为 0。对于每个基础字符集，成员的值是非负且互不相同的。源集和执行集的数字都大于前一个。执行字符集和执行宽字符集分别是基础执行字符集和基础宽字符集的超集实现。执行字符集成员的值和成员集合是特定区域的。

### 5.4 预处理标记

标记:

- 头文件名
- 导入关键字
- 模块关键字
- 导出关键字
- 标识符
- 字符字面量
- 用户定义字符字面量
- 字符串
- 用户定义字符串
- 运算符
- 不属于上述的非空白字符

每个在翻译 (5.6) 中转换的预处理标记都应具有关键字、标识符或运算符或标点的词法形式。

预处理标记是翻译阶段 3 到 6 期间语言的最小元素。预处理标记的类别有：头文件名、由导入和模块指令产生的标记（导入关键字、模块关键字和导出关键字）、标识符、字面量（包括用户定义字面量）、字符串字面量（包括用户定义字面量）、在词法上不匹配其他预处理标记的空白字符。如果 * 或 " 字符匹配成功，则行为是未定义的。预处理标记可以由由 (5.7) 组成的空白或空白字符（空格、水平空格、换行、制表符和分页符）分隔。如第 15 节所述，在翻译阶段 4 期间，空白出现在预处理标记之间仅作为多个标记，或者出现在字符字面量或字符串的字符之间。

如果输入流已解析到给定字符的预处理标记：

如果下一个字符开始了一个作为原始字符串前缀和初始双引号的字符序列：

```编码前缀=原始字符串
```

否则，如果接三个字符是 <: 且随后的字符不是 :，则 < 被视为一个独立的预处理标记，而不是可选标记的第一个。

否则，下一个是匹配预处理标记语法的最长字符序列，即使这会导致。

示例 1:

```
#define "x"
const char s = "y";
```

示例 2:

```
#include
```

示例 3:

```
x += y
```

[注 1：注释字符 //、/* 和 /** 在 // 注释中没有特殊含义，被视为与其他字符相同。同样，注释 // 和 /* 在 /* 注释中没有特殊含义.—注]

### 5.8 头文件名称 (Header names)

```
header-name:
  * h-char-sequence
  * q-char-sequence "
h-char-sequence:
  h-char
  h-char-sequence h-char
h-char:
  any member of the source character set except \ or new-line and \
q-char-sequence:
  q-char
  q-char-sequence q-char
q-char:
  any member of the source character set except new-line and "
```

+ 1 [注 1：头文件名称标记仅出现在 #include 预处理指令中，或在实现定义的指令中、_has_include 预处理表达式中，或者在 import 标记的某些出现之后（见 5.4）。—注]

header-names 中的序列以一种实现定义的方式映射到头文件或外部文件名，如 15.3 所示。

+ 2 在 q-char-sequence 或 h-char-sequence 中出现字符 ' 或 / 或字符序列 /* 或 // 是取决于支持的，并具有实现定义的语义，在 h-char-sequence 中出现字符 ' ' 也是如此。

### 5.9 预处理数字 (Preprocessing numbers)

```
pp-number:
  digit
  pp-number digit
  pp-number identifier-nondigit
  pp-number ' digit
  pp-number ' nondigit
  pp-number e sign
  pp-number E sign
  pp-number p sign
  pp-number P sign
  pp-number .
```

+ 1 预处理数字在词法上包含所有整数字面量标记 (5.13.2) 和所有浮点字面量标记。

+ 2 预处理数字没有类型或值；它在成功转换为整数字面量或浮点字面量后才会获得这二者。

### 5.10 标识符 (Identifiers)

```
identifier:
  identifier-nondigit
  identifier-nondigit digit
  identifier digit
identifier-nondigit:
  nondigit
  universal-character-name
```

> 17 因此，表示转义序列的字符序列可能会导致错误（如果被解释为与转义序列对应的字符），或者具有完全不同的含义，取决于实现。

# ISO/IEC 14882:2020(E)

nondigit: 以下之一

a b c d e f g h i j k l m

p q r s t u v w x y z

A B C D E F G H I J K L M

NP Q R S T U V W X Y Z -

digit: 以下之一

0 1 2 3 4 5 6 7 8 9

+ 一个任意长度的字母和数字序列。标识符中的每个通用字符名称应指定一个字符，其编码在 ISO/10646 中落在表 2 指定的范围之一。起始元素应为一个通用字符名称，该名称指定的字符的编码落在表 3 指定的范围之一。大写字母和小写字母是不同的。所有显著性字符¹¹¹

表 2：允许的字符范围

| 00A8 | 00AA | 00AD | 00B2-00B5 |
| 00B7-008A | 008C-008E | 00C0-00D6 | 00D8-00F6 | 00F8-00FF |
| 0100-017F | 1681-018D | 180F-01FF | | |
| 200B-200D | 202A-202E | 2054 | 2060-206F | | |
| 2070-218F | 2460-247F | 2776-2793 | 2C00-2DFF | 2E80-2FFFF |
| 3004-3007 | 3021-302F | 3031-037F | | |
| F900-FFD3 | FD40-FD6F | FE50-FE6A | FE47-FE9F | | |
| 10000-1FFFF | 20000-2FFD | 30000-3FFFF | 40000-4FFD | 50000-5FFFF |
| 60000-6FFFF | 70000-7FFFF | 80000-8FFFF | 90000-9FFFF | A0000-AFFF |
| B0000-BFFFF | C0000-CFFF | D0000-DFFF | E0000-EFFFF | |

表 3：不允许的字符范围（组合字符）

| 0300-036F | 1DC0-1FFD | 20D0-20FF | FE20-FE2F |

+ 表 4 中的标识符在引用语法时具有特殊含义。除非另有规定，否则对于给定的标识符是否具有特殊含义的任何歧义都将该标记解释为普通标识符。

表 4：具有特殊含义的标识符

| final | import | override |

+ 此外，某些标识符保留供 C++ 使用，不应被使用；

+ (3.1) 每个包含双下划线或以下划线开头跟大写字母的标识符都留给实现。

+ (3.2) 每个以下划线开头的标识符都留给实现，作为全局命名空间中的名称。

keyword:

import

module

export

>18) 在无法处理扩展字符的系统中，可以使用通用字符名称的编码来形成有效的标识符。例如，可以使用某些未使用的字符或字符序列来编码 .。C++ 不对显著性字符设置翻译限制。在 C++ 中，所有标识符的大写字母和小写字母都是不同的。§11 ISO/IEC 2020 — 版权所有

表 5 所示的标识符被留作关键字使用（它们在第 7 阶段无条件地视为关键字，属性标记除外）。[注 1：register 关键字留作以后使用。]

表 5：关键字

| alignas | constinit | false | public | true |
| alignof | const_cast | float | register | try |
| asm | | recast | typedef |
| auto | co_await | friend | requires | typeid |
| bool | co_return | goto | return | typename |
| if | yield | inline | short | union |
| case | decltype | | signed | unsigned |
| catch | delete | int | sizeof | using |
| char8_t | | static | void |
| char16_t | double | namespace | static_cast | volatile |
| char32_t | dynamic_cast | | struct |
| class | else | switch | null |
| concept | | nullptr | template |
| const | explicit | operator | this |
| constexpr | export | private | thread_local |

此外，表 6 所示的某些运算符和标点 (5.5) 的替代表示是被保留的，且不应使用。

表 6：替代表示

| | and_eq | bitand | bitor | not |
| or_eq | or | xor | not_eq |

### 5.12 运算符和标点 (Operators and punctuators)

C++ 程序的词法表示包含一些预处理的标记，它们用于运算符或标点：

```
preprocessing-or-punct:
  preprocessing-token
  operator
  operator-or-punct: one of
  { } [ ] ( )
  < > | / / &=
  ! != >= <=
  << >> >= <=
  and or not bitand bitor
  and_eq or_eq xor_eq
```

每个 operator-or-punctuator 在翻译阶段 7 (5.2) 中被转换为单个标记。

### 5.13 字面量 (Literals)

### 5.13.1 字面量的种类 (Kinds of literals)

有几种字面量¹¹

- literal:
  integer-literal
  character-literal
  floating-point-literal
  string-literal
  boolean-literal
  pointer-literal
  user-defined-literal

### 5.13.2 整数字面量 (Integer literals)

- integer-literal:
  binary-literal integer-suffix-opt
  octal-literal integer-suffix-opt
  decimal-literal integer-suffix-opt
  hexadecimal-literal integer-suffix-opt

- binary-literal:
  0 binary-digit
  0B binary-digit
  binary-literal-opt binary-digit

- octal-literal:
  0
  octal-literal-opt octal-digit

- decimal-literal:
  nonzero-digit
  decimal-literal-opt digit

- hexadecimal-literal:
  hexadecimal-prefix hexadecimal-digit-sequence

- binary-digit:
  one of one
  0 1

- octal-digit:
  one of one
  0 1 2 3 4 5 6 7

- nonzero-digit:
  one of one
  1 2 3 4 5 6 7 8 9

- hexadecimal-prefix:
  one of one
  0x 0X

- hexadecimal-digit-sequence:
  hexadecimal-digit
  hexadecimal-digit-sequence-opt hexadecimal-digit

- hexadecimal-digit:
  one of one
  0 1 2 3 4 5 6 7 8 9
  a b c d e f
  A B C D E F

- integer-suffix:
  unsigned-suffix long-suffix-opt
  unsigned-suffix long-suffix-opt
  long-suffix unsigned-suffix-opt
  long-suffix unsigned-suffix-opt

- unsigned-suffix:
  one of one
  U

- long-suffix:
  one of one
  L

> 19) “字面量”一词在本文泛指 ISO C 中被称为“常量”的标记。

# ISO/IEC 14882:2020(E)

long-long-suffix: 以下之一

LL

在整数字面量中，二进制位、八进制位、数字位或十六进制位的数字序列被解释为表 7 所示的基数 N 整数；数字序列中词法上的第一个数字是最高位数字。

> *注 1：在确定值时，忽略前缀和任何可选的分隔引号。 — 结束注释*

表 7: 整数字面量的基数 [tab:lex,icon,base]

| 整数字面量类型 | 基数 N |
|---|---|
| 二进制进制字面量 | 2 |
| 八进制字面量 | 8 |
| 十进制字面量 | 10 |
| 十六进制字面量 | 16 |

带有 f 和 F 的十六进制位表示直到十五的十进制值。

[示例 1 数值可以写为 12、0xC 或 0b110。整数字面量 1048576、0X100000、0x1000 和 0'004'000 都具有相同的值。 — 示例]

整数字面量的类型是表 8 列表中与其可选整数后缀相对应的第一个类型，其值可以在该类型中表示。整数字面量是一个值。

表 8: 整数字面量的类型 [tab:lex,icon,type]

| 整数后缀 | 十进制字面量 | 除十进制字面量外的整数字面量 |
|---|---|---|
| 无 | | int |
| | | unsigned int |
| | | long int |
| | | unsigned long int |
| | | long long int |
| | | unsigned long int |
| u 或 U | | unsigned int |
| | | unsigned long int |
| | | unsigned long int |
| | | unsigned long int |
| 1 或 L | | long int |
| | | long int |
| | | unsigned int |
| | | unsigned long int |
| | | unsigned long int |
| 同时包含 u 或 U 和 1 或 L | | unsigned int |
| | | unsigned long int |
| | | long long int |
| 11 或 LL | | long long int |
| | | unsigned long int |
| 同时包含 u 或 U 和 11 或 LL | | unsigned long int |
| | | unsigned long int |
