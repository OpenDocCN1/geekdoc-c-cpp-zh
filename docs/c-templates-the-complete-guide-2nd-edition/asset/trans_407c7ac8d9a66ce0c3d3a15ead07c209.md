

```
template<typename T, typename... Types>
void g(Types... values) {
    T v(values...);
}
```

```
bool and_all() { return true; }
template<typename T>
  bool and_all(T cond) { return cond; }
template<typename T, typename... Ts>
  bool and_all(T cond, Ts... conds) {
    return cond && and_all(conds...);
  }
```

```
template<typename... T> bool g() {
    return and_all(trait<T>()...);
}
```

```
template<typename... T> bool g() {
    return (trait<T>() && ... && true);
}
```

```
template<typename T>
class Tree {
    friend class Factory;  // OK even if first declaration of Factory
    friend class Node<T>;  // error if Node isn't visible
};
```

```
```cpp
template<typename T1, typename T2>
void combine(T1, T2);

class Mixer {
    friend void combine<>(int&, int&);
                              // OK: T1 = int&, T2 = int&
    friend void combine<int, int>(int, int);
                              // OK: T1 = int, T2 = int
    friend void combine<char>(char, int);
                              // OK: T1 = char T2 = int
    friend void combine<char>(char&, int);
                              // ERROR: doesn't match combine() template
    friend void combine<>(long, long) { ... }
                              // ERROR: definition not allowed!
};
```
```

```
```cpp
void multiply(void*);        // ordinary function

template<typename T>
void multiply(T);             // function template

class Comrades {
    friend void multiply(int) { }
                         // defines a new function ::multiply(int)

    friend void ::multiply(void*);
                         // refers to the ordinary function above,
                         // not to the multiply<void*> instance

    friend void ::multiply(int);
                         // refers to an instance of the template

    friend void ::multiply<double*>(double*);
                         // qualified names can also have angle brackets,
                         // but a template must be visible

    friend void ::error() { }
                         // ERROR: a qualified friend cannot be a definition
};
```
```

```
template<typename T>
class Node {
    Node<T>* allocate();
    ...
};

template<typename T>
class List {
    friend Node<T>* Node<T>::allocate();
    ...
};
```

```
template<typename T>
class Creator {
    friend void feed(Creator<T>) { // every T instantiates a different function ::feed()
        ...
    }
};

int main()
{
    Creator<void> one;
    feed(one);                     // instantiates ::feed(Creator<void>)
    Creator<double> two;
    feed(two);                     // instantiates ::feed(Creator<double>)
}
```

```
int x;

class B {
    public:
        int i;
};

class D : public B {
};

void f(D* pd)
{
    pd->i = 3;  // finds B::i
    D::x = 2;   // ERROR: does not find ::x in the enclosing scope
}
```

```
```cpp
extern int count;                          // #1

int lookup_example(int count)              // #2
{
    if (count < 0) {
        int count = 1;                      // #3
        lookup_example(count);              // unqualified count refers to #3
    }
    return count + ::count;                 // the first (unqualified) count refers to #2;
                                            // the second (qualified) count refers to #1
}
```
```

```
namespace BigMath {
    class BigNumber {
        ...
    };
    bool operator < (BigNumber const&, BigNumber const&);
    ...
}

using BigMath::BigNumber;

void g (BigNumber const& a, BigNumber const& b)
{
    ...
    BigNumber x = ::max(a,b);
    ...
}
```

details/adl.cpp

```
#include <iostream>

namespace X {
    template<typename T> void f(T);
}

namespace N {
    using namespace X;
    enum E { e1 };
    void f(E) {
        std::cout << "N::f(N::E) called\n";
    }
}

void f(int)
{
    std::cout << "::f(int) called\n";
}

int main()
{
    ::f(N::e1);    // qualified function name: no ADL
    f(N::e1);      // ordinary lookup finds ::f() and ADL finds N::f(),
                  // the latter is preferred
}
```

```
template<typename T>
class C {
    ...
    friend void f();
    friend void f(C<T> const&);
    ...
};

void g (C<int>* p)
{
    f();    // is f() visible here?
    f(*p);  // is f(C<int> const&) visible here?
}
```

```
```cpp
details/inject.cpp

#include <iostream>

int C;
class C {
  private:
    int i[2];
  public:
    static int f() {
      return sizeof(C);
    }
};

int f()
{
        return sizeof(C);
}

int main()
{
    std::cout << "C::f() = " << C::f() << ','
              << " ::f() = " << ::f() << '\n';
}
```
```

```
```cpp
template<template<typename> class TT> class X {
};

template<typename T> class C {
    C* a;        // OK: same as “C<T>* a;”
    C<void>& b;  // OK
    X<C> c;      // OK: C without a template argument list denotes the template C
    X<::C> d;    // OK: ::C is not the injected class name and therefore always
                 //     denotes the template
};
```
```

```
```cpp
template<int I, typename... T> class V {
    V* a;          // OK: same as "V<I, T...>* a;"
    V<0, void> b;  // OK
};
```
```

```
template<typename T> class C {
    using Type = T;

    struct I {
        C* c;               // C refers to a current instantiation
        C<Type>* c2;        // C<Type> refers to a current instantiation
        I* i;               // I refers to a current instantiation
    };
    struct J {
        C* c;               // C refers to a current instantiation
        C<Type>* c2;        // C<Type> refers to a current instantiation
        I* i;               // I refers to an unknown specialization,
                            // because I does not enclose J
        J* j;               // J refers to a current instantiation
    };
};
```

```
template<> struct C<int>::I {
    // definition of the specialization
};
```

```
template<bool B>
class Invert {
    public:
        static bool const result = !B;
};

void g()
{
    bool test = Invert<(1>0)>::result;  // parentheses required!
}
```

```
List<List<int>> a;
// ^-- no space between right angle brackets
```

names/anglebrackethack.cpp

```
#include <iostream>

template<int I> struct X {
    static int const c = 2;
};

template<> struct X<0> {
    typedef int c;
};

template<typename T> struct Y {
    static int const c = 3;
};

static int const c = 4;

int main()
{
    std::cout << (Y<X<1> >::c >::c::c) << ' ';
    std::cout << (Y<X< 1>>::c >::c::c) << '\n';
}
```

```
template<typename T> struct G {};
struct S;
G<::S> gs;    // valid since C++11, but an error before that
```

```
template<typename₁ T>
struct S : typename₂ X<T>::Base {
    S() : typename₃ X<T>::Base(typename₄ X<T>::Base(0)) {
    }
    typename₅ X<T> f() {
        typename₆ X<T>::C * p;    // declaration of pointer p
        X<T>::D * q;             // multiplication!
    }
    typename₇ X<int>::C * s;

    using Type = T;
    using OtherType = typename₈ S<T>::Type;
};
```

```
template<typename T>
class Shell {
    public:
        template<int N>
        class In {
            public:
                template<int M>
                class Deep {
                    public:
                    virtual void f();
                };
        };
};

template<typename T, int N>
class Weird {
    public:
        void case1 (
            typename Shell<T>::template In<N>::template Deep<N>* p) {
        p->template Deep<N>::f();  // inhibit virtual call
    }
}
```

```
template<typename T>
class BXT {
    public:
        using Mystery = T;
        template<typename U>
        struct Magic;
};

template<typename T>
class DXTT : private BXT<T> {
    public:
        using typename BXT<T>::Mystery;
        Mystery* p;  // would be a syntax error without the earlier typename
};
```

