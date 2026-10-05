(6.5.12) inclusive-OR-expression:
exclusive-OR-expression
inclusive-OR-expression | exclusive-OR-expression

(6.5.13) logical-AND-expression:
inclusive-OR-expression
logical-AND-expression && inclusive-OR-expression

(6.5.14) logical-OR-expression:
logical-AND-expression
logical-OR-expression || logical-AND-expression

(6.5.15) conditional-expression:
logical-OR-expression
logical-OR-expression ? expression : conditional-expression

(6.5.16) assignment-expression:
conditional-expression
unary-expression assignment-operator assignment-expression

```
assignment-operator: one of
= *= /= %= += -= <= <= >= &= ^ = |
```

(6.5.17) expression:
assignment-expression
expression , assignment-expression

(6.6) constant-expression:
conditional-expression

# A.2.2 Declarations

(6.7) declaration:
declaration-specifiers init-declarator-list_opt ;\nstatic_assert-declaration

(6.7) declaration-specifiers:
storage-class-specifier declaration-specifiers_opt
type-specifier declaration-specifiers_opt
type-qualifier declaration-specifiers_opt
function-specifier declaration-specifiers_opt
alignment-specifier declaration-specifiers_opt

(6.7) init-declarator-list:
init-declarator
init-declarator-list , init-declarator