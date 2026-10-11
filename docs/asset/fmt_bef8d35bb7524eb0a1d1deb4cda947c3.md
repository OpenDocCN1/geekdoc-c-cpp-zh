
包含或逻辑表达式（`inclusive-or-expression`）:
`exclusive-or-expression`
`inclusive-or-expression | exclusive-or-expression`
逻辑与表达式（`logical-and-expression`）:
`exclusive-or-expression`
`logical-and-expression && inclusive-or-expression`
逻辑或表达式（`logical-or-expression`）:
`logical-and-expression`
`logical-or-expression || logical-and-expression`
条件表达式（`conditional-expression`）:
`logical-or-expression`
`logical-or-expression ? assignment-expression`
`throw` 表达式（`throw-expression`）:
`throw assignment-expression_opt`
赋值表达式（`assignment-expression`）:
`conditional-expression`:
`logical-or-expression assignment-operator initializer-clause`
`throw-expression`
赋值运算符（`assignment-operator`）: 之一
`* = /= % += -= >> << &= = |`
表达式（`expression`）:
`assignment-expression`
`expression , assignment-expression`
常量表达式（`constant-expression`）:
`conditional-expression`

# A.5 语句（Statements）

语句（`statement`）:
`labeled-statement`
`attribute-specifier-seq_opt expression-statement`
`attribute-specifier-seq_opt compound-statement`
`attribute-specifier-seq_opt selection-statement`
`attribute-specifier-seq_opt iteration-statement`
`attribute-specifier-seq_opt jump-statement`
`declaration-statement`
`attribute-specifier-seq_opt try-block`
`init` 语句（`init-statement`）:
`expression-statement`
`simple-declaration`
条件（`condition`）:
`expression`
`attribute-specifier-seq_opt decl-specifier-seq decl brace-or-equal-initializer`
标记语句（`labeled-statement`）:
`attribute-specifier-seq_opt identifier : statement`
`attribute-specifier-seq_opt case constant-expression : statement`
`attribute-specifier-seq_opt default : statement`
表达式 语句可选（`expression-statement_opt`）:
`expression ;`
复合语句（`compound-statement`）:
`{ statement-seq_opt }`

©ISO/IEC 2017 – 版权所有

§ A.5

# ISO/IEC 14882:2017(E)

语句序列（`statement-seq`）:
`statement`
`statement-seq`
语句（`statement`）:
`if-specifier_opt ( condition )`
`if constexpr-opt ( condition ) statement`
`if ( condition ) statement`
`else-if-statement`
迭代语句（`iteration-statement`）:
`while ( expression )`
`do while ( expression )`
`for ( expression )`
`for ( expression ) statement`
`for ( condition ) statement`
跳转 语句（`jump-statement`）:
`break;`
`continue;`
表达式 语句（`expression-statement`）:
`expression ;`
复合语句（`compound-statement`）:
`{ statement-seq }`
标记语句（`labeled-statement`）:
`identifier : statement`
`try` 块（`try-block`）:
`attribute-specifier-seq_opt catch-block`
`attribute-specspec-_opt exception-handler`

# A.6 声明（Declarations）

声明序列（`declaration-seq`）:
`declaration`
`declaration-seq`
声明（`declaration`）:
`attribute-specifier-seq declaration`
`attribute-specifier_opt decl-specifier-seq`
`type-ifier`
`type-declaration`
`type-definition`
`function-declaration`
`template-guide`
`explicit-instantiation`
`explicit-specialization`
`linkage-specification`
`namespace-definition`
`empty-declaration`
`type-specifier`
`type-specifier attribute-specifier`
`opt`
`type-ifier`
`qualifier`
`type-ifier-spec:`
`seq:`
`ifier--spec--opt`
`type-specifier-specifier`

`--type-spec::`
`type-specifier`
`class-specifier`
`enum-specifier`

# ISO/IEC 14882:2017(E)

`defining-type-specifier-seq`:

`defining-type-specifier attribute-specifier-seq_opt`

`defining-type-specifier type-specifier`

`simple-type-specifier`:

`nested-name-specifier_opt type-name`

`nested-name-specifier template simple-template-id`

`nested-name-specifier_opt template-name`

`char`

`16_t`

`char32_t`

`wchar_t`

`bool`

`short`

`int`

`long`

`signed`

`unsigned`

`float`

`double`

`void`

`auto`

`decltype-specifier`

`type-name`:

`class-name`

`enum`

`type-name`

`simple-template-id`

`decltype-specifier`:

`decltype ( expression )`

`decltype ( auto )`

`elaborated-id-type-specifier`:

`class-key attribute-specifier-seq_opt nested-name-specifier_opt identifier`

`class-key nested-name-specifier_opt simple-template-id`

`enum nested-name-specifier_opt identifier`

`enum-name`:

`identifier`

`enum-specifier`:

`enum-head { enumerator-list_opt }`

`enum-head ( enumerator-list , )`

`enum-head`:

`enum-key attribute-specifier-seq_opt enum-head-name_opt enum-base_opt`

`enum-head-name`:

`nested-name-specifier_opt identifier`

`opaque-enum-declaration`:

`enum-key attribute-specifier-seq_opt nested-name-specifier_opt identifier enum-base_opt ;`

`enum-key`:

`enum`

`enum class`

`enum struct`

# ISO/IEC 14882:2017(E)

```cpp
enum-base:
  : type-specifier-seq
  enumerator-list:
    enumerator-definition
    enumerator-list , enumerator-definition
  enumerator-definition:
    enumerator
    enumerator = constant-expression
enumerator:
  identifier attribute-specifier-seq_opt
namespace-name:
  identifier
  namespace-alias
namespace-definition:
  named-namespace-definition
  unnamed-namespace-definition
  nested-namespace-definition
named-namespace-definition:
  inline_opt namespace attribute-specifier-seq_opt identifier { }
unnamed-namespace-definition:
  inline_opt namespace attribute-specifier-seq_opt { namespace-body }
nested-namespace-definition:
  namespace enclosing-namespace-specifier :: { namespace-body }
enclosing-namespace-specifier:
  identifier
  enclosing-namespace-specifier :: identifier
namespace-body:
  declaration-seq_opt
namespace-alias:
  identifier
namespace-alias-definition:
  namespace-specifier = qualified-namespace-specifier;
qualified-namespace-specifier:
  nested-name-specifier_opt namespace-name
using-declaration:
  using using-declarator-list;
using-declarator-list:
  using-declarator ..._opt
  using-declarator-list , using-declarator ..._opt
using-declarator:
  typename_opt nested-name unqualified-id
using-directive:
  attribute-specifier-seq_opt using namespace nested-name-specifier_opt namespace-name;
asm-definition:
  attribute-specifier-seq_opt asm { string-literal };
linkage-specification:
  extern string-literal { declaration-seq_opt }
  extern string-literal declaration
```

# ISO/IEC 14882:2017(E)

```cpp
attribute-specifier-seq:
attribute-specifier-seq_opt attribute-specifier
attribute-specifier:
  [ attribute-using-prefix_opt attribute-list ]
  alignment-specifier:
  alignas ( type-id . . opt )
  alignas ( constant-expression ... opt )
attribute-using-prefix:
  using attribute-namespace :
attribute-list:
  attribute_opt
  attribute-list, attribute_opt
  attribute ...
  attribute-list, attribute ...
attribute:
  attribute-token attribute-argument-clause_opt
attribute-token:
  identifier
  attribute-scoped-token
attribute-scoped:
  attribute-namespace :: identifier
attribute-namespace:
  identifier
attribute-argument-clause:
  ( balanced-token-seq_opt )
balanced-token-seq:
  balanced-token
  balanced-token-seq balanced-token
balanced-token:
  { balanced-token-seq_opt }
  { balanced-token-seq_opt }
  { balanced-token-seq_opt }
  any token other than a parenthesis, a bracket, or brace
```

## A.7 声明符

```cpp
init-declarator-list:
  init-declarator
  init-declarator-list, init-declarator
init-declarator:
  declarator initializer_opt
declarator:
  ptr-declarator
  ptr-declarator parameters-and-qualifiers trailing-return-type
ptr-declarator:
  noptr-declarator
  ptr-operator ptr-declarator
```

![](img/feea898746c6066176386930de01055d_1433_0.png)

# ISO/IEC 14882:2017(E)

```cpp
noptr-declarator:
  declarator-id attribute-specifier-seq_opt
noptr-declarator parameters-and-qualifiers
noptr-declarator [ constant-expression_opt ] attribute-specifier-seq_opt
{ 
- ptr-declarator:
parameters-and-qualifiers:
( parameter-declaration-clause ) cv-qualifier-seq_opt
ref-qualifier_opt noctce-specifier-opt attribute-specifier-seq_opt
trailing-return-type:
-> type-id:
ptr-operator:
* attribute-specifier-seq_opt cv-qualifier-seq_opt
& attribute-specifier-seq_opt
&& attribute-specifier-seq_opt
cv-qualifier-seq:
cv-qualifier cv-qualifier-seq_opt
cv-declarator:
const
volatile
ref-qualifier:
&
&&
declarator-id:
..._opt identifier
type-id:
type-specifier-seq abstract-declarator_opt
defining-type-id:
type-specifier-seq abstract-declarator_opt
abstract-declarator:
  ptr-declarator
noptr-declarator_opt parameters-and-qualifiers trailing-return-type
abstract-pack-declarator
ptr-declarator:
noptr-declarator
ptr-operator abstract-declarator_opt
noptr-abstract-declarator:
```
