# 21 • More about Inheritance 693

To derive a class with protected access we use the word protected in its declaration. The public and protected members of the base class become protected members of the derived class. With private access, they are accessible from the functions of the derived class, but not from outside. The main difference between private and protected inheritance is when we derive a new class from the derived class. With private inheritance, the second derived class does not have direct access to the members of the base class because they become private in the first derivation. For example, let's add class C in the following program:

```
class C : private B
{
public:
    void f();
}
```

```
void C::f() // All the following actions are not allowed.
{
    add(1);
    sub(2);
    cout << v+r << '\n';
}
```

The members and functions of the A class have become private members of the B class, is not allowed to access them directly from class C. On the other hand, if inheritance is protected, access is allowed.

```
#include <iostream> // Example 21.3
```

```
class A
{
protected:
    void f() const {std::cout << v << ' '};
public:
    int v;
    A() : v(10) {};
}
```

```
class B : protected A
{
protected:
    int r;
    void g() const {std::cout << r << '\n';
public:
    B() : r(20) {};
}
```

```
class C : protected B
{
public:
    void h();
}
```

```
void C::h() // All the following actions are allowed.
{
    v = r = 30;
    g();
    f();
}
```