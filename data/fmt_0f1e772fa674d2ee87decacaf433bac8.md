
# A.5 语句

语句:

```
labelled-statement
attribute-specifier-seq_opt expression-statement
attribute-specifier-seq_opt compound-statement
attribute-specifier-seq_opt selection-statement
attribute-specifier-seq_opt iteration-statement
attribute-specifier-seq_opt jump-statement
declaration-statement
attribute-specifier-seq_opt try-block
```

标签语句:

```
attribute-specifier-seq_opt identifier : statement
attribute-specifier-seq_opt case constant-expression : statement
attribute-specifier-seq_opt default : statement
```

表达式语句:

```
expression_opt;
```

复合语句:

```
{ statement-seq_opt }
```

语句序列:

```
statement
statement-seq statement
```

选择语句:

```
if ( condition ) statement
if ( condition ) statement else statement
switch ( condition ) statement
```

条件:

```
expression
attribute-specifier-seq_opt decl-specifier-seq
```

循环语句:

```
while ( condition ) statement
do statement while ( expression )
for ( condition ) statement
for ( for-init-statement ) statement
for ( for-range ) statement
```

for-init-statement:

```
expression
specifier
simple-declarator
```

for-range-initializer:

```
expression
braced-init-list;
```

跳转语句:

```
break;
continue;
return_opt;
goto;
```

声明语句:

```
declaration
```

# A.6 声明

声明序列:

```
declaration
declaration-seq
```

声明:

```
declaration
```

对象声明:

```
init-declarator
```

函数声明:

```
type-specifier-seq function-declarator_opt ( parameter-list )
```

变量声明:

```
type-specifier-seq declarator
```

外部声明:

```
extern declaration-qualified-id
```

类型声明:

```
using-declaration
```

命名空间声明:

```
namespace-definition
```

命名空间定义:

```
namespace-specifier-specifier
namespace-alias
```

别名声明:

```
using-declaration
```

类声明:

```
class-specifier
```

const限定限定符:

```
cv-qualifier
volatile
```

存储限定符:

```
storage-class-specifier
```

类型限定符序列:

```
type-specifier-seq
```

声明符:

```
ptr-operator new-declarator_opt
nptr-new-declarator
```

指针-新声明符:

```
[ attribute-specifier-seq_opt
nptr-new-declarator [ constant-expression ] attribute-specifier-seq_opt
```

新类型声明符:

```
type-specifier-seq new-declarator_opt
```

新位置表达式:

```
::opt_opt new-placement_opt new-type new-initializer_opt
::opt_opt new-placement_opt ( type-id ) new-initializer_opt
```

新初始化:

```
( expression-list )
brace-init-list
```

删除表达式:

```
::opt_delete cast-expression
::opt_delete [ ] cast-expression
```

初始化:

```
( expression-list )
brace-init-list
```

括号初始化列表:

```
{ initializer-list_opt }
```

一元表达式:

```
一元运算符：以下之一
* & + - ~
```

转换表达式:

```
unary-expression
( type-id ) cast-expression
```

pm表达式:

```
cast-expression
pm-expression * cast-expression
pm-expression ->* cast-expression
```

乘法表达式:

```
pm-expression
multiplicative-expression * pm-expression
multiplicative-expression / pm-expression
multiplicative-expression % pm-expression
```

加法表达式:

```
multiplicative-expression
additive-expression + multiplicative-expression
additive-expression - multiplicative-expression
```

移位表达式:

```
additive-expression
shift-expression << additive-expression
shift-expression >> additive-expression
```

关系表达式:

```
shift-expression
relational-expression < shift-expression
relational-expression > shift-expression
relational-expression <= shift-expression
relational-expression >= shift-expression
```

相等表达式:

```
relational-expression
equality-expression == relational-expression
equality-expression != relational-expression
```

与表达式:

```
equality-expression
and-expression & equality-expression
```

异或表达式:

```
and-expression
exclusive-or-expression ^ and-expression
```

包含或表达式:

```
exclusive-or-expression
inclusive-or-expression | exclusive-or-expression
```

逻辑与表达式:

```
inclusive-or-expression
logical-and-expression && inclusive-or-expression
```

逻辑或表达式:

```
logical-and-expression
logical-or-expression || logical-and-expression
```

条件表达式:

```
logical-or-expression
logical-or-expression ? expression : assignment-expression
```

throw表达式:

```
throw assignment-expression_opt
```

赋值表达式:

```
conditional-expression
logical-or-expression operator initializer-clause
```

赋值运算符:

```
*= %= /= -= += >>= <<= &= ^= |=
```

表达式:

```
assignment-expression
expression , assignment-expression
```

# ISO/IEC N4296

一元运算符：以下之一

* & + - ~

新表达式:

```
::opt_opt new-placement_opt new-type new-initializer_opt
::opt_opt new-placement_opt ( type-id ) new-initializer_opt
```

new-placement:

```
( expression-list )
```

new-type-id:

```
type-specifier-seq new-declarator_opt
```

new-declarator:

```
ptr-operator new-declarator_opt
nptr-new-declarator
```

ptr-new-declarator:

```
[ attribute-specifier-seq_opt
nptr-new-declarator [ constant-expression ] attribute-specifier-seq_opt
```

new-initializer:

```
( expression-list )
brace-init-list
```

delete表达式:

```
::opt_delete cast-expression
::opt_delete [ ] cast-expression
```

noexcept:

```
noexcept ( expression )
```

转换表达式:

```
unary-expression
( type-id ) cast-expression
```

pm表达式:

```
cast-expression
pm-expression * cast-expression
pm-expression ->* cast-expression
```

乘法表达式:

```
pm-expression
multiplicative-expression * pm-expression
multiplicative-expression / pm-expression
multiplicative-expression % pm-expression
```

加法表达式:

```
multiplicative-expression
additive-expression + multiplicative-expression
additive-expression - multiplicative-expression
```

移位表达式:

```
additive-expression
shift-expression << additive-expression
shift-expression >> additive-expression
```

关系表达式:

```
shift-expression
relational-expression < shift-expression
relational-expression > shift-expression
relational-expression <= shift-expression
relational-expression >= shift-expression
```

相等表达式:

```
relational-expression
equality-expression == relational-expression
equality-expression != relational-expression
```

与表达式:

```
equality-expression
and-expression & equality-expression
```

异或表达式:

```
and-expression
exclusive-or-expression ^ and-expression
```

包含或表达式:

```
exclusive-or-expression
inclusive-or-expression | exclusive-or-expression
```

逻辑与表达式:

```
inclusive-or-expression
logical-and-expression && inclusive-or-expression
```

逻辑或表达式:

```
logical-and-expression
logical-or-expression || logical-and-expression
```

条件表达式:

```
logical-or-expression
logical-or-expression ? expression : assignment-expression
```

throw表达式:

```
throw assignment-expression_opt
```

赋值表达式:

```
conditional-expression
logical-or-expression operator initializer-clause
```

赋值运算符：以下之一

```
*= %= /= -= += >>= <<= &= ^= |=
```

表达式:

```
assignment-expression
expression , assignment-expression
```
