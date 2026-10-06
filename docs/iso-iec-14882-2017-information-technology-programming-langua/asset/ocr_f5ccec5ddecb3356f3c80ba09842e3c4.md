# ISO/IEC 14882:2017(E)

4 Complete objects and subobjects of class type have nonzero size.¹⁰⁷ [Note: Class objects can be assigned, as arguments to functions, and returned by functions (except objects of which copying or moving has been restricted; see 15.8). Other plausible operators, such as equality comparison, can be defined by the user; see 16.5.— end note]

5 A union is defined with the class-key union; it holds at least one data member at a time (12.3) [Note: Aggregates of class type are described in 11.6.1.— end note]

6 A trivially copyable class is a class:

A trivial class is a class that is trivially copyable and has one or more default constructors (15.1), all of which are either deleted or trivial and at least one of which is not; [Note: a trivially copyable class or trivial class has no virtual functions or baseline class.— end note]

7 A class is a standard-layout class if:

```
(7.7)    has no element set M(S) of types (defined below) as a base class.¹⁰⁸
```

M(X) is defined as follows:

```
(7.10)   If X is an array-class with element type Xᵢ, the set M(X) consists of Xᵢ and the elements of M(Xᵢ).
(7.11)   If X is a non-class, non-array, the set M(X) is empty.
```

[Note: M(X) is the set of all non-base class subobjects that are guaranteed in a standard-layout class to be at a zero offset in X.— end note]

Example:

```
struct B { int }; // standard-layout class
struct C : B { }; // standard-layout class
struct D : C { }; // standard-layout class
struct E : D { }; // not a standard-layout class
```

Base class subobjects are not constrained.

¹⁰⁷ ensures that two subobjects have the same class type and belong to the same most derived object are not allocated at the same address (8.10).

¹⁰⁸ ensures that...

Classes

©ISO/IEC 2017 - All rights reserved

238