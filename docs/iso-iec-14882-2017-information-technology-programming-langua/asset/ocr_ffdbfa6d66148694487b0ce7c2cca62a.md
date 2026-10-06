# ISO/IEC 14882:2017(E)

lookup (8.3.5) continues. If the result of the lookup is ambiguous or inaccessible, or if the lookup selects a placement deallocation function, the program is ill-formed.

Any deallocation function for class X is a static member (even if not explicitly declared static). [Example:

```
class X {
    void operator delete(void*);
    void operator delete(void*, std::size_t);
};

class Y {
    void operator delete(void*, std::size_t);
    void operator delete(void*);
};

// end example
```

Since member allocation and deallocation functions are static they cannot be virtual. [Note: However, when the cast-expression of a delete-expression refers to an array of class type, because the deallocation function actually called is looked up in the scope of the object that is the dynamic type of the object, if the destructor is virtual, the effect is static. For example,

```
struct B {
    virtual ~B();
    void operator delete(void*, std::size_t);
};

struct D : B {
    void operator delete(void*);
};

void f() {
    B* bp = new D;
    delete bp; // uses: D::operator delete(void*)
}

void f(int i) {
    D* dp = new D[i];
    delete dp; // uses: D::operator delete[](void*, std::size_t);
    B* bp = new D[i];
    delete bp; // undefined behavior
};
```

Here, storage for the non-array object of class D is deallocated by D::operator delete(), due to the virtual destructor....Note: Virtual destructors have no effect on the deallocation function actually called when the cast-expression of a delete-expression refers to an array of objects of class type. For example,

```
struct B {
    virtual ~B();
    void operator delete(void*, std::size_t);
}
```

```
struct D : B {
    void operator delete(void*, std::size_t);
}
```

```
void f(int i) {
    D* dp = new D[i];
    delete dp; // uses: D::operator delete[](void*, std::size_t);
    B* bp = new D[i];
    delete bp; // undefined behavior
}
```

// end note

Access to the deallocation function is checked statically. Hence, even though a different one might actually

©ISO/IEC 2017 – All rights reserved 290