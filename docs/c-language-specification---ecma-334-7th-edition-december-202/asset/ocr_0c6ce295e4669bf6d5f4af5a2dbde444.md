Example: Given an enum_type E with and underlying type of int, a conversion from E to byte is processed as an explicit numeric conversion (§10.3.2) from int to byte, and a conversion from byte to E is processed as an implicit numeric conversion (§10.2.3) from byte to int. end example

# 10.3.4 Explicit nullable conversions

The explicit nullable conversions are those nullable conversions (§10.6.1) derived from explicit and implicit predefined conversions.

# 10.3.5 Explicit reference conversions

The explicit reference conversions are:

+   - From object and dynamic to any other reference_type.
+   - From any class_type S to any class_type T, provided S is a base class of T.
+   - From any class_type S to any interface_type T, provided S is not sealed and provided S does not implement T.
+   - From any interface_type S to any class_type T, provided T is not sealed or provided T implements S.
+   - From any interface_type S to any interface_type T, provided S is not derived from T.
+   - From an array_type S with an element type S₁ to an array_type T with an element type T₁, provided all of the following are true:
+     - S and T differ only in element type. In other words, S and T have the same number of dimensions.
+     - An explicit reference conversion exists from S₁ to T₁.
+   - From System.Array and the interfaces it implements, to any array_type.
+   - From a single-dimensional array_type S[] to System.Collections.Generic.IList<T>, System.Collections.Generic.IReadOnlyList<T>, and its base interfaces, provided that there is an identity conversion or explicit reference conversion from S to T.
+   - From System.Collections.Generic.IList<S>, System.Collections.Generic.IReadOnlyList<S>, and their base interfaces to a single-dimensional array type T[], provided that there is an identity conversion or explicit reference conversion from S to T.
+   - From System.Delegate and the interfaces it implements to any delegate_type.
+   - From a reference type S to a reference type T if it has an explicit reference conversion from S to a reference type T₀ and T₀ and there is an identity conversion from T₀ to T.
+   - From a reference type S to an interface or delegate type T if it there is an explicit reference conversion from S to an interface or delegate type T₀ and either T₀ is variance-convertible to T or T is variance-convertible to T₀ §18.2.3.3.
+   - From D<S₁...Sₙ> to D<T₁...Tₙ> where D<X₁...Xₙ> is a generic delegate type, D<S₁...Sₙ> is not compatible with or identical to D<T₁...Tₙ>, and for each type parameter Xᵢ of D the following holds:
+     - If Xᵢ is invariant, then Sᵢ is identical to Tᵢ.
+     - If Xᵢ is covariant, then there is an identity conversion, implicit reference conversion or explicit reference conversion from Sᵢ to Tᵢ.
+     - If Xᵢ is contravariant, then Sᵢ and Tᵢ are either identical or both reference types.