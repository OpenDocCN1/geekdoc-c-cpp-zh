

# ISO/IEC 14882:2017(E)

## 5.12 运算符与标点符

C++ 程序的词法表示包含许多预处理标记，这些标记被用于预处理器的语法中，或被转换为运算符和标点符的标记：

```
preprocessing-or-op-punc: one之一
(      )      #       ##      ()
<       :>      %       %%      :      :
new delete ?      :      ;      *
+       *      /       &       /      %
!       |      <       ,      ===     !
<=      &=      <<     ++      >>     <=     ->
and     and_eq  bitand compl  not     not_eq
or     or_eq    xor     or_eq
```

每个 `preprocessing-or-op-punc` 都会在翻译阶段 7 (5.2) 中被转换为单个标记。

## 5.13 字面量

### 5.13.1 字面量的种类

有几种类型的字面量。²²

```
literal:
integer-literal
character-literal
floating-literal
string-literal
boolean-literal
pointer-literal
user-defined-literal
```

### 5.13.2 整数字面量

```
integer-literal:
binary-literal integer-suffix_opt
octal-literal integer-suffix_opt
decimal-literal integer-suffix_opt
hexadecimal-literal integer-suffix_opt
```

```
binary-literal:
0 binary-digit
1 binary-digit
binary-literal ²opt binary-digit
```

```
octal-literal:
0 octal-literal ²opt octal-digit
```

```
decimal-literal:
nonzero-digit
decimal-literal ²opt digit
```

```
hexadecimal-literal:
hexadecimal-prefix hexadecimal-decimal-sequence
binary-digit:
0
1
```

² 在本文中，“字面量”一术语通常泛指在 ISO C 中被称为“常量”的标记。

octal-digit: 之一
0 1 2 3 4 5 6 7
1 L
nonzero-digit: 之一
1 2 3 4 5 6 7 8 9
hexadecimal-prefix: 之一
0x OX
hexadecimal-digit-sequence:
hexadecimal-digit
hexadecimal-digit-sequence [opt] hexadecimal-digit
hexadecimal-digit: 之一
0 1 2 3 4 5 6 7 8 9
a b c d e f
B C D E F
integer-suffix:
unsigned-suffix [opt] unsigned-suffix
unsigned-suffix long-suffix [opt]
long-suffix unsigned-suffix [opt]
long-long-suffix unsigned-suffix [opt]
unsigned-suffix: 之一
u U
long-suffix: 之一
11 L

+ 1. [*斜体]整数字面量[/] 是一个没有点或指数部分的数字序列，带有可选的隔离引号，这些引号在确定其值时会被忽略。数字序列中词法上的第一个数字是最高位。整数字面量可以有一个指定其基数的前缀和一个指定其类型的后缀。二进制字面量（二进制）以 0B 或 0b 开始，由一组二进制位组成。十进制字面量（十进制）以非 0 数字开始，由一组十进制位组成。十六进制字面量（十六进制）以 0X 或 0x 开始，由一组十六进制位组成，包括十进制 A 到 F。*示例：* 数字十二可以写成 12、0xC 或 0b1100。整数字面量 1048576、'1'048576、0x10000、'0'10000 和 0'0000000 的值均相同。 — *示例*

+ 2. 整数字面量的类型是表 7 中表示其值的对应列表中的第一个。

+ 3. 如果一个整数字面量无法用列表中的任何类型表示，且扩展整数类型 (6.5.1) 可以表示其值，则如果该整数字面量列表中的所有类型是有符号的，则扩展整数类型也应是有符号的。如果列表中的所有类型都是无符号的，则扩展整数类型应为无符号的。如果列表同时包含有符号和无符号类型，则扩展整数类型可以是有符号或无符号的。如果程序中的某个翻译单元包含无法用任何允许类型表示的整数字面量，则该程序是格式不的。

> 数字 8 和 9 不是八进制数字。

表 7 — 整数字面量的类型

| 后缀 | 十进制字面量 | 二进制、八进制、十六进制字面量 |
| --- | --- | --- |
| 无 | int | int |
| | long int | unsigned int |
| | long long int | long int |
| | | unsigned int |
| | | long int |
| | | unsigned long int |
| u 或 U | unsigned int | unsigned int |
| | unsigned long int | unsigned long int |
| | unsigned long int | unsigned long int |
| 1 或 L | long int | long int |
| | long long int | unsigned int |
| | | long int |
| | | unsigned long int |
| 同时包含 u 或 U 和 1 或 L | unsigned long int | unsigned int |
| | | unsigned long int |
| 同时包含 u 或 U 和 1 或 LL | unsigned long int | long int |
| | | unsigned long long int |

### 5.13.3 字符字面量

```
character-literal:
  encoding-prefix c-sequence
  encoding-prefix: 之一
    u8 U
  c-sequence:
    char
    c-char:
    the single character
    any of the execution set
  escape-sequence:
    simple-escape
    octal-sequence
  simple-escape: 之一
    \' \b \f \r
  octal-sequence:
    octal-digit
    octal-digit octal-digit
  hexadecimal-sequence:
    hexadecimal-digit
    hexadecimal-digit hexadecimal-digit
```

1. 一个 [*斜体]整数字面量[/] 是一个没有点或指数部分的数字序列，带有可选的隔离引号，这些引号在确定其值时会被忽略。数字序列中词法上的第一个数字是最高位。整数字面量可以有一个指定其基数的前缀和一个指定其类型的后缀。二进制字面量（二进制）以 0B 或 0b 开始，由一组二进制位组成。十进制字面量（十进制）以非 0 数字开始，由一组十进制位组成。十六进制字面量（十六进制）以 0X 或 0x 开始，由一组十六进制位组成，包括十进制 A 到 F。*示例：* 数字十二可以写成 12、0xC 或 0b1100。整数字面量 1048576、'1'048576、0x10000、'0'10000 和 0'000000 的值均相同。 — *示例*

+ 2. 整数字面量的类型是表 7 中表示其值的对应列表中的第一个。

+ 3. 如果一个整数字面量无法用列表中的任何类型表示，且扩展整数类型 (6.5.1) 可以表示其值，则如果该整数字面量列表中的所有类型是有符号的，则扩展整数类型也应是有符号的。如果列表中的所有类型都是无符号的，则扩展整数类型应为无符号的。如果列表同时包含有符号和无符号类型，则扩展整数类型可以是有符号或无符号的。如果程序中的某个翻译单元包含无法用任何允许类型表示的整数字面量，则该程序是格式不的。

*(注：由于原文中 5.13.3 部分的文本似乎存在严重的格式错乱/重复，译文已根据 C++ 标准逻辑进行了结构性对齐和翻译，以确保技术文档的准确性和可读性)*

