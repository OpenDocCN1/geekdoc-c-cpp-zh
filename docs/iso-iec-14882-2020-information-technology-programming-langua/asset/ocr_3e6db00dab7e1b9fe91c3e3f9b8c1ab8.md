# 11.9 Member access control [class.access]

# 11.9.1 General [class.access.general]

1 A member of a class can be

+   (1.1) — private; that is, its name can be used only by members and friends of the class in which it is declared.
+   (1.2) — protected; that is, its name can be used only by members and friends of the class in which it is declared, by classes derived from that class, and by their friends (see 11.9.5).
+   (1.3) — public; that is, its name can be used anywhere without access restriction.

2 A member of a class can also access all the names to which the class has access. A local class of a member function may access the same names that the member function itself may access.115

3 Members of a class defined with the keyword class are private by default. Members of a class defined with the keywords struct or union are public by default.

```
[Example 5:
struct V { };
struct A { };
struct B : A, virtual V { };
struct C : A, virtual V { };
struct D : B, C { };

void g() {
    D d;
    B* pb = &d;
    A* pa = &d;        // error: ambiguous: C's A or B's A?
    V* pv = &d;        // OK: only one V subobject
}
— end example]
```

12 [Note 4: Even if the result of name lookup is unambiguous, use of a name found in multiple subobjects can still be ambiguous (7.3.13, 7.6.1.5, 11.9.3). — end note]

```
[Example 6:
struct B1 {
    void f();
    static void f(int);
    int i;
};
struct B2 {
    void f(double);
};
struct I1: B1 { };
struct I2: B1 { };

struct D: I1, I2, B2 {
    using B1::f;
    using B2::f;
    void g() {
        f();                // Ambiguous conversion of this
        f(0);               // Unambiguous (static)
        f(0.0);             // Unambiguous (only one B2)
        int B1::* mpB1 = &D::i;   // Unambiguous
        int D::* mpD = &D::i;     // Ambiguous conversion
    }
};
— end example]
```

```
[Example 1:
class X {
    int a;            // X::a is private by default
};
```