# ISO/IEC 14882:2017(E)

type-parameter:
type-parameter-key ... opt identifier_opt
type-parameter-key identifier_opt * type-id
template < template-parameter-list > type-parameter-key ... opt identifier_opt
template < template-parameter-list > type-parameter-key identifier_opt * = id-expression
class-name

type-parameter-key:
class
typename
simple-template-id:
template-name < template-argument-list_opt>
template-id:
simple-template-id
operator-function-id < template-argument-list_opt>
list-operator-id < template-argument-list_opt>

template-name:
identifier
template-argument-list:
template-argument ... opt
template-argument-list , template-argument ... opt
template-argument:
constant-expression
type-id
id-expression
typename-specifier:
typename nested-name-specifier identifier
typename nested-name-specifier template_opt simple-template-id

explicit-instantiation:
extern_opt template declaration
explicit_specifier:
template < > declaration

deduction-guide:
explicit < ( parameter-declaration-clause ) -> simple-template-id ;

# A.13 Exception handling [gram.except]

try-block:
try compound-statement handler-seq
function-try-block:
try c-initializer_opt compound-statement handler-seq
handler-seq:
handler handler-seq_opt
handler:
catch ( exception-declaration ) compound-statement

exception-declaration:
attribute-specifier-seq_opt type-specifier-seq declarator
attribute-specifier-seq_opt type-specifier-seq abstract-declarator_opt
...