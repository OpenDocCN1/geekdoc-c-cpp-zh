
# 13.5.2.3 Atomic constraints [temp.constr.atomic]

1 An atomic constraint is formed from an expression E and a mapping from the template parameters that appear within E to template arguments that are formed via substitution during constraint normalization in the declaration of a constrained entity (and, therefore, can involve the unsubstituted template parameters of the constrained entity), called the parameter mapping (13.5.3).

> [Note 1: Atomic constraints are formed by constraint normalization (13.5.4). E is never a logical AND expression (7.6.14) nor a logical OR expression (7.6.15). — end note]

2 Two atomic constraints, e1 and e2, are identical if they are formed from the same appearance of the same expression and if, given a hypothetical template A whose template-parameter-list consists of template-parameters corresponding and equivalent (13.7.7.2) to those mapped by the parameter mappings of the expression, a template-id naming A whose template-arguments are the targets of the parameter mapping of e1 is the same (13.6) as a template-id naming A whose template-arguments are the targets of the parameter mapping of e2.

> [Note 2: The comparison of parameter mappings of atomic constraints operates in a manner similar to that of declaration matching with alias template substitution (13.7.8).]

```
[Example 1:
template <unsigned N> constexpr bool Atomic = true;
template <unsigned N> concept C = Atomic<N>;
template <unsigned N> concept Add1 = C<N + 1>;
template <unsigned N> concept AddOne = C<N + 1>;
template <unsigned M> void f()
  requires Add1<2 * M>;
template <unsigned M> int f()
  requires AddOne<2 * M> && true;

int x = f<0>();      // OK, the atomic constraints from concept C in both fs are Atomic<N>
                    // with mapping similar to N ↦ 2 * M + 1

template <unsigned N> struct WrapN;
template <unsigned N> using Add1Ty = WrapN<N + 1>;
template <unsigned N> using AddOneTy = WrapN<N + 1>;
template <unsigned M> void g(Add1Ty<2 * M> *);
template <unsigned M> void g(AddOneTy<2 * M> *);

void h() {
  g<0>(nullptr);    // OK, there is only one g
}
— end example]
```

This similarity includes the situation where a program is ill-formed, no diagnostic required, when the meaning of the program depends on whether two constructs are equivalent, and they are functionally equivalent but not equivalent.

```
[Example 2:
template <unsigned N> void f2()
  requires Add1<2 * N>;
template <unsigned N> int f2()
  requires Add1<N * 2> && true;
void h2() {
  f2<0>();          // ill-formed, no diagnostic required:
}
```

Here, requires (!sad<typename T::type>) requires that there is a nested type that is not sad, whereas requires (!sad_nested_type<T>) requires that there is no sad nested type. — end example] — end note]

```
template <class T> int f3(T) requires (!sad<typename T::type>);
int i3 = f3(42);        // error: associated constraints not satisfied due to substitution failure

template <class T> concept sad_nested_type = sad<typename T::type>;
template <class T> int f4(T) requires (!sad_nested_type<T>);
int i4 = f4(42);        // OK, substitution failure contained within sad_nested_type
```

[Example 1:

```
template<typename T> concept C = true;
```

```
template<C T> void f1(T);
template<typename T> requires C<T> void f2(T);
template<typename T> void f3(T) requires C<T>;
```

The functions f1, f2, and f3 have the associated constraint C<T>.

```
template<typename T> concept C1 = true;
template<typename T> concept C2 = sizeof(T) > 0;
```

```
template<C1 T> void f4(T) requires C2<T>;
template<typename T> requires C1<T> && C2<T> void f5(T);
```

The associated constraints of f4 and f5 are C1<T> ∧ C2<T>.

```
template<C1 T> requires C2<T> void f6();
template<C2 T> requires C1<T> void f7();
```

The associated constraints of f6 are C1<T> ∧ C2<T>, and those of f7 are C2<T> ∧ C1<T>. — end example]

4 When determining whether a given introduced constraint-expression C₁ of a declaration in an instantiated specialization of a templated class is equivalent (13.7.7.2) to the corresponding constraint-expression C₂ of a declaration outside the class body, C₁ is instantiated. If the instantiation results in an invalid expression, the constraint-expressions are not equivalent.

[Note 1: This can happen when determining which member template is specialized by an explicit specialization declaration. — end note]

[Example 2:

```
template <class T> concept C = true;
template <class T> struct A {
  template <class U> U f(U) requires C<typename T::type>;   // #1
  template <class U> U f(U) requires C<T>;                  // #2
};
```

```
template <> template <class U>
U A<int>::f(U u) requires C<int> { return u; }           // OK, specializes #2
```

Substituting int for T in C<typename T::type> produces an invalid expression, so the specialization does not match #1. Substituting int for T in C<T> produces C<int>, which is equivalent to the constraint-expression for the specialization, so it does match #2. — end example]

# 13.5.4 Constraint normalization [temp.constr.normal]

1 The normal form of an expression E is a constraint (13.5.2) that is defined as follows:

+   (1.1) — The normal form of an expression ( E ) is the normal form of E.

+   (1.2) — The normal form of an expression E1 || E2 is the disjunction (13.5.2.2) of the normal forms of E1 and E2.

+   (1.3) — The normal form of an expression E1 && E2 is the conjunction of the normal forms of E1 and E2.

+   (1.4) — The normal form of a concept-id C<A₁, A₂, …, Aₙ> is the normal form of the constraint-expression of C, after substituting A₁, A₂, …, Aₙ for C’s respective template parameters in the parameter mappings in each atomic constraint. If any such substitution results in an invalid type or expression, the program is ill-formed; no diagnostic is required.

[Example 1:

```
template<typename T> concept A = T::value || true;
template<typename U> concept B = A<U*>;
template<typename V> concept C = B<V&>;
```

Normalization of B’s constraint-expression is valid and results in T::value (with the mapping T ↦ U*) ∨ true (with an empty mapping), despite the expression T::value being ill-formed for a pointer type T. Normalization of C’s constraint-expression results in the program being ill-formed, because it would form the invalid type V&* in the parameter mapping. — end example]

+   (1.5) — The normal form of any other expression E is the atomic constraint whose expression is E and whose parameter mapping is the identity mapping.

2  The process of obtaining the normal form of a *constraint-expression* is called *normalization*.

> [*Note 1*: Normalization of *constraint-expressions* is performed when determining the associated constraints (13.5.2) of a declaration and when evaluating the value of an *id-expression* that names a concept specialization (7.5.4). — *end note*]

> 3  [*Example 2*:

```
template<typename T> concept C1 = sizeof(T) == 1;
template<typename T> concept C2 = C1<T> && 1 == 2;
template<typename T> concept C3 = requires { typename T::type; };
template<typename T> concept C4 = requires (T x) { ++x; }

template<C2 U> void f1(U);       // #1
template<C3 U> void f2(U);       // #2
template<C4 U> void f3(U);       // #3
```

The associated constraints of #1 are sizeof(T) == 1 (with mapping T ↦ U) ∧ 1 == 2.
The associated constraints of #2 are requires { typename T::type; } (with mapping T ↦ U).
The associated constraints of #3 are requires (T x) { ++x; } (with mapping T ↦ U). — *end example*]

# 13.5.5  Partial ordering by constraints

1  A constraint *P subsumes* a constraint *Q* if and only if, for every disjunctive clause *Pᵢ* in the disjunctive normal form of *P*, *Pᵢ* subsumes every conjunctive clause *Qⱼ* in the conjunctive normal form of *Q*, where

+   (1.1) — a disjunctive clause *Pᵢ* subsumes a conjunctive clause *Qⱼ* if and only if there exists an atomic constraint *Pᵢₐ* in *Pᵢ* for which there exists an atomic constraint *Qⱼᵦ* in *Qⱼ* such that *Pᵢₐ* subsumes *Qⱼᵦ*, and
+   
+   (1.2) — an atomic constraint *A* subsumes another atomic constraint *B* if and only if *A* and *B* are identical using the rules described in 13.5.2.3.

> [*Example 1*: Let *A* and *B* be atomic constraints (13.5.2.3). The constraint *A ∧ B* subsumes *A*, but *A* does not subsume *A ∧ B*. The constraint *A* subsumes *A ∨ B*, but *A ∨ B* does not subsume *A*. Also note that every constraint subsumes itself. — *end example*]

2  [*Note 1*: The subsumption relation defines a partial ordering on constraints. This partial ordering is used to determine

+   (2.1) — the best viable candidate of non-template functions (12.4.4),
+   
+   (2.2) — the address of a non-template function (12.5),
+   
+   (2.3) — the matching of template template arguments (13.4.4),
+   
+   (2.4) — the partial ordering of class template specializations (13.7.6.3), and
+   
+   (2.5) — the partial ordering of function templates (13.7.7.3).
+   
+   — *end note*]

3  A declaration D1 is *at least as constrained* as a declaration D2 if

+   (3.1) — D1 and D2 are both constrained declarations and D1’s associated constraints subsume those of D2; or
+   
+   (3.2) — D2 has no associated constraints.

4  A declaration D1 is *more constrained* than another declaration D2 when D1 is at least as constrained as D2, and D2 is not at least as constrained as D1.

> [*Example 2*:

```
template<typename T> concept C1 = requires (T t) { --t; };
template<typename T> concept C2 = C1<T> && requires (T t) { *t; };

template<C1 T> void f(T);        // #1
template<C2 T> void f(T);        // #2
template<typename T> void g(T);  // #3
template<C1 T> void g(T);        // #4
```

134) A constraint is in disjunctive normal form when it is a disjunction of clauses where each clause is a conjunction of atomic constraints. For atomic constraints A, B, and C, the disjunctive normal form of the constraint A ∧ (B ∨ C) is (A ∧ B) ∨ (A ∧ C). Its disjunctive clauses are (A ∧ B) and (A ∧ C).

135) A constraint is in conjunctive normal form when it is a conjunction of clauses where each clause is a disjunction of atomic constraints. For atomic constraints A, B, and C, the constraint A ∧ (B ∨ C) is in conjunctive normal form. Its conjunctive clauses are A and (B ∨ C).
