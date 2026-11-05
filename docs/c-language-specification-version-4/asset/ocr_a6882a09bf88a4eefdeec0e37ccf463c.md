+   - If E is an explicitly typed anonymous function with parameter types U₁...Uₖ and T is a delegate type or expression tree type with parameter types V₁...Vₖ then for each Uᵢ an *exact inference* (§7.5.2.8) is made *from* Uᵢ *to* the corresponding Vᵢ.

# 7.5.2.8 Exact inferences

An *exact inference from a type U to a type V* is made as follows:

+   - If V is one of the *unfixed* Xᵢ, then U is added to the set of exact bounds for Xᵢ.
+   - Otherwise, sets V₁...Vₖ and U₁...Uₖ are determined by checking if any of the following cases apply:
+     - V is an array type V₁[...] and U is an array type U₁[...] of the same rank
+     - V is the type V₁? and U is the type U₁?
+     - V is a constructed type C<V₁...Vₖ> and U is a constructed type C<U₁...Uₖ>
+   If any of these cases apply then an *exact inference* is made from each Uᵢ to the corresponding Vᵢ.
+   - Otherwise, no inferences are made.

# 7.5.2.9 Lower-bound inferences

A *lower-bound inference from a type U to a type V* is made as follows:

+   - If V is one of the *unfixed* Xᵢ, then U is added to the set of lower bounds for Xᵢ.
+   - Otherwise, sets U₁...Uₖ and V₁...Vₖ are determined by checking if any of the following cases apply:
+     - V is an array type V₁[...] and U is an array type U₁[...] (or a type parameter whose effective base type is U₁[...]) of the same rank
+     - V is one of IEnumerable<V₁>, ICollection<V₁> or IList<V₁> and U is a one-dimensional array type U₁[] (or a type parameter whose effective base type is U₁[])
+     - V is the type V₁? and U is the type U₁?
+     - V is a constructed class, struct, interface or delegate type C<V₁...Vₖ> and there is a unique type C<U₁...Uₖ> such that U (or, if U is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) C<U₁...Uₖ>.
+   (The “uniqueness” restriction means that in the case interface C<T>{} class U: C<X>, C<Y>{}, then no inference is made when inferring from U to C<T> because U₁ could be X or Y.)
+   If any of these cases apply then an inference is made from each Uᵢ to the corresponding Vᵢ as follows:
+     - If Uᵢ is not known to be a reference type then an *exact inference* is made
+     - Otherwise, if U is an array type then a *lower-bound inference* is made
+     - Otherwise, if V is C<V₁...Vₖ> then inference depends on the i-th type parameter of C:
+       - If it is covariant then a *lower-bound inference* is made.
+       - If it is contravariant then an *upper-bound inference* is made.
+       - If it is invariant then an *exact inference* is made.
+   - Otherwise, no inferences are made.