When an instance method is invoked, the result of evaluating the instance expression becomes the instance represented by *this* (§11.7.12). A method group is permitted in an *invocation_expression* (§11.7.8) or a *delegate_creation_expression* (§11.7.15.6), and can be implicitly converted to a compatible delegate type (§10.8). In any other context, an expression classified as a method group causes a compile-time error.

+   - An event access. Every event access has an associated type, namely the type of the event. Furthermore, an event access may have an associated instance expression. An event access may appear as the left-hand operand of the += and -= operators (§11.18.4). In any other context, an expression classified as an event access causes a compile-time error. When an accessor of an instance event access is invoked, the result of evaluating the instance expression becomes the instance represented by *this* (§11.7.12).

A property access or indexer access is always reclassified as a value by performing an invocation of the *get_accessor* or the *set_accessor*. The particular accessor is determined by the context of the property or indexer access: If the access is the target of an assignment, the *set_accessor* is invoked to assign a new value (§11.18.2). Otherwise, the *get_accessor* is invoked to obtain the current value (§11.2.2).

An *instance accessor* is a property access on an instance, an event access on an instance, or an indexer access.

# 11.2.2 Values of expressions

Most of the constructs that involve an expression ultimately require the expression to denote a *value*. In such cases, if the actual expression denotes a namespace, a type, a method group, or nothing, a compile-time error occurs. However, if the expression denotes a property access, an indexer access, or a variable, the value of the property, indexer, or variable is implicitly substituted:

+   - The value of a variable is simply the value currently stored in the storage location identified by the variable. A variable shall be considered definitely assigned (§9.4) before its value can be obtained, or otherwise a compile-time error occurs.
+   - The value of a property access expression is obtained by invoking the *get_accessor* of the property. If the property has no *get_accessor*, a compile-time error occurs. Otherwise, a function member invocation (§11.6.6) is performed, and the result of the invocation becomes the value of the property access expression.
+   - The value of an indexer access expression is obtained by invoking the *get_accessor* of the indexer. If the indexer has no *get_accessor*, a compile-time error occurs. Otherwise, a function member invocation (§11.6.6) is performed with the argument list associated with the indexer access expression, and the result of the invocation becomes the value of the indexer access expression.

# 11.3 Static and Dynamic Binding

# 11.3.1 General

*Binding* is the process of determining what an operation refers to, based on the type or value of expressions (arguments, operands, receivers). For instance, the binding of a method call is determined based on the type of the receiver and arguments. The binding of an operator is determined based on the type of its operands.

In C# the binding of an operation is usually determined at compile-time, based on the compile-time type of its subexpressions. Likewise, if an expression contains an error, the error is detected and reported by the compiler. This approach is known as *static binding*.