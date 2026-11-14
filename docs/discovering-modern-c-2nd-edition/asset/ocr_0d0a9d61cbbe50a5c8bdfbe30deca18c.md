if the latter can represent all values of the former; otherwise, both are converted to `unsigned long long`.

+   - Otherwise, if one operand is a `long` and the other an `unsigned`, then the `unsigned` is converted to `long` if the latter can represent all values of the former; otherwise, both are converted to `unsigned long`.
+   - Otherwise, if either operand is `long`, the other is converted to `long`;
+   - Otherwise, if either operand is `unsigned`, the other is converted to `unsigned`;
+   - Otherwise, both operands are converted to `int`.

As a consequence, programs with mixed `signed` and `unsigned` integers have platform-dependent behavior since the conversion rules depend on the sizes of integer types. Source: [62, §10.5.3].

# C.3.4 Narrowing

A `Narrowing Conversion` is an implicit conversion:

+   - From a floating-point type to an integer type; or
+   - From `long double` to `double` or `float`, or from `double` to `float`, except where the source is a constant expression and the actual value after conversion is within the range of values that can be represented (even if it cannot be represented exactly); or
+   - From an integer type or unscoped enumeration type to a floating-point type, except where the source is a constant expression and the actual value after conversion will fit into the target type and will produce the original value when converted back to the original type; or
+   - From an integer type or unscoped enumeration type to an integer type that cannot represent all the values of the original type, except where the source is a constant expression and the actual value after conversion will fit into the target type and will produce the original value when converted back to the original type.

Source: ISO standard.