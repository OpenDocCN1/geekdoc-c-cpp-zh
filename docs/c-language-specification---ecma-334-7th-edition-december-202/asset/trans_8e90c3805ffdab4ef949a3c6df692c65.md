

```
long* p6 = stackalloc[] { 11, 12L, 13 };
// Converts all and returns long*
long* p7 = stackalloc long[] { 11, 12, 13 };
}
```

*示例结束*

与访问数组或 Span<T> 类型的 stackalloc 分配块不同，访问指针类型的 stackalloc 分配块的元素是不安全操作，并且不会进行范围检查。

示例：在以下代码中

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {
            return "-2147483648";
        }
        int n = value >= 0 ? value : -value;
        unsafe
        {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do
            {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0)
            {
                *--p = '-';
            }
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }
    static void Main()
    {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

在 IntToString 方法中使用 stackalloc 表达式在栈上分配一个 16 字符的缓冲区。方法返回时，该缓冲区会被自动丢弃。

但请注意，IntToString 可以在安全模式下重写；也就是说，不使用指针，如下所示：

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {
            return "-2147483648";
        }
        int n = value >= 0 ? value : -value;
        Span<char> buffer = stackalloc char[16];
        int idx = 16;
        do
        {
            buffer[--idx] = (char)(n % 10 + '0');
            n /= 10;
        } while (n != 0);
        if (value < 0)
        {
            buffer[--idx] = '-';
        }
        return buffer.Slice(idx).ToString();
    }
}
```

*示例结束*

**条件规范性文本结束。**

## A. 语法

本条款为资料性内容。

### A.1 总则

本附录包含规范中出现的语法产生式，包括用于不安全代码的可选产生式。产生式在此处出现的顺序与它们在规范中出现的顺序相同。

### A.2 词法语法

```
// Source: $6.3.1 General
DEFAULT  : 'default' ;
NULL     : 'null' ;
TRUE     : 'true' ;
FALSE    : 'false' ;
ASTERISK : '*' ;
SLASH    : '/' ;

// Source: $6.3.1 General
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

// Source: $6.3.2 Line terminators
New_Line
  : New_Line Character
  | '\u000D\u000A'  // carriage return, line feed
  ;

// Source: $6.3.3 Comments
Comment
  : Single_Line_Comment
  | Delimited_Comment
;
fragment Single_Line_Comment
  : '//' Input_Character*
  ;

fragment Input_Character
  // anything but New_Line_Character
  : ~('\\u000D' | '\\u000A' | '\\u0085' | '\\u2028' | '\\u2029')
  ;

fragment New_Line_Character
  : '\\u000D' // carriage return
  | '\\u000A' // line feed
  | '\\u0085' // next line
  | '\\u2028' // line separator
  | '\\u2029' // paragraph separator
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

// Source: $6.3.4 White space
Whitespace
  : [p{Zs}] // any character with Unicode class Zs
  | '\\u0009' // horizontal tab
  | '\\u000B' // vertical tab
  | '\\u000C' // form feed
  ;

// Source: $6.4.1 General
token
  : identifier
  | keyword
  | Integer_Literal
  | Real_Literal
  | Character_Literal
  | String_Literal
  | operator_or_punctuator
  ;

// Source: $6.4.2 Unicode character escape sequences
fragment Unicode_Escape_Sequence
  : '\\u' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
  | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
  | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
;

 // Source: §6.4.3 Identifiers
identifier
  : Simple_Identifier
  | contextual_keyword
  ;

Simple_Identifier
  : Available_Identifier
  | Escaped_Identifier
  ;

fragment Available_Identifier
  // excluding keywords or contextual keywords, see note below
  : Basic_Identifier
  ;

fragment Escaped_Identifier
  // Includes keywords and contextual keywords prefixed by '@'.
  // See note below.
  : '@' Basic_Identifier
  ;

fragment Basic_Identifier
  : Identifier_Start_Character Identifier_Part_Character*
  ;

fragment Identifier_Start_Character
  : Letter_Character
  | Underscore_Character
  ;

fragment Underscore_Character
  : '_'  // underscore
  | '\\u005f' // Unicode_Escape_Sequence for underscore
  ;

fragment Identifier_Part_Character
  : Letter_Character
  | Decimal_Digit_Character
  | Connecting_Character
  | Combining_Character
  | Formatting_Character
  ;

fragment Letter_Character
  // Category Letter, all subcategories; category Number, subcategory letter.
  // [\\p{L}\\p{Nl}]
  // Only escapes for categories L & Nl allowed. See note below.
  | Unicode_Escape_Sequence
  ;

fragment Combining_Character
// Category Mark, subcategories non-spacing and spacing combining.
: [\p{Mn}\p{Mc}]
// Only escapes for categories Mn & Mc allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Decimal_Digit_Character
// Category Number, subcategory decimal digit.
: [\p{Nd}]
// Only escapes for category Nd allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Connecting_Character
// Category Punctuation, subcategory connector.
: [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Formatting_Character
// Category Other, subcategory format.
: [\p{Cf}]
// Only escapes for category Cf allowed, see note below.
| Unicode_Escape_Sequence
;

// Source: $6.4.4 Keywords
keyword
: 'abstract' | 'as' | 'base' | 'bool' | 'break'
| 'byte' | 'case' | 'catch' | 'char' | 'checked'
| 'class' | 'const' | 'continue' | 'decimal' | DEFAULT
| 'delegate' | 'do' | 'double' | 'else' | 'enum'
| 'event' | 'explicit' | 'extern' | FALSE | 'finally'
| 'fixed' | 'float' | 'for' | 'foreach' | 'goto'
| 'if' | 'implicit' | 'in' | 'int' | 'interface'
| 'internal' | 'is' | 'lock' | 'long' | 'namespace'
| 'new' | NULL | 'object' | 'operator' | 'out'
| 'override' | 'params' | 'private' | 'protected' | 'public'
| 'readonly' | 'ref' | 'return' | 'sbyte' | 'sealed'
| 'short' | 'sizeof' | 'stackalloc' | 'static' | 'string'
| 'struct' | 'switch' | 'this' | 'throw' | TRUE
| 'try' | 'typeof' | 'uint' | 'ulong' | 'unchecked'
| 'unsafe' | 'ushort' | 'using' | 'virtual' | 'void'
| 'volatile' | 'while'
;

// Source: $6.4.4 Keywords
contextual_keyword
: 'add' | 'alias' | 'ascending' | 'async' | 'await'
| 'by' | 'descending' | 'dynamic' | 'equals' | 'from'
| 'get' | 'global' | 'group' | 'into' | 'join'
| 'let' | 'nameof' | 'on' | 'orderby' | 'partial'
| 'remove' | 'select' | 'set' | 'unmanaged' | 'value'
| 'var' | 'when' | 'where' | 'yield'
;
 // Source: $6.4.5.1 General
literal
  : boolean_literal
  | Integer_literal
  | Real_Literal
  | Character_Literal
  | String_Literal
  | null_literal
;

// Source: $6.4.5.2 Boolean literals
boolean_literal
  : TRUE
  | FALSE
;

// Source: $6.4.5.3 Integer literals
Integer_Literal
  : Decimal_Integer_Literal
  | Hexadecimal_Integer_Literal
  | Binary_Integer_Literal
;

fragment Decimal_Integer_Literal
  : Decimal_Digit Decorated_Decimal_Digit* Integer_Type_Suffix?
;

fragment Decorated_Decimal_Digit
  : '_' * Decimal_Digit
;

fragment Decimal_Digit
  : '0'..'9'
;

fragment Integer_Type_Suffix
  : 'U' | 'u' | 'L' | 'l' |
  'UL' | 'UI' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
;

fragment Hexadecimal_Integer_Literal
  : ('0x' | '0X') Decorated_Hex_Digit+ Integer_Type_Suffix?
;

fragment Decorated_Hex_Digit
  : '_' * Hex_Digit
;

fragment Hex_Digit
  : '0'..'9' | 'A'..'F' | 'a'..'f'
;

fragment Binary_Integer_Literal

