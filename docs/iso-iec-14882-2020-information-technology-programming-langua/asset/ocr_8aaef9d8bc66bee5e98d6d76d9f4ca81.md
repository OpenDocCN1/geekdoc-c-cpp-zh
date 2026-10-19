# ISO/IEC 14882:2020(E)

```
int f(const volatile int *);
int f(const int *);
int i;
int j = f(&i);    // calls f(const int*)
```

— end example]

or, if not that,

+   (3.2.6) — S1 and S2 include reference bindings (9.4.4), and the types to which the references refer are the same type except for top-level cv-qualifiers, and the type to which the reference initialized by S2 refers is more cv-qualified than the type to which the reference initialized by S1 refers.

[Example 6:

```
int f(const int &);
int f(int &);
int g(const int &);
int g(int);

int i;
int j = f(i);    // calls f(int &)
int k = g(i);    // ambiguous
```

```
struct X {
    void f() const;
    void f();
};
void g(const X& a, X b) {
    a.f();    // calls X::f() const
    b.f();    // calls X::f()
}
```

— end example]

+   (3.3) — User-defined conversion sequence U1 is a better conversion sequence than another user-defined conversion sequence U2 if they contain the same user-defined conversion function or constructor or they initialize the same class in an aggregate initialization and in either case the second standard conversion sequence of U1 is better than the second standard conversion sequence of U2.

[Example 7:

```
struct A {
    operator short();
} a;
int f(int);
int f(float);
int i = f(a);    // calls f(int), because short → int is
                 // better than short → float.
```

— end example]

4 Standard conversion sequences are ordered by their ranks: an Exact Match is a better conversion than a Promotion, which is a better conversion than a Conversion. Two conversion sequences with the same rank are indistinguishable unless one of the following rules applies:

+   (4.1) — A conversion that does not convert a pointer or a pointer to member to bool is better than one that does.

+   (4.2) — A conversion that promotes an enumeration whose underlying type is fixed to its underlying type is better than one that promotes to the promoted underlying type, if the two are different.

+   (4.3) — If class B is derived directly or indirectly from class A, conversion of B* to A* is better than conversion of B* to void*, and conversion of A* to void* is better than conversion of B* to void*.

+   (4.4) — If class B is derived directly or indirectly from class A and class C is derived directly or indirectly from B,

+   (4.4.1) — conversion of C* to B* is better than conversion of C* to A*,

[Example 8:

```
struct A {};
struct B : public A {};
```