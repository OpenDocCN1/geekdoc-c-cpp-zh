encompassed type can be found, then the conversion is ambiguous and a compile-time error occurs.

+   - Otherwise, Sₓ is the most-encompassing type in the combined set of source types of the operators in U. If exactly one most-encompassing type cannot be found, then the conversion is ambiguous and a compile-time error occurs.
+   - Find the most-specific target type, Tₓ, of the operators in U:
+     - If any of the operators in U convert to T, then Tₓ is T.
+     - Otherwise, if any of the operators in U convert to types that are encompassed by T, then Tₓ is the most-encompassing type in the combined set of target types of those operators. If exactly one most-encompassing type cannot be found, then the conversion is ambiguous and a compile-time error occurs.
+     - Otherwise, Tₓ is the most-encompassed type in the combined set of target types of the operators in U. If no most-encompassed type can be found, then the conversion is ambiguous and a compile-time error occurs.
+   - Find the most-specific conversion operator:
+     - If U contains exactly one user-defined conversion operator that converts from Sₓ to Tₓ, then this is the most-specific conversion operator.
+     - Otherwise, if U contains exactly one lifted conversion operator that converts from Sₓ to Tₓ, then this is the most-specific conversion operator.
+     - Otherwise, the conversion is ambiguous and a compile-time error occurs.
+   - Finally, apply the conversion:
+     - If E does not already have the type Sₓ, then a standard explicit conversion from E to Sₓ is performed.
+     - The most-specific user-defined conversion operator is invoked to convert from Sₓ to Tₓ.
+     - If Tₓ is not T, then a standard explicit conversion from Tₓ to T is performed.

A user-defined explicit conversion from a type S to a type T exists if a user-defined explicit conversion exists from a variable of type S to T.

# 10.6 Conversions involving nullable types

# 10.6.1 Nullable Conversions

Nullable conversions permit predefined conversions that operate on non-nullable value types to also be used with nullable forms of those types. For each of the predefined implicit or explicit conversions that convert from a non-nullable value type S to a non-nullable value type T (§10.2.2, §10.2.3, §10.2.4, §10.2.11, §10.3.2 and §10.3.3), the following nullable conversions exist:

+   - An implicit or explicit conversion from S? to T?
+   - An implicit or explicit conversion from S to T?
+   - An explicit conversion from S? to T.

A nullable conversion is itself classified as an implicit or explicit conversion.