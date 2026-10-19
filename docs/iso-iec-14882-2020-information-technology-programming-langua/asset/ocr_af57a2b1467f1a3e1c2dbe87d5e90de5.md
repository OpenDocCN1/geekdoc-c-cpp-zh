# ISO/IEC 14882:2020(E)

(7.1) — If C is not an initializer-list constructor and the initializer list has a single element of type cv U, where U is X or a class derived from X, the implicit conversion sequence has Exact Match rank if U is X, or Conversion rank if U is derived from X.

(7.2) — Otherwise, the implicit conversion sequence is a user-defined conversion sequence with the second standard conversion sequence an identity conversion.

If multiple constructors are viable but none is better than the others, the implicit conversion sequence is the ambiguous conversion sequence. User-defined conversions are allowed for conversion of the initializer list elements to the constructor parameter types except as noted in 12.4.4.2.

[Example 3:

```
struct A {
    A(std::initializer_list<int>);
};
void f(A);
f( {'a', 'b'} );        // OK: f(A(std::initializer_list<int>)) user-defined conversion

struct B {
    B(int, double);
};
void g(B);
g( {'a', 'b'} );        // OK: g(B(int, double)) user-defined conversion
g( {1.0, 1.0} );        // error: narrowing

void f(B);
f( {'a', 'b'} );        // error: ambiguous f(A) or f(B)

struct C {
    C(std::string);
};
void h(C);
h({"foo"});            // OK: h(C(std::string("foo")))

struct D {
    D(A, C);
};
void i(D);
i({ {1,2}, {"bar"} });  // OK: i(D(A(std::initializer_list<int>{1,2}), C(std::string("bar"))))
— end example]
```

8 Otherwise, if the parameter has an aggregate type which can be initialized from the initializer list according to the rules for aggregate initialization (9.4.2), the implicit conversion sequence is a user-defined conversion sequence with the second standard conversion sequence an identity conversion.

[Example 4:

```
struct A {
    int m1;
    double m2;
};

void f(A);
f( {'a', 'b'} );        // OK: f(A(int,double)) user-defined conversion
f( {1.0} );             // error: narrowing
— end example]
```

9 Otherwise, if the parameter is a reference, see 12.4.4.2.5.

[Note 2: The rules in this subclause will apply for initializing the underlying temporary for the reference. — end note]

[Example 5:

```
struct A {
    int m1;
    double m2;
};
```