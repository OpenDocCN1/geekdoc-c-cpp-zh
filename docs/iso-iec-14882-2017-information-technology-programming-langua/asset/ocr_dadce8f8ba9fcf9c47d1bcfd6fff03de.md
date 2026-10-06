# ISO/IEC 14882:2017(E)

```
};
void f(A);
f('a', 'b'); 
    // OK: f(A(std::initializer_list<int>)) user-defined conversion

struct B {
    B(int, double);
};
void g(B);
g('a', 'b'); 
    // OK: g(B(int, double)) user-defined conversion
g(1.0, 1.0); 
// error: narrowing

void f(B);
f('a', 'b'); 
    // error: ambiguous f(A) or f(B)

struct C {
    C(std::string);
};
void h(C);
h("foo"); 
    // OK: h(C(std::string("foo")))

struct D {
    D(A);
};
void i(D);
i({1, 2}, "bar"); // OK: i(D(std::initializer_list<int>{1,2}), C(std::string("bar\)))
-- end example
```

Otherwise, if the parameter is an aggregate type which can be initialized from the initializer list according to the rules for aggregate initialization (11.6.1), the implicit conversion sequence is a user-defined conversion sequence with the second standard conversion sequence an identity conversion. Example:

```
struct A {
    int m1;
    double m2;
};

void f(A);
f('a', 'b'); 
    // OK: f(A(int,double)) user-defined conversion
f(1.0); 
// error: narrowing
-- end example
```

Otherwise, if the parameter is a reference, see 16.3.3.1.4. [Note: The rules in this section will apply for initializing the underlying template for the reference.— note] [Example:

```
struct A {
    int m1;
    double m2;
};

void f(const A&);
f('a', 'b'); 
    // OK: f(A(int,double)) user-defined conversion
f(1.0) ; 
// error: narrowing

void g(const double&);
g((i1));n    // same conversion as int to double
-- end example
```