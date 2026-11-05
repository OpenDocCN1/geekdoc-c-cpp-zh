```
const object i = 5;    // error: boxing conversion not permitted
const object str = "hello"; // error: implicit reference conversion
}
```

the initialization of i is an error because a boxing conversion is required. The initialization of str is an error because an implicit reference conversion from a non-null value is required.

*end example*

Whenever an expression fulfills the requirements listed above, the expression is evaluated at compile-time. This is true even if the expression is a subexpression of a larger expression that contains non-constant constructs.

The compile-time evaluation of constant expressions uses the same rules as run-time evaluation of non-constant expressions, except that where run-time evaluation would have thrown an exception, compile-time evaluation causes a compile-time error to occur.

Unless a constant expression is explicitly placed in an unchecked context, overflows that occur in integral-type arithmetic operations and conversions during the compile-time evaluation of the expression always cause compile-time errors (§12.8.19).

Constant expressions are required in the contexts listed below and this is indicated in the grammar by using constant_expression. In these contexts, a compile-time error occurs if an expression cannot be fully evaluated at compile-time.

+   - Constant declarations (§15.4)
+   - Enumeration member declarations (§19.4)
+   - Default arguments of formal parameter lists (§15.6.2)
+   - case labels of a switch statement (§13.8.3).
+   - goto case statements (§13.10.4)
+   - Dimension lengths in an array creation expression (§12.8.16.5) that includes an initializer.
+   - Attributes (§22)
+   - In a constant_pattern (§11.2.3)

An implicit constant expression conversion (§10.2.11) permits a constant expression of type int to be converted to sbyte, byte, short, ushort, uint, or ulong, provided the value of the constant expression is within the range of the destination type.

# 12.24 Boolean expressions

A boolean_expression is an expression that yields a result of type bool; either directly or through application of operator true in certain contexts as specified in the following:

```
boolean_expression
  : expression
  ;
```

The controlling conditional expression of an if_statement (§13.8.2), while_statement (§13.9.2), do_statement (§13.9.3), or for_statement (§13.9.4) is a boolean_expression. The controlling conditional expression of the ?: operator (§12.18) follows the same rules as a boolean_expression, but for reasons of operator precedence is classified as a null_coalescing_expression.