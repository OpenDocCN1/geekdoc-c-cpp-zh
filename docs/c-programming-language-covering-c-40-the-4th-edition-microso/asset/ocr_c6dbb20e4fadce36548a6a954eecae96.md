# 7.12 Conditional Logical Operators

The && and || operators are called the conditional logical operators. They are also called the “short-circuiting” logical operators.

conditional-and-expression:
    inclusive-or-expression
    conditional-and-expression && inclusive-or-expression

conditional-or-expression:
    conditional-or-expression
    conditional-or-expression || conditional-and-expression

The && and || operators are conditional versions of the & and | operators:

+   - The operation x && y corresponds to the operation x & y, except that y is evaluated only if x is not false.
+   - The operation x || y corresponds to the operation x | y, except that y is evaluated only if x is not true.

If an operand of a conditional logical operator has the compile-time type dynamic, then the expression is dynamically bound (§7.2.2). In this case, the compile-time type of the expression is dynamic, and the resolution described below will take place at runtime using the runtime type of those operands that have the compile-time type dynamic.

An operation of the form x && y or x || y is processed by applying overload resolution (§7.3.4) as if the operation was written x & y or x | y. Then,

+   - If overload resolution fails to find a single best operator, or if overload resolution selects one of the predefined integer logical operators, a binding-time error occurs.
+   - Otherwise, if the selected operator is one of the predefined boolean logical operators (§7.11.3) or nullable boolean logical operators (§7.11.4), the operation is processed as described in §7.12.1.
+   - Otherwise, the selected operator is a user-defined operator, and the operation is processed as described in §7.12.2.

It is not possible to directly overload the conditional logical operators. However, because the conditional logical operators are evaluated in terms of the regular logical operators, overloads of the regular logical operators are, with certain restrictions, also considered overloads of the conditional logical operators. This situation is described further in §7.12.2.