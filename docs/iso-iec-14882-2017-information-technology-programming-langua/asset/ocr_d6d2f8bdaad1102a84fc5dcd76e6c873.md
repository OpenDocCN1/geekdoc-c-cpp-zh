# ISO/IEC 14882:2017(E)

```
template<class T, class U>
struct Outer {
    template<class X, class Y> struct Inner<T, Y>;n    template<class Y> struct Inner<T, Y> {};
    template<class X> struct Inner<T, U> {};
}
```

Outer<int, int> out;
Outer<int, int>::Inner<int> is redeclared #1b. (It is not defined but noted as being associated with a definition in Outer<T, U>.) #2 is also a redeclaration of #1a. It is noted as associated with a definition, so it is an invalid redeclaration of the same partial specialization.

```
template<typename T> struct Friend f(int size_of(T));
    template<typename U> friend f(U);
ff;
```

Unless a member of a class template or a member template has been explicitly instantiated or explicitly specialized, the specialization of the member is implicitly instantiated when the specialization is referenced in a context that requires a definition; in particular, the initialization (and any associated side effects) of a static data member does not occur unless the static data member is used in a way that requires the definition of the static data member to exist.

Unless a function template specialization has been explicitly instantiated or explicitly specialized, the function template specialization is implicitly instantiated when the specialization is referenced in a context that requires a function definition; a function declaration from a friend function definition is implicitly instantiated when it is referenced in a context that requires a function definition to exist. Unless a call is a function template specialization or a member function of an explicitly specialized class template, a default argument for a function template or a member of a class template is implicitly instantiated when the function is called in a context that requires the value of the default argument.

5 | [Example]:

```
template<class T> struct Z {
    void f();
    void g();
    void h();};
```

```
void n() {
    Z<int> a;
    Z<char>* b;
    Z<double>* q;
```

```
a.f();
p->g();
}
```

Nothing in this example requires class Z<double>; Z<int>::f() is instantiated; Z<char>::g() is required, and instantiation of Z<char>::g() is required.

6 Unless a variable template specialization has been explicitly instantiated or explicitly specialized, the variable template specialization is implicitly instantiated when the specialization is used. A default template argument