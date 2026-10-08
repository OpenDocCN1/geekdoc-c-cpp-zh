
```
=         =      |      >>    >=    <=    !=

  <=         |      ||       --       >

  and and_eq bitand bitor compl not not_eq ->

  or_eq xor      or_eq
```

```
literal:
integer-literal
character-literal
floating-literal
string-literal
boolean-literal
pointer-literal
user-defined-literal

integer-literal:
binary-literal integer-suffix_opt
octal-literal integer-suffix_opt
decimal-literal integer-suffix_opt
hexadecimal-literal integer-suffix_opt

binary-literal:
0b binary-digit
0 binary-digit
binary-literal 'opt binary-digit

octal-literal:
0
octal-literal 'opt octal-digit

decimal-literal:
nonzero-digit
decimal-literal 'opt digit

hexadecimal-literal:
0x hexadecimal-digit
0X hexadecimal-digit
hexadecimal-literal 'opt hexadecimal-digit

binary-digit:
0
1

octal-digit: one of
0 1 2 3 4 5 6 7

nonzero-digit: one of
1 2 3 4 5 6 7 8 9

hexadecimal-digit: one of
0 1 2 3 4 5 6 7 8 9
a b c d e f A B C D E F

integer-suffix:
unsigned-suffix long-suffix_opt
long-suffix unsigned-suffix

unsigned-suffix: one of
u
long-suffix: one of
1 L
long-long-suffix: one of
1 LL

character-literal:
encoding-prefix<opt> c-char-sequence
encoding-prefix<opt>: one of
u L
c-char-sequence:
c-char
c-char-sequence s-char
c-char:
源字符集中任何成员，但双引号 '"'、反斜杠 '\' 或换行符
escape-sequence
universal-character-name
escape-sequence:
simple-escape-sequence
octal-escape-sequence
hexadecimal-escape-sequence: one of
\x hexadecimal-digit

octal-escape-sequence:
\ octal-digit
octal-digit
hexadecimal-escape-sequence:
\ octal-digit
octal-digit

floating-literal:
fractional-constant exponent-part<opt> floating-suffix<opt>
fractional-constant:
digit-sequence<opt> digit-sequence
exponent-part:
sign<opt> digit-sequence
sign: one of
+
digit-sequence:
digit
digit-sequence <opt> digit
floating-suffix: one of
f L
string-literal:
encoding-prefix<opt> s-char-sequence<opt>
encoding-prefix<opt> raw-string

s-char-sequence:
s-char
c-char-sequence s-char
c-char:
源字符集中任何成员，但双引号 '"'、反斜杠 '\' 或换行符
escape-sequence
universal-character-name
raw-string:
* d-char-sequence-opt ( r-char-sequence-opt ) d-char-opt
r-sequence:
c-char
c-char-sequence
c-char:
源字符集中任何成员，但空格、左括号 (、右括号 ) 以及反斜杠 \
d-char-sequence:
c-char
c-char:
源字符集中任何成员，但空格、左括号 (、右括号 ) 以及反斜杠 \ 控制字符表示水平制表符、垂直制表符、换行符
boolean-literal:
false
true
pointer-literal:
nullptr
user-defined-literal:
user-defined-integer-literal
user-defined-floating-literal
user-defined-string-literal
user-defined-integer-literal:
decimal-literal ud-suffix
octal-literal ud-suffix
hexadecimal-literal ud-suffix
binary-literal ud-suffix
user-defined-floating-literal:
fractional-constant exponent-part_opt ud-suffix
digit-sequence exponent-part ud-suffix
user-defined-string-literal:
string-literal ud-suffix
user-defined-character-literal:
```

## A.3 基本概念
`translation-unit`: `declaration-seq_opt`

## A.4 表达式

`primary-expression`: `literal` `this` `(` `expression` `)` `id-expression` `fold-expression`
`id-expression`: `unqualified-id`
`qualified-id`: `identifier` `operator-function-id` `conversion-function-id` `class-name` `dectype-specifier` `template-id`
`qualified-id`: `nested-name-specifier` `template_opt` `unqualified-id`
`nested-name-specifier`: `::` `type-name` `::` `dectype-specifier` `::` `nested-name-specifier` `template_opt` `simple-template-id`
`lambda-expression`: `lambda-introducer` `lambda-declarator_opt` `compound-statement`
`lambda-introducer`: `[` `lambda-capture_opt` `]`
`lambda-capture`: `capture-default` `capture-list` `capture-default` , `capture-list`
`capture-default`: `&`
`capture-list`: `capture` `...opt` `capture-list` , `capture` `...opt`
`capture`: `simple-capture` `init-capture`
`simple-capture`: `identifier` `&` `this`

```
init-capture:

  identifier initializer

  & identifier initializer

lambda-declarator:

  ( parameter-declaration-clause ) mutable-opt

  exception-specification-opt attribute-specifier-seq-opt trailing-return-type-opt

fold-expression:

  ( cast-expression fold-operator . . )

  ( ... fold-operator cast-expression )

  ( cast-expression fold-operator . . . fold-operator cast-expression )

fold-operator: one of

  + * / % | << >>

  += -= != * *= &= = << >> && =

  = = ! < >= == && || , * -

postfix-expression:

  primary-expression

  postfix-expression [ expression ]

  postfix-expression [ braced-list ]

  postfix-expression [ expression-list-opt ]

  simple-type-specifier ( expression-list-opt )

  typename-specifier ( expression-list-opt )

  typename-specifier braced-list

  postfix-expression . template-opt id-expression

postfix-expression -> template-opt id-expression

postfix-expression . pseudo-destructor-name

postfix-expression -> pseudo-destructor-name

postfix-expression ++

postfix-expression --

  dynamic cast < type-id > ( expression )

  static_cast < type-id > ( expression )

  reinterpret_cast < type-id > ( expression )

  const_cast < type-id > ( expression )

type-id ( expression )

type-id ( type-id )

expression-list:

  initializer-list

pseudo-destructor-name:

  nested-name-specifier-opt type-name ::= type-name

  nested-name-specifier template simple-template-id ::= type-name

  - type-name

  - decltype-specifier

unary-expression:

  postfix-expression

  ++ cast-expression

  -- cast-expression

  unary-operator cast-expression

  sizeof unary-expression

  sizeof ( type-id )

  sizeof . . ( identifier )

  aligned ( type-id )

  noexcept-expression

new-expression

  delete-expression
```

# ISO/IEC N4296

一元运算符：以下之一
* `&` `+` `-` `~`

新表达式（new）：
```
::opt_opt new-placement_opt new-type new-initializer_opt

  ::opt_opt new-placement_opt ( type-id ) new-initializer_opt
```
`new-placement`:
  `(` `expression-list` `)`
`new-type-id`:
  `type-specifier-seq` `new-declarator_opt`
`new-declarator`:
  `ptr-operator` `new-declarator_opt`
  `nptr-new-declarator`
`ptr-new-declarator`:
  `[` `attribute-specifier-seq_opt`
  `nptr-new-declarator` `[` `constant-expression` `]` `attribute-specifier-seq_opt`
`new-initializer`:
  `(` `expression-list` `)`
  `brace-init-list`
`delete`表达式:
  `::opt_delete` `cast-expression`
  `::opt_delete` `[` `]` `cast-expression`
`noexcept`:
  `noexcept` `(` `expression` `)`
转换表达式:
  `unary-expression`
  `(` `type-id` `)` `cast-expression`
`pm`表达式:
  `cast-expression`
  `pm-expression` `*` `cast-expression`
  `pm-expression` `->*` `cast-expression`
乘法表达式:
  `pm-expression`
  `multiplicative-expression` `*` `pm-expression`
  `multiplicative-expression` `/` `pm-expression`
  `multiplicative-expression` `%` `pm-expression`
加法表达式:
  `multiplicative-expression`
  `additive-expression` `+` `multiplicative-expression`
  `additive-expression` `-` `multiplicative-expression`
移位表达式:
  `additive-expression`
  `shift-expression` `<<` `additive-expression`
  `shift-expression` `>>` `additive-expression`
关系表达式:
  `shift-expression`
  `relational-expression` `<` `shift-expression`
  `relational-expression` `>` `shift-expression`
  `relational-expression` `<=` `shift-expression`
  `relational-expression` `>=` `shift-expression`
相等表达式:
  `relational-expression`
  `equality-expression` `==` `relational-expression`
  `equality-expression` `!=` `relational-expression`
```
与表达式:

equality-expression

and-expression & equality-expression

异或表达式:

and-expression

exclusive-or-expression * and exclusive-or-expression

包含或表达式:

exclusive-or-expression

inclusive-or-expression | exclusive-or-expression

逻辑与表达式:

inclusive-or-expression

logical-and-expression & inclusive-or-expression

逻辑或表达式:

logical-and-expression

logical-or-expression | logical-or-expression

条件表达式:

logical-or-expression

logical-or-expression ? expression : assignment-expression

throw表达式:

throw assignment-expression_opt

赋值表达式:

conditional-expression

logical-or-expression operator initializer-clause

throw-expression

赋值运算符：以下之一

* = % / = - = >> << &= =

表达式:

assignment-expression

expression , assignment-expression
```

# A.5 语句 (Statements)

语句:
`labelled-statement`
`attribute-specifier-seq_opt` `expression-statement`
`attribute-specifier-seq_opt` `compound-statement`
`attribute-specifier-seq_opt` `selection-statement`
`attribute-specifier-seq_opt` `iteration-statement`
`attribute-specifier-seq_opt` `jump-statement`
`declaration-statement`
`attribute-specifier-seq_opt` `try-block`

标签语句:
`attribute-specifier-seq_opt` `identifier` : `statement`
