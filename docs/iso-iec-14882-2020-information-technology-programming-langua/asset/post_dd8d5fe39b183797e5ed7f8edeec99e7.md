
## 11.7.4 Abstract classes [class.abstract]

```cpp
struct VB1 : virtual A {
    void f();
};

// note virtual derivation

struct VB2 : virtual A {
    void f();
};

struct Error : VB1, VB2 {
};

// error

struct Okay : VB1, VB2 {
    void f();
};
```

Both VB1::f and VB2::f override A::f but there is no overrider of both of them in class Error. This example is therefore ill-formed. Class Okay is well-formed, however, because Okay::f is a final overrider. — end example

15 [Example 9: The following example uses the well-formed classes from above.

```cpp
struct VB1a : virtual A {
};

// does not declare f

struct Da : VB1a, VB2 {
};

void f() {
    VB1a* vb1ap = new Da;
    vb1ap->f();
}

// calls VB2::f
```

— end example

16 Explicit qualification with the scope operator (7.5.4.3) suppresses the virtual call mechanism.

[Example 10:

```cpp
class B { public: virtual void f() {}; };
class D : public B { public: void f() {}; };

void D::f() { /* ... */ B::f(); }
```

Here, the function call in D::f really does call B::f and not D::f. — end example

17 A function with a deleted definition (9.5) shall not override a function that does not have a deleted definition. Likewise, a function that does not have a deleted definition shall not override a function with a deleted definition.

18 A constexpr virtual function shall not override a virtual function that is not constexpr. A constexpr virtual function shall not be overridden by a virtual function that is not constexpr.

1 [Note 1: The abstract class mechanism supports the notion of a general concept, such as a shape, of which only more concrete variants, such as circle and square, can actually be used. An abstract class can also be used to define an interface for which derived classes provide a variety of implementations. — end note]

2 A virtual function is specified as a pure virtual function by using a pure-specifier (11.4) in the function declaration in the class definition.

[Note 2: Such a function can be inherited: see below. — end note]

A class is an abstract class if it has at least one pure virtual function.

[Note 3: An abstract class can be used only as a base class of some other class; no objects of an abstract class can be created except as subobjects of a class derived from it (6.2, 11.4). — end note]

A pure virtual function need be defined only if called with, or as if with (11.4.7), the qualified-id syntax (7.5.4.3).

[Example 1:

```cpp
class point { /* ... */ };
class shape {
    point center;
    // abstract class
public:
    point where() { return center; }
    void move(point p) { center=p; draw(); }
    virtual void rotate(int) = 0; // pure virtual
    virtual void draw() = 0;      // pure virtual
};
```

— end example]

> [Note 4: A function declaration cannot provide both a pure-specifier and a definition. — end note]

[Example 2:

```cpp
struct C {
    virtual void f() = 0 { };    // error
};
```

— end example]

> [Note 5: An abstract class type cannot be used as a parameter or return type of a function being defined (9.3.4.6) or called (7.6.1.3), except as specified in 9.2.9.3. Further, an abstract class type cannot be used as the type of an explicit type conversion (7.6.1.9, 7.6.1.10, 7.6.1.11), because the resulting prvalue would be of abstract class type (7.2.1). However, pointers and references to abstract class types can appear in such contexts. — end note]

A class is abstract if it contains or inherits at least one pure virtual function for which the final overrider is pure virtual.

[Example 3:

```cpp
class ab_circle : public shape {
    int radius;
public:
    void rotate(int) { }
    // ab_circle::draw() is a pure virtual
};
```

Since shape::draw() is a pure virtual function ab_circle::draw() is a pure virtual by default. The alternative declaration,

```cpp
class circle : public shape {
    int radius;
public:
    void rotate(int) { }
    void draw();                // a definition is required somewhere
};
```

would make class circle non-abstract and a definition of circle::draw() must be provided. — end example]

> [Note 6: An abstract class can be derived from a class that is not abstract, and a pure virtual function can override a virtual function which is not pure. — end note]

Member functions can be called from a constructor (or destructor) of an abstract class; the effect of making a virtual call (11.7.3) to a pure virtual function directly or indirectly for the object being created (or destroyed) from such a constructor (or destructor) is undefined.

## 11.8 Member name lookup [class.member.lookup]

1 Member name lookup determines the meaning of a name (id-expression) in a class scope (6.4.7). Name lookup can result in an ambiguity, in which case the program is ill-formed. For an unqualified-id, name lookup begins in the class scope of this; for a qualified-id, name lookup begins in the scope of the nested-name-specifier. Name lookup takes place before access control (6.5, 11.9).

2 The following steps define the result of name lookup for a member name f in a class scope C.

3 The lookup set for f in C, called S(f,C), consists of two component sets: the declaration set, a set of members named f; and the subobject set, a set of subobjects where declarations of these members (possibly including using-declarations) were found. In the declaration set, using-declarations are replaced by the set of designated members that are not hidden or overridden by members of the derived class (9.9), and type declarations (including injected-class-names) are replaced by the types they designate. S(f,C) is calculated as follows:

4 If C contains a declaration of the name f, the declaration set contains every declaration of f declared in C that satisfies the requirements of the language construct in which the lookup occurs.

> [Note 1: Looking up a name in an elaborated-type-specifier (6.5.5) or base-specifier (11.7), for instance, ignores all non-type declarations, while looking up a name in a nested-name-specifier (6.5.4) ignores function, variable, and enumerator declarations. As another example, looking up a name in a using-declaration (9.9) includes the declaration of a class or enumeration that would ordinarily be hidden by another declaration of that name in the same scope. — end note]

If the resulting declaration set is not empty, the subobject set contains C itself, and calculation is complete.

5 Otherwise (i.e., C does not contain a declaration of f or the resulting declaration set is empty), S(f, C) is initially empty. If C has base classes, calculate the lookup set for f in each direct base class subobject Bi, and merge each such lookup set S(f, Bi) in turn into S(f, C).

6 The following steps define the result of merging lookup set S(f, Bi) into the intermediate S(f, C):

- (6.1) — If each of the subobject members of S(f, Bi) is a base class subobject of at least one of the subobject members of S(f, C), or if S(f, Bi) is empty, S(f, C) is unchanged and the merge is complete. Conversely, if each of the subobject members of S(f, C) is a base class subobject of at least one of the subobject members of S(f, Bi), or if S(f, C) is empty, the new S(f, C) is a copy of S(f, Bi).

- (6.2) — Otherwise, if the declaration sets of S(f, Bi) and S(f, C) differ, the merge is ambiguous: the new S(f, C) is a lookup set with an invalid declaration set and the union of the subobject sets. In subsequent merges, an invalid declaration set is considered different from any other.

- (6.3) — Otherwise, the new S(f, C) is a lookup set with the shared set of declarations and the union of the subobject sets.

7 The result of name lookup for f in C is the declaration set of S(f, C). If it is an invalid set, the program is ill-formed.

[Example 1:

```cpp
struct A { int x; };
struct B { float x; };
struct C: public A, public B { };
struct D: public virtual C { };
struct E: public virtual C { char x; };
struct F: public D, public E { };
int main() {
    F f;
    f.x = 0;
}
// S(x,A) = { { A::x }, { A } }
// S(x,B) = { { B::x }, { B } }
// S(x,C) = { invalid, { A in C, B in C } }
// S(x,D) = S(x,C)
// S(x,E) = { { E::x }, { E } }
// S(x,F) = S(x,E)
// OK, lookup finds E::x
```

S(x, F) is unambiguous because the A and B base class subobjects of D are also base class subobjects of E, so S(x, D) is discarded in the first merge step. — end example]

8 If the name of an overloaded function is unambiguously found, overload resolution (12.4) also takes place before access control. Ambiguities can often be resolved by qualifying a name with its class name.

[Example 2:

```cpp
struct A {
    int f();
};

struct B {
    int f();
};

struct C : A, B {
    int f() { return A::f() + B::f(); }
};
```

— end example]

> 9 [Note 2: A static member, a nested type or an enumerator defined in a base class T can unambiguously be found even if an object has more than one base class subobject of type T. Two base class subobjects share the non-static member subobjects of their common virtual base classes. — end note]

[Example 3:

```cpp
struct V {
    int v;
};
```

— end example]
