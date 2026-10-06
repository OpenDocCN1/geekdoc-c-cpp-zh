# ISO/IEC 14882:2017(E)

```
};
template<class T> struct A { X::Y ab; }; // OK
template<class T> struct A<T> { X::Y ab; }; // OK
// end example
```

A member of a class template may be declared a friend of a non-template class. In this case, the corresponding member of every specialization of the primary class and class template partial specializations is a friend of the class granting friendship. For explicit specializations and specializations of partial specializations, the corresponding member is the member (if any) that has the same name, kind (type, function, class template, or function template), template parameters, and signature as the member of the class template instantiation that would otherwise have been generated. [Example:

```
template<> T> struct A {
struct B {
void f();
struct D {
void g();
};
};
template<> struct A<int> {
struct B {
int f();
struct D {
void g();
};
}
```

```
class C {
template<class T> friend struct A<T>:::B; // grants friendship to A<int>::B even though
template<class T> friend void A<T>::f(); // it is not a specialization of A<T>::B
template<class T> friend void A<T>::D::g(); // because its return type does not match
template<class T> friend void A<T>::D::g(); // does not grant friendship to A<int>::g())
// because A<int>::D is not a specialization of A<T>::D
};
// end example
```

[Note: A friend declaration may declare a member of an namespace scope (17.6.5). — end note]

A friend template shall not be declared in a local class.

Friend declarations shall not declare partial specializations. [Example:

```
template<class T> class A {
class X {
template<class T> friend class A<T*>; // error
};
// end example
```

When a friend declaration refers to a specialization of a function template, the function parameter declaration shall not include default arguments, shall not be used in such a declaration.