
```
hex-digits::
    hex-digit
    hex-digits hex-digit

hex-digit:: one of
    0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f
```

整型字面量的类型按如下方式确定：

- 如果字面量没有后缀，则其类型为能够表示其值的这些类型中的第一个：int、uint、long、ulong。
- 如果字面量带有后缀 U 或 u，则其类型为能够表示其值的这些类型中的第一个：uint、ulong。
- 如果字面量带有后缀 L 或 l，则其类型为能够表示其值的这些类型中的第一个：long、ulong。
- 如果字面量带有后缀 UL、Ul、uL、ul、LU、Lu、lU 或 lu，则其类型为 ulong。

如果整型字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

> [注意：从风格上考虑，建议在书写 long 类型字面量时使用“L”而不是“l”，因为字母“l”很容易与数字“1”混淆。注意结束]

为了允许将尽可能最小的 int 和 long 值写成整型字面量，存在以下两条规则：

- 当表示值 2147483648（2^31）且没有整型类型后缀的整型字面量作为一元减号运算符标记（§12.8.3）之后紧邻的标记出现时，结果（两个标记的结果）是类型为 int、值为 -2147483648（-2^31）的常量。在所有其他情况下，这种整型字面量的类型为 uint。
- 当表示值 9223372036854775808（2^63）且没有整型类型后缀或整型类型后缀为 L 或 l 的整型字面量作为一元减号运算符标记（§12.8.3）之后紧邻的标记出现时，结果（两个标记的结果）是类型为 long、值为 -9223372036854775808（-2^63）的常量。在所有其他情况下，这种整型字面量的类型为 ulong。

## 7.4.5.4 实数字面量

实数字面量用于书写 float、double 和 decimal 类型的值。

```
real-literal::
    decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
    . decimal-digits exponent-part_opt real-type-suffix_opt
    decimal-digits exponent-part real-type-suffix_opt
    decimal-digits real-type-suffix

exponent-part::
    e sign_opt decimal-digits
    E sign_opt decimal-digits

sign:: one of
    + -

real-type-suffix:: one of
    F f D d M m
```

如果未指定实型类型后缀，则实数字面量的类型为 double。否则，实型类型后缀决定实数字面量的类型，如下所示：

- 带有后缀 F 或 f 的实数字面量类型为 float。[示例：字面量 1f、1.5f、1e10f 和 123.456F 均为 float 类型。示例结束]
- 带有后缀 D 或 d 的实数字面量类型为 double。[示例：字面量 1d、1.5d、1e10d 和 123.456D 均为 double 类型。示例结束]
- 带有后缀 M 或 m 的实数字面量类型为 decimal。[示例：字面量 1m、1.5m、1e10m 和 123.456M 均为 decimal 类型。示例结束] 此字面量通过取精确值转换为 decimal 值，如有必要，使用银行家舍入法（§9.3.8）舍入到最接近的可表示值。除非值被舍入，否则字面量中出现的任何小数位数都会保留。[注意：因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、小数位数为 3 的 decimal。注意结束]

如果指定字面量的量级太大，无法在指示的类型中表示，则发生编译时错误。[注意：特别地，实数字面量永远不会产生浮点无穷大。但是，非零实数字面量可能会被舍入为零。注意结束]

float 或 double 类型的实数字面量的值通过使用 IEC 60559“舍入到最接近”模式确定，其中平局打破为“偶数”（最低有效位为零的值），并且所有数字均视为有效。

[注意：在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，但 1.F 不是。注意结束]

## 7.4.5.5 字符字面量

字符字面量表示单个字符，由引号中的字符组成，如 'a'。

```
character-literal::
  ' character '

character::
  single-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-character::
  Any character except ' (U+0027), \ (U+005C), and new-line-character

simple-escape-sequence:: one of
  \' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence::
  \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt
```

[注意：字符字面量中反斜杠字符（\\）之后的字符必须是以下字符之一：'、\"、\\、0、a、b、f、n、r、t、u、U、x、v。否则，发生编译时错误。注意结束]

> [注意：使用 \x 十六进制转义序列产生式可能容易出错且难以阅读，因为 \x 后面的十六进制数字位数可变。例如，在以下代码中：
string good = "\x9Good text";
string bad = "\x9Bad text";
乍看之下，两个字符串中的前导字符可能相同（U+0009，制表符）。实际上第二个字符串以 U+9BAD 开头，因为单词“Bad”中的所有三个字母都是有效的十六进制数字。从风格上考虑，建议避免使用 \x，而使用特定转义序列（本例中为 \t）或固定长度的 \u 转义序列。注意结束]

十六进制转义序列表示单个 Unicode UTF-16 代码单元，其值由“\x”后面的十六进制数字构成。

如果字符字面量表示的值大于 U+FFFF，则发生编译时错误。

字符字面量中的 Unicode 转义序列（§7.4.2）应处于 U+0000 到 U+FFFF 的范围内。

```
verbatim-string-literal::
  @" verbatim-string-literal-characters_opt "
verbatim-string-literal-characters::
  verbatim-string-literal-character
  verbatim-string-literal-characters verbatim-string-literal-character
verbatim-string-literal-character::
  single-verbatim-string-literal-character
  quote-escape-sequence
single-verbatim-string-literal-character::
  Any character except "
quote-escape-sequence::
  ""
```

```
[Example: The example
string a = "Happy birthday, Joel";      // Happy birthday, Joel
string b = @"Happy birthday, Joel";     // Happy birthday, Joel
string c = "hello \t world";            // hello    world
string d = @"hello \t world";           // hello \t world
string e = "Joe said \"Hello\" to me";  // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt";   // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

展示了各种字符串字面量。最后一个字符串字面量 j 是跨多行的逐字字符串字面量。引号之间的字符（包括换行符等空白）均逐字保留，每一对双引号字符替换为一个这样的字符。示例结束

> [注意：逐字字符串字面量中的任何换行都是结果字符串的一部分。如果用于形成换行的确切字符对应用程序具有语义相关性，那么任何将源代码中的换行转换为不同格式（例如在“\n”和“\r\n”之间）的工具都会改变应用程序行为。开发人员在此类情况下应小心。注意结束]

> [注意：由于十六进制转义序列可以有可变数量的十六进制数字，字符串字面量 "\x123" 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以改为写 "\x00123" 或 "\x12" + "3"。注意结束]

字符串字面量的类型为 string。

每个字符串字面量不一定都会产生新的字符串实例。当两个或多个根据字符串相等运算符（§12.11.8）等价的字符串字面量出现在同一程序集中时，这些字符串字面量引用同一个字符串实例。[示例：例如，由以下代码产生的输出

```
class Test
{
  static void Main() {
    object a = "hello";
    object b = "hello";
    System.Console.WriteLine(a == b);
  }
}
```

为 True，因为这两个字面量引用同一个字符串实例。示例结束]
