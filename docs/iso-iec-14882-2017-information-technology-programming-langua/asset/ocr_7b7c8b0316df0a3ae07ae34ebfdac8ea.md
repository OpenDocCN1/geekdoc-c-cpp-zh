# ISO/IEC 14882:2017(E)

```
void h(char,int);
int m() {
 f(kg);      // error: ambiguous
 f(kh);      // OK: void h(char,int) is a unique match
f(koo);     // error: type deduction fails because foo is a template
}
```

// end example

20 A template-type-parameter cannot be deduced from the type of a function default argument. [Example:

```
template <class T> void f(T = 5, T = 7);
void g() {
 f(1);\      // OK: call f<int>(1,7)
 f();       // error: cannot deduce T
 f(int());  // OK: call f<int>(5,7)
}
```

// end example

21 The template-type corresponding to a template-parameter is deduced from the template-argument of a class template used in the argument list of a function call. [Example:

```
template <class T> class X struct A {};
template <class T> class X<T> void f(X<T> {});
template <class T> class X<T> struct B {};
A<B> ab;
f(A<B>);
```

// end example

22 [Note: Argument deduction involving parameter packs (17.5.3) can deduce zero or more arguments for each parameter. — end example]

```
template<class> struct X {};
template<class A, class ArgsTypes> struct X(int, ArgsTypes...) {};
template<class...> class Types {};
template<class T, class... Types> struct Y(T, Types&...) { {};
```

```
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

In a case where declaration-id refers to a specialization of a template, template argument deduction is performed to identify the specialization to which the declaration refers. Specifically, this is done for explicit specializations (17.7.2), explicit specializations (17.7.3), and friend friend declarations (17.5.4). This is also done to determine whether a deduction template specialization matches a pattern operator (17.4.2, 8.3.4). In all cases, F is the type of function considered as a potential match and A is the function from the declaration or the type of the deallocation function that would match the placement operator new as described in 8.3.4. The deduction is done as