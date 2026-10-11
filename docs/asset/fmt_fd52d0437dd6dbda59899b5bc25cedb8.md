
# ISO/IEC 14882:2017(E)

``` 
hexadecimal-floating-literal:
hexadecimal-prefix hexadecimal-fractional-constant binary-exponent-part suffix-opt
hexadecimal-prefix hexadecimal-digit-sequence binary-exponent-part suffix-opt

fractional-constant:
digit-sequence-opt . digit-sequence
digit-sequence

hexadecimal-fractional-constant:
hexadecimal-digit-sequence-opt . hexadecimal-digit-sequence
hexadecimal-digit-sequence

exponent-part:
sign-opt digit-sequence
E sign-opt digit-sequence

binary-exponent-part:
p sign-opt digit-sequence
F sign-opt digit-sequence

sign: 一个:
-

digit-sequence:
digit
digit-sequence 'opt digit

floating-suffix: 一个:
f L P

string-literal:
encoding-prefix-opt "s-sequence-opt"
encoding-prefix-opt R raw-string

s-char-sequence:
s-char
s-char-sequence s-char

s-char:
字符集中的除双引号 " \ 或换行符以外的成员

raw-string:
* d-char-sequence-opt ( r-char-sequence-opt ) d-char-sequence-opt *

r-char-sequence:
r-char
r-char-sequence r-char

d-char-sequence:
d-char
d-char-sequence d-char

d-char:
基础字符集中的成员，除：
空格、左括号 (、右括号 )、反斜杠 \
以及代表水平制表符、分页符和换行的控制字符。

boolean-literal:
false
true

pointer-literal:
nullptr

user-defined-integer-literal:
user-defined-integer-literal
user-defined-floating-literal
user-defined-string-literal
user-defined-character-literal

user-defined-integer-suffix:
decimal-literal-suffix-opt
octal-literal-suffix-opt
hexadecimal-literal-suffix-opt
binary-literal-suffix-opt

user-defined-floating-literal:
fractional-constant exponent-part-opt suffix-opt
digit-sequence exponent-part suffix-opt
hexadecimal-prefix hexadecimal-fractional-constant binary-exponent-part suffix-opt

user-defined-string-literal:
string-literal-ud-suffix
character-literal-ud-suffix

ud-suffix:
identifier
```

# A.3 基本概念 [gram.basic]

``` 
translation-unit:
declaration-seq<qopt>
```

# A.4 表达式 [gram.expr]

``` 
primary-expression:
literal
this
( expression )
id-expression
lambda-expression
fold-expression

id-expression:
unqualified-id
qualified-id

unqualified-id:

identifier

operator-function-id

conversion-function-id

literal-operator-id

- class-name

- decltype-specifier

- template-id

qualified-id:

nested-name-specifier template.opt unqualified-id

nested-name-specifier:

  ::

type-name ::

namespace-space ::

decltype-specifier ::

nested-name-specifier identifier ::

nested-name-specifier template.opt simple-template-id ::

lambda-expression:

lambda-introducer lambda-declarator.opt compound-statement

lambda-introducer:

  [ lambda-capture.opt ]

lambda-declarator:

  ( parameter-declaration-clause ) decl-specifier.seq.opt

nocept-specifier.opt attribute-specifier.seq.opt trailing-return-type.opt

lambda-capture:

  capture-default

capture-list

capture-default

lambda-default:

  &

capture-list:

  capture ...opt

  capture-list , capture ...opt

capture:

  simple-capture

init-capture

simple-capture:

  identifier

& identifier

this

& this

init-capture:

  identifier initializer

& identifier initializer

fold-expression:

  ( cast-expression fold-operator ... )

  ( ... fold-operator cast-expression )

  ( cast-expression fold-operator ... fold-operator cast-expression )
```

# ISO/IEC 14882:2017(E)

折叠运算符（fold-operator）: 之一
+ * / % - & << >>
+= -= *= /= %= &= |= <<= >>= ^ *=
!= != < <= >= && || , .* *-*

``` 
后缀表达式（postfix-expression）:
primary-expression
postfix-expression [ expr-or-braced-init-list ]
postfix-expression ( expression-list_opt ) \
simple-type-specifier [ expression-list_opt ]
typename-specifier [ braced-init-list ]
simple-type-specifier braced-init-list
postfix-expression . template_opt id-expression
postfix-expression > template_opt id-expression
postfix-expression * pseudo-destructor-name
postfix-expression ++
postfix-expression --

dynamic_cast < type-id > ( expression )
static_cast < type-id > ( expression )
reinterpret_cast < type-id > ( expression )
const_cast < type-id > ( expression )
typeid ( type-id )

表达式列表（expression-list）:
initializer-list

伪标识符名（pseudo-specifier-name）:
nested-name-specifier template_opt type-name :: :: type-name
nested-name-specifier template simple-template-id :: :: type-name
type-specifier
-- decl-specifier

一元表达式（unary-expression）:
postfix-expression
++ cast-expression
-- cast-expression
unary-operator cast-expression
sizeof unary-expression
sizeof ( type-id )
sizeof ( ... ( identifier ) )
alignof ( type-id )
noexcept-expression
new-expression
deleter-expression

一元运算符（unary-operator）: 之一
* & | !

new 表达式（new-expression）:
::opt new-placement_opt new-type-id new-initializer_opt
::opt opt new-placement_opt ( type-id ) new-initializer_opt

new 放置（new-placement）:
{ expression-list }

new 类型标识（new-type-id）:
type-specifier-seq new-declarator_opt
```

# ISO/IEC 14882:2017(E)

``` 
new-declarator:

ptr-operator new-declarator_opt

optr-new-declarator

optr-new-declarator:

 [ expression ] attribute-specifier-seq_opt

optr-new-declarator [ constant-expression ] attribute-specifier-seq_opt

new-initializer:

 { expression-list_opt }

braced-init-list

delete 表达式（delete-expression）:

 ::_opt delete cast-expression

 ::_opt delete [ ] cast-expression

noexcept-expression:

 noexcept ( expression )

cast 表达式（cast-expression）:

unary-cast-expression

 ( type-id ) cast-expression

pm 表达式（pm-expression）:

 cast-expression

pm-expression * cast-expression

pm-expression -> cast-expression

乘法表达式（multiplicative-expression）:

 multiplicative-expression

multiplicative-expression * multiplicative-expression

multiplicative-expression / multiplicative-expression

multiplicative-expression % multiplicative-expression

加法表达式（additive-expression）:

 multiplicative-expression

additive-expression + multiplicative-expression

additive-expression - multiplicative-expression

位移表达式（shift-expression）:

 additive-expression

shift-expression << additive-expression

shift-expression >> additive-expression

关系表达式（relational-expression）:

 shift-expression

relational-expression < shift-expression

relational-expression > shift-expression

relational-expression <= shift-expression

relational-expression >= shift-expression

等价表达式（equality-expression）:

 relational-expression

equality-expression == relational-expression

equality-expression != relational-expression

与逻辑表达式（and-expression）:

 equality-expression

and-expression & equality-expression

异或逻辑表达式（exclusive-or-expression）:

 and-expression

 exclusive-or-expression ~ and-expression
```
