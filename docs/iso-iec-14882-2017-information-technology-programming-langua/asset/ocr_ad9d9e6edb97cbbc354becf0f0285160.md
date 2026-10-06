# ISO/IEC 14882:2017(E)

```
A* p1;                                // A is the current instantiation
<A>* p2;                               // <A> is the current instantiation
<A>* p3;                               // <A> is not the current instantiation
::<A>* p4;                              // ::<A> is the current instantiation
class B {
    B* p1;                               // B is the current instantiation
    <A>::B* p2;                            // <A>:B is the current instantiation
    typename A<T>::B* p3;               // A<T>::B is not the current instantiation
};

template <class T> class A<T> {
    A* p1;                                // <A> is the current instantiation
    <A>* p2;                                // <A> is not the current instantiation
};

template <class T1, class T2, int> struct B {
    BT1, I* B1;                             // refers to the current instantiation
    BT2, I* B2;                             // not the current instantiation
    typedef int my_I;
    static const int my_I = I0;
    static const int my_I2 = I0;
    static const int my_I3 = my_I;
    BnT1, T2, my2 = B3;                     // refers to the current instantiation
    BnT1, T2, my2 = B4;                     // not the current instantiation
    BnT1, T2, my13 = B5;                    // refers to the current instantiation
};
```

-- end example

+   4 A dependent base class is a class that is a dependent type and is not the current instantiation. [Note: A base class can be the current instantiation in the case of a nested class enclosing such a base. [Example:

```
template<T> struct A {
    typedef int M;
    struct B {
        typedef void M;
        struct C;
    };

template<T> struct A<T>::B : A<T> {
    M;
};

// OK, A<T>:::M
```

-- end example

+   5 A name is a member of the current instantiation if it is

+   (5.1) An unqualified name that, when looked up, refers to at least one member of a class that is the current instantiation or a non-dependent base class. [Note: This can only occur when looking up a name in a scope defined by the definition of a class template. -- end note]

+   (5.2) A qualified-id in which the named-name-specifier refers to the current instantiation and, when looked up, refers to at least one member of a class that is the current instantiation or a non-dependent base class thereof. [Note: If no member is found, and the current instantiation has any dependent base classes, then the qualified-id is a member of an unknown specialization; see below. -- end note]