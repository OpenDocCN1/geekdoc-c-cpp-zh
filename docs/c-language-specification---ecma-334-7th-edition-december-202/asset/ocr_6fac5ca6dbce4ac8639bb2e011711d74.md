Example: Examples of operators include +, -, *, /, and new. Examples of operands include literals, fields, local variables, and expressions. end example

There are three kinds of operators:

+   - Unary operators. The unary operators take one operand and use either prefix notation (such as -x) or postfix notation (such as x++).
+   - Binary operators. The binary operators take two operands and all use infix notation (such as x + y).
+   - Ternary operator. Only one ternary operator, ?:, exists; it takes three operands and uses infix notation (c ? x : y).

The order of evaluation of operators in an expression is determined by the precedence and associativity of the operators (§12.4.2).

Operands in an expression are evaluated from left to right.

Example: In F(i) + G(i++) * H(i), method F is called using the old value of i, then method G is called with the old value of i, and, finally, method H is called with the new value of i. This is separate from and unrelated to operator precedence. end example

Certain operators can be overloaded. Operator overloading (§12.4.3) permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type.

# 12.4.2 Operator precedence and associativity

When an expression contains multiple operators, the precedence of the operators controls the order in which the individual operators are evaluated.

Note: For example, the expression x + y * z is evaluated as x + (y * z) because the * operator has higher precedence than the binary + operator. end note

The precedence of an operator is established by the definition of its associated grammar production.

Note: For example, an additive_expression consists of a sequence of multiplicative_expressions separated by + or - operators, thus giving the + and - operators lower precedence than the *, /, and % operators. end note

Note: The following table summarizes all operators in order of precedence from highest to lowest:

| Subclause | Category | Operators |
|---|---|---|
| §12.8 | Primary | x.y x?.y f(x) a[x] a?[x] x++ x-- new typeof default checked unchecked delegate stackalloc |
| §12.9 | Unary | + - ! ~ ++x --x (T)x await x |
| §12.10 | Multiplicative | * / % |
| §12.10 | Additive | + - |
| §12.11 | Shift | << >> |
| §12.12 | Relational and type-testing | < > <= >= is as |
| §12.12 | Equality | == != |
| §12.13 | Logical AND | & |
| §12.13 | Logical XOR | ^ |