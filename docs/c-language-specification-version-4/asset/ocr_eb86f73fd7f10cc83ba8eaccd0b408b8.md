# B.1.9 Operators and punctuators

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
>| 

right-shift-assignment:
>|= 

# B.1.10 Pre-processing directives

pp-directive:
pp-declaration
pp-conditional
pp-line
pp-diagnostic
pp-region
pp-pragma

conditional-symbol:
Any identifier-or-keyword except true or false

pp-expression:
whitespace_opt pp-or-expression whitespace_opt

pp-or-expression:
pp-and-expression
pp-or-expression whitespace_opt || whitespace_opt pp-and-expression

pp-and-expression:
pp-equality-expression
pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression

pp-equality-expression:
pp-unary-expression
pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression

pp-unary-expression:
pp-primary-expression
! whitespace_opt pp-unary-expression

pp-primary-expression:
true
false
conditional-symbol
( whitespace_opt pp-expression whitespace_opt )

pp-declaration:
whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line