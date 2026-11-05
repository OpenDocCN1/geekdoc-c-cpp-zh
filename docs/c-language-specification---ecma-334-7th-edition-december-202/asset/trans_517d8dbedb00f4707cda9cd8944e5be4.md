
示例结束

如果某个标记序列在上下文中可以被解析为以 *类型实参列表*（§8.4.2）结尾的 *简单名称*（§12.8.4）、*成员访问*（§12.8.7）或 *指针成员访问*（§23.6.3），则需要检查紧跟闭合 > 标记之后的标记，看它是否是：

-   属于 ( ) ] } : ; , . ? == != | ^ && || & [ ; 之一；或
-   属于关系运算符 < > <= >= is as 之一；或
-   出现在查询表达式中的上下文查询关键字；或
-   在某些上下文中，*标识符* 被视为消歧标记。这些上下文是指：被消歧的标记序列紧接在关键字 is、case 或 out 之一的前面，或者在解析元组字面量的第一个元素时出现（此时该标记序列前面是 ( 或 :，且标识符后面跟有 ,），或者在解析元组字面量的后续元素时出现。

如果后续标记位于此列表中，或是处于此类上下文中的标识符，则 *类型实参列表* 会保留为 *简单名称*、*成员访问* 或 *指针成员访问* 的一部分，并且该标记序列的任何其他可能解析都将被丢弃。否则，即使该标记序列没有其他可能的解析，*类型实参列表* 也不会被视为 *简单名称*、*成员访问* 或 *指针成员访问* 的一部分。（这些规则不适用于在 *命名空间或类型名称*（§7.8）中解析 *类型实参列表* 的情况。）

> 注意：这些规则不适用于在 *命名空间或类型名称*（§7.8）中解析 *类型实参列表* 的情况。注意结束

示例：以下语句：

```
    F(G<A, B>(7));
```

根据此规则，这将被解释为对 F 的一次调用，调用带一个参数，该参数是对泛型方法 G 的一次调用，其中 G 有两个类型实参和一个常规实参。以下语句：

```
    F(G<A, B>7);
    F(G<A, B>>7);
```

将各自被解释为对 F 的调用，且带有两个参数。以下语句：

```
    x = F<A> + y;
```

将被解释为小于运算符、大于运算符和一元加运算符，就好像该语句写作 x = (F < A) > (+y) 一样，而不是将其解释为带有 *类型实参列表* 后跟二元加运算符的 *简单名称*。在以下语句：

```
    x = y is C<T> && z;
```

中，由于 *类型实参列表* 后存在消歧标记 &&，标记 C<T> 被解释为带有 *类型实参列表* 的 *命名空间或类型名称*。

表达式 (A < B, C > D) 是一个含有两个元素的元组，每个元素都是一个比较表达式。

表达式 (A<B,C> D, E) 是一个含有两个元素的元组，其中第一个元素是声明表达式。

调用 M(A < B, C > D, E) 有三个实参。

调用 M(out A<B,C> D, E) 有两个实参，第一个实参是一个 out 声明。

表达式 e is A<B> C 使用的是声明模式。

case 标签 case A<B> C: 使用的是声明模式。

*示例结束*

关系表达式（§12.12.1）可以具有“relational_expression is type”或“relational_expression is constant_pattern”的形式，二者都可能是限定标识符的有效解析。在这种情况下，会尝试将其作为类型（§7.8.1）进行绑定；然而，如果该尝试失败，则将其作为表达式绑定，并且结果必须是常量。

## 6.3 词法分析

### 6.3.1 概述

为方便起见，词法文法定义并引用了以下命名的词法标记：

```
DEFAULT   : 'default' ;
NULL      : 'null' ;
TRUE      : 'true' ;
FALSE     : 'false' ;
ASTERISK  : '*' ;
SLASH     : '/' ;
```

尽管这些是词法规则，但这些名称全部使用大写字母拼写，以便与普通词法规则名称区分开来。

*注意：这些便利规则是对通常不为由字面量字符串定义的标记提供显式标记名称这一惯例的例外。注意结束*

*输入* 产生式定义了 C# 编译单元的词法结构。

```
input
    : input_section?
    ;

input_section
    : input_section_part+
    ;

input_section_part
    : input_element* New_Line
    | PP_Directive
    ;

input_element
    : Whitespace
    | Comment
    | token
    ;
```

*注意：上述文法由 ANTLR 解析规则描述，它定义的是 C# 编译单元的词法结构，而非词法标记。注意结束*

五个基本元素构成了 C# 编译单元的词法结构：行终止符（§6.3.2）、空白（§6.3.4）、注释（§6.3.3）、标记（§6.4）和预处理指令（§6.5）。在这些基本元素中，只有标记在 C# 程序的语法文法（§6.2.4）中是重要的。

C# 编译单元的词法处理包括将文件缩减为标记序列，该序列成为语法分析的输入。行终止符、空白和注释可用于分隔标记，预处理指令可能导致编译单元的某些部分被跳过，但除此之外，这些词法元素对 C# 程序的语法结构没有影响。

当多个词法文法产生式与编译单元中的某个字符序列匹配时，词法处理总是形成最长的可能词法元素。

示例：字符序列 // 被处理为单行注释的开始，因为该词法元素比单个 / 标记更长。示例结束

某些标记由一组词法规则定义：一条主规则和一条或多条子规则。后者在文法中用 fragment 标记，以指示该规则定义了另一个标记的一部分。片段规则在词法规则的自上而下排序中不被考虑。

注意：在 ANTLR 中，fragment 是一个关键字，其行为与本处定义的行为相同。注意结束

### 6.3.2 行终止符

行终止符将 C# 编译单元的字符划分为行。

```
New_Line
  : New_Line_Character
  | '\u000D\u000A'  // carriage return, line feed
  ;
```

为了与添加文件结束标记的源代码编辑工具兼容，并使编译单元能够被视为一系列正确终止的行，对 C# 程序中的每个编译单元按顺序应用以下变换：

- 如果编译单元的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果编译单元非空，且最后一个字符不是回车符（U+000D）、换行符（U+000A）、下一行字符（U+0085）、行分隔符（U+2028）或段落分隔符（U+2029），则在编译单元末尾添加一个回车符（U+000D）。

注意：额外的回车符允许程序以没有终止换行符的 PP_Directive（§6.5）结束。注意结束

### 6.3.3 注释

支持两种形式的注释：分隔注释和单行注释。

分隔注释以字符 /* 开头，以字符 */ 结束。分隔注释可以占据一行的一部分、整行或多行。

示例：以下示例：

```
/* Hello, world program
   This program writes "hello, world" to the console
*/
class Hello
{
    static void Main()
    {
        System.Console.WriteLine("hello, world");
    }
}
```

包含一个分隔注释。

示例结束

单行注释以字符 // 开头，并延伸到该行末尾。

示例：以下示例：

```
// Hello, world program
// This program writes "hello, world" to the console
//
//
class Hello // any name will do for this class
{
    static void Main() // this method must be named "Main"
    {
        System.Console.WriteLine("hello, world");
    }
}
```

展示了多个单行注释。

示例结束

```
Comment
  : Single_Line_Comment
  | Delimited_Comment
  ;

fragment Single_Line_Comment
  : '//' Input_Character*
  ;

fragment Input_Character
  // anything but New_Line_Character
  : ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029')
  ;

fragment New_Line_Character
  : '\u000D' // carriage return
  | '\u000A' // line feed
  | '\u0085' // next line
  | '\u2028' // line separator
  | '\u2029' // paragraph separator
  ;

fragment Delimited_Comment
  : '/*' Delimited_Comment_Section* ASTERISK+ '/'
  ;

fragment Delimited_Comment_Section
  : SLASH
  | ASTERISK* Not_Slash_Or_Asterisk
  ;

fragment Not_Slash_Or_Asterisk
  : ~('/' | '*')  // Any except SLASH or ASTERISK
  ;
```

