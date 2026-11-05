
*注释结束*

十六进制转义序列表示单个 Unicode UTF-16 代码单元，其值由跟随在 "\x" 之后的十六进制数构成。

如果字符字面量所表示的值大于 U+FFFF，则发生编译时错误。

字符字面量中的 Unicode 转义序列（§6.4.2）应位于 U+0000 到 U+FFFF 的范围内。

简单转义序列表示一个 Unicode 字符，如下表所述。

| 转义序列 | 字符名称 | Unicode 码位 |
| :--- | :--- | :--- |
| `\'` | 单引号 | U+0027 |
| `\"` | 双引号 | U+0022 |
| `\\` | 反斜杠 | U+005C |
| `\0` | 空字符 | U+0000 |
| `\a` | 警报 | U+0007 |
| `\b` | 退格 | U+0008 |
| `\f` | 换页 | U+000C |
| `\n` | 换行 | U+000A |
| `\r` | 回车 | U+000D |
| `\t` | 水平制表符 | U+0009 |
| `\v` | 垂直制表符 | U+000B |

*字符字面量* 的类型是 char。

## 6.4.5.6 字符串字面量

C# 支持两种形式的字符串字面量：*常规字符串字面量* 和 *逐字字符串字面量*。常规字符串字面量由包含在双引号中的零个或多个字符组成，如 "hello"，并且可以同时包含简单转义序列（例如用于制表符的 \t）以及十六进制和 Unicode 转义序列。

逐字字符串字面量由一个 @ 字符后跟一个双引号字符、零个或多个字符以及一个结束双引号字符组成。

*示例*：一个简单的示例是 @"hello"。*示例结束*

在逐字字符串字面量中，分隔符之间的字符按原样解释，唯一例外是 *引号转义序列*，它表示一个双引号字符。特别地，简单转义序列以及十六进制和 Unicode 转义序列在逐字字符串字面量中不会被处理。逐字字符串字面量可以跨越多行。

```
String_Literal
    : Regular_String_Literal
    | Verbatim_String_Literal
    ;

fragment Regular_String_Literal
    : '"' Regular_String_Literal_Character* '"'
    ;
```

```
fragment Regular_String_Literal_Character
: Single_Regular_String_Literal_Character
| Simple_Escape_Sequence
| Hexadecimal_Escape_Sequence
| Unicode_Escape_Sequence
;

fragment Single_Regular_String_Literal_Character
: ~["\\u000D\u000A\u0085\u2028\u2029]   // anything but ", \, and
New_Line_Character
;

fragment Verbatim_String_Literal
: '@' Verbatim_String_Literal_Character* '"'
;

fragment Verbatim_String_Literal_Character
: Single_Verbatim_String_Literal_Character
| Quote_Escape_Sequence
;

fragment Single_Verbatim_String_Literal_Character
: ~["']   // anything but quotation mark (U+0022)
;

fragment Quote_Escape_Sequence
: '""'
;
```

## 示例：该示例

```
string a = "Happy birthday, Joel"; // Happy birthday, Joel
string b = @"Happy birthday, Joel"; // Happy birthday, Joel
string c = "hello \t world"; // hello world
string d = @"hello \t world"; // hello \t world
string e = "Joe said \"Hello\" to me"; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt"; // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

展示了各种字符串字面量。最后一个字符串字面量 j 是一个跨越多行的逐字字符串字面量。引号之间的字符（包括诸如换行字符之类的空白）按原样保留，并且每一对双引号字符都替换为一个这样的字符。

示例结束

注意：逐字字符串字面量中的任何换行都是结果字符串的一部分。如果用于构成换行的确切字符与应用程序在语义上相关，那么任何将源代码中的换行转换为不同格式（例如在 "\n" 和 "\r\n" 之间）的工具都将改变应用程序行为。开发人员在此类情况下应小心。注释结束

注意：由于十六进制转义序列可以具有可变数量的十六进制数字，字符串字面量 "\x123" 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以改为写 "\x00123" 或 "\x12" + "3"。注释结束

String_Literal 的类型是 string。

每个字符串字面量不一定产生新的字符串实例。当两个或更多根据字符串相等运算符（§11.11.8）等价的字符串字面量出现在同一程序集中时，这些字符串字面量引用同一个字符串实例。

示例：例如，由以下代码产生的输出

```
class Test
{
    static void Main()
    {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```

为 True，因为这两个字面量引用同一个字符串实例。

示例结束

## 6.4.5.7 空字面量

```
null_literal
    : NULL
    ;
```

注意：null_literal 是解析器规则，因为它不引入新的标记种类。注释结束

null_literal 表示 null 值。它没有类型，但可以通过空字面量转换（§10.2.7）转换为任何引用类型或可空值类型。

## 6.4.6 运算符和标点符号

运算符和标点符号有若干种类。运算符用于表达式中，描述涉及一个或多个操作数的运算。

示例：表达式 a + b 使用 + 运算符将两个操作数 a 和 b 相加。示例结束

标点符号用于分组和分隔。

```
operator_or_punctuator
    : '{' | '}' | '[' | ']' | '(' | ')' | '.' | ',' | '::' | ';'
    | '+' | '-' | ASTERISK | SLASH | '%' | '&' | '|' | '~'
    | '=' | '<' | '>' | '?' | '??' | ':' | '++' | '--' | '&&' | '||'
    | '>=' | '==' | '!=' | '<=' | '>=' | '+=' | '-=' | '*=' | '/=' | '%='
    | '&=' | '^=' | '|'
    ;
```

```
right_shift
    : '>' '>'
    ;
```

```
right_shift_assignment
    : '>' '>='
    ;
```

注意：right_shift 和 right_shift_assignment 是解析器规则，因为它们不引入新的标记种类，而是表示两个标记的序列。operator_or_punctuator 规则仅用于描述目的，并不在语法中的其他地方使用。注释结束

right_shift 由两个标记 > 和 > 组成。类似地，right_shift_assignment 由两个标记 > 和 >= 组成。与句法语法中的其他产生式不同，在这些产生式的每一个中，两个标记之间不允许出现任何种类的字符（甚至空白）。这些产生式被特殊处理，以便能够正确处理 type_parameter_lists（§14.2.3）。

注意：在 C# 添加泛型之前，>> 和 >>= 都是单个标记。然而，泛型的语法使用 < 和 > 字符来分隔类型参数和类型实参。通常希望使用嵌套构造类型，例如 List<Dictionary<string, int>>。为了不要求程序员用空格分隔 > 和 >，这两个 operator_or_punctuator 的定义被更改了。注释结束

## 6.5 预处理指令

### 6.5.1 总则

预处理指令提供了有条件地跳过编译单元各节、报告错误和警告条件以及描绘源代码不同区域的能力。

注意：术语“预处理指令”仅为了与 C 和 C++ 编程语言保持一致而使用。在 C# 中，没有单独的预处理步骤；预处理指令作为词法分析阶段的一部分进行处理。注释结束

```
PP_Directive
  : PP_Start PP_Kind PP_New_Line
  ;

fragment PP_Kind
  : PP_Declaration
  | PP_Conditional
  | PP_Line
  | PP_Diagnostic
  | PP_Region
  | PP_Pragma
  ;

// Only recognised at the beginning of a line
fragment PP_Start
  : { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace? // see note below
  ;

fragment PP_Whitespace
  : ( [p{Zs}]  // any character with Unicode class Zs
    | '\u0009' // horizontal tab
    | '\u000B' // vertical tab
    | '\u000C' // form feed
    )+
  ;
```
