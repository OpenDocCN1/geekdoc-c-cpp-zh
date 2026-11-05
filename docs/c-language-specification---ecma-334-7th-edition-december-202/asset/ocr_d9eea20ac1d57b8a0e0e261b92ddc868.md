The left operand of an assignment shall be an expression classified as a variable, or, except for `= ref`, a property access, an indexer access, an event access or a tuple. A declaration expression is not directly permitted as a left operand, but may occur as a step in the evaluation of a deconstructing assignment.

The `=` operator is called the *simple assignment operator*. It assigns the value or values of the right operand to the variable, property, indexer element or tuple elements given by the left operand. The left operand of the simple assignment operator shall not be an event access (except as described in §15.8.2). The simple assignment operator is described in §12.21.2.

The operator `= ref` is called the *ref assignment operator*. It makes the right operand, which must be a *variable_reference* (§9.5), the referent of the reference variable designated by the left operand. The ref assignment operator is described in §12.21.3.

The assignment operators other than the `=` and `= ref` operators are called the *compound assignment operators*. These operators perform the indicated operation on the two operands, and then assign the resulting value to the variable, property, or indexer element given by the left operand. The compound assignment operators are described in §12.21.4.

The `+=` and `-=` operators with an event access expression as the left operand are called the *event assignment operators*. No other assignment operator is valid with an event access as the left operand. The event assignment operators are described in §12.21.5.

The assignment operators are right-associative, meaning that operations are grouped from right to left.

*Example:* An expression of the form `a = b = c` is evaluated as `a = (b = c)`. *end example*

# ### 12.21.2 Simple assignment

The `=` operator is called the simple assignment operator.

If the left operand of a simple assignment is of the form `E.P` or `E[E1]` where `E` has the compile-time type `dynamic`, then the assignment is dynamically bound (§12.3.3). In this case, the compile-time type of the assignment expression is `dynamic`, and the resolution described below will take place at run-time based on the run-time type of `E`. If the left operand is of the form `E[E1]` where at least one element of `E1` has the compile-time type `dynamic`, and the compile-time type of `E` is not an array, the resulting indexer access is dynamically bound, but with limited compile-time checking (§12.6.5).

A simple assignment where the left operand is classified as a tuple is also called a *deconstructing assignment*. If any of the tuple elements of the left operand has an element name, a compile-time error occurs. If any of the tuple elements of the left operand is a `declaration_expression` and any other element is not a `declaration_expression` or a simple discard, a compile-time error occurs.

The type of a simple assignment `x = y` is the type of an assignment to `x` of `y`, which is recursively determined as follows:

+   - If `x` is a tuple expression `(x1, ..., xn)`, and `y` can be deconstructed to a tuple expression `(y1, ..., yn)` with `n` elements (§12.7), and each assignment to `xi` of `yi` has the type `Ti`, then the assignment has the type `(T1, ..., Tn)`.
+   - Otherwise, if `x` is classified as a variable, the variable is not `readonly`, `x` has a type `T`, and `y` has an implicit conversion to `T`, then the assignment has the type `T`.
+   - Otherwise, if `x` is classified as an implicitly typed variable (i.e. an implicitly typed declaration expression) and `y` has a type `T`, then the inferred type of the variable is `T`, and the assignment has the type `T`.