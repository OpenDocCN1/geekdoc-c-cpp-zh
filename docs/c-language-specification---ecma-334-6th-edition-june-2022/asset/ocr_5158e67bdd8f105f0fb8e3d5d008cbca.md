with different types systems, or they may be objects that are programmatically setup to implement their own binding semantics for different operations.

The mechanism by which a dynamic object implements its own semantics is implementation-defined. A given interface – again implementation-defined – is implemented by dynamic objects to signal to the C# run-time that they have special semantics. Thus, whenever operations on a dynamic object are dynamically bound, their own binding semantics, rather than those of C# as specified in this specification, take over.

While the purpose of dynamic binding is to allow interoperability with dynamic objects, C# allows dynamic binding on all objects, whether they are dynamic or not. This allows for a smoother integration of dynamic objects, as the results of operations on them may not themselves be dynamic objects, but are still of a type unknown to the programmer at compile-time. Also, dynamic binding can help eliminate error-prone reflection-based code even when no objects involved are dynamic objects.

# 11.3.4 Types of subexpressions

When an operation is statically bound, the type of a subexpression (e.g., a receiver, and argument, an index or an operand) is always considered to be the compile-time type of that expression.

When an operation is dynamically bound, the type of a subexpression is determined in different ways depending on the compile-time type of the subexpression:

+   - A subexpression of compile-time type dynamic is considered to have the type of the actual value that the expression evaluates to at run-time
+   - A subexpression whose compile-time type is a type parameter is considered to have the type which the type parameter is bound to at run-time
+   - Otherwise, the subexpression is considered to have its compile-time type.

# 11.4 Operators

# 11.4.1 General

Expressions are constructed from operands and operators. The operators of an expression indicate which operations to apply to the operands.

Example: Examples of operators include +, -, *, /, and new. Examples of operands include literals, fields, local variables, and expressions. end example

There are three kinds of operators:

+   - Unary operators. The unary operators take one operand and use either prefix notation (such as -x) or postfix notation (such as x++).
+   - Binary operators. The binary operators take two operands and all use infix notation (such as x + y).
+   - Ternary operator. Only one ternary operator, ?:, exists; it takes three operands and uses infix notation (? x : y).

The order of evaluation of operators in an expression is determined by the precedence and associativity of the operators (§11.4.2).

Operands in an expression are evaluated from left to right.