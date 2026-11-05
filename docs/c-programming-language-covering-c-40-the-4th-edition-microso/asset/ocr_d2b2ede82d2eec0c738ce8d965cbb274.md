# 7.5.2.7 Explicit Parameter Type Inferences

An explicit parameter type inference is made from an expression E to a type T in the following way:

+   - If E is an explicitly typed anonymous function with parameter types U₁...Uₖ and T is a delegate type or expression tree type with parameter types V₁...Vᵣ, then for each Uᵢ an exact inference (§7.5.2.8) is made from Uᵢ to the corresponding Vᵢ.

# 7.5.2.8 Exact Inferences

An exact inference from a type U to a type V is made as follows:

+   - If V is one of the unfixed Xᵢ, then U is added to the set of exact bounds for Xᵢ.
+   - Otherwise, sets V₁...Vₖ and U₁...Uᵢ are determined by checking if any of the following cases apply:
+     - V is an array type V₁[...] and U is an array type U₁[...] of the same rank.
+     - V is the type V? and U is the type U?.
+     - V is a constructed type C<V₁...Vₖ> and U is a constructed type C<U₁...Uₖ>.
+     - If any of these cases apply, then an exact inference is made from each Uᵢ to the corresponding Vᵢ.
+   - Otherwise, no inferences are made.

# 7.5.2.9 Lower-Bound Inferences

A lower-bound inference from a type U to a type V is made as follows:

+   - If V is one of the unfixed Xᵢ, then U is added to the set of lower bounds for Xᵢ.
+   - Otherwise, sets U₁...Uₖ and V₁...Vₖ are determined by checking if any of the following cases apply:
+     - V is an array type V₁[...] and U is an array type U₁[...] (or a type parameter whose effective base type is U₁[...]) of the same rank.
+     - V is one of IEnumerable<V₁>, ICollection<V₁>, or IList<V₁> and U is a one-dimensional array type U₁[] (or a type parameter whose effective base type is U₁[]).

> VLADIMIR RESHETNIKOV Of course, this bullet (and the corresponding bullet in the next paragraph) mentions interfaces from namespace System.Collections.Generic.