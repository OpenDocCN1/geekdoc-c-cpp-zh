Constant expressions occur in the contexts listed below. In these contexts, a compile-time error occurs if an expression cannot be fully evaluated at compile time.

+   - Constant declarations (§10.4).
+   - Enumeration member declarations (§14.3).
+   - case labels of a switch statement (§8.7.2).
+   - goto case statements (§8.9.3).
+   - Dimension lengths in an array creation expression (§7.6.10.4) that includes an initializer.
+   - Attributes (§17).

An implicit constant expression conversion (§6.1.8) permits a constant expression of type int to be converted to sbyte, byte, short, ushort, uint, or ulong, provided the value of the constant expression is within the range of the destination type.

# 7.20 Boolean Expressions

A boolean-expression is an expression that yields a result of type bool, either directly or through application of operator true in certain contexts as specified in the following.

```
boolean-expression:
    expression
```

The controlling conditional expression of an if-statement (§8.7.1), while-statement (§8.8.1), do-statement (§8.8.2), or for-statement (§8.8.3) is a boolean-expression. The controlling conditional expression of the ?: operator (§7.14) follows the same rules as a boolean-expression, but for reasons of operator precedence is classified as a conditional-or-expression.

A boolean-expression is required to be implicitly convertible to bool or of a type that implements operator true. If neither requirement is satisfied, a binding-time error occurs.

When a boolean expression cannot be implicitly converted to bool but does implement operator true, then following evaluation of the expression, the operator true implementation provided by that type is invoked to produce a bool value.