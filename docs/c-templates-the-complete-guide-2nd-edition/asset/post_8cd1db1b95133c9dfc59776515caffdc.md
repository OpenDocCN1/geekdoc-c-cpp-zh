
```cpp
namespace N {
    class X {
        ...
    };

    template<int I> void select(X*);
}

void g (N::X* xp)
{
    select<3>(xp);  // ERROR: no ADL!
}
```

```cpp
template<typename T> void select();
```

```cpp
template<typename T> void typeDependent1(T x)
{
    x;      // the expression type-dependent, because the type of x can vary
}
```

```cpp
template<int N> void valueDependent1()
{
    N;      // the expression is value-dependent but not type-dependent,
            // because N has a fixed type but a varying constant value
}
```

```cpp
template<typename T> void valueDependent2(T x)
{
    sizeof(x);  // the expression is value-dependent but not type-dependent
}
```

```cpp
template<typename T> void maybeDependent(T const& x)
{
    sizeof(sizeof(x));
}
```

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_1567_0.png)

```cpp
void f() { }

template<int x> void nondependentCall()
{
    f(x);    // x is value-dependent, so f() is nondependent;
             // this call will never succeed
}
```

```cpp
template<int N> void instantiationDependentBound()
{
    constexpr int x = sizeof(N);
    constexpr int y = sizeof(N) + 1;
    int array[x - y];  // array will have a negative size in all instantiations
}
```

```cpp
template<typename X>
class Base {
    public:
        int basefield;
        using T = int;
};

class D1: public Base<Base<void>> {  // not a template case really
    public:
        void f() { basefield = 3; }      // usual access to inherited member
};

template<typename T>
class D2 : public Base<double> {     // nondependent base
    public:
        void f() { basefield = 7; }     // usual access to inherited member
        T strange;                      // T is Base<double>::T, not the template parameter!
};
```

```cpp
template<typename T>
class DD : public Base<T> {    // dependent base
    public:
        void f() { basefield = 0; }  // #1 problem...
};

template<>  // explicit specialization
class Base<bool> {
    public:
        enum { basefield = 42 };    // #2 tricky!
};

void g (DD<bool>& d)
{
    d.f();
                            // #3 oops?
}
```

```cpp
// Variation 2:
template<typename T>
class DD2 : public Base<T> {
    public:
        void f() { Base<T>::basefield = 0; }
};
```

```cpp
template<typename T>
class B {
    public:
        enum E { e1 = 6, e2 = 28, e3 = 496 };
        virtual void zero(E e = e1);
        virtual void one(E&);
};

template<typename T>
class D : public B<T> {
    public:
        void f() {
            typename D<T>::E e;    // this->E would not be valid syntax
            this->zero();          // D<T>::zero() would inhibit virtuality
            one(e);                // one is dependent because its argument
                                   // is dependent
        }
};
```

```cpp
// Variation 3:
template<typename T>
class DD3 : public Base<T> {
    public:
        using Base<T>::basefield;    // #1 dependent name now in scope
        void f() { basefield = 0; }  // #2 fine
};
```

```cpp
template<typename T> class C;  // #1 declaration only

C<int>* p = 0;  // #2 fine: definition of C<int> not needed

template<typename T>
class C {
    public:
        void f();  // #3 member declaration
};  // #4 class template definition completed

void g (C<int>& c)  // #5 use class template declaration only
{
    c.f();  // #6 use class template definition;
            //   will need definition of C::f()
            //   in this translation unit
}

template<typename T>
void C<T>::f()  // required definition due to #6
{
}
```

```cpp
template<typename T>
class C {
    public:
        C(int);         // a constructor that can be called with a single parameter
};
                        // may be used for implicit conversions

void candidate(C<double>);  // #1
void candidate(int) { }     // #2

int main()
{
    candidate(42);  // both previous function declarations can be called
}
```

```cpp
template<typename T> class Q {
    using Type = typename T::Type;
};

Q<int>* p = 0;      // OK: the body of Q<int> is not substituted
```

details/lazy1.hpp

```cpp
template<typename T>
class Safe {
};

template<int N>
class Danger {
    int arr[N];                // OK here, although would fail for N<=0
};

template<typename T, int N>
class Tricky {
public:
    void noBodyHere(Safe<T> = 3); // OK until usage of default value results in an error
    void inClass() {
        Danger<N> noBoomYet;     // OK until inClass() is used with N<=0
    }
    struct Nested {
        Danger<N> pfev;          // OK until Nested is used with N<=0
    };
    union {
                            // due anonymous union:
        Danger<N> anonymous;    // OK until Tricky is instantiated with N<=0
        int align;
    };
    void unsafe(T (*p)[N]);     // OK until Tricky is instantiated with N<=0
    void error() {
        Danger<-1> boom;        // always ERROR (which not all compilers detect)
    }
};
```

details/lazy2.cpp

```cpp
template<typename T>
class VirtualClass {
  public:
    virtual ~VirtualClass() {}
    virtual T vmem(); // Likely ERROR if instantiated without definition
};

int main()
{
  VirtualClass<int> inst;
}
```

```cpp
namespace N {
    template<typename> void g() {}
    enum E { e };
}

template<typename> void f() {}

template<typename T> void h(T p) {
    f<int>(p);  // #1
    g<int>(p);  // #2 ERROR
}

int main() {
    h(N::e);    // calls template h with T = N::E
}
```

```cpp
class MyInt {
    public:
        MyInt(int i);
};

MyInt operator - (MyInt const&);

bool operator > (MyInt const&, MyInt const&);

using Int = MyInt;

template<typename T>
void f(T i)
{
    if (i>0) {
        g(-i);
    }
}
// #1
void g(Int)
{
    // #2
    f<Int>(42);  // point of call
    // #3
}
// #4
```

```cpp
template<typename T>
void f1(T x)
{
    g1(x);  // #1
}

void g1(int)
{
}

int main()
{
    f1(7);  // ERROR: g1 not found!
}
// #2 POI for f1<int>(int)
```

```cpp
template<typename T>
class S {
    public:
        T m;
};
// #1
unsigned long h()
{
    // #2
    return (unsigned long)sizeof(S<int>);
    // #3
}
// #4
```

```cpp
template<typename T>
class S {
public:
    using I = int;
};

// #1
template<typename T>
void f()
{
    S<char>::I var1 = 41;
    typename S<T>::I var2 = 42;
}

int main()
{
    f<double>();
}
// #2: #2a, #2b
```

```cpp
// ===== t.hpp:
// common header (inclusion model)
template<typename T>
class S {
    public:
        void f();
};

template<typename T>
void S<T>::f()    // member definition
{
}

void helper(S<int>*);

// ===== a.cpp:
#include "t.hpp"

void helper(S<int>* s)
{
    s->f();    // #1 first point of instantiation of S::f
}

// ===== b.cpp:
#include "t.hpp"

int main()
{
    S<int> s;
    helper(&s);
    s.f();    // #2 second point of instantiation of S::f
}
```

```cpp
template<typename T>
void f(T)
{
}
```

```cpp
// four valid explicit instantiations:
template void f<int>(int);
template void f<>(float);
template void f(long);
template void f(char);
```

```cpp
template<typename T>
class S {
    public:
        void f() {
        }
};

template void S<int>::f();

template class S<void>;
```

```cpp
// ===== translation unit 1:
template<typename T> void f(); // no definition: prevents instantiation
// in this translation unit
void g()
{
    f<int>();
}

// ===== translation unit 2:
template<typename T> void f()
{
    // implementation
}

template void f<int>();     // manual instantiation

void g();

int main()
{
    g();
}
```

```cpp
//——— f.hpp:
template<typename T> void f(); // no definition: prevents instantiation

//——— t.hpp:
#include "f.hpp"
template<typename T> void f()  // definition
{
    // implementation
}

//——— f.cpp:
#include "t.hpp"

template void f<int>();      // manual instantiation
```
