# 11.3.4 Explicit nullable conversions

The explicit nullable conversions are those nullable conversions (§11.6.1) derived from explicit and implicit predefined conversions.

# 11.3.5 Explicit reference conversions

The explicit reference conversions are:

+   - From object and dynamic to any other reference-type.
+   - From any class-type S to any class-type T, provided S is a base class of T.
+   - From any class-type S to any interface-type T, provided S is not sealed and provided S does not implement T.
+   - From any interface-type S to any class-type T, provided T is not sealed or provided T implements S.
+   - From any interface-type S to any interface-type T, provided S is not derived from T.
+   - From an array-type S with an element type Se to an array-type T with an element type Te, provided all of the following are true:
+     - S and T differ only in element type. In other words, S and T have the same number of dimensions.
+     - An explicit reference conversion exists from Se to Te.
+   - From System.Array and the interfaces it implements, to any array-type.
+   - From a single-dimensional array-type S[] to System.Collections.Generic.IList<T>, System.Collections.Generic.IReadOnlyList<T>, and its base interfaces, provided that there is an identity conversion or explicit reference conversion from S to T.
+   - From System.Collections.Generic.IList<S>, System.Collections.Generic.IReadOnlyList<S>, and their base interfaces to a single-dimensional array type T[], provided that there is an identity conversion or explicit reference conversion from S to T.
+   - From System.Delegate and the interfaces it implements to any delegate-type.
+   - From a reference type S to a reference type T if it has an explicit reference conversion from S to a reference type T0 and T0 to T and there is an identity conversion from T0 to T.
+   - From a reference type S to an interface or delegate type T if there is an explicit reference conversion from S to an interface or delegate type T0 and either T0 is variance-convertible to T or T is variance-convertible to T0 (§18.2.3).
+   - From D<S1...Sn> to D<T1...Tn> where D<X1...Xn> is a generic delegate type, D<S1...Sn> is not compatible with or identical to D<T1...Tn>, and for each type parameter Xi of D the following holds:
+     - If Xi is invariant, then Si is identical to Ti.
+     - If Xi is covariant, then there is an identity conversion, implicit reference conversion or explicit reference conversion from Si to Ti.
+     - If Xi is contravariant, then Si and Ti are either identical or both reference types.
+   - Explicit conversions involving type parameters that are known to be reference types. For more details on explicit conversions involving type parameters, see §11.3.8.

The explicit reference conversions are those conversions between reference-types that require run-time checks to ensure they are correct.

For an explicit reference conversion to succeed at run-time, the value of the source operand shall be null, or the type of the object referenced by the source operand shall be a type that can be converted to the destination type by an implicit reference conversion (§11.2.7). If an explicit reference conversion fails, a System.InvalidCastException is thrown.

Reference conversions, implicit or explicit, never change the referential identity of the object being converted. [Note: In other words, while a reference conversion can change the type of the reference, it never changes the type or value of the object being referred to. end note]