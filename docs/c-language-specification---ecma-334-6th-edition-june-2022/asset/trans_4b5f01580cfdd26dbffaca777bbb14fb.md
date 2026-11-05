
```csharp
if (@bool)
{
    System.Console.WriteLine("true");
}
else
{
    System.Console.WriteLine("false");
}
}
}
class Class1
{
    static void M()
    {
        c1\u0061ss.st\u0061tic(true);
    }
}
```

定义了一个名为“class”的类，该类具有一个名为“static”的静态方法，该方法接受一个名为“bool”的参数。请注意，由于关键字中不允许使用 Unicode 转义，因此标记“c1\u0061ss”是一个标识符，并且与“@class”是同一个标识符。

*以及示例*

如果两个标识符按顺序应用以下转换后完全相同，则认为它们是同一个标识符：

- 如果使用了前缀“@”，则将其移除。
- 每个 *Unicode_Escape_Sequence* 都会转换为其对应的 Unicode 字符。
- 移除任何 *Formatting_Characters*。

包含两个连续下划线字符（U+005F）的标识符保留给实现使用；但是，如果定义了此类标识符，则不要求进行诊断。

> *注意：* 例如，实现可能会提供以两个下划线开头的扩展关键字。*注意结束*

## 6.6.4 关键字

*关键字* 是一种类似标识符的字符序列，它是保留的，除非前面加上 @ 字符，否则不能用作标识符。

```text
keyword
       : 'abstract'  | 'as'        | 'base'       | 'bool'       | 'break'
       | 'byte'      | 'case'      | 'catch'      | 'char'       | 'checked'
       | 'class'     | 'const'     | 'continue'   | 'decimal'    | DEFAULT
       | 'delegate'  | 'do'        | 'double'     | 'else'       | 'enum'
       | 'event'     | 'explicit'  | 'extern'     | 'FALSE'      | 'finally'
       | 'fixed'     | 'float'     | 'for'        | 'foreach'    | 'goto'
       | 'if'        | 'implicit'  | 'in'         | 'int'        | 'interface'
       | 'internal'  | 'is'        | 'lock'       | 'long'       | 'namespace'
       | 'new'       | NULL        | 'object'     | 'operator'   | 'out'
       | 'override'  | 'params'    | 'private'    | 'protected'  | 'public'
       | 'readonly'  | 'ref'       | 'return'     | 'sbyte'      | 'sealed'
       | 'short'     | 'sizeof'    | 'stackalloc' | 'static'     | 'string'
| 'struct' | 'switch' | 'this' | 'throw' | TRUE
| 'try' | 'typeof' | 'uint' | 'ulong' | 'unchecked'
| 'unsafe' | 'ushort' | 'using' | 'virtual' | 'void'
| 'volatile' | 'while' |
;
```

**上下文关键字** 是一种类似标识符的字符序列，它在某些上下文中具有特殊含义，但不是保留的，并且可以在这些上下文之外以及前面加上 @ 字符时用作标识符。

```
contextual_keyword
: 'add' | 'alias' | 'ascending' | 'async' | 'await'
| 'by' | 'descending' | 'dynamic' | 'equals' | 'from'
| 'get' | 'global' | 'group' | 'into' | 'join'
| 'let' | 'nameof' | 'on' | 'orderby' | 'partial'
| 'remove' | 'select' | 'set' | 'value' | 'var'
| 'when' | 'where' | 'yield'
;
```

> *注意：* 规则 keyword 和 contextual_keyword 是解析器规则，因为它们不引入新的标记种类。所有关键字和上下文关键字都由隐式词法规则定义，因为它们在语法中以字面字符串形式出现（§6.2.3）。注意结束

在大多数情况下，上下文关键字的语法位置使其永远不会与普通标识符用法混淆。例如，在属性声明中，get 和 set 标识符具有特殊含义（§14.7.3）。在这些位置中，绝不允许使用 get 或 set 以外的标识符，因此这种用法不会与将这些词用作标识符的用法冲突。

在某些情况下，语法不足以区分上下文关键字用法与标识符。在所有此类情况下，将规定如何消除两者之间的歧义。例如，隐式类型局部变量声明（§12.6.2）中的上下文关键字 var 可能与名为 var 的已声明类型冲突，在这种情况下，已声明的名称优先于将该标识符用作上下文关键字。

另一个此类消歧示例是上下文关键字 await（§11.8.8.1），它仅在声明为 async 的方法内部被视为关键字，但可在其他地方用作标识符。

与关键字一样，上下文关键字可以通过在前面加上 @ 字符来用作普通标识符。

> *注意：* 当用作上下文关键字时，这些标识符不能包含 Unicode_Escape_Sequences。注意结束

## 6.4.5 字面量

### 6.4.5.1 概述

字面量（§11.7.2）是值的源代码表示形式。

```
literal
: boolean_literal
| integer_literal
| Real_literal
| Character_literal
| String_literal
| null_literal
;
```

> 注意：literal 是解析器规则，因为它对其他标记种类进行分组，并且不引入新的标记种类。注意结束

### 6.4.5.2 布尔字面量

有两个布尔字面量值：true 和 false。

```
boolean_literal
    : TRUE
    | FALSE
    ;
```

> 注意：boolean_literal 是解析器规则，因为它对其他标记种类进行分组，并且不引入新的标记种类。注意结束

boolean_literal 的类型是 bool。

### 6.4.5.3 整数字面量

整数字面量用于写入 int、uint、long 和 ulong 类型的值。整数字面量有两种可能的形式：十进制和十六进制。

```
Integer_Literal
    : Decimal_Integer_Literal
    | Hexadecimal_Integer_Literal
    ;

fragment Decimal_Integer_Literal
    : Decimal_Digit+ Integer_Type_Suffix?
    ;

fragment Decimal_Digit
    : '0'..'9'
    ;

fragment Integer_Type_Suffix
    : 'U' | 'u' | 'L' | 'l' | 'UL' | 'Ul' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
    ;

fragment Hexadecimal_Integer_Literal
    : ('0x' | '0X') Hex_Digit+ Integer_Type_Suffix?
    ;

fragment Hex_Digit
    : '0'..'9' | 'A'..'F' | 'a'..'f'
    ;
```

整数字面量的类型确定如下：

- 如果字面量没有后缀，则其类型为这些类型中第一个能够表示其值的类型：`int`、`uint`、`long`、`ulong`。
- 如果字面量带有 `U` 或 `u` 后缀，则其类型为这些类型中第一个能够表示其值的类型：`uint`、`ulong`。
- 如果字面量带有 `L` 或 `l` 后缀，则其类型为这些类型中第一个能够表示其值的类型：`long`、`ulong`。
- 如果字面量带有 `UL`、`Ul`、`uL`、`ul`、`LU`、`Lu`、`lU` 或 `lu` 后缀，则其类型为 `ulong`。

注意：因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、标度为 3 的十进制数。注意结束

如果指定字面量的量值太大，无法在指示的类型中表示，则会发生编译时错误。

注意：特别是，Real_Literal 绝不会产生浮点无穷大。但是，非零 Real_Literal 可能会舍入为零。注意结束

类型为 float 或 double 的实数字面量的值通过使用 IEC 60559“舍入到最接近”模式确定，平局打破为“偶数”（最低有效位为零的值），并且所有数字都被视为有效。

注意：在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，但 1.F 不是。注意结束

### 6.4.5.5 字符字面量

字符字面量表示单个字符，由引号中的字符组成，如 'a'。

```
Character_Literal
    : '\'' Character '\''
    ;

fragment Character
    : Single_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    ;

fragment Single_Character
    : ~['\\'\u000D\u000A\u0085\u2028\u2029]    // anything but ', \, and
New_Line_Character
    ;

fragment Simple_Escape_Sequence
    : '\\''' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' | '\\f' | '\\n' | '\\r' |
    '\\t' | '\\v'
    ;

fragment Hexadecimal_Escape_Sequence
    : '\\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
    ;
```

注意：在 Character 中，反斜杠字符（\）后面的字符必须是以下字符之一：'、"、\、0、a、b、f、n、r、t、u、U、x、v。否则，会发生编译时错误。注意结束

注意：使用 \x Hexadecimal_Escape_Sequence 产生式可能容易出错且难以阅读，因为 \x 后面的十六进制数字数量可变。例如，在以下代码中：
string good = "\x9Good text";
string bad = "\x9Bad text";
乍看之下，两个字符串中的前导字符可能相同（U+0009，制表符）。实际上，第二个字符串以 U+9BAD 开头，因为单词“Bad”中的所有三个字母都是有效的十六进制数字。作为风格问题，建议避免使用 \x，而改用特定转义序列（本例中为 \t）或固定长度的 \u 转义序列。

