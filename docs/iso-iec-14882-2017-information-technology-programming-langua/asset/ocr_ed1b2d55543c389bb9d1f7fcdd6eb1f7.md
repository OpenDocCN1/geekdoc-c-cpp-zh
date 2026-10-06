# ISO/IEC 14882:2017(E)

is permitted to inspect the initial sequence of any standard-layout struct members; see 12.2— end note]

The size of a union is sufficient to contain the largest of its non-static data members. Each non-static data member is allocated as if it were the sole member of a struct. [Note: A standard-layout union and its non-static data members are pointer-interconvertible (6.9.2, 8.2.9)]. As a consequence, all non-static data members of such a union have the same address.—end note]

A union can have member functions (including constructors and destructors), but it should not have virtual (13.3) functions. A union shall not have base classes. A union shall not be used as a base class. If a union contains a non-static data member of reference type the program is ill; [Note: Absent member initializes (12.2), if any non-static data member of a union has a non-trivial default constructor (15.1), copy constructor (15.8), move constructor (15.8), copy assignment operator (15.8), move assignment operator (15.8), or destructor (15.8), the corresponding function of the union must be user-provided—or it will be implicitly defined (11.4.3) for the union.—end note]

+   [4] Example: Considering the following union:
```cpp
union {
    int i;
    float f;
    std::string s;
};
```

Since (24.3) does non-trivial versions of any of the special member functions, U will have an implicit default constructor, copy/move constructor, copy/move assignment operator, and destructor. To use U, all of these member functions must be user-provided.—end example]

+   5 When the left operand of an assignment operator involves a member of such union (8.2.5) that nominates an member, it may extend the lifetime of that union member, as described below. For an expression E, the defined set S(E) of subexpressions of U follows:

+   (5.1) If E is of the form A.B, S contains the elements of S(A), and also contains A.B if B names a member of a non-class, non-array type, or a class with a trivial constructor that is not deleted, or an array of such types.

+   (5.2) Otherwise, S(E) is empty.

+   (5.3) In an expression of the form E1 = E2 that uses the built-assignment operator (8.18) or a trivial assignment operator (6.8), for each element X of S(E1), if modification of X would induce behavior at the beginning of the storage; no initialization is performed and the beginning of its lifetime is extended after the value computation of the left and right union, if any (6.8).—end note] [Note: This ends the lifetime of the previously-active member of the
```cpp
union {
    int x; int y[4];
    struct {
        struct a;
        union {
            struct {
                int b; int k;
            } c;
            int f;
        } c;
        c.b.a.y[3] = 4 // does not start lifetime of any union member
// OK: c.b.a.y[3] contains c.b and c.b.a.y;
return c.b.a.y[3]; // OK: c.b.a.y refers to newly created (see 6.8)
}
struct {
    int a; int k;
};
``` [Example]:

§ 12.3 ©ISO/IEC 2017 — All rights reserved