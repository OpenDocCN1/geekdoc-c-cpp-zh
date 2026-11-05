# 7.5.2.10 Upper-bound inferences

An upper-bound inference from a type U to a type V is made as follows:

+   - If V is one of the unfixed X_i then U is added to the set of upper bounds for X_i.
+   - Otherwise, sets V₁...V_k and U₁...U_k are determined by checking if any of the following cases apply:
+     - U is an array type U₁[...] and V is an array type V₁[...] of the same rank
+     - U is one of IEnumerable<U₀>, ICollection<U₀> or IList<U₀> and V is a one-dimensional array type V_e[]
+     - U is the type U₁? and V is the type V₁?
+     - U is constructed class, struct, interface or delegate type C<U₁...U_k> and V is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type C<V₁...V_k>
+       (The "uniqueness" restriction means that if we have interface C<T>{} class V<Z>: C<X<Z>>, C<X<Z>>{}, then no inference is made when inferring from C<U₁> to V<Q>. Inferences are not made from U₁ to either X<Q> or Y<Q>.)

If any of these cases apply then an inference is made from each U_i to the corresponding V_i as follows:

+   - If U_i is not known to be a reference type then an exact inference is made
+   - Otherwise, if V is an array type then an upper-bound inference is made
+   - Otherwise, if U is C<U₁...U_k> then inference depends on the i-th type parameter of C:
+     - If it is covariant then an upper-bound inference is made.
+     - If it is contravariant then a lower-bound inference is made.
+     - If it is invariant then an exact inference is made.
+   - Otherwise, no inferences are made.

# 7.5.2.11 Fixing

An unfixed type variable X_i with a set of bounds is fixed as follows:

+   - The set of candidate types U_j starts out as the set of all types in the set of bounds for X_i.
+   - We then examine each bound for X_i in turn: For each bound U of X_i, all types U_j which are not identical to U are removed from the candidate set. For each lower bound U of X_i, all types U_j to which there is not an implicit conversion from U are removed from the candidate set. For each upper bound U of X_i, all types U_j from which there is not an implicit conversion to U are removed from the candidate set.
+   - If among the remaining candidate types U_j there is a unique type V from which there is an implicit conversion to all the other candidate types, then X_i is fixed to V.
+   - Otherwise, type inference fails.

# 7.5.2.12 Inferred return type

The inferred return type of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation. The inferred return type is determined as follows:

+   - If the body of F is an expression, then the inferred return type of F is the type of that expression.