# ISO/IEC 14882:2017(E)

user-defined conversion sequences are not considered. [Note: These rules prevent more than one user-defined
conversion from being applied during overload resolution, avoiding infinite recursion. — end note]
[Example:

```
struct Y { int; };
struct A { operator int(); };
Y y = A(); // A::operator int() is not a candidate

struct X;
struct B { operator X(); };
B b;
X x(b); // B::operator X is not a candidate
— end example]
```

+   5 For the case where the parameter is not a reference, the implicit conversion sequence is, see 16.6.3.4.

+   6 When the parameter has the same type, the implicit conversion sequence is the one required to convert
the argument to the argument expression. The implicit conversion sequence is [Note: When the parameter has a class
type, the conceptual conversion sequence, defined in Clause 16; is defined
in terms of constructors and is not a convert. — end note]. Any difference in top-level qualification for that case is [Example: A parameter of type A
can be initialized from an argument of type const. The implicit conversion sequence for the
identity sequence; contains no “conversion” from const to A. — end note]. When the parameter has
a class type and the argument has the same type, the implicit conversion sequence is an
identity sequence. When the parameter is a reference the implicit conversion sequence is
derived-to-base conversion from the derived class to the base class.
[Note: This is no standard conversion; derived-to-base conversion exists only in the description
im implicit conversion sequences (16.6.3.1.1).

+   7 In all contexts, converting to an object parameter or converting to the left operand of
an assignment operation only only standard conversion sequences are allowed.

+   8 If no conversions are required to match an argument to a parameter type, the implicit conversion sequence is
the standard conversion sequence identifying the identity conversion

+   9 If no sequence of conversions exist to convert the argument to a parameter type, an implicit
conversion sequence cannot be formed.

+   10 If several sequences of conversions exist that each convert the argument to the parameter type, the
implicit conversion sequence ambiguous with the parameter is defined to the unique conversion sequence
designated the ambiguous conversion sequence. For the purpose of ranking implicit conversion sequences as
described in 16.6.3.2, the ambiguous conversion sequence is treated as a user-defined conversion sequence. [Note: This rule prevents
aunction from becoming non-viable because of an ambiguous conversion sequence for one of its parameters.
[Example:

```
class B;
class A { operator B(); };
class B { operator A(); };
class C { C(B); };
void f() {}
oid(C)
B b;
f(b);
// ill-formed: ambiguous because there is a conversion b -> C (via constructor)
// and an (ambiguous) conversion b -> A (via constructor or conversion function)

void f(B) { }
```

§ 16.6.3.1 ©ISO/IEC 2017 – All rights reserved 325