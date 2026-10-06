# ISO/IEC 14882:2017(E)

class for another class using the private access specifier, the public and protected members of the base class are accessible as private members of the derived class.

In the absence of an access-specifier for a base class, public is assumed when the derived class is defined with the class-key struct and private is assumed when the class is defined with the class-key class. Example:

```
class B { /* ... */ };
class D1 : private B { /* ... */ };
class D2 : public B { /* ... */ };
class D3 : public B { /* ... */ };
struct D5 : private B { /* ... */ };
struct D6 : private B { /* ... */ };
class D7 : protected B { /* ... */ };
struct D8 : protected B { /* ... */ };
```

Here is a private base of D2, D4, and D6, a private base of D1, D3, D5, and a protected base of D7 and D8; example:

> [Note: A member of a private base is accessible as an inherited name, but inaccessible directly. Because of the rules on pointer conversions (7.11) and explicit casts (8.4), a conversion from a pointer to a derived class to a pointer to an inaccessible base class might be ill-formed if an implicit conversion is used, well-formed if an explicit cast is used. Example.

```
class B {
public:
 int mi;
 static int si;
};
class D : private B {
class DD : public D {
 void f();
};
```

```
void DD::f() {
nmi = 3;
si = 3;
:B b;
mi = 3;
b.si = 3;
:B::si = 3;
:B* bpl = this;
:B* bpl = ((B*)this);
bp2-mi = 3;
}
```

+   A base class of N is accessible in R, if

+   (4.1) an invented public member of B would be a public member of N, or

+   (4.2) R occurs in a base or friend of class N, and an invented public member of B would be a private or protected member of N, or

+   (4.3) R occurs in a base or friend of class N, and an invented public member of B would be

As specified previously in Clause 14, private members of a base class remain inaccessible to derived classes unless declarations within the base definition are used to grant access explicitly.

§ 14.2

©ISO/IEC 2017 - All rights reserved

270