```
struct Z : Y, virtual W { using Y::Y; };
Z z(0);                // OK: initialization of Y does not invoke default constructor of X

template<class T> struct Log : T {
    using T::T;        // inherits all constructors from class T
    ~Log() { std::clog << "Destroying wrapper" << std::endl; }
};
```

Class template Log wraps any class and forwards all of its constructors, while writing a message to the standard log whenever an object of class Log is destroyed. — end example]

2 If the constructor was inherited from multiple base class subobjects of type B, the program is ill-formed.

```
[Example 2:
struct A { A(int); };
struct B : A { using A::A; };

struct C1 : B { using B::B; };
struct C2 : B { using B::B; };

struct D1 : C1, C2 {
    using C1::C1;
    using C2::C2;
};

struct V1 : virtual B { using B::B; };
struct V2 : virtual B { using B::B; };

struct D2 : V1, V2 {
    using V1::V1;
    using V2::V2;
};

D1 d1(0);            // error: ambiguous
D2 d2(0);            // OK: initializes virtual B base class, which initializes the A base class
                     // then initializes the V1 and V2 base classes as if by a defaulted default constructor

struct M { M(); M(int); };
struct N : M { using M::M; };
struct O : M {};
struct P : N, O { using N::N; using O::O; };
P p(0);              // OK: use M() to initialize N's base class,
                     // use M() to initialize O's base class
— end example]
```

3 When an object is initialized by an inherited constructor, initialization of the object is complete when the initialization of all subobjects is complete.

# 11.10.5 Construction and destruction [class.cdtor]

1 For an object with a non-trivial constructor, referring to any non-static member or base class of the object before the constructor begins execution results in undefined behavior. For an object with a non-trivial destructor, referring to any non-static member or base class of the object after the destructor finishes execution results in undefined behavior.

```
[Example 1:
struct X { int i; };
struct Y : X { Y(); };                // non-trivial
struct A { int a; };
struct B : public A { int j; Y y; };  // non-trivial

extern B bobj;
B* pb = &bobj;                       // OK
int* p1 = &bobj.a;                   // undefined behavior: refers to base class member
int* p2 = &bobj.y.i;                 // undefined behavior: refers to member's member
```