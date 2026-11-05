Note: The reason that short circuiting uses the ‘not true’ and ‘not false’ conditions is to enable user-defined conditional operators to define when short circuiting applies. User-defined types could be in a state where operator true returns false and operator false returns false. In those cases, neither && nor || would short circuit. end note

If an operand of a conditional logical operator has the compile-time type `dynamic`, then the expression is dynamically bound (§11.3.3). In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.

An operation of the form x && y or x || y is processed by applying overload resolution (§11.4.5) as if the operation was written x & y or x | y. Then,

+   - If overload resolution fails to find a single best operator, or if overload resolution selects one of the predefined integer logical operators or nullable Boolean logical operators (§11.12.5), a binding-time error occurs.
+   - Otherwise, if the selected operator is one of the predefined Boolean logical operators (§11.12.4), the operation is processed as described in §11.13.2.
+   - Otherwise, the selected operator is a user-defined operator, and the operation is processed as described in §11.13.3.

It is not possible to directly overload the conditional logical operators. However, because the conditional logical operators are evaluated in terms of the regular logical operators, overloads of the regular logical operators are, with certain restrictions, also considered overloads of the conditional logical operators. This is described further in §11.13.3.

# 11.13.2 Boolean conditional logical operators

When the operands of && or || are of type bool, or when the operands are of types that do not define an applicable operator & or operator |, but do define implicit conversions to bool, the operation is processed as follows:

+   - The operation x && y is evaluated as x ? y : false. In other words, x is first evaluated and converted to type bool. Then, if x is true, y is evaluated and converted to type bool, and this becomes the result of the operation. Otherwise, the result of the operation is false.
+   - The operation x || y is evaluated as x ? true : y. In other words, x is first evaluated and converted to type bool. Then, if x is true, the result of the operation is true. Otherwise, y is evaluated and converted to type bool, and this becomes the result of the operation.

# 11.13.3 User-defined conditional logical operators

When the operands of && or || are of types that declare an applicable user-defined operator & or operator |, both of the following shall be true, where T is the type in which the selected operator is declared:

+   - The return type and the type of each parameter of the selected operator shall be T. In other words, the operator shall compute the logical AND or the logical OR of two operands of type T, and shall return a result of type T.
+   - T shall contain declarations of operator true and operator false.