User defined conversions are not considered by the is operator.

Note: As the is operator is evaluated at runtime, all type arguments have been substituted and there are no open types (§8.4.3) to consider. end note

Note: The is operator can be understood in terms of compile-time types and conversions as follows, where C is the compile-time type of E:

+   - If the compile-time type of e is the same as T, or if an implicit reference conversion (§10.2.8), boxing conversion (§10.2.9), wrapping conversion (§10.6), or an explicit unwrapping conversion (§10.6) exists from the compile-time type of E to T:
+     - If C is of a non-nullable value type, the result of the operation is true.
+     - Otherwise, the result of the operation is equivalent to evaluating E != null.
+   - Otherwise, if an explicit reference conversion (§10.3.5) or unboxing conversion (§10.3.6) exists from C to T, or if C or T is an open type (§8.4.3), then runtime checks as above must be performed.
+   - Otherwise, no reference, boxing, wrapping, or unwrapping conversion of E to type T is possible, and the result of the operation is false. A compiler may implement optimisations based on the compile-time type.

end note

# 11.11.12 The as operator

The as operator is used to explicitly convert a value to a given reference type or nullable value type. Unlike a cast expression (§11.8.7), the as operator never throws an exception. Instead, if the indicated conversion is not possible, the resulting value is null.

In an operation of the form E as T, E shall be an expression and T shall be a reference type, a type parameter known to be a reference type, or a nullable value type. Furthermore, at least one of the following shall be true, or otherwise a compile-time error occurs:

+   - An identity (§10.2.2), implicit nullable (§10.2.6), implicit reference (§10.2.8), boxing (§10.2.9), explicit nullable (§10.3.4), explicit reference (§10.3.5), or wrapping (§8.3.11) conversion exists from E to T.
+   - The type of E or T is an open type.
+   - E is the null literal.

If the compile-time type of E is not dynamic, the operation E as T produces the same result as

```
E is T ? (T)(E) : (T)null
```

except that E is only evaluated once. The compiler can be expected to optimize E as T to perform at most one runtime type check as opposed to the two runtime type checks implied by the expansion above.

If the compile-time type of E is dynamic, unlike the cast operator the as operator is not dynamically bound (§11.3.3). Therefore the expansion in this case is:

```
E is T ? (T)(object)(E) : (T)null
```

Note that some conversions, such as user defined conversions, are not possible with the as operator and should instead be performed using cast expressions.

Example: In the example