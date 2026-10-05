#  6.5.13 Logical AND operator

#  Syntax

```
logical-AND-expression:
inclusive-OR-expression
logical-AND-expression && inclusive-OR-expression
```

#  Constraints

Each of the operands shall have scalar type.

#  Semantics

The && operator shall yield 1 if both of its operands compare unequal to 0; otherwise, it yields 0. The result has type int.

Unlike the bitwise binary & operator, the && operator guarantees left-to-right evaluation; if the second operand is evaluated, there is a sequence point between the evaluations of the first and second operands. If the first operand compares equal to 0, the second operand is not evaluated.

#  6.5.14 Logical OR operator

#  Syntax

```
logical-OR-expression:
logical-AND-expression
logical-OR-expression || logical-AND-expression
```

#  Constraints

Each of the operands shall have scalar type.

#  Semantics

The || operator shall yield 1 if either of its operands compare unequal to 0; otherwise, it yields 0. The result has type int.

Unlike the bitwise | operator, the || operator guarantees left-to-right evaluation; if the second operand is evaluated, there is a sequence point between the evaluations of the first and second operands. If the first operand compares unequal to 0, the second operand is not evaluated.