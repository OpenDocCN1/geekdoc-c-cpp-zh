+   - U is constructed class, struct, interface or delegate type `C<U1...U>` and V is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type `C<V1...V>`
+   - ('The "uniqueness" restriction means that given an interface C<T>{} class V<Z>: C<X<Z>>, C<X<Z>>{}}, then no inference is made when inferring from C<U1> to V<Q>. Inferences are not made from U1 to either X<Q> or Y<Q>.) If any of these cases apply then an inference is made from each U1 to the corresponding V1 as follows:
+   - If U1 is not known to be a reference type then an exact inference is made
+   - Otherwise, if V is an array type then an upper-bound inference is made
+   - Otherwise, if U is C<U1...U> then inference depends on the i-th type parameter of C:
+     - If it is covariant then an upper-bound inference is made.
+     - If it is contravariant then a lower-bound inference is made.
+     - If it is invariant then an exact inference is made.
+   - Otherwise, no inferences are made.

# 12.6.3.12 Fixing

An unfixed type variable X₁ with a set of bounds is fixed as follows:

+   - The set of candidate types Uₑ starts out as the set of all types in the set of bounds for X₁.
+   - Each bound for X₁ is examined in turn: For each exact bound U of X₁, all types Uₑ that are not identical to U are removed from the candidate set. For each lower bound U of X₁, all types Uₑ to which there is not an implicit conversion from U are removed from the candidate set. For each upper-bound U of X₁, all types Uₑ from which there is not an implicit conversion to U are removed from the candidate set.
+   - If among the remaining candidate types Uₑ there is a unique type V to which there is an implicit conversion from all the other candidate types, then X₁ is fixed to V.
+   - Otherwise, type inference fails.

# 12.6.3.13 Inferred return type

The inferred return type of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.

The inferred effective return type is determined as follows:

+   - If the body of F is an expression that has a type, then the inferred effective return type of F is the type of that expression.
+   - If the body of F is a block and the set of expressions in the block's return statements has a best common type T (§12.6.3.15), then the inferred effective return type of F is T.
+   - Otherwise, an effective return type cannot be inferred for F.

The inferred return type is determined as follows: If F is async and the body of F is either an expression classified as nothing (§12.2), or a block where no return statements have expressions, the inferred return type is «TaskType» (§15.15.1).