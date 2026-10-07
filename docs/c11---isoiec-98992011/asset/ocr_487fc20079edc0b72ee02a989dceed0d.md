# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

(6.5.3) unary-operator: one of
& * + ~ !

(6.5.4) cast-expression:
unary-expression
( type-name ) cast-expression

(6.5.5) multiplicative-expression:
cast-expression
multiplicative-expression * cast-expression
multiplicative-expression / cast-expression
multiplicative-expression % cast-expression

(6.5.6) additive-expression:
multiplicative-expression
additive-expression + multiplicative-expression
additive-expression - multiplicative-expression

(6.5.7) shift-expression:
additive-expression
shift-expression << additive-expression
shift-expression >> additive-expression

(6.5.8) relational-expression:
shift-expression
relational-expression < shift-expression
relational-expression > shift-expression
relational-expression <= shift-expression
relational-expression >= shift-expression

(6.5.9) equality-expression:
relational-expression
equality-expression == relational-expression
equality-expression != relational-expression

(6.5.10) AND-expression:
equality-expression
AND-expression & equality-expression

(6.5.11) exclusive-OR-expression:
AND-expression
exclusive-OR-expression ^ AND-expression