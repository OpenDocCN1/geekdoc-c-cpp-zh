If operator overload resolution resolves to either delegate equality operator, and the binding-time types of both operands are delegate types as described in §19 rather than System.Delegate, and there is no identity conversion between the binding-type operand types, a binding-time error occurs.

> > Note: This rule prevents comparisons which can never consider non-null values as equal due to being references to instances of different types of delegates. end note

# 11.11.10 Equality operators between nullable value types and the null literal

The == and != operators permit one operand to be a value of a nullable value type and the other to be the null literal, even if no predefined or user-defined operator (in unlifted or lifted form) exists for the operation.

For an operation of one of the forms

x == null    null == x    x != null    null != x

where x is an expression of a nullable value type, if operator overload resolution (§11.4.5) fails to find an applicable operator, the result is instead computed from the HasValue property of x. Specifically, the first two forms are translated into !x.HasValue, and the last two forms are translated into x.HasValue.

# 11.11.11 The is operator

The is operator is used to check if the run-time type of an object is compatible with a given type. The check is performed at runtime. The result of the operation E is T, where E is an expression and T is a type other than dynamic, is a Boolean value indicating whether E is non-null and can successfully be converted to type T by a reference conversion, a boxing conversion, an unboxing conversion, a wrapping conversion, or an unwrapping conversion.

The operation is evaluated as follows:

+   1. If E is an anonymous function, a compile-time error occurs
+   2. If E is a method group or the null literal, of if the value of E is null, the result is false.
+   3. Otherwise:
+   4. Let R be the runtime type of E.
+   5. Let D be derived from R as follows:
+   6. If R is a nullable value type, D is the underlying type of R.
+   7. Otherwise, D is R.
+   8. The result depends on D and T as follows:
+   9. If T is a reference type, the result is true if:
+      - D and T are the same type,
+      - D is a reference type and an implicit reference conversion from D to T exists, or
+      - Either: D is a value type and a boxing conversion from D to T exists. Or: D is a value type and T is an interface type implemented by D.
+   10. If T is a nullable value type, the result is true if D is the underlying type of T.
+   11. If T is a non-nullable value type, the result is true if D and T are the same type.
+   12. Otherwise, the result is false.