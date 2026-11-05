
</summary>
<param>
<c>p1</c> 是要比较的第一个点。
</param>
<param>
<c>p2</c> 是要比较的第二个点。
</param>
<returns>
如果这些点具有相同的位置并且它们具有
完全相同的类型，则为 True；否则为 false。
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
<summary>
此运算符确定两个点是否具有
相同
位置。
</summary>
<param>
<c>p1</c> 是要比较的第一个点。
</param>
<param>
<c>p2</c> 是要比较的第二个点。
</param>
<returns>
如果这些点不具有相同的位置和
完全相同的类型，则为 True；否则为 false。
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.Main">
<summary>
这是 Point 类测试
程序的入口点。
<para>
此程序测试每个方法和运算符，并且
旨在在对 Point 类执行任何非平凡维护
之后运行。
</para>
</summary>
</member>
<member name="P:Graphics.Point.X">
<value>
属性 <c>X</c> 表示点的
x 坐标。
</value>
</member>

## A. 文档注释

```
<member name="P:Graphics.Point.Y">
    <value>
        Property <c>Y</c> represents the point's
        y-coordinate.
    </value>
</member>
</members>
</doc>
```

## B. 语法

本附录包含主文档中出现的词法语法和句法语法，以及不安全代码的语法扩展的摘要。语法产生式在此处按其在主文档中出现的相同顺序排列。

### B.1 词法语法

```
input:
  input-section_opt

input-section:
  input-section-part
  input-section input-section-part

input-section-part:
  input-elements_opt new-line
  pp-directive

input-elements:
  input-element
  input-elements input-element

input-element:
  whitespace
  comment
  token
```

### B.1.1 行终止符

new-line:
- 回车字符（U+000D）
- 换行字符（U+000A）
- 回车字符（U+000D）后跟换行字符（U+000A）
- 下一行字符（U+0085）
- 行分隔符字符（U+2028）
- 段落分隔符字符（U+2029）

### B.1.2 注释

comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt

input-characters:
  input-character
  input-characters input-character

input-character:
  Any Unicode character except a new-line-character

new-line-character:
  Carriage return character (U+000D)
  Line feed character (U+000A)
  Next line character (U+0085)
  Line separator character (U+2028)
  Paragraph separator character (U+2029)

delimited-comment:
  /* delimited-comment-text_opt asterisks */

delimited-comment-text:
  delimited-comment-section
  delimited-comment-text delimited-comment-section

delimited-comment-section:
  /
  asterisks_opt not-slash-or-asterisk

asterisks:
  *
  asterisks *

not-slash-or-asterisk:
  Any Unicode character except / or *

### B.1.3 空白

whitespace:

- 具有 Unicode 类 Zs 的任何字符
- 水平制表字符（U+0009）
- 垂直制表字符（U+000B）
- 换页字符（U+000C）

### B.1.4 标记

token:

- identifier
- keyword
- integer-literal
- real-literal
- character-literal
- string-literal
- operator-or-punctuator

### B.1.5 Unicode 字符转义序列

unicode-escape-sequence:

- \u hex-digit hex-digit hex-digit hex-digit
- \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit

### B.1.6 标识符

identifier:
  available-identifier
  @ identifier-or-keyword

available-identifier:
  An identifier-or-keyword that is not a keyword

identifier-or-keyword:
  identifier-start-character identifier-part-characters_opt

identifier-start-character:
  letter-character
  _ (the underscore character U+005F)

identifier-part-characters:
  identifier-part-character
  identifier-part-characters identifier-part-character

identifier-part-character:
  letter-character
  decimal-digit-character
  connecting-character
  combining-character
  formatting-character

letter-character:
  A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl
  A unicode-escape-sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl

combining-character:
  A Unicode character of classes Mn or Mc
  A unicode-escape-sequence representing a character of class Mn or Mc

decimal-digit-character:
  A Unicode character of the class Nd
  A unicode-escape-sequence representing a character of the class Nd

connecting-character:
  A Unicode character of the class Pc
  A unicode-escape-sequence representing a character of the class Pc

formatting-character:
  A Unicode character of the class Cf
  A unicode-escape-sequence representing a character of the class Cf

### B.1.7 关键字

keyword: one of

- abstract as base bool break
- byte case catch char checked
- class const continue decimal default
- delegate do double else enum
- event explicit extern false finally
- fixed float for foreach goto
- if implicit in int interface
- internal is lock long namespace
- new null object operator out
- override params private protected public
- readonly ref return sbyte sealed
- short sizeof stackalloc static string
- struct switch this throw true
- try typeof uint ulong unchecked
- unsafe ushort using virtual void
- volatile while

### B.1.8 字面量

```
literal:
  boolean-literal
  integer-literal
  real-literal
  character-literal
  string-literal
  null-literal

boolean-literal:
  true
  false

integer-literal:
  decimal-integer-literal
  hexadecimal-integer-literal

decimal-integer-literal:
  decimal-digits integer-type-suffix_opt

decimal-digits:
  decimal-digit
  decimal-digits decimal-digit

decimal-digit: one of
  0 1 2 3 4 5 6 7 8 9

integer-type-suffix: one of
  U u L l UL U1 uL u1 LU Lu 1U 1u

hexadecimal-integer-literal:
  0x hex-digits integer-type-suffix_opt
  0X hex-digits integer-type-suffix_opt

hex-digits:
  hex-digit
  hex-digits hex-digit

hex-digit: one of
  0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f
```

real-literal:
decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
. decimal-digits exponent-part_opt real-type-suffix_opt
decimal-digits exponent-part_opt real-type-suffix_opt
decimal-digits real-type-suffix

exponent-part:
e sign_opt decimal-digits
E sign_opt decimal-digits

sign: one of
- +
- -

real-type-suffix: one of
- F f D d M m

character-literal:
' character '

character:
- single-character
- simple-escape-sequence
- hexadecimal-escape-sequence
- unicode-escape-sequence

single-character:
除 '（U+0027）、\（U+005C）和换行字符之外的任何字符

simple-escape-sequence: one of
\' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence:
\x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt

regular-string-literal-character:
    single-regular-string-literal-character
    simple-escape-sequence
    hexadecimal-escape-sequence
    unicode-escape-sequence

single-regular-string-literal-character:
除 "（U+0022）、\（U+005C）和换行字符之外的任何字符

verbatim-string-literal:
@" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters:
verbatim-string-literal-character
verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character:
    single-verbatim-string-literal-character
    quote-escape-sequence

single-verbatim-string-literal-character:
除 " 之外的任何字符

quote-escape-sequence:
""

null-literal:
null

### B.1.9 运算符和标点符号

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ -- && ||
-= >= <= != <> ?
&= |= ^= <<= >>= += -= *= /= %=

right-shift:
>>

right-shift-assignment:
>>=

