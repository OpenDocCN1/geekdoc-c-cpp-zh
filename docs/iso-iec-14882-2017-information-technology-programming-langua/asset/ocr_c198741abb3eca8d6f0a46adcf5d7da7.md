# ISO/IEC 14882:2017(E)

```
int g(int);

int i;
int j = f(i); // calls f(int &)
int k = g(i); // ambiguous

struct X {
    void f() const;
    void f();
};
void g(const X& a, X b) { // calls X::f() const
    a.f();
    b.f();
}

// end example]
```

(3.3) User-defined conversion U1 is a better conversion sequence than another user-defined conversion U2 if they contain the same user-defined conversion function or they initialize the same class in an aggregate initialization and in either case the second standard conversion sequence of U1 is better than the second standard conversion sequence of U2: [Example:

```
struct A {
    operator short();
};
int f(int);
int f(float);
int i = f(a); // calls f(int), because short -> int is
// better than short -> float.

// end example]
```

+   4 Standard conversion sequences are ordered by their ranks: An Match is better than a Promotion, which is better than a Conversion. Two sequences with the same rank are indistinguishable unless one of the following rules:

+   (4.1) A conversion that does not convert a pointer, to member, or std::nullptr_t to bool is better than one that does.

+   (4.2) A conversion that promotes an enumeration to its underlying type is better than one that promotes to the promoted underlying type, if the two are different.

+   (4.3) If class B is derived directly or indirectly from class A, conversion of B* to A* is better than conversion of B* to void*, and conversion of A* to void* is better than conversion of B* to void.

+   (4.4) If class B is derived directly or indirectly from class C and C is derived directly or indirectly from B,

+   (4.4.1) conversion of C to B* is better than conversion of C* to A*, [Example:

struct A {
    struct B : public A;
    struct C : public B;
};
* pc;
int f(A*);\int f(B*);
int i = f(pc); // calls f(B*)

// end example]

+   (4.4.2) binding of an expression of type C to a reference to type B is better than binding an expression of type C to a reference to type A.