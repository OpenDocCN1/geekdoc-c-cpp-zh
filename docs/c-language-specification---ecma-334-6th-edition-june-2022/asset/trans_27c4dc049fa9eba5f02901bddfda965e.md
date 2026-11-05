
// Source: $6.4.5.1 通用
literal
  : boolean_literal
  | Integer_Literal
  | Real_Literal
  | Character_Literal
  | String_Literal
  | null_literal
  ;

// Source: $6.4.5.2 布尔字面量
boolean_literal
  : TRUE
  | FALSE
  ;

// Source: $6.4.5.3 整数字面量
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

// Source: $6.4.5.4 实数字面量
Real_Literal
  : Decimal_Digit+ '.' Decimal_Digit+ Exponent_Part? Real_Type_Suffix?
  | '.' Decimal_Digit+ Exponent_Part? Real_Type_Suffix?
  | Decimal_Digit+ Exponent_Part Real_Type_Suffix?
  | Decimal_Digit+ Real_Type_Suffix
  ;

fragment Exponent_Part
  : ('e' | 'E') Sign? Decimal_Digit+
  ;

fragment Sign
  : '+' | '-'
  ;

fragment Real_Type_Suffix
  : 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
  ;

// Source: §6.4.5.5 字符字面量
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
  : -['\'\u000D\u000A\u0005\u2028\u2029]    // 除了 ', \, 和 New_Line_Character 之外的任何内容
  ;

fragment Simple_Escape_Sequence
  : '\\'' | '\"' | '\\' | '\0' | '\a' | '\b' | '\f' | '\n' | '\r' | '\t' | '\v'
  ;

fragment Hexadecimal_Escape_Sequence
  : '\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
  ;

// Source: §6.4.5.6 字符串字面量
String_Literal
  : Regular_String_Literal
  | Verbatim_String_Literal
  ;

fragment Regular_String_Literal
  : '"' Regular_String_Literal_Character* '"'
  ;

fragment Regular_String_Literal_Character
  : Single_Regular_String_Literal_Character
  | Simple_Escape_Sequence
  | Hexadecimal_Escape_Sequence
  | Unicode_Escape_Sequence
  ;

fragment Single_Regular_String_Literal_Character
  : -['"\u000D\u000A\u0005\u2028\u2029]    // 除了 ", \, 和 New_Line_Character 之外的任何内容
  ;

fragment Verbatim_String_Literal
    : @" Verbatim_String_Literal_Character* "
    ;

fragment Verbatim_String_Literal_Character
    : Single_Verbatim_String_Literal_Character
    | Quote_Escape_Sequence
    ;

fragment Single_Verbatim_String_Literal_Character
    : ~[""]   // 除了引号 (U+0022) 之外的任何内容
    ;

fragment Quote_Escape_Sequence
    : '""'
    ;

// Source: $6.4.5.7 空字面量
null_literal
    : NULL
    ;

// Source: $6.4.6 运算符和标点符号
operator_or_punctuator
    : '{' | '}' | '[' | ']' | '(' | ')' | '.' | ',' | ':' | ';' | '?' | '~'
    | '+' | '-' | ASTERISK | SLASH | '%' | '&' | '|' | '^' | '!' | '~'
    | '=' | '<' | '>' | '?' | '??' | '::' | '++' | '--' | '&&' | '||' | '~?'
    | '=>' | '==' | '!=' | '<=' | '>=' | '+=' | '-=' | '*=' | '/=' | '%='
    | '&=' | '|=' | '^=' | '<<' | '<<=' | '=>'
    ;

right_shift
    : '>' '>'
    ;

right_shift_assignment
    : '>>='
    ;

// Source: $6.5.1 通用
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

// 仅在行首识别
fragment PP_Start
: { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace? // 请参阅下文注释
;

fragment PP_Whitespace
: [ \p{Zs} ] // 具有 Unicode 类别 Zs 的任何字符
| '\\u0009' // 水平制表符
| '\\u000C' // 换页符
)+
;

fragment PP_New_Line
: PP_Whitespace? Single_Line_Comment? New_Line
;

// Source: $6.5.2 条件编译符号
fragment PP_Conditional_Symbol
: Basic_Identifier // 必须不等于标记 TRUE 或 FALSE，请参阅下文注释
;

// Source: $6.5.3 预处理表达式
fragment PP_Expression
: PP_Whitespace? PP_Or_Expression PP_Whitespace?
;

fragment PP_Or_Expression
: PP_And_Expression (PP_Whitespace? '||' PP_Whitespace? PP_And_Expression)*
;

fragment PP_And_Expression
: PP_Equality_Expression (PP_Whitespace? '&&' PP_Whitespace?
PP_Equality_Expression)*
;

fragment PP_Equality_Expression
: PP_Unary_Expression (PP_Whitespace? ('==' | '!=') PP_Whitespace?
PP_Unary_Expression)*
;

fragment PP_Unary_Expression
: PP_Primary_Expression
| '!' PP_Whitespace? PP_Unary_Expression
;

fragment PP_Primary_Expression
: TRUE
| FALSE
| PP_Conditional_Symbol
| '(' PP_Whitespace? PP_Expression PP_Whitespace? ')'
;

// Source: $6.5.4 定义指令
fragment PP_Declaration
: 'define' PP_Whitespace PP_Conditional_Symbol
| 'undef' PP_Whitespace PP_Conditional_Symbol
;

// Source: $6.5.5 条件编译指令
fragment PP_Conditional
  : PP_If_Section
  | PP_Elif_Section
  | PP_Else_Section
  | PP_Endif
  ;

fragment PP_If_Section
  : 'if' PP_Whitespace PP_Expression
  ;

fragment PP_Elif_Section
  : 'elif' PP_Whitespace PP_Expression
  ;

fragment PP_Else_Section
  : 'else'
  ;

fragment PP_Endif
  : 'endif'
  ;

// Source: $6.5.6 诊断指令
fragment PP_Diagnostic
  : 'error' PP_Message?
  | 'warning' PP_Message?
  ;

fragment PP_Message
  : PP_Whitespace Input_Character*
  ;

// Source: $6.5.7 区域指令
fragment PP_Region
  : PP_Start_Region
  | PP_End_Region
  ;

fragment PP_Start_Region
  : 'region' PP_Message?
  ;

fragment PP_End_Region
  : 'endregion' PP_Message?
  ;

// Source: $6.5.8 行指令
fragment PP_Line
  : 'line' PP_Whitespace PP_Line_Indicator
;

fragment PP_Line_Indicator
    : Decimal_Digit+ PP_Whitespace PP_Compilation_Unit_Name
    | Decimal_Digit+
    | DEFAULT
    | 'hidden'
    ;

fragment PP_Compilation_Unit_Name
    : '"' PP_Compilation_Unit_Name_Character+ '"'
    ;

fragment PP_Compilation_Unit_Name_Character
    // 除了 " 之外的任何 Input_Character
    : ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029' | '#')
    ;

// Source: §6.5.9 pragma 指令
fragment PP_Pragma
    : 'pragma' PP_Pragma_Text?
    ;

fragment PP_Pragma_Text
    : PP_Whitespace Input_Character*
    ;

## A.3 语法

// Source: §7.8.1 通用
namespace_name
    : namespace_or_type_name
    ;

type_name
    : namespace_or_type_name
    ;

namespace_or_type_name
    : identifier type_argument_list?
    | namespace_or_type_name '.' identifier type_argument_list?
    | qualified_alias_member
    ;

// Source: §8.1 通用
type
    : reference_type
    | value_type
    | type_parameter
    | pointer_type     // 不安全代码支持
    ;

// Source: §8.2.1 通用
reference_type
    : class_type
    | interface_type
    | array_type
    | delegate_type
    | 'dynamic'
    ;

class_type
    : type_name
    | 'object'
    | 'string'
    ;

interface_type
    : type_name
    ;

array_type
    : non_array_type rank_specifier+
    ;

non_array_type
    : value_type
    | class_type
    | interface_type
    | delegate_type
    | 'dynamic'
    | type_parameter
    | pointer_type      // 不安全代码支持
    ;

rank_specifier
    : '[' ','* ']'
    ;

delegate_type
    : type_name
    ;

// Source: §8.3.1 通用
value_type
    : non_nullable_value_type
    | nullable_value_type
    ;

non_nullable_value_type
    : struct_type
    | enum_type
    ;

struct_type
    : type_name
    | simple_type
    ;

simple_type
  : numeric_type
  | 'bool'
  ;

numeric_type
  : integral_type
  | floating_point_type
  | 'decimal'
  ;

integral_type
  : 'sbyte'
  | 'byte'
  | 'short'
  | 'ushort'
  | 'int'
  | 'uint'
  | 'long'
  | 'ulong'
  | 'char'
  ;

floating_point_type
  : 'float'
  | 'double'
  ;

enum_type
  : type_name
  ;

nullable_value_type
  : non_nullable_value_type '?'
  ;

// Source: §8.4.2 类型参数
type_argument_list
  : '<' type_arguments '>'
  ;

type_arguments
  : type_argument (',' type_argument)*
  ;

type_argument
  : type
  ;

// Source: §8.5 类型参数
type_parameter
  : identifier
  ;

// Source: §8.8 非托管类型
