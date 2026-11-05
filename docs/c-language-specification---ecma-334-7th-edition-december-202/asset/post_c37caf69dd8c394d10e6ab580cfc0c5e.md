
- X₁ has a non-empty set of bounds
- If no such type variables exist and there are still unfixed type variables, type inference fails.
- Otherwise, if no further unfixed type variables exist, type inference succeeds.
- Otherwise, for all arguments Eᵢ with corresponding parameter type Tᵢ where the output types (§12.6.3.5) contain unfixed type variables Xₖ but the input types (§12.6.3.4) do not, an output type inference (§12.6.3.7) is made from Eᵢ to Tᵢ. Then the second phase is repeated.

## 12.6.3.4 Input types

If E is a method group or implicitly typed anonymous function and T is a delegate type or expression tree type then all the parameter types of T are input types of E with type T.

## 12.6.3.5 Output types

If E is a method group or an anonymous function and T is a delegate type or expression tree type then the return type of T is an output type of E with type T.

## 12.6.3.6 Dependence

An unfixed type variable X₁ depends directly on an unfixed type variable Xₐ if for some argument Eᵥ with type Tᵥ, Xₐ occurs in an input type of Eᵥ with type Tᵥ, and X₁ occurs in an output type of Eᵥ with type Tᵥ.

Xₐ depends on X₁ if Xₐ depends directly on X₁ or if X₁ depends directly on Xᵥ, and Xᵥ depends on Xₐ. Thus "depends on" is the transitive but not reflexive closure of "depends directly on".

## 12.6.3.7 Output type inferences

An output type inference is made from an expression E to a type T in the following way:

- If E is an anonymous function with inferred return type U (§12.6.3.13) and T is a delegate type or expression tree type with return type Tᵣ, then a lower-bound inference (§12.6.3.10) is made from U to Tᵣ.
- Otherwise, if E is a method group and T is a delegate type or expression tree type with parameter types T₁...Tᵥ and return type Tᵣ, and overload resolution of E with the types T₁...Tᵥ yields a single method with return type U, then a lower-bound inference is made from U to Tᵣ.
- Otherwise, if E is an expression with type U, then a lower-bound inference is made from U to T.
- Otherwise, no inferences are made.

## 12.6.3.8 Explicit parameter type inferences

An explicit parameter type inference is made from an expression E to a type T in the following way:

- If E is an explicitly typed anonymous function with parameter types U₁...Uᵥ and T is a delegate type or expression tree type with parameter types V₁...Vᵥ, then for each Uᵢ an exact inference (§12.6.3.9) is made from Uᵢ to the corresponding Vᵢ.

## 12.6.3.9 Exact inferences

An exact inference from a type U to a type V is made as follows:

- If V is one of the unfixed Xᵢ then U is added to the set of exact bounds for Xᵢ.
- Otherwise, sets V₁...Vₑ and U₁...Uₑ are determined by checking if any of the following cases apply:
  - V is an array type V₁[...] and U is an array type U₁[...] of the same rank
  - V is the type V_i? and U is the type U_i
  - V is a constructed type C<V_1...V_e> and U is a constructed type C<U_1...U_e>
If any of these cases apply then an exact inference is made from each U_i to the corresponding V_i.
- Otherwise, no inferences are made.

## 12.6.3.10 Lower-bound inferences

A lower-bound inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i, then U is added to the set of lower bounds for X_i.
- Otherwise, if V is the type V_i? and U is the type U_i? then a lower bound inference is made from U_i to V_i.
- Otherwise, sets U_1...U_e and V_1...V_e are determined by checking if any of the following cases apply:
  - V is an array type V_1[...] and U is an array type U_1[...] of the same rank
  - V is one of IEnumerable<V_i>, ICollection<V_i>, IReadOnlyList<V_i>, IReadOnlyCollection<V_i> or IList<V_i> and U is a single-dimensional array type U_1[]
  - V is a constructed class, struct, interface or delegate type C<V_1...V_e> and there is a unique type C<U_1...U_e> such that U (or, if U is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) C<U_1...U_e>.
  - {"The "uniqueness" restriction means that in the case interface C<T>{ class U : C<X>, C<Y>{}, then no inference is made when inferring from U to C<T> because U_i could be X or Y."}
If any of these cases apply then an inference is made from each U_i to the corresponding V_i as follows:
  - If U_i is not known to be a reference type then an exact inference is made
  - Otherwise, if U is an array type then a lower-bound inference is made
  - Otherwise, if V is C<V_1...V_e> then inference depends on the i-th type parameter of C:
    - If it is covariant then a lower-bound inference is made.
    - If it is contravariant then an upper-bound inference is made.
    - If it is invariant then an exact inference is made.
- Otherwise, no inferences are made.

## 12.6.3.11 Upper-bound inferences

An upper-bound inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i, then U is added to the set of upper bounds for X_i.
- Otherwise, sets V_1...V_e and U_1...U_e are determined by checking if any of the following cases apply:
  - U is an array type U_1[...] and V is an array type V_1[...] of the same rank
  - U is one of IEnumerable<U_i>, ICollection<U_i>, IReadOnlyList<U_i>, IReadOnlyCollection<U_i> or IList<U_i> and V is a single-dimensional array type V_1[]
  - U is the type U_i? and V is the type V_i?
  - U is a constructed class, struct, interface or delegate type `C<U1...Ue>` and V is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type `C<V1...Ve>`
  - ('The "uniqueness" restriction means that given an interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}, then no inference is made when inferring from C<U1> to V<Q>. Inferences are not made from U1 to either X<Q> or Y<Q>.)
If any of these cases apply then an inference is made from each U_i to the corresponding V_i as follows:
  - If U_i is not known to be a reference type then an exact inference is made
  - Otherwise, if V is an array type then an upper-bound inference is made
  - Otherwise, if U is C<U1...Ue> then inference depends on the i-th type parameter of C:
    - If it is covariant then an upper-bound inference is made.
    - If it is contravariant then a lower-bound inference is made.
    - If it is invariant then an exact inference is made.
- Otherwise, no inferences are made.

## 12.6.3.12 Fixing

An unfixed type variable X₁ with a set of bounds is fixed as follows:

- The set of candidate types Uₑ starts out as the set of all types in the set of bounds for X₁.
- Each bound for X₁ is examined in turn: For each exact bound U of X₁, all types Uₑ that are not identical to U are removed from the candidate set. For each lower bound U of X₁, all types Uₑ to which there is not an implicit conversion from U are removed from the candidate set. For each upper-bound U of X₁, all types Uₑ from which there is not an implicit conversion to U are removed from the candidate set.
- If among the remaining candidate types Uₑ there is a unique type V to which there is an implicit conversion from all the other candidate types, then X₁ is fixed to V.
- Otherwise, type inference fails.

## 12.6.3.13 Inferred return type

The inferred return type of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.

The inferred effective return type is determined as follows:

- If the body of F is an expression that has a type, then the inferred effective return type of F is the type of that expression.
- If the body of F is a block and the set of expressions in the block's return statements has a best common type T (§12.6.3.15), then the inferred effective return type of F is T.
- Otherwise, an effective return type cannot be inferred for F.

The inferred return type is determined as follows: If F is async and the body of F is either an expression classified as nothing (§12.2), or a block where no return statements have expressions, the inferred return type is «TaskType» (§15.15.1).
