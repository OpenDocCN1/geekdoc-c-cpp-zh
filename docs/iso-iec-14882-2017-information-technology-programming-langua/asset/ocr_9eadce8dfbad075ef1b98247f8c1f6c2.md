# ISO/IEC 14882:2017(E)

# 17.5.1.3 Static data members of class templates

A definition for a static data member or static data member template may be provided in a namespace enclosing the definition of the static member's class template. [Example:
```cpp
template<class T> class X {
    static T s;
};
template<class T> X>::s = 0;
struct limits {
    template<class T>
    static const T min;
};
template<class T>
    const T limits::min = {};
// end example
```

+   2 An explicit specialization of a static data member declared as an array of unknown bound can have a different bound from its definition, if any. [Example:
```cpp
template<class T> struct A {
    static int i[];
};
template<class T> int A<T>::i[4]; // 4 elements
template<> int A<int>::i = { 1 }; // OK: 1 element
// end example
```

# 17.5.1.4 Enumeration members of class templates

An enumeration member of a class template may be defined outside the class template definition. [Example:
```cpp
template<class T> struct A {
    enum E : T;
    static int a;
};
template<class T> enum A<T>::E : T { e1, e2 };
template<> int A<int>::a = A<int>::e1;
// end example
```

# 17.5.2 Member templates

+   1 A template can be declared within a class or class template; such a template is called a member template. A member template can be defined within or outside its class definition or class template definition. A member template of a class template that is defined outside its class template definition shall be specified with the template-parameters of the class template followed by the template-parameters of the member template. [Example:
```cpp
template<class T> struct string {
    template<class T2> int compare(const T2&);
    template<class T2> string(const T2& s) { /* ... */ }
};
template<class T> template<class T2> int string<T>::compare(const T2&) const {
}
// end example
```