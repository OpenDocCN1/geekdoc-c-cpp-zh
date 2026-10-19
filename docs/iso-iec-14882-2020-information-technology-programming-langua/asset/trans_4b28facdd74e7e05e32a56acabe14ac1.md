

# ISO/IEC 14882:2020(E)

```
binary-exponent-part:
    p sign_opt digit-sequence
    P sign_opt digit-sequence

sign: one of
    + -

digit-sequence:
    digit
    digit-sequence opt digit

floating-point-suffix: one of
    f l F L
```

1 浮点字面量的类型由其浮点后缀决定，如表 10 所述。

## 表 10：浮点字面量的类型 [tab:lex.fcon.type]

| floating-point-suffix | type |
|---|---|
| none | double |
| f or F | float |
| l or L | long double |

2 浮点字面量的有效数字是十进制浮点字面量的 fractional-constant 或 digit-sequence，或十六进制浮点字面量的 hexadecimal-fractional-constant 或 hexadecimal-digit-sequence。在有效数字中，数字或十六进制数字序列以及可选的句点被解释为基数 N 的实数 s，其中 N 对于十进制浮点字面量为 10，对于十六进制浮点字面量为 16。 [注 1：确定值时，任何可选的分隔单引号都被忽略。——注结束]

如果存在 exponent-part 或 binary-exponent-part，则浮点字面量的指数 e 是将可选符号和数字序列解释为基数 10 整数的结果。否则，指数 e 为 0。字面量的缩放值为 s × 10^e 对于十进制浮点字面量，以及 s × 2^e 对于十六进制浮点字面量。

> [示例 1：浮点字面量 49.625 和 0xC.68p+2 具有相同的值。浮点字面量 1.602'176'565e-19 和 1.602176565e-19 具有相同的值。——示例结束]

3 如果缩放值不在其类型的可表示值范围内，则程序格式错误。否则，浮点字面量的值是如果可表示则为缩放值，否则为最接近缩放值的较大或较小的可表示值，以实现定义的方式选择。

## 5.13.5 字符串字面量 [lex.string]

```
string-literal:
    encoding-prefix_opt " s-char-sequence_opt "
    encoding-prefix_opt R raw-string

s-char-sequence:
    s-char
    s-char-sequence s-char

s-char:
    any member of the basic source character set except the double-quote ", backslash \, or new-line character
    escape-sequence
    universal-character-name

raw-string:
    " d-char-sequence_opt ( r-char-sequence_opt ) d-char-sequence_opt "

r-char-sequence:
    r-char
    r-char-sequence r-char

r-char:
    any member of the source character set, except a right parenthesis ) followed by
    the initial d-char-sequence (which may be empty) followed by a double quote ".

d-char-sequence:
    d-char
    d-char-sequence d-char
```

# ISO/IEC 14882:2020(E)

*d-char:* 除了空格、左括号 (、右括号 )、反斜杠 \ 以及表示水平制表符、垂直制表符、换页符和换行的控制字符之外，基本源字符集的任何成员。

1 具有 R 前缀的 *string-literal* 是 *raw string literal*。*d-char-sequence* 用作分隔符。*raw-string* 的终止 *d-char-sequence* 与初始 *d-char-sequence* 相同的字符序列。*d-char-sequence* 最多应包含 16 个字符。

2 [注 1：字符 ‘(‘ 和 ‘)’’ 允许出现在 *raw-string* 中。因此，R"delimiter((a|b))delimiter" 等价于 "(a|b)"。——注结束]

3 [注 2：原始字符串字面量中的源文件换行会导致结果执行字符串字面量中出现换行。假设以下示例中各行开头没有空白，断言将成功：

```
const char* p = R"(a\
b
c)";
assert(std::strcmp(p, "a\\\n\nb\nc") == 0);
```

——注结束

4 [示例 1：原始字符串 R"a( )\ a" )a" 等价于 "\n)\\na\"\n"。原始字符串 R"(x = \"y\")" 等价于 "x = \"\\\"y\\\"\" 。——示例结束]

5 在翻译阶段 6 之后，不以 *encoding-prefix* 开头的 *string-literal* 是 *ordinary string literal*。普通字符串字面量具有类型“n 个 const char 的数组”，其中 n 为如下定义的字符串大小，具有静态存储期 (6.7.5)，并用给定的字符初始化。

6 以 u8 开头的 *string-literal*，例如 u8"asdf"，是 *UTF-8 string literal*。UTF-8 字符串字面量具有类型“n 个 const char8_t 的数组”，其中 n 为如下定义的字符串大小；对象表示 (6.8) 的每个连续元素具有字符串的 UTF-8 编码的对应代码单元的值。

7 普通字符串字面量和 UTF-8 字符串字面量也称为窄字符串字面量。

8 以 u 开头的 *string-literal*，例如 u"asdf"，是 *UTF-16 string literal*。UTF-16 字符串字面量具有类型“n 个 const char16_t 的数组”，其中 n 为如下定义的字符串大小；数组的每个连续元素具有字符串的 UTF-16 编码的对应代码单元的值。

[注 3：单个 c-char 可能产生 UTF-16 字符形式的高低代理对的多个 char16_t 字符。代理对是对单个代码点作为两个 16 位代码单元序列的表示。——注结束]

9 以 U 开头的 *string-literal*，例如 U"asdf"，是 *UTF-32 string literal*。UTF-32 字符串字面量具有类型“n 个 const char32_t 的数组”，其中 n 为如下定义的字符串大小；数组的每个连续元素具有字符串的 UTF-32 编码的对应代码单元的值。

10 以 L 开头的 *string-literal*，例如 L"asdf"，是 *wide string literal*。宽字符串字面量具有类型“n 个 const wchar_t 的数组”，其中 n 为如下定义的字符串大小；它用给定的字符初始化。

11 在翻译阶段 6 (5.2) 中，相邻的 *string-literals* 会被连接。如果两个 *string-literals* 具有相同的 *encoding-prefix*，则 resulting concatenated *string-literal* 具有该 *encoding-prefix*。如果一个 *string-literal* 没有 *encoding-prefix*，则将其视为具有与另一个操作数相同的 *encoding-prefix* 的 *string-literal*。如果 UTF-8 字符串字面量标记与宽字符串字面量标记相邻，则程序格式错误。任何其他连接都是条件支持的，具有实现定义的行为。

[注 4：此连接是解释，而不是转换。因为解释发生在翻译阶段 6（在每个字符从 *string-literal* 翻译为来自适当字符集的值之后），所以 *string-literal* 的初始原始性对连接的解释或格式良好性没有影响。——注结束]

表 11 给出了一些有效连接的示例。

## 表 11：字符串字面量连接 [tab:lex.string.concat]

| Source | Means | Source | Means | Source | Means |
|---|---|---|---|---|---|
| u"a" u"b" u"ab" | U"a" U"b" U"ab" | L"a" L"b" L"ab" |
| u"a" "b" u"ab" | U"a" "b" U"ab" | L"a" "b" L"ab" |
| "a" u"b" u"ab" | "a" U"b" U"ab" | "a" L"b" L"ab" |

连接字符串中的字符保持区分。

> [示例 2：
> "\xA" "B"
> 连接后包含两个字符 '\xA' 和 'B'（而不是单个十六进制字符 '\xAB'）。
> ——示例结束]

12 在任何必要的连接之后，在翻译阶段 7 (5.2) 中，'\0' 会被追加到每个 string-literal，以便扫描字符串的程序可以找到其结束位置。

13 非原始字符串字面量中的转义序列和通用字符名具有与字符字面量 (5.13.3) 相同的含义，除了单引号 ' 可以由其本身或转义序列 \' 表示，双引号 " 必须前面加上 \，并且 UTF-16 字符串字面量中的通用字符名可能产生代理对。在窄字符串字面量中，通用字符名可能由于多字节编码而映射到一个以上的 char 或 char8_t 元素。char32_t 或宽字符串字面量的大小是转义序列、通用字符名和其他字符的总数量，外加终止 U'\0' 或 L'\0' 的一个。UTF-16 字符串字面量的大小是转义序列、通用字符名和其他字符的总数量，外加每个需要代理对的字符的一个，外加终止 u'\0' 的一个。

> [注 5：char16_t 字符串字面量的大小是代码单元的数量，而不是字符的数量。——注结束]

> [注 6：任何通用字符名都必须对应于范围 [0, D800) 或 [E000, 10FFFF]（十六进制）内的代码点 (5.3)。——注结束]

窄字符串字面量的大小是转义序列和其他字符的总数量，外加每个通用字符名的多字节编码的至少一个，外加终止 '\0' 的一个。

14 评估字符串字面量会产生具有静态存储期的字符串字面量对象，从给定的字符按上述方式初始化。是否所有字符串字面量都是不同的（即存储在不重叠的对象中）以及对字符串字面量的连续求值是否产生相同或不同的对象是未指定的。

> [注 7：尝试修改字符串字面量的效果是未定义的。——注结束]

## 5.13.6 布尔字面量 [lex.bool]

+   boolean-literal:
+     false
+     true

1 布尔字面量是关键字 false 和 true。此类字面量是 prvalues 且具有类型 bool。

## 5.13.7 指针字面量 [lex.nullptr]

+   pointer-literal:
+     nullptr

1 指针字面量是关键字 nullptr。它是类型 std::nullptr_t 的 prvalue。

> [注 1：std::nullptr_t 是一个不同的类型，既不是指针类型也不是指向成员的指针类型；相反，此类型的 prvalue 是空指针常量，可以转换为空指针值或空成员指针值。请参见 7.3.12 和 7.3.13。——注结束]

## 5.13.8 用户定义字面量 [lex.ext]

+   user-defined-literal:
+     user-defined-integer-literal
+     user-defined-floating-point-literal
+     user-defined-string-literal
+     user-defined-character-literal

