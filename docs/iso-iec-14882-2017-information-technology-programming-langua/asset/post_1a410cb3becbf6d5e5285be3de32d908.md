
# ISO/IEC 14882:2017(E)

```cpp
D<int> d;
D2 d2;
f(d);      // calls f(B<int>&)
f(D2);      // calls f(B<int>&)
}
```

// end example

A template argument T, a template argument TT or a template non-type argument i can be deduced if P and A have one of the following:

```cpp
T
const T
T*
T&
T&&
(T<integer-constant<T>>) // (where template-name refers to a class template)
type(T)
T(T)
T T::*
type T::*
T T::*
T (type::*)())
type (type::*)()
type (type::*) (T)
type (type::*) (T)
T (type::*) (T)
T (type::*) (T)

T (type::*) (T)
```

```cpp
[list1]
template-name-<i> // (where template-name refers to a class template)
TT<T>
TT<>>
```

where (T) represents a parameter-type-list (11.3.5) where no parameter type contains a T. Similarly, <...> represents template argument lists where at least one argument contains a T, <...> represents template argument lists where at least one argument contains a T, <> represents template argument lists where no arguments contain a T or i.

If P has a form that contains <> or <>, then each argument P_i of the template argument list P is compared with the argument A_i of the corresponding argument list of A. If the argument list of P contains a pack expansion that is not the last argument, the entire argument list is a non-deduced context. If P_i is a pack expansion, then the pattern of P is compared with each remaining argument in the template argument list of A. Each deduction template arguments for subsequent positions in the template parameter packs expanded by P_i, partial ordering (17.8.2.4), if A_i, was originally a pack expansion:

- if P does not contain a template argument to A_i, then A_i is ignored;
- otherwise, if P_i is not a pack expansion, template argument deduction fails.

Example:

```cpp
template<class T1, class... Z> class S<T1, const Z&...> { }; // #1
template<class T1, class... Z> class S<T1, const Z&...> {}; // #2
```

# ISO/IEC 14882:2017(E)

```cpp
template<class T1, class T2> class S<T1, const T2> { }; // #3
int s, const int& s; // both #2 and #3 match; #3 is more specialized
```

```cpp
template<class T, class...> struct A { }; // #1
template<class T1, class T2, class...> struct A<T1, T2, U...> { }; // #2
template<class T1, class T2> struct A<T1, T2> { }; // #3
template struct A<int*>; // selects #2
```

— example
10. Similarly if P has a form that contains (T), then parameter type P_i of the respective parameter-type-list (11.5) of P is compared with the parameter type A_i of A. If P and A_i are types originated during the deduction of the address of a function (17.8.2.2) or when deducting template arguments from a function (17.8.2.6) and P_i and A_i are parameters of the top-level parameter-type of P and A_i, respectively, P_i is adjusted if it is changed to the template type (i.e. T& is changed to simply T). [Note: As a result, when P_i is adjusted the adjusted P_i, will to be deduced as T_i, where T_i and A_i are.] — end example:

```cpp
template<class T> void f(T&);
template<class T> void f(int) { // #1
template<class T> void f(int*) { // #2
void g(int i) {
  f(i);
}
//
  calls f<int>(int, i.e., #1
  calls f<int>(int, i.e., #2
```

— example
If the parameter-declaration corresponding to P is a function parameter pack, then type of its declaration-id is compared with each remaining parameter type in the parameter-type of A. Each comparison deduction template arguments for subsequent positions in the template packs expanded by the function parameter pack. During partial ordering (17.8.2.4), if A_i was originally a function parameter pack:

- if P does not contain a function pack type corresponding to A_i, then A_i, is ignored;
- otherwise, if P, is not a function parameter pack, template argument deduction fails.

Example:
template<class T,...> void f(T, U...) {} // #1
template<class T> void f(T) {} // #2
void f(int*) { // selects #1

— example
11. These forms can be used in the same way as T is for composition of types. [Example:
int* (char[6]) is of the form

```cpp
template_name<T> (type)
which is a variant of
type (*int) and T is char[6]. — end example
12 Template arguments cannot be deduced from function arguments than the one specified above.
13. When the value of the argument concerning a non-type parameter P that is declared with an expression, the template parameters in the type of P are deduced from the type of the value. [Example:

```cpp
template<long n> struct A {
template<typename T> struct C;
template<typename T, int n> struct CC<n> {
    using Q = T;
};
using R = long; // OK: T was deduced from long
using R = CC<n>::Q; // template argument in the type A<n> is size_t. [Example:
```cpp
template<typename T> struct;
template<typename T, int n> struct CC<n> {
    using Q = T;
}
using V = decltype(sizeof(O));
using V = CC<2>::Q; // OK: T was deduced from int[2]
```
14 Example:
```cpp
template<class T, int i> void f(int[i]);
int v[10];
void g() {
    f(v);
}
// end example
```
15 [Note: Except for reference and pointer types, a major array is not part of a function parameter type and cannot be deduced from argument:

```cpp
template<int i> void f1(int[10][i]);
template<int i> void f2(int[i][20]);
template<int i> void f3(int (a)[20]);

void g() {
    int v[10][20]; // i was deduced to 20
    f1(v); // OK
    f2(v); // error: cannot deduce-template argument 1
    f3(v); // OK: i was deduced to 10
}
// end note
```
16 [Note: If, in the declaration of a template function with a non-type parameter, the template parameter is used in a subexpression in the function parameter list, the expression is a non-deduced context as seen above. [Example:

```cpp
template<int i> class A { /* ... };
template<int i> void g(A<i+1>);
template<int i> void f(A<i+1>, A<i+1>);
```

# ISO/IEC 14882:2017(E)

```cpp
void k() {
<int> a1;
<int> a2;

g(a1);          // error: deduction fails for expression i+1
f<double>(a1);  // OK
f(a1, a2);      // OK
} // end example --

[ Note: Template parameters do not participate in template argument deduction if they are used only in non-deduced contexts. For example,
template<int, typename T>
deduce<(typename A<T>):: x,
T;                // T is not deduced here
typename B::y;   // T is deduced here
<int> a;
B<77> b;

int x = deduce<77>(a.x, b.y);
 // T is deduced to be int, a.x must be convertible to A<int>::x
 // T is explicitly specified to be 77, b.y must be convertible to B<77>:: -- end note

If P has a form that contains <i>, and if the type of i differs from the type of the corresponding template parameter deduction fails. If P has a form that contains [<i], and if the type of i is not an integral type, deduction fails. [ Example:
template<int> class A { / ... *; };
template<short s> void g(B<a>);
void k() {
<int> a;
f(a);
f<i>(a); // error: deduction fails for conversion from int to short
} // end example

A template-argument can be deduced from a function, pointer to function, or pointer to member function type.
[Example:
template<class T> void f(void(*T,int));
template<class T> void foo(T,int);
void g(int,int);
g(char,int);

void h(int,int,int); // The template name corresponding to a template-parameter of type may be deduced from an array bound, the resulting value will always be true because the array bound will be nonzero.

> 142 The template-argument corresponding to a template-parameter of type may be deduced from an array bound, the resulting value will always be true because the array bound will be nonzero.

# ISO/IEC 14882:2017(E)

```cpp
void h(char,int); // The template name corresponding to a template-parameter of type may be deduced from an array bound, the resulting value will always be true because the array bound will be nonzero.
void g() {
f(kg);      // error: ambiguous
f(kh);      // OK: void h(char,int)
f(koo);     // error: type foo is a template
}
```

#IEC 14882:017(E)

20 A-type-parameter cannot be deduced from a function default argument. [Example:

```cpp
template<class T> void f(T = 5, T = 7);
void g() {
f(1); // OK: call f<int>(5,7)
f(); // error: cannot deduce T
f(int()); // OK: call f<int>(5,7)
}
```
// end example

21 The template-argument corresponding to a template-parameter is deduced from the template-argument of a class template used in a function call. [Example:

```cpp
template<class T> class X A {};
template<class T> class X<T> void f(X<T> {});
template <class T> class X<T> struct B {};
A<B> ab;
f(A<B>);
```
// end example (Wait, the OCR text has some garble in the later parts, let me re-align based on the provided flow)

Re-aligning page 429-430:
22 [Note: Argument deduction involving parameter packs (17.5.3) can deduce zero or more arguments for each parameter. — end example

```cpp
template<class> struct X {};
template<class A, class ArgsTypes> struct X(int, ArgsTypes...) {};
template<class...> class Types {};
template<class T, class... Types> struct Y(T, Types&...) { {};
```

```cpp
template<class...> void f(void(Types...));
Xint x1;
X(int, float, double) x2; // uses primary specialization; ArgTypes contains float, double
X(int, hot) x3; // uses primary template; Types is empty
Y(int, float, double) y2; // uses partial specialization; T is int; Types contains float, double
int f = f(y); // uses primary template; Types contains int, float
// OK: call f contains int
```
// end example

# 17.8.2.6 Deducing arguments from a function declaration [temp.deduct].

In a case where declaration-id refers to a specialization of a template, template argument deduction is performed to identify the specialization to which the declaration refers. Specifically, this is done for explicit specializations (17.7.2), explicit specializations (17.7.3), and friend friend declarations (17.5.4). This is also done to determine whether a deduction specialization matches a pattern operator (17.4.2, 8.3.4). In all cases, F is the type of function considered as a potential match and A is the function from the declaration or the type of the deallocation function that would match the placement operator new as described in 8.3.4. The deduction is done as
