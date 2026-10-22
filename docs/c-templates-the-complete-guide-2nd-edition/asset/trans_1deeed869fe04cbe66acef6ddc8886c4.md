

```
template<typename R = void, typename T>
R* addressof(T& value);  // OK: if not explicitly specified, R will be void
```

```
template<typename T = void>
class Value;

template<typename T = void>
class Value;  // ERROR: repeated default argument
```

```
template<typename T>
class C;
...
template<typename T = int>
class C<T*>;            // ERROR
```

```
template<typename... Ts = int> struct X;    // ERROR
```

```
struct S {
    template<typename = void> friend void f();    // ERROR: not a definition
    template<typename = void> friend void g() {    // OK so far
    }
};
template<typename> void g();    // ERROR: g() was given a default template argument
                                 // when defined; no other declaration may exist here
```

details/implicit.cpp

```
template<typename DstT, typename SrcT>
DstT implicit_cast (SrcT const& x)  // SrcT can be deduced, but DstT cannot
{
    return x;
}

int main()
{
    double value = implicit_cast<double>(-1);
}
```

```
template<typename ... Ts, int N>
void f(double (&)[N+1], Ts ... ps);  // useless declaration because N
// cannot be specified or deduced
```

```
```cpp
template<typename Func, typename T>
void apply (Func funcPtr, T x)
{
    funcPtr(x);
}

template<typename T> void single(T);

template<typename T> void multi(T);
template<typename T> void multi(T*);

int main()
{
    apply(&single<int>, 3);  // OK
    apply(&multi<int>, 7);   // ERROR: no single multi<int>
}
```
```

```
template<typename T> RT1 test(typename T::X const*);
template<typename T> RT2 test(...);
```

```
template<typename T>
void clear (T p)
{
    *p = 0;    // requires that the unary * be applicable to T
}

int main()
{
    int a;
    clear(a);  // ERROR: int doesn't support the unary *
}
```

```
template<char const* str>
class Message {
    ...
};

extern char const hello[] = "Hello World!";
char const hello11[] = "Hello World!";

void foo()
{
    static char const hello17[] = "Hello World!";

    Message<hello>  msg03;    // OK in all versions
    Message<hello11> msg11;   // OK since C++11
    Message<hello17> msg17;   // OK since C++17
}
```

```
template<typename T, T nontypeParam>
class C;

struct Base {
    int i;
} base;

struct Derived : public Base {
} derived;

C<Base*, &derived>* err1; // ERROR: derived-to-base conversions are not considered

C<int&, base.i>* err2;     // ERROR: fields of variables aren't considered to be variables

int a[10];
C<int*, &a[0]>* err3;      // ERROR: addresses of array elements aren't acceptable either
```

```
#include <list>
    // declares in namespace std:
    //  template<typename T, typename Allocator = allocator<T>>
    //  class list;

template<typename T1, typename T2,
        template<typename> class Cont>  // Cont expects one parameter
class Rel {
    ...
};

Rel<int, double, std::list> rel;  // ERROR before C++17: std::list has more than
//                          one template parameter
```

```
#include <list>

template<typename T1, typename T2,
    template<typename...> class Cont> // Cont expects any number of
class Rel {
    ...
};

Rel<int, double, std::list> rel;  // OK: std::list has two template parameters
//     but can be used with one argument
```

```
#include <list>
#include <map>
    // declares in namespace std:
    // template<typename Key, typename T,
    //           typename Compare = less<Key>,
    //           typename Allocator = allocator<pair<Key const, T>>>
    // class map;
#include <array>
    // declares in namespace std:
    // template<typename T, size_t N>
    // class array;

template<template<typename...> > class TT>
class AlmostAnyTmpl {
};

AlmostAnyTmpl<std::vector> withVector; // two type parameters
AlmostAnyTmpl<std::map> withMap;        // four type parameters
AlmostAnyTmpl<std::array> withArray;    // ERROR: a template type parameter pack
                                         // doesn't match a nontype template parameter
```

```
template<typename T, int I>
class Mix;

using Int = int;

Mix<int, 3*3>* p1;
Mix<Int, 4+5>* p2;  // p2 has the same type as p1
```

```
template<typename... Types>
class Tuple {
    // provides operations on the list of types in Types
};

int main() {
    Tuple<> t0;        // Types contains an empty list
    Tuple<int> t1;     // Types contains int
    Tuple<int, float> t2; // Types contains int and float
}
```

```
template<typename... Types>
class Tuple {
    public:
        static constexpr std::size_t length = sizeof...(Types);
};

int a1[Tuple<int>::length];            // array of one integer
int a3[Tuple<short, int, long>::length]; // array of three integers
```

```
template<typename... Types>
class MyTuple : public Tuple<Types...> {
    // extra operations provided only for MyTuple
};

MyTuple<int, float> t2;  // inherits from Tuple<int, float>
```

```
template<typename T1, typename T2>
class MyTuple : public Tuple<T1, T2> {
    // extra operations provided only for MyTuple
};
```

```
template<typename T1, typename T2, typename T3>
class MyTuple : public Tuple<T1, T2, T3> {
    // extra operations provided only for MyTuple
};
```

```
template<typename... Types>
class PtrTuple : public Tuple<Types*...> {
    // extra operations provided only for PtrTuple
};

PtrTuple<int, float> t3; // Inherits from Tuple<int*, float*>
```

```
template<typename T1, typename T2, typename T3>
class PtrTuple : public Tuple<T1*, T2*, T3*> {
    // extra operations provided only for PtrTuple
};
```

```
template<typename... Mixins>
class Point : public Mixins... {    // base class pack expansion
    double x, y, z;
public:
    Point() : Mixins()... { }        // base class initializer pack expansion

    template<typename Visitor>
    void visitMixins(Visitor visitor) {
        visitor(static_cast<Mixins&>(*this)...); // call argument pack expansion
    }
};

struct Color { char red, green, blue; };
struct Label { std::string name; };
Point<Color, Label> p;            // inherits from both Color and Label
```

```
template<typename... Ts>
struct Values {
    template<Ts... Vs>
    struct Holder {
    };
};

int i;
Values<char, int, int*>::Holder<'a', 17, &i> valueHolder;
```

```
```cpp
template<typename... Mixins>
class Point : public Mixins...
{
    double x, y, z;
public:
    // default constructor, visitor function, etc. elided
    Point(Mixins... mixins)    // mixins is a function parameter pack
        : Mixins(mixins)... { } // initialize each base with the supplied mixin value
};

struct Color { char red, green, blue; };
struct Label { std::string name; };
Point<Color, Label> p(0x7F, 0, 0x7F}, {"center"});
```
```

```
template<typename... Types>
void print(Types... values);

int main
{
    std::string welcome("Welcome to ");
    print(welcome, "C++ ", 2011, '\n'); // calls print<std::string, char const*, int, char>
}
```

```
```cpp
template<typename T> void c_style(int, T...);
template<typename... T> void pack(int, T...);
```
```

```
template<typename F, typename T1, typename T2, typename T3>
void forwardCopy(F f, T1 const& v1, T2 const& v2, T3 const& v3) {
    f(T1(v1), T2(v2), T3(v3));
}
```

```
template<typename... OuterTypes>
class Nested {
    template<typename... InnerTypes>
    void f(InnerTypes const&... innerValues) {
        g(OuterTypes(InnerTypes(innerValues)... )...);
    }
};
```

```
template<typename O1, typename O2>
class Nested {
    template<typename I1, typename I2, typename I3>
    void f(I1 const& iv1, I2 const& iv2, I3 const& iv3) {
        g(O1(I1(iv1), I2(iv2), I3(iv3)),
            O2(I1(iv1), I2(iv2), I3(iv3)),
            O3(I1(iv1), I2(iv2), I3(iv3));
    }
};
```

