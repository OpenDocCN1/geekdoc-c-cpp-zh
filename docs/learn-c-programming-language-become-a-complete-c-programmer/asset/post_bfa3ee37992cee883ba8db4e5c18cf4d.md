
```cpp
};
void Derived::f() final // error: final out of class {
// ...
}
```

### 20.3.4.2 final

```cpp
void g() final // OK {
// ...
}
```

Like override (§20.3.4.1), `final` is a contextual keyword. That is, `final` has a special meaning in a few contexts but can be used as an ordinary identifier elsewhere. For example:

```cpp
int final = 7;
struct Dx : Base {
    int final;
    int f() final
    {
        return final + ::final;
    }
};
```

Don’t indulge in such cleverness; it complicates maintenance. The only reason that `final` is a contextual keyword, rather than an ordinary keyword, is that there exist a significant amount of code that has used `final` as an ordinary identifier for decades. The other contextual keyword is `override` (§20.3.4.1).

## 20.3.5 using Base Members

Functions do not overload across scopes (§12.3.3). For example:

```cpp
struct Base {
    void f(int);
};

struct Derived : Base {
    void f(double);
};

void use(Derived d) {
    d.f(1); // call Derived::f(double)
    Base& br = d;
    br.f(1); // call Base::f(int)
}
```

This can surprise people, and sometimes we want overloading to ensure that the best matching member function is used. As for namespaces, `using`-declarations can be used to add a function to a scope. For example:

```cpp
struct D2 : Base {
    using Base::f; // bring all fs from Base into D2
    void f(double);
```

not do anything like that.

We solve the problem by simply saying that the constructors should be inherited:

```cpp
template<class T>
struct Vector : std::vector<T> {
    using vector<T>::vector; // inherit constructors
    T& operator[](size_type i) { check(i); return this->elem(i); }
    const T& operator[](size_type i) const { check(i); return this->elem(i); }
    void check(size_type i) { if (this->size()<i) throw Bad_index(i); }
};

Vector<int> v { 1, 2, 3, 5, 8 }; // OK: use initializer-list constructor from std::vector
```

This use of `using` is exactly equivalent to its use for ordinary functions (§14.4.5, §20.3.5).

If you so choose, you can shoot yourself in the foot by inheriting constructors in a derived class in which you define new member variables needing explicit initialization:

```cpp
struct B1 {
    B1(int) {}
};

struct D1 : B1 {
    using B1::B1; // implicitly declares D1(int)
    string s; // string has a default constructor
    int x; // we “forgot” to provide for initialization of x
};

void test() {
    D1 d {6}; // oops: d.x is not initialized
    D1 e; // error: D1 has no default constructor
}
```

The reason that `D1::s` is initialized and `D1::x` is not is that the inheriting constructor is equivalent to a constructor that simply initializes the base. In this case, we might equivalently have written:

```cpp
struct D1 : B1 {
    D1(int i) : B1(i) {}
    string s; // string has a default constructor
    int x; // we “forgot” to provide for initialization of x
};
```

One way to remove the bullet from your foot is by adding an in-class member initializer (§17.4.4):

```cpp
struct D1 : B1 {
    using B1::B1; // implicitly declares D1(int)
    int x {0}; // note: x is initialized
};

void test() {
    D1 d {6}; // d.x is zero
}
```

Most often it is best to avoid being clever and restrict the use of inheriting constructors to the simple cases where no data members are added.

## 20.3.6 Return Type Relaxation

There is a relaxation of the rule that the type of an overriding function must be the same as the type of the virtual function it overrides. That is, if the original return type was **B\***, then the return type of the overriding function may be **D\***, provided **B** is a public base of **D**. Similarly, a return type of **B&** may be relaxed to **D&**. This is sometimes called the *covariant return* rule.

This relaxation applies only to return types that are pointers or references, and not to “smart pointers” such as **unique_ptr** (§5.2.1). In particular, there is not a similar relaxation of the rules for argument types because that would lead to type violations.

Consider a class hierarchy representing different kinds of expressions. In addition to the operations for manipulating expressions, the base class **Expr** would provide facilities for making new expression objects of the various expression types:

```cpp
class Expr {
public:
    Expr(); // default constructor
    Expr(const Expr&); // copy constructor
    virtual Expr* new_expr() = 0;
    virtual Expr* clone() = 0;
    // ...
};
```

The idea is that `new_expr()` makes a default object of the type of the expression and `clone()` makes a copy of the object. Both will return an object of some specific class derived from `Expr`. They can never just return a “plain `Expr`” because `Expr` was deliberately and appropriately declared to be an abstract class.

A derived class can override `new_expr()` and/or `clone()` to return an object of its own type:

```cpp
class Cond : public Expr {
public:
    Cond();
    Cond(const Cond&);
    Cond* new_expr() override { return new Cond(); }
    Cond* clone() override { return new Cond(*this); }
    // ...
};
```

This means that given an object of class `Expr`, a user can create a new object of “just the same type.” For example:

```cpp
void user(Expr * p)
{
    Expr* p2 = p->new_expr();
    // ...
}
```

The pointer assigned to `p2` is declared to point to a “plain `Expr`,” but it will point to an object of a type derived from `Expr`, such as `Cond`.

The return type of `Cond::new_expr()` and `Cond::clone()` is `Cond*` rather than `Expr*`. This allows a `Cond` to be cloned without loss of type information. Similarly, a derived class `Addition` would have a `clone()` returning an `Addition*`. For example:

```cpp
void user2(Cond * pc, Addition* pa)
{
    Cond* p1 = pc->clone();
    Addition* p2 = pa->clone();
    // ...
}
```

If we use `clone()` for an `Expr` we only know that the result is an `Expr*`:

```cpp
void user3(Cond * pc, Expr* pe)
{
    Cond* p1 = pc->clone();
    Cond* p2 = pe->clone(); // error: Expr::clone() returns an Expr*
    // ...
}
```

Because functions such as `new_expr()` and `clone()` are `virtual` and they (indirectly) construct objects, they are often called *virtual constructors*. Each simply uses a constructor to create a suitable object.

To make an object, a constructor needs the exact type of the object it is to create. Consequently, a constructor cannot be `virtual`. Furthermore, a constructor is not quite an ordinary function. In particular, it interacts with memory management routines in ways ordinary member functions don’t. So, you cannot take a pointer to a constructor and pass that to an object creation function.

Both of these restrictions can be circumvented by defining a function that calls a constructor and returns a constructed object. This is fortunate because creating a new object without knowing its exact type is often useful. The `Ival_box_maker` (§21.2.4) is an example of a class designed specifically to do that.

## 20.4 Abstract Classes

Many classes resemble class `Employee` in that they are useful as themselves, as interfaces for derived classes, and as part of the implementation of derived classes. For such classes, the techniques described in §20.3.2 suffice. However, not all classes follow that pattern. Some classes, such as a class `Shape`, represent abstract concepts for which objects cannot exist. A `Shape` makes sense only as the base of some class derived from it. This can be seen from the fact that it is not possible to provide sensible definitions for its virtual functions:

```cpp
class Shape {
public:
    virtual void rotate(int) { throw runtime_error{"Shape::rotate"}; } // inelegant
    virtual void draw() const { throw runtime_error{"Shape::draw"}; }
    // ...
};
```

Trying to make a shape of this unspecified kind is silly but legal:

```cpp
Shape s; // silly: “shapeless shape”
```

It is silly because every operation on `s` will result in an error.

A better alternative is to declare the virtual functions of class `Shape` to be pure virtual functions. A virtual function is “made pure” by the “pseudo initializer” `=0`:

```cpp
class Shape { // abstract class
public:
    virtual void rotate(int) = 0; // pure virtual function
    virtual void draw() const = 0; // pure virtual function
    virtual bool is_closed() const = 0; // pure virtual function
    // ...
    virtual ~Shape(); // virtual
};
```

A class with one or more pure virtual functions is an abstract class, and no objects of that abstract class can be created:

```cpp
Shape s; // error: variable of abstract class Shape
```

An abstract class is intended as an interface to objects accessed through pointers and references (to preserve polymorphic behavior). Consequently, it is usually important for an abstract class to have a virtual destructor (§3.2.4, §21.2.2). Because the interface provided by an abstract class cannot be used to create objects using a constructor, abstract classes don’t usually have constructors.

An abstract class can be used only as an interface to other classes. For example:

```cpp
class Point { /* ... */ };

class Circle : public Shape {
public:
    void rotate(int) override { }
    void draw() const override;
    bool is_closed() const override { return true; }
```
