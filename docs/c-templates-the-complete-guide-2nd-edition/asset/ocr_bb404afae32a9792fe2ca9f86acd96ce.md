```
struct S {
    void f1();     // implicit *this parameter is an lvalue reference (see below)
    void f2() &&;  // implicit *this parameter is an rvalue reference
    void f3() &;   // implicit *this parameter is an lvalue reference
};
```