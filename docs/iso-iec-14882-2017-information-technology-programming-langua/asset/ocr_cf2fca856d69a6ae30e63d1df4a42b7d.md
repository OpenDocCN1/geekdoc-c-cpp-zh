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
delelete-expression:
 ::_opt delete cast-expression
 ::_opt delete [ ] cast-expression
nocecept-expression:
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