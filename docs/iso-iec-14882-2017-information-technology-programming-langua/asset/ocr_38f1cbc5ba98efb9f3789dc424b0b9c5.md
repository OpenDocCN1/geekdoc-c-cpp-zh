# ISO/IEC 14882:2017(E)

(12.4) — for a temporary object when its lifetime ends (7.4, 15.2).

In each case, the context of the invocation is the context of the construction of the object. The destructor is also invoked implicitly through the use of a delete-expression (8.3.5) for a constructed object allocated by a new-expression (8.3.4); the context of the invocation is the delete-expression. [Note: An array of class contains several subobjects for which the destructor is invoked. — end note] A destructor can also be invoked implicitly. A destructor is potentially invoked if it is deleted or as specified in 8.3.4, 15.6.2, and 18.1. A program is illformed if a potentially deleted is not accessed from the context of the invocation.

At the point of invoking a virtual destructor (including an implicit delete (15.8)), the non-array deallocation function is defined as if the expression delete appearing in a non-virtual destructor of the object’s class (see 8.3.5). If the lookup fails or the deallocation function has a deleted definition (11.4), the program is illformed. [Note: This assures that a function corresponding to the dynamic type of an object is available for the delete-expression (15.5). — end note]

In an explicit destructor call, the destructor is rarely needed. One of such calls is invoked as specified by a type-name or delete-specifier that denotes the destructor’s class. The invocation of a destructor is subject to the usual rules for member functions (12.2.1); that is, if the object is not of the destructor’s class type and not of a class derived from the destructor’s class type (including when the destructor is invoked via a null pointer), [Note: Invoking delete on a null pointer does not call the destructor; see 8.5. — end note]

```
struct B {
    virtual ~B() {}
};
struct D : B {
    ~D() {}
};

D D {
    typedef B as Alias;
    B* Ptr = &D_object;
};

void f() {
    D_object::~B();
    Ptr->~B();
    Ptr->~Alias();
    Ptr->*Alias::~B();
    Ptr->*Alias::~Alias();
}
```

[Note: An explicit destructor call must be written using a member access operator (8.2.5) or a qualified-id (8.1); in particular, the unary-expression -X() in a member function is not an explicit destructor call (8.3.1). — end note]

[Note: Explicit calls of destructors are rarely needed. One of such calls is for objects placed at specific addresses using a placement new-expression. Such use of explicit placement and destruction of objects is necessary to cope with dedicated hardware resources and for writing memory management facilities. For example,

```
void operator new(std::size_t, void* p) { return p; }
struct X {
    ~X();
};
void f(X* p);
```

§ 15.4 ISO/IEC 2017 – All rights reserved 288