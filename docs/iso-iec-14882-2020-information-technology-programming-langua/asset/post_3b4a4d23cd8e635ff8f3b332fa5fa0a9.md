
+   (3.2) — a string literal object (5.13.5),
+   (3.3) — the result of a typeid expression (7.6.1.8),
+   (3.4) — a predefined __func__ variable (9.5.1), or
+   (3.5) — a subobject (6.7.2) of one of the above.

4 [Example 1:

```
template<const int* pci> struct X { /* ... */ };
int ai[10];
X<ai> xi;    // array to pointer and qualification conversions

struct Y { /* ... */ };
template<const Y& b> struct Z { /* ... */ };
Y y;
Z<y> z;    // no conversion, but note extra cv-qualification

template<int (&pa)[5]> struct W { /* ... */ };
int b[5];
W<b> w;    // no conversion

void f(char);
void f(int);

template<void (*pf)(int)> struct A { /* ... */ };
A<&f> a;    // selects f(int)

template<auto n> struct B { /* ... */ };
B<5> b1;    // OK, template parameter type is int
B<'a'> b2;    // OK, template parameter type is char
B<2.5> b3;    // OK, template parameter type is double
B<void(0)> b4;    // error: template parameter type cannot be void
— end example]
```

5 [Note 2: A string-literal (5.13.5) is not an acceptable template-argument for a template-parameter of non-class type.

[Example 2:

```
template<class T, T p> class X {
    /* ... */
};

X<const char*, "Studebaker"> x; // error: string literal object as template-argument
X<const char*, "Knope" + 1> x2; // error: subobject of string literal object as template-argument

const char p[] = "Vivisectionist";
X<const char*, p> y;    // OK

struct A {
    constexpr A(const char*) {}
};

X<A, "Pyrophoricity"> z;    // OK, string-literal is a constructor argument to A
— end example]
— end note]
```

6 [Note 3: A temporary object is not an acceptable template-argument when the corresponding template-parameter has reference type.

[Example 3:

```
template<const int& CRI> struct B { /* ... */ };

B<1> b1;    // error: temporary would be required for template argument

int c = 1;
```

```
Y<C> yc;      // OK
Z<D> zd;      // OK
— end example]
```

[Example 3:

```
template <class T> struct eval;

template <template <class, class...> class TT, class T1, class... Rest>
struct eval<TT<T1, Rest...>> { };

template <class T1> struct A;
template <class T1, class T2> struct B;
template <int N> struct C;
template <class T1, int N> struct D;
template <class T1, class T2, int N = 17> struct E;
```

```
eval<A<int>> eA;      // OK: matches partial specialization of eval
eval<B<int, float>> eB;      // OK: matches partial specialization of eval
eval<C<17>> eC;      // error: C does not match TT in partial specialization
eval<D<int, 17>> eD;      // error: D does not match TT in partial specialization
eval<E<int, float>> eE;      // error: E does not match TT in partial specialization
```

— end example]

[Example 4:

```
template<typename T> concept C = requires (T t) { t.f(); };
template<typename T> concept D = C<T> && requires (T t) { t.g(); };

template<template<C> class P> struct S { };

template<C> struct X { };
template<D> struct Y { };
template<typename T> struct Z { };
```

```
S<X> s1;      // OK, X and P have equivalent constraints
S<Y> s2;      // error: P is not at least as specialized as Y
S<Z> s3;      // OK, P is at least as specialized as Z
```

— end example]

4 A template template-parameter P is at least as specialized as a template template-argument A if, given the following rewrite to two function templates, the function template corresponding to P is at least as specialized as the function template corresponding to A according to the partial ordering rules for function templates (13.7.7.3). Given an invented class template X with the template-head of A (including default arguments and requires-clause, if any):

+   (4.1) — Each of the two function templates has the same template parameters and requires-clause (if any), respectively, as P or A.
+   (4.2) — Each function template has a single function parameter whose type is a specialization of X with template arguments corresponding to the template parameters from the respective function template where, for each template parameter PP in the template-head of the function template, a corresponding template argument AA is formed. If PP declares a template parameter pack, then AA is the pack expansion PP... (13.7.4); otherwise, AA is the id-expression PP.

If the rewrite produces an invalid type, then P is not at least as specialized as A.

## 13.5 Template constraints [temp.constr]

### 13.5.1 General [temp.constr.general]

1 [Note 1: Subclause 13.5 defines the meaning of constraints on template arguments. The abstract syntax and satisfaction rules are defined in 13.5.2. Constraints are associated with declarations in 13.5.3. Declarations are partially ordered by their associated constraints (13.5.5). — end note]

## 13.5.2 Constraints [temp.constr.constr]

### 13.5.2.1 General [temp.constr.constr.general]

1 A *constraint* is a sequence of logical operations and operands that specifies requirements on template arguments. The operands of a logical operation are constraints. There are three different kinds of constraints:
- conjunctions (13.5.2.2),
- disjunctions (13.5.2.2), and
- atomic constraints (13.5.2.3).

2 In order for a constrained template to be instantiated (13.9), its associated constraints (13.5.3) shall be satisfied as described in the following subclauses.

> [Note 1: Forming the name of a specialization of a class template, a variable template, or an alias template (13.3) requires the satisfaction of its constraints. Overload resolution (12.4.3) requires the satisfaction of constraints on functions and function templates. — end note]

## 13.5.2.2 Logical operations [temp.constr.op]

1 There are two binary logical operations on constraints: conjunction and disjunction.

> [Note 1: These logical operations have no corresponding C++ syntax. For the purpose of exposition, conjunction is spelled using the symbol ∧ and disjunction is spelled using the symbol ∨. The operands of these operations are called the left and right operands. In the constraint A ∧ B, A is the left operand, and B is the right operand. — end note]

2 A *conjunction* is a constraint taking two operands. To determine if a conjunction is *satisfied*, the satisfaction of the first operand is checked. If that is not satisfied, the conjunction is not satisfied. Otherwise, the conjunction is satisfied if and only if the second operand is satisfied.

3 A *disjunction* is a constraint taking two operands. To determine if a disjunction is *satisfied*, the satisfaction of the first operand is checked. If that is satisfied, the disjunction is satisfied. Otherwise, the disjunction is satisfied if and only if the second operand is satisfied.

4 [Example 1:

```
template<typename T>
  constexpr bool get_value() { return T::value; }

template<typename T>
  requires (sizeof(T) > 1) && (get_value<T>())
    void f(T);      // has associated constraint sizeof(T) > 1 ∧ get_value<T>()

void f(int);

f('a'); // OK: calls f(int)
```

In the satisfaction of the associated constraints (13.5.3) of f, the constraint sizeof(char) > 1 is not satisfied; the second operand is not checked for satisfaction. — end example]

> 5 [Note 2: A logical negation expression (7.6.2.2) is an atomic constraint; the negation operator is not treated as a logical operation on constraints. As a result, distinct negation constraint-expressions that are equivalent under 13.7.7.2 do not subsume one another under 13.5.5. Furthermore, if substitution to determine whether an atomic constraint is satisfied (13.5.2.3) encounters a substitution failure, the constraint is not satisfied, regardless of the presence of a negation operator.

[Example 2:

```
template <class T> concept sad = false;

template <class T> int f1(T) requires (!sad<T>);
template <class T> int f1(T) requires (!sad<T>) && true;
int i1 = f1(42);        // ambiguous, !sad<T> atomic constraint expressions (13.5.2.3)
                       // are not formed from the same expression

template <class T> concept not_sad = !sad<T>;
template <class T> int f2(T) requires not_sad<T>;
template <class T> int f2(T) requires not_sad<T> && true;
int i2 = f2(42);        // OK, !sad<T> atomic constraint expressions both come from not_sad
```
