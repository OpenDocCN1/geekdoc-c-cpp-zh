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
unary-assignment-operator assignment-expression

(6.5.17) assignment-operator: one of
* = /= % += - = << >> >= &=6 ^ = |

(6.6) constant-expression:
conditional-expression

# A.2.2 Declarations

(6.7) declaration:
declaration-specifiers init-declarator-list_opt ;
static-assert-declaration

(6.7) declaration-specifiers:
storage-class-spec declaration-specifiers_opt
type-spec declaration-specifiers_opt
type-qualifier declaration-specifiers_opt
function-spec declaration-specifiers_opt
alignment-spec declaration-specifiers_opt

(6.7) init-declarator:
init-declarator
init-declarator-list , init-declarator

§A.2.2 Language syntax summary 467