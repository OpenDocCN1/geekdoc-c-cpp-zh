
# ISO/IEC 14882:2017(E)

fold-operator: one of
+ * / % - & << >>
+= -= *= /= %= &= |= <<= >>= ^ *=
!= != < <= >= && || , .* *-*

postfix-expression:
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

expression-list:
initializer-list

pseudo-specifier-name:
nested-name-specifier template_opt type-name :: :: type-name
nested-name-specifier template simple-template-id :: :: type-name
type-specifier
-- decl-specifier

unary-expression:
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

unary-operator: one of
* & | !

new-expression:
::opt new-placement_opt new-type-id new-initializer_opt
::opt opt new-placement_opt ( type-id ) new-initializer_opt

new-placement:
{ expression-list }

new-type-id:
type-specifier-seq new-declarator_opt

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
delete-expression:
 ::_opt delete cast-expression
 ::_opt delete [ ] cast-expression
noexcept-expression:
 noexcept ( expression )
cast-expression:
unary-cast-expression
 ( type-id ) cast-expression
pm-expression:
 cast-expression
pm-expression * cast-expression
pm-expression -> cast-expression
multiplicative-expression:
 multiplicative-expression
multiplicative-expression * multiplicative-expression
multiplicative-expression / multiplicative-expression
multiplicative-expression % multiplicative-expression
additive-expression:
 multiplicative-expression
additive-expression + multiplicative-expression
additive-expression - multiplicative-expression
shift-expression:
 additive-expression
shift-expression << additive-expression
shift-expression >> additive-expression
relational-expression:
 shift-expression
relational-expression < shift-expression
relational-expression > shift-expression
relational-expression <= shift-expression
relational-expression >= shift-expression
equality-expression:
 relational-expression
equality-expression == relational-expression
equality-expression != relational-expression
and-expression:
 equality-expression
and-expression & equality-expression
exclusive-or-expression:
 and-expression
 exclusive-or-expression ~ and-expression
```

inclusive-or-expression:
exclusive-or-expression
inclusive-or-expression | exclusive-or-expression
logical-and-expression:
exclusive-or-expression
logical-and-expression && inclusive-or-expression
logical-or-expression:
logical-and-expression
logical-or-expression || logical-and-expression
conditional-expression:
logical-or-expression
logical-or-expression ? assignment-expression
throw-expression:
throw assignment-expression_opt
assignment-expression:
conditional-expression:
logical-or-expression assignment-operator initializer-clause
throw-expression
assignment-operator: one of
* = /= % += -= >> << &= = |
expression:
assignment-expression
expression , assignment-expression
constant-expression:
conditional-expression

# A.5 Statements

statement:
labeled-statement
attribute-specifier-seq_opt expression-statement
attribute-specifier-seq_opt compound-statement
attribute-specifier-seq_opt selection-statement
attribute-specifier-seq_opt iteration-statement
attribute-specifier-seq_opt jump-statement
declaration-statement
attribute-specifier-seq_opt try-block
init-statement:
expression-statement
simple-declaration
condition:
expression
attribute-specifier-seq_opt decl-specifier-seq decl brace-or-equal-initializer
labeled-statement:
attribute-specifier-seq_opt identifier : statement
attribute-specifier-seq_opt case constant-expression : statement
attribute-specifier-seq_opt default : statement
expression-statement_opt:
expression ;
compound-statement:
{ statement-seq_opt }

©ISO/IEC 2017 – All rights reserved

§ A.5

# ISO/IEC 14882:2017(E)

statement-seq:
statement
statement-seq
statement:
if-specifier_opt ( condition )
if constexpr-opt ( condition ) statement
if ( condition ) statement
else-if-statement
iteration-statement:
while ( expression )
do while ( expression )
for ( expression )
for ( expression_opt ( condition ) statement
for ( expression ; init_opt ; condition ) statement
jump-statement:
break;
continue;
goto identifier;
expression-statement:
expression ;
compound-statement:
{ statement-seq_opt }
labeled-statement:
identifier : statement
try-block:
attribute-specifier-seq_opt catch-block-seq_opt 
attribute-specifier-seq_opt exception-handler

# A.6 Declarations

declaration-seq:
declaration
declaration-seq
declaration:
attribute-specifier-seq_opt declaration
attribute-specifier-seq_opt decl-specifier-seq
declaration-declaration
type-declaration
type-definition
function-declaration
template-guide
explicit-instantiation
explicit-specialization
linkage-specification
namespace-definition
empty-declaration
type-specifier
type-specifier attribute-specifier-opt
  type-specifier-seq
type-specifier:
  simple-type-specifier
  elaborated-type-specifier
  typename-qualifier
type-specifier-seq:
  type-specifier attribute-specifier-opt
  type-specifier type-specifier
defining-type-specifier:
  type-specifier
  class-specifier
  enum-specifier

# ISO/IEC 14882:2017(E)

```
defining-type-specifier-seq
defining-type-specifier attribute-specifier-seq_opt
defining-type-specifier type-specifier
simple-type-specifier:
nested-name-specifier_opt type-name
nested-name-specifier template simple-template-id
nested-name-specifier_opt template-name
char
16_t
char32_t
wchar_t
bool
short
int
long
signed
unsigned
float
double
void
auto
decltype-specifier
type-name:
class-name
enum
type-name
simple-template-id
decltype-specifier:
decltype ( expression )
decltype ( auto )
elaborated-id-type-specifier:
class-key attribute-specifier-seq_opt nested-name-specifier_opt identifier
class-key nested-name-specifier_opt simple-template-id
enum nested-name-specifier_opt identifier
enum-name:
identifier
enum-specifier:
enum-head { enumerator-list_opt }
enum-head ( enumerator-list , )
enum-head:
enum-key attribute-specifier-seq_opt enum-head-name_opt enum-base_opt
enum-head-name:
nested-name-specifier_opt identifier
opaque-enum-declaration:
enum-key attribute-specifier-seq_opt nested-name-specifier_opt identifier enum-base_opt ;
enum-key:
enum
enum class
enum struct
```

empty-declaration:
  attribute-specifier-seq;
decl-specifier:
  storage-class-specifier
  defining-type-specifier
  function-specifier
  friend
  typedef
  constexpr
  inline
decl-specifier-seq:
  storage-class-specifier
  defining-type-specifier
  function-specifier
  friend
  typedef
  constexpr
  inline
storage-class-specifier:
  static
  thread_local
extern
  mutable
function-specifier:
  virtual
  explicit
typedef-name:
  identifier
type-specifier:
  simple-type-specifier
  elaborated-type-specifier
  typename-qualifier
type-specifier-seq:
  type-specifier attribute-specifier-opt
  type-specifier type-specifier
