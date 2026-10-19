

```
[Example 1:

Source file "X.h":

namespace Q {
  struct X { };
}

Source file "G.h":

namespace Q {
  void g_impl(X, X);
}

Module interface unit of M1:

module;
#include "X.h"
#include "G.h"
export module M1;
export template<typename T>
void g(T t) {
  g_impl(t, Q::X{ });    // ADL in definition context finds Q::g_impl, g_impl not discarded
}

Module interface unit of M2:

module;
#include "X.h"
export module M2;
import M1;
void h(Q::X x) {
  g(x);                   // OK
}

— end example
```

```
[Example 2:

Module interface unit of Std:

export module Std;
export template<typename Iter>
void indirect_swap(Iter lhs, Iter rhs)
{
  swap(*lhs, *rhs);       // swap not found by unqualified lookup, can be found only via ADL
}

Module interface unit of M:

export module M;
import Std;

struct S { /* ... */ };
void swap(S&, S&);        // #1

void f(S* p, S* q)
{
  indirect_swap(p, q);    // finds #1 via ADL in instantiation context
}

— end example
```

```
[Example 3:

Source file "X.h":

struct X { /* ... */ };
X operator+(X, X);

Module interface unit of F:

export module F;
```

## 13.9.2 Implicit instantiation [temp.inst]

1 A template specialization E is a declared specialization if there is a reachable explicit instantiation definition (13.9.3) or explicit specialization declaration (13.9.4) for E, or if there is a reachable explicit instantiation declaration for E and E is not

+   - an inline function,
+   - declared with a type deduced from its initializer or return value (9.2.9.6),
+   - a potentially-constant variable (7.7), or
+   - a specialization of a templated class.

> [Note 1: An implicit instantiation in an importing translation unit cannot use names with internal linkage from an imported translation unit (6.6). — end note]

2 Unless a class template specialization is a declared specialization, the class template specialization is implicitly instantiated when the specialization is referenced in a context that requires a completely-defined object type or when the completeness of the class type affects the semantics of the program.

> [Note 2: In particular, if the semantics of an expression depend on the member or base class lists of a class template specialization, the class template specialization is implicitly generated. For instance, deleting a pointer to class type depends on whether or not the class declares a destructor, and a conversion between pointers to class type depends on the inheritance relationship between the two classes involved. — end note]

[Example 1:

```
template<class T> class B { /* ... */ };
template<class T> class D : public B<T> { /* ... */ };

void f(void*);
void f(B<int>*);

void g(D<int>* p, D<char>** pp, D<double>* ppp) {
    f(p);            // instantiation of D<int> required: call f(B<int>*)
    B<char>* q = pp; // instantiation of D<char> required: convert D<char>** to B<char>*
    delete ppp;      // instantiation of D<double> required
}
```

— end example

If a class template has been declared, but not defined, at the point of instantiation (13.8.5.1), the instantiation yields an incomplete class type (6.8).

[Example 2:

```
template<class T> class X;
X<char> ch;        // error: incomplete type X<char>
```

— end example

> [Note 3: Within a template declaration, a local class (11.6) or enumeration and the members of a local class are never considered to be entities that can be separately instantiated (this includes their default arguments, noexcept-specifiers, and non-static data member initializers, if any, but not their type-constraints or requires-clauses). As a result, the dependent names are looked up, the semantic constraints are checked, and any templates used are instantiated as part of the instantiation of the entity within which the local class or enumeration is declared. — end note]

3 The implicit instantiation of a class template specialization causes

+   (3.1) — the implicit instantiation of the declarations, but not of the definitions, of the non-deleted class member functions, member classes, scoped member enumerations, static data members, member templates, and friends; and
+   (3.2) — the implicit instantiation of the definitions of deleted member functions, unscoped member enumerations, and member anonymous unions.

The implicit instantiation of a class template specialization does not cause the implicit instantiation of default arguments or noexcept-specifiers of the class member functions.

[Example 3:

```
template<class T>
struct C {
    void f() { T x; }
```

// instantiation of Z<char>::g() required
}
Nothing in this example requires class Z<double>, Z<int>::g(), or Z<char>::f() to be implicitly instantiated. — end example

7 Unless a variable template specialization is a declared specialization, the variable template specialization is implicitly instantiated when it is referenced in a context that requires a variable definition to exist or if the existence of the definition affects the semantics of the program. A default template argument for a variable template is implicitly instantiated when the variable template is referenced in a context that requires the value of the default argument.

8 The existence of a definition of a variable or function is considered to affect the semantics of the program if the variable or function is needed for constant evaluation by an expression (7.7), even if constant evaluation of the expression is not required or if constant expression evaluation does not use the definition.

[Example 6:

```
template<typename T> constexpr int f() { return T::value; }
template<bool B, typename T> void g(decltype(B ? f<T>() : 0));
template<bool B, typename T> void g(...);
template<bool B, typename T> void h(decltype(int{B ? f<T>() : 0}));
template<bool B, typename T> void h(...);
void x() {
  g<false, int>(0); // OK, B ? f<T>() : 0 is not potentially constant evaluated
  h<false, int>(0); // error, instantiates f<int> even though B evaluates to false and
                    // list-initialization of int from int cannot be narrowing
}
```

— end example

9 If the function selected by overload resolution (12.4) can be determined without instantiating a class template definition, it is unspecified whether that instantiation actually takes place.

[Example 7:

```
template <class T> struct S {
  operator int();
};

void f(int);
void f(S<int>&);
void f(S<float>);

void g(S<int>& sr) {
  f(sr); // instantiation of S<int> allowed but not required
         // instantiation of S<float> allowed but not required
};
```

— end example

10 If a function template or a member function template specialization is used in a way that involves overload resolution, a declaration of the specialization is implicitly instantiated (13.10.4).

11 An implementation shall not implicitly instantiate a function template, a variable template, a member template, a non-virtual member function, a member class, a static data member of a class template, or a substatement of a constexpr if statement (8.5.2), unless such instantiation is required.

[Note 5: The instantiation of a generic lambda does not require instantiation of substatements of a constexpr if statement within its compound-statement unless the call operator template is instantiated. — end note]

It is unspecified whether or not an implementation implicitly instantiates a virtual member function of a class template if the virtual member function would not otherwise be instantiated. The use of a template specialization in a default argument shall not cause the template to be implicitly instantiated except that a class template may be instantiated where its complete type is needed to determine the correctness of the default argument. The use of a default argument in a function call causes specializations in the default argument to be implicitly instantiated.

12 Implicitly instantiated class, function, and variable template specializations are placed in the namespace where the template is defined. Implicitly instantiated specializations for members of a class template are

