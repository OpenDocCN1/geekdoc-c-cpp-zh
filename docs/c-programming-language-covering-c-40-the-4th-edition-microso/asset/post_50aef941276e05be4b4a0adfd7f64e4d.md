
> PETER SESTOFT Although probably not intended to, the previous annotation may leave the impression that a type inference algorithm for a Hindley–Milner-style type system (that is, ML let polymorphism) must use backtracking. In particular, the Damas–Milner algorithm (1978) does not use backtracking. That said, use of backtracking would be overkill for C# type inference, because in C# all type parameters must be explicitly specified. In contrast, the Damas–Milner algorithm will invent enough type parameters to find the most general ("principal") type for a given expression. That problem is known to be complete for exponential time.

## 7.5.2.1 The First Phase

For each of the method arguments E_i:

- If E_i is an anonymous function, an explicit parameter type inference (§7.5.2.7) is made from E_i to T_i.
- Otherwise, if E_i has a type U and x_i is a value parameter, then a lower-bound inference is made from U to T_i.
- Otherwise, if E_i has a type U and x_i is a ref or out parameter, then an exact inference is made from U to T_i.
- Otherwise, no inference is made for this argument.

## 7.5.2.2 The Second Phase

The second phase proceeds as follows:

- All unfixed type variables X_i that do not depend on (§7.5.2.5) any X_j are fixed (§7.5.2.10).
- If no such type variables exist, all unfixed type variables X_i are fixed for which both of the following hold:
  - There is at least one type variable X_j that depends on X_i.
  - X_i has a non-empty set of bounds.
- If no such type variables exist and there are still unfixed type variables, type inference fails.
- Otherwise, if no further unfixed type variables exist, type inference succeeds.
- Otherwise, for all arguments E_i with corresponding parameter type T_i where the output types (§7.5.2.4) contain unfixed type variables X_i but the input types (§7.5.2.3) do not, an output type inference (§7.5.2.6) is made from E_i to T_i. Then the second phase is repeated.

## 7.5.2.3 Input Types

If E is a method group or implicitly typed anonymous function and T is a delegate type or expression tree type, then all the parameter types of T are *input types of* E *with type* T.

## 7.5.2.4 Output Types

If E is a method group or an anonymous function and T is a delegate type or expression tree type, then the return type of T is an *output type of* E *with type* T.

## 7.5.2.5 Dependence

An unfixed type variable X_i depends directly on an unfixed type variable X_j if for some argument E_i with type T_i, X_j occurs in an *input type* of E_i with type T_i and X_j occurs in an *output type* of E_i with type T_i.

X_i depends on X_j if X_i depends directly on X_j or if X_i depends directly on X_k and X_k depends directly on X_j. Thus “depends on” is the transitive but not reflexive closure of “depends directly on.”

> > **VLADIMIR RESHETNIKOV** A type parameter could possibly directly or indirectly depend on itself.

## 7.5.2.6 Output Type Inferences

An *output type inference* is made from an expression E to a type T in the following way:

- If E is an anonymous function with inferred return type U (§7.5.2.12) and T is a delegate type or expression tree type with return type T_b, then a *lower-bound inference* (§7.5.2.9) is made *from* U *to* T_b.
- Otherwise, if E is a method group and T is a delegate type or expression tree type with parameter types T_1…T_k and return type T_b, and overload resolution of E with the types T_1…T_k yields a single method with return type U, then a *lower-bound inference* is made *from* U *to* T_b.

> > **VLADIMIR RESHETNIKOV** This step applies only if all method type parameters occurring in the delegate parameter types are already fixed. Overload resolution does not try to select the best method based on incomplete type information.

- Otherwise, if E is an expression with type U, then a *lower-bound inference* is made *from* U *to* T.
- Otherwise, no inferences are made.

## 7.5.2.7 Explicit Parameter Type Inferences

An explicit parameter type inference is made from an expression E to a type T in the following way:

- If E is an explicitly typed anonymous function with parameter types U₁...Uₖ and T is a delegate type or expression tree type with parameter types V₁...Vᵣ, then for each Uᵢ an exact inference (§7.5.2.8) is made from Uᵢ to the corresponding Vᵢ.

## 7.5.2.8 Exact Inferences

An exact inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i, then U is added to the set of exact bounds for X_i.
- Otherwise, sets V₁...Vₖ and U₁...Uᵢ are determined by checking if any of the following cases apply:
  - V is an array type V₁[...] and U is an array type U₁[...] of the same rank.
  - V is the type V? and U is the type U?.
  - V is a constructed type C<V₁...Vₖ> and U is a constructed type C<U₁...Uₖ>.
- If any of these cases apply, then an exact inference is made from each Uᵢ to the corresponding Vᵢ.
- Otherwise, no inferences are made.

## 7.5.2.9 Lower-Bound Inferences

A lower-bound inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i, then U is added to the set of lower bounds for X_i.
- Otherwise, sets U₁...Uₖ and V₁...Vₖ are determined by checking if any of the following cases apply:
  - V is an array type V₁[...] and U is an array type U₁[...] (or a type parameter whose effective base type is U₁[...]) of the same rank.
  - V is one of IEnumerable<V₁>, ICollection<V₁>, or IList<V₁> and U is a one-dimensional array type U₁[] (or a type parameter whose effective base type is U₁[]).
> VLADIMIR RESHETNIKOV Of course, this bullet (and the corresponding bullet in the next paragraph) mentions interfaces from namespace System.Collections.Generic.
  - V is the type V₁? and U is the type U₁?.
  - V is a constructed class, struct, interface, or delegate type C<V₁...Vₙ> and there is a unique type C<U₁...Uₙ> such that U (or, if U is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) C<U₁...Uₙ>.

(The “uniqueness” restriction means that in the case interface C<T>{ class U: C<X>, C<Y>{}, then no inference is made when inferring from U to C<T> because Uᵢ could be X or Y.)

> **VLADIMIR RESHETNIKOV** The same inference rule applies to constructed enum types. Although enum types cannot have type parameters in their declarations, they can still be generic if nested within a generic class or struct type.

If any of these cases apply, then an inference is made from each Uᵢ to the corresponding Vᵢ as follows:

- If Uᵢ is not known to be a reference type, then an *exact inference* is made.
- Otherwise, if U is an array type, then a *lower-bound inference* is made.
- Otherwise, if V is C<V₁...Vₙ>, then inference depends on the i-th type parameter of C:
  - If it is covariant, then a *lower-bound inference* is made.
  - If it is contravariant, then an *upper-bound inference* is made.
  - If it is invariant, then an *exact inference* is made.
- Otherwise, no inferences are made.

## 7.5.2.10 Upper-Bound Inferences

An upper-bound inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i, then U is added to the set of upper bounds for X_i.
- Otherwise, sets V₁...Vₙ and U₁...Uₙ are determined by checking if any of the following cases apply:
  - U is an array type Uᵢ[...] and V is an array type Vᵢ[...] of the same rank.
  - U is one of IEnumerable<Uᵢ>, ICollection<Uᵢ>, or IList<Uᵢ> and V is a one-dimensional array type Vᵢ[].
  - U is the type Uᵢ? and V is the type Vᵢ?.
