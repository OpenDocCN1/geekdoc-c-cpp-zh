# ISO/IEC 14882:2017(E)

```
struct D : B, C {

void g() {
 D d;
 B* pb = &d;
A* pa = &d;
 V* pv = &d; // error, ambiguous: C's A or B's A?
 // OK: only one V subobject
}
// end example
```

+   [Note: Even if the result of name lookup is unambiguous, a name found in multiple subobjects might still be ambiguous (7.12, 8.2.5, 14.2). — end note] [Example:

```
struct B1 {
void f();
 static void f(int);
 int i;
};
struct B2 {
void f(double);
};
struct I1 : B1 {;
struct I2 : B1 {;

struct D : I1, I2, B2 {
using B1::f;
using B2::f;
void g() {
 f(); // Ambiguous conversion of this
f(0); // Unambiguous (static)
f(0.0); // Unambiguous (only one B2)
 int I1::mp81 = &d; // Unambiguous
 int D::mp8 = &d; // Ambiguous conversion
}
}; // end example
```

# 13.3 Virtual functions

+   1 [Note: Virtual functions support dynamic binding and object-oriented programming. — end note] A class that declares a virtual function is called a polymorphic class.

+   2 If a virtual function vf is declared in a class Base and in a class Derived, derived directly or indirectly from Base, a member function with the same name, parameter-list (11.3.5), cv-qualification, and ref-qualifier (or absence of same) as Base::vf is then, declared: vf is virtual (whether or not it is declared) and overrides any virtual function of it. A virtual member function C::vf of a class S is a final overrider unless the derived class (4.5) of S is a base subclass (if) declares or inherits another member function that overrides vf. A derived class, if a virtual member function of a base subclass has more than one overrider the program is ill-formed. [Example:

```
struct A {
void f();
}
```

+   111 A function with the same name but a different parameter list (Clause 16) as a virtual function is not necessarily virtual and does not override. The use of the virtual in the specification of an overriding function is legal but redundant [has empty semantics]. Access control (Clause 14) is not considered in determining override.