# ISO/IEC 14882:2017(E)

6 A member of an explicitly specialized class is not implicitly instantiated from the member declaration of the class template; instead, the member of the class template specialization itself be explicitly defined if its definition is required. In this case, the definition of the class template specialization shall be in scope at the point at the member is defined. The definition of an explicitly specialized class is unrelated to the definition of a generated specialization. That is, members need not have the same names, types, etc. as the members of a generated specialization. Members of an explicitly specialized class are defined in the same manner as members of normal classes, and not using the template<> syntax. The same is true when defining a member of an explicitly specialized member class. However, template<> is used in defining a member of an explicitly specialized member class template that is specialized as a class template. [Example:

```
template<> struct A {
    struct B;
    template<class D> struct C { };
}
```

```
template<> struct A<int> {
    void f(int);
};
```

```
void h() {
    A<int> a;
    a.f(16); // A<int>::f must be defined somewhere
}
```

```
// template<> not used when defining a member of an explicitly specialized member class template
void A<int>::f(int) { /* ... */ }
```

```
template<> struct A<char>:B {
    void f();
};
```

```
// template<> is used when defining a member of an explicitly specialized member class template
void A<char>::B::f() { /* ... */ }
```

```
template<> template<class D> struct A<char>::C {
    void f();
};
```

```
// template<> specialized as a class template
template<> class<class U> void A<char>::C::f() { /* ... */ }
```

```
template<> struct A<short>:B {
    void f();
};
```

```
void A<short>::B::f() { /* ... */ } // error: template<> not permitted
```

```
template<> template<class U> struct A<short>::C {
    void f();
};
```

```
void A<short>::C::f() { /* ... */ } // error: template<> required
// end example]
```

6 If a template, a member or member of a class template is explicitly specialized then before the first use of that specialization that would cause an implicit instantiation to take place, in every translation unit in which such a use occurs; no diagnostic is required. If