+   - From T to a type parameter U, provided T depends on U (§10.1.5). At run-time, if U is a value type, then T and U are necessarily the same type and no conversion is performed. Otherwise, if T is a value type, the conversion is executed as a boxing conversion. Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.
+   - From the null literal to T, provided T is known to be a reference type.
+   - From T to a reference type I if it has an implicit conversion to a reference type S0 and S0 has an identity conversion to S. At run-time the conversion is executed the same way as the conversion to S0.
+   - From T to an interface type I if it has an implicit conversion to an interface or delegate type I0 and I0 is variance-convertible to I (§13.1.3.2). At run-time, if T is a value type, the conversion is executed as a boxing conversion. Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.

If T is known to be a reference type (§10.1.5), the conversions above are all classified as implicit reference conversions (§6.1.6). If T is not known to be a reference type, the conversions above are classified as boxing conversions (§6.1.7).

# 6.1.11 User-defined implicit conversions

A user-defined implicit conversion consists of an optional standard implicit conversion, followed by execution of a user-defined implicit conversion operator, followed by another optional standard implicit conversion. The exact rules for evaluating user-defined implicit conversions are described in §6.4.4.

# 6.1.12 Anonymous function conversions and method group conversions

Anonymous functions and method groups do not have types in and of themselves, but may be implicitly converted to delegate types or expression tree types. Anonymous function conversions are described in more detail in §6.5 and method group conversions in §6.6.

# 6.2 Explicit conversions

The following conversions are classified as explicit conversions:

+   - All implicit conversions.
+   - Explicit numeric conversions.
+   - Explicit enumeration conversions.
+   - Explicit nullable conversions.
+   - Explicit reference conversions.
+   - Explicit interface conversions.
+   - Unboxing conversions.
+   - Explicit dynamic conversions
+   - User-defined explicit conversions.

Explicit conversions can occur in cast expressions (§7.7.6).

The set of explicit conversions includes all implicit conversions. This means that redundant cast expressions are allowed.

The explicit conversions that are not implicit conversions are conversions that cannot be proven to always succeed, conversions that are known to possibly lose information, and conversions across domains of types sufficiently different to merit explicit notation.