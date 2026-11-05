

character-literal:
' character '

character:
single-character
simple-escape-sequence
hexadecimal-escape-sequence
unicode-escape-sequence

single-character:
除 ' (U+0027)、\ (U+005C) 和换行字符之外的任何字符

simple-escape-sequence: 以下之一
\' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence:
\x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt

string-literal:
regular-string-literal
verbatim-string-literal

regular-string-literal:
" regular-string-literal-characters_opt "

regular-string-literal-characters:
regular-string-literal-character
regular-string-literal-characters regular-string-literal-character

regular-string-literal-character:
single-regular-string-literal-character
simple-escape-sequence
hexadecimal-escape-sequence
unicode-escape-sequence

single-regular-string-literal-character:
除 " (U+0022)、\ (U+005C) 和换行字符之外的任何字符

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

## B.1.9 运算符和标点符号

operator-or-punctuator: 以下之一
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
>>

right-shift-assignment:
>>=

## B.1.10 预处理指令

pp-directive:
pp-declaration
pp-conditional
pp-line
pp-diagnostic
pp-region
pp-pragma

conditional-symbol:
除 true 或 false 之外的任何标识符或关键字

pp-expression:
whitespace_opt pp-or-expression whitespace_opt

pp-or-expression:
pp-and-expression
pp-or-expression whitespace_opt || whitespace_opt pp-and-expression

pp-and-expression:
pp-equality-expression
pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression

pp-equality-expression:
pp-unary-expression
pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression

pp-unary-expression:
pp-primary-expression
! whitespace_opt pp-unary-expression

pp-primary-expression:
true
false
conditional-symbol
( whitespace_opt pp-expression whitespace_opt )

pp-declaration:
whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

## C# 语言规范

```
pp-new-line:
    whitespace_opt single-line-comment_opt new-line

pp-conditional:
    pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line conditional-section_opt

pp-elif-sections:
    pp-elif-section
    pp-elif-sections pp-elif-section

pp-elif-section:
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line conditional-section_opt

pp-else-section:
    whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt

pp-endif:
    whitespace_opt # whitespace_opt endif pp-new-line

conditional-section:
    input-section
    skipped-section

skipped-section:
    skipped-section-part
    skipped-section skipped-section-part

skipped-section-part:
    skipped-characters_opt new-line
    pp-directive

skipped-characters:
    whitespace_opt not-number-sign input-characters_opt

not-number-sign:
    Any input-character except #

pp-diagnostic:
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message

pp-message:
    new-line
    whitespace input-characters_opt new-line

pp-region:
    pp-start-region conditional-section_opt pp-end-region

pp-start-region:
    whitespace_opt # whitespace_opt region pp-message

pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
file-name:
    " file-name-characters "
file-name-characters:
    file-name-character
    file-name-characters file-name-character
file-name-character:
    Any input-character except "
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
pragma-body:
    pragma-warning-body
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
warning-action:
    disable
    restore
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
```

## B.2 语法文法

### B.2.1 基本概念

```
namespace-name:
    namespace-or-type-name
type-name:
    namespace-or-type-name
namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member
```

### B.2.2 类型

```
type:
    value-type
    reference-type
    type-parameter
```

value-type:
  struct-type
  enum-type

struct-type:
  type-name
  simple-type
  nullable-type

simple-type:
  numeric-type
  bool

numeric-type:
  integral-type
  floating-point-type
  decimal

integral-type:
  sbyte
  byte
  short
  ushort
  int
  uint
  long
  ulong
  char

floating-point-type:
  float
  double

nullable-type:
  non-nullable-value-type ?

non-nullable-value-type:
  type

enum-type:
  type-name

reference-type:
  class-type
  interface-type
  array-type
  delegate-type

class-type:
  type-name
  object
  dynamic
  string

interface-type:
  type-name

```
rank-specifiers:
    rank-specifier
    rank-specifiers rank-specifier
rank-specifier:
    [ dim-separators_opt ]
dim-separators:
    ,
    dim-separators ,
delegate-type:
    type-name
type-argument-list:
    < type-arguments >
type-arguments:
    type-argument
    type-arguments , type-argument
type-argument:
    type
type-parameter:
    identifier
```

### B.2.3 变量

variable-reference:
    expression

### B.2.4 表达式

argument-list:
    argument
    argument-list , argument

argument:
    argument-name_opt argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference

primary-expression:
    primary-no-array-creation-expression
    array-creation-expression

primary-no-array-creation-expression:
literal
simple-name
parenthesized-expression
member-access
invocation-expression
element-access
this-access
base-access
post-increment-expression
post-decrement-expression
object-creation-expression
delegate-creation-expression
anonymous-object-creation-expression
typeof-expression
checked-expression
unchecked-expression
default-value-expression
anonymous-method-expression
simple-name:
identifier type-argument-list_opt
parenthesized-expression:
( expression )
member-access:
primary-expression . identifier type-argument-list_opt
predefined-type . identifier type-argument-list_opt
qualified-alias-member . identifier
predefined-type: 以下之一
bool byte char decimal double float int long
object sbyte short string uint ulong ushort
invocation-expression:
primary-expression ( argument-list_opt )
element-access:
primary-no-array-creation-expression [ argument-list ]
this-access:
this
base-access:
base . identifier
base [ argument-list ]
post-increment-expression:
primary-expression ++
post-decrement-expression:
primary-expression --
object-creation-expression:
new type ( argument-list_opt ) object-or-collection-initializer_opt
new type object-or-collection-initializer

object-or-collection-initializer:
    object-initializer
    collection-initializer
object-initializer:
    { member-initializer-list_opt }
    { member-initializer-list , }
member-initializer-list:
    member-initializer
    member-initializer-list , member-initializer
member-initializer:
    identifier = initializer-value
initializer-value:
    expression
    object-or-collection-initializer
collection-initializer:
    { element-initializer-list }
    { element-initializer-list , }
element-initializer-list:
    element-initializer
    element-initializer-list , element-initializer
element-initializer:
    non-assignment-expression
    { expression-list }
expression-list:
    expression
    expression-list , expression
array-creation-expression:
    new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
    new array-type array-initializer
    new rank-specifier array-initializer
delegate-creation-expression:
    new delegate-type ( expression )
anonymous-object-creation-expression:
    new anonymous-object-initializer
anonymous-object-initializer:
    { member-declarator-list_opt }
    { member-declarator-list , }
member-declarator-list:
    member-declarator
    member-declarator-list , member-declarator
member-declarator:
    simple-name
    member-access
    identifier = expression

