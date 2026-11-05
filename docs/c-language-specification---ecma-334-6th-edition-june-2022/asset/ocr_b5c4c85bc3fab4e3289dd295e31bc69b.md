+   - V is one of `IEnumerable<V1>`, `ICollection<V1>`, `IReadOnlyList<V1>`, `IReadOnlyCollection<V1>` or `IList<V1>` and U is a single-dimensional array type U1[]
+   - V is a constructed `class`, `struct`, `interface` or `delegate` type C<V1...V> and there is a unique type C<U1...U> such that U (or, if U is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) C<U1...U>.
+   - (The "uniqueness" restriction means that in the case interface C<T>{} class U: C<X>, C<Y>{}, then no inference is made when inferring from U to C<T> because U1 could be X or Y.) If any of these cases apply then an inference is made from each U1 to the corresponding V1 as follows:
+   - If U1 is not known to be a reference type then an exact inference is made
+   - Otherwise, if U is an array type then a lower-bound inference is made
+   - Otherwise, if V is C<V1...V> then inference depends on the i-th type parameter of C:
+     - If it is covariant then a lower-bound inference is made.
+     - If it is contravariant then an upper-bound inference is made.
+     - If it is invariant then an exact inference is made.
+   - Otherwise, no inferences are made.

# 11.6.3.11 Upper-bound inferences

An upper-bound inference from a type U to a type V is made as follows:

+   - If V is one of the unfixed X_i, then U is added to the set of upper bounds for X_i.
+   - Otherwise, sets V1...Ve and U1...Ue are determined by checking if any of the following cases apply:
+     - U is an array type U1[...] and V is an array type V1[...] of the same rank
+     - U is one of `IEnumerable< Ue>`, `ICollection< Ue>`, `IReadOnlyList< Ue>`, `IReadOnlyCollection< Ue>` or `IList< Ue>` and V is a single-dimensional array type Ve[]
+     - U is the type U1? and V is the type V1?
+     - U is constructed class, struct, interface or delegate type C<U1...U> and V is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type C<V1...V>.
+     - (The "uniqueness" restriction means that if we have interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}, then no inference is made when inferring from C<U1> to V<Q>. Inferences are not made from U1 to either X<Q> or Y<Q>.) If any of these cases apply then an inference is made from each U1 to the corresponding V1 as follows:
+     - If U1 is not known to be a reference type then an exact inference is made
+     - Otherwise, if V is an array type then an upper-bound inference is made
+     - Otherwise, if U is C<U1...U> then inference depends on the i-th type parameter of C:
+       - If it is covariant then an upper-bound inference is made.
+       - If it is contravariant then a lower-bound inference is made.
+       - If it is invariant then an exact inference is made.