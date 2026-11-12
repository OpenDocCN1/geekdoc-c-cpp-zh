
```cpp
8 void f(A arg)
9 {
10    A a = 1;
11    A b = "Lin";
12    a = 2;
13    f(3);
14    f({1, 2});
15 }
```

### Solution of Question 191

This is a valid code. A constructor declared without the function-specifier explicit specifies a conversion from the types of its parameters to the type of its class. Such a constructor is called a converting constructor.

- A a = 1 is same as A a = A(1)
- A b = "Lin" is same as A b = A("Lin", 0);
- a = 2 is same as a = A(2)
- f(3) is equivalent to f(A(3))
- f({1,2}) is equivalent to calling f(A(1, 2))

## Question 192 — conversion operator

Will all three calls depicted below invoke the supplied conversion constructor?

```cpp
1 struct A
2 {
3    operator int();
4 };
5
6 void f(A a)
7 {
8    int i = int(a);
9    i = (int)a;
10   i = a;
11 }
```

### Solution of Question 192

Yes, in all three cases the value assigned will be converted by A::operator int().

## Question 193 — destructor

What is the output of the program below?

### Program 13.13: destructor

```cpp
#include <iostream>

struct B
{
    virtual ~B()
    {
        std::cout << "B::~B()" << std::endl;
    }
};

struct D : B
{
    ~D()
    {
        std::cout << "D::~D()" << std::endl;
    }
};

int main()
{
    D d;
    typedef B B1;

    B* bptr = &d;

    d.B::~B();

    bptr->~B();

    bptr->~B1();

    bptr->B1::~B();

    bptr->B1::~B1();
}
```

### Solution of Question 193

```
B::~B()
D::~D()
D::~D()
B::~B()
B::~B()
D::~D()
B::~B()
```

- `d.B::~B();` calls B’s destructor
- `bptr->~B();` calls D’s destructor

## Question 196 — signature of deallocation function

Provide the signature(s) of deallocation function(s) for a given class A.

### Solution of Question 196

```cpp
class A
{
    void operator delete(void*);
    void operator delete[](void*, std::size_t);
};
```

Any deallocation function for a class A is a static member (even if not explicitly declared static).

## Question 197 — delete and virtual

What is the output of the program?

### Program 13.14: delete and virtual

```cpp
#include <iostream>

struct B
{
    virtual ~B()
    {
        std::cout << "B::~B()" << std::endl;
    }

    void operator delete(void*, std::size_t)
    {
        std::cout << "B::operator_delete" << std::endl;
    }
};

struct D : B
{
    void operator delete(void*)
    {
        std::cout << "D::operator_delete" << std::endl;
    }
};

int main()
{
    B* bp = new D;
    delete bp;
}
```

### Solution of Question 197

It prints:

```
B::~B()
D::operator_delete
```

Since member allocation and deallocation functions are static they cannot be virtual. However, when the cast-expression of a delete-expression refers to an object of class type, because the deallocation function actually called is looked up in the scope of the class that is the dynamic type of the object, if the destructor is virtual, the effect is the dynamic type of the object.

Here, storage for the non-array object of class D is deallocated by `D::operator delete()`, due to the virtual destructor (i.e., `delete bp` calls `D::operator delete(void*)`).

Please note that access to the deallocation function is checked statically. Hence, even though a different one might actually be executed, the statically visible deallocation function is required to be accessible. If `B::operator delete()` had been private above, the delete expression would have been ill-formed.

## Question 198 — base class initializer

Review the program?

### Program 13.15: base class initializer

```
struct A
{
    A();
};

struct B: virtual A { };

struct C: A, B
{
    C();
};

C::C(): A() { }
```

### Solution of Question 198

Compiler error is:

```
mem_initializer.cpp:13:9: error:
base class initializer 'A' names both a direct
base class and an inherited virtual base class
C::C(): A() { }
          ^

1 error generated.
```

If a *mem-initializer-id* is ambiguous because it designates both a direct non-virtual base class and an inherited virtual base class, the *mem-initializer* is ill-formed.

Here, C::C(): A() is ill-formed : which A ?

## Question 199 — pack expansion and initializer

Is this program valid one ?

```cpp
1 template<class... Mixins>
2 class X : public Mixins...
3 {
4 public:
5     X(const Mixins&... mixins)
6         :
7         Mixins(mixins)... { }
8 };
```

### Solution of Question 199

Yes. A *mem-initializer* followed by an ellipsis is a *pack expansion* that initializes the base classes specified by a pack expansion in the *base-specifier-list* for the class.

## Question 200 — non-trivial constructor

Is this program valid one ?

```cpp
1 struct W { int j; };
2 struct X : public virtual W { };
3 struct Y
4 {
5     int *p;
6     X x;
7     Y() : p(&x.j) { }
8 };
```

### Solution of Question 200

No.

For an object with a non-trivial constructor, referring to any non-static member or base class of the object before the constructor begins execution results in undefined behavior.

For an object with a non-trivial destructor, referring to any non-static member or base class of the object after the destructor finishes execution results in undefined behavior.

Here, `Y() : p(&x.j)` will lead to undefined behavior because *x* is not yet constructed.

## Question 201 — initializer and this

Review the program.

```cpp
virtual void f();
};
struct A : virtual V {};
struct B : virtual V
{
    B(V*, A*);
};
struct D : A, B
{
    D() : B((A*)this, this) { }
};
B::B(V* v, A* a)
{
    typeid(*this);
    typeid(*v);
    typeid(*a);
    dynamic_cast<B*>(v);
    dynamic_cast<B*>(a);
}
```

### Solution of Question 202

*dynamic_cast*s can be used during construction or destruction.

When a *dynamic_cast* is used in a constructor (including the *mem-initializer* or *brace-or-equal-initializer* for a non-static data member) or in a destructor, or used in a function called (directly or indirectly) from a constructor or destructor, if the operand of the *dynamic_cast* refers to the object under construction or destruction, this object is considered to be a most derived object that has the type of the constructor or destructor’s class.

If the operand of the *dynamic_cast* refers to the object under construction or destruction and the static type of the operand is not a pointer to or object of the constructor or destructor’s own class or one of its bases, the *dynamic_cast* results in undefined behavior.

Here,

- `typeid(*this)` is `type_info` for B.
- `typeid(*v)` is well-defined: `*v` has type V, a base of B yields `type_info` for B.
- `typeid(*a)` has undefined behavior: type A not a base of B
- `dynamic_cast<B*>(v)` is well-defined: v of type V*, V base of B results in B*.
- `dynamic_cast<B*>(a)` has undefined behavior, a has type A*, A not a base of B.

## Question 203 — inheriting constructors

Enlist the constructors available in D1 and D2.

```cpp
struct B1
{
    B1(int);
};

struct B2
{
    B2(int = 13, int = 42);
};

struct D1 : B1
{
    using B1::B1;
};

struct D2 : B2
{
    using B2::B2;
};
```

### Solution of Question 203

The candidate set of inherited constructors in D1 for B1 is

- B1(const B1&)
- B1(B1&&)
- B1(int)

The set of constructors present in D1 is

- D1(), implicitly-declared default constructor, ill-formed if odr-used
- D1(const D1&), implicitly-declared copy constructor, not inherited
- D1(D1&&), implicitly-declared move constructor, not inherited
- D1(int), implicitly-declared inheriting constructor

The candidate set of inherited constructors in D2 for B2 is

- B2(const B2&)
- B2(B2&&)
- B2(int = 13, int = 42)
- B2(int = 13)
- B2()

The set of constructors present in D2 is

- D2(), implicitly-declared default constructor, not inherited
- D2(const D2&), implicitly-declared copy constructor, not inherited
- D2(D2&&), implicitly-declared move constructor, not inherited
- D2(int, int), implicitly-declared inheriting constructor
- D2(int), implicitly-declared inheriting constructor

## Question 204 — hiding

Review the program.

### Program 13.18: hiding

```cpp
struct B
{
    int f(int);
};
struct D : B
{
    int f(const char*);
};
void h(D* pd)
{
    pd->f(1);
    pd->B::f(1);
    pd->f("Ben");
}
```

### Solution of Question 204

Compiler error is:
