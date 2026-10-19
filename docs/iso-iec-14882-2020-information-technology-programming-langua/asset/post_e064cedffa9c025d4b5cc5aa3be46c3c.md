
```
struct A {
    int a;
    static int  s;
    enum { e };
};
struct B : A, virtual V { };
struct C : A, virtual V { };
struct D : B, C { };

void f(D* pd) {
    pd->v++;
    pd->s++;
    int i = pd->e;
    pd->a++;
}
— end example]
```

10 [Note 3: When virtual base classes are used, a hidden declaration can be reached along a path through the subobject lattice that does not pass through the hiding declaration. This is not an ambiguity. The identical use with non-virtual base classes is an ambiguity; in that case there is no unique instance of the name that hides all the others. — end note]

[Example 4:

```
struct V { int f();  int x; };
struct W { int g();  int y; };
struct B : virtual V, W {
    int f();  int x;
    int g();  int y;
};
struct C : virtual V, W { };

struct D : B, C { void glorp(); };
```

![Figure 6: Name lookup [fig:class.lookup]](img/f00894146489220e5849acc131e0a0e1_308_0.png)

As illustrated in Figure 6, the names declared in V and the left-hand instance of W are hidden by those in B, but the names declared in the right-hand instance of W are not hidden at all.

```
void D::glorp() {
    x++;
    f();
    y++;
    g();
}
— end example]
```

11 An explicit or implicit conversion from a pointer to or an expression designating an object of a derived class to a pointer or reference to one of its base classes shall unambiguously refer to a unique object representing the base class.

[Example 5:

```
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

[Example 6:

```
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

## 11.9 Member access control [class.access]

### 11.9.1 General [class.access.general]

1 A member of a class can be

-   (1.1) — private; that is, its name can be used only by members and friends of the class in which it is declared.
-   (1.2) — protected; that is, its name can be used only by members and friends of the class in which it is declared, by classes derived from that class, and by their friends (see 11.9.5).
-   (1.3) — public; that is, its name can be used anywhere without access restriction.

2 A member of a class can also access all the names to which the class has access. A local class of a member function may access the same names that the member function itself may access.115

3 Members of a class defined with the keyword class are private by default. Members of a class defined with the keywords struct or union are public by default.

[Example 1:

```
class X {
    int a;            // X::a is private by default
};

struct S {
    int a;
};
// S::a is public by default
— end example]
```

4 Access control is applied uniformly to all names, whether the names are referred to from declarations or expressions.

[Note 1: Access control applies to names nominated by friend declarations (11.9.4) and using-declarations (9.9). — end note]

In the case of overloaded function names, access control is applied to the function selected by overload resolution.

[Note 2: Because access control applies to names, if access control is applied to a typedef name, only the accessibility of the typedef name itself is considered. The accessibility of the entity referred to by the typedef is not considered. For example,

```
class A {
    class B { };
    public:
        typedef B BB;
};

void f() {
    A::BB x;        // OK, typedef name A::BB is public
    A::B y;         // access error, A::B is private
}
```

— end note]

5 [Note 3: Access to members and base classes is controlled, not their visibility (6.4.10). Names of members are still visible, and implicit conversions to base classes are still considered, when those members and base classes are inaccessible. — end note]

The interpretation of a given construct is established without regard to access control. If the interpretation established makes use of inaccessible member names or base classes, the construct is ill-formed.

6 All access controls in 11.9 affect the ability to access a class member name from the declaration of a particular entity, including parts of the declaration preceding the name of the entity being declared and, if the entity is a class, the definitions of members of the class appearing outside the class’s member-specification.

[Note 4: This access also applies to implicit references to constructors, conversion functions, and destructors. — end note]

7 [Example 2:

```
class A {
    typedef int I;      // private member
    I f();
    friend I g(I);
    static I x;
    template<int> struct Q;
    template<int> friend struct R;
protected:
    struct B { };
};
```

```
A::I A::f() { return 0; }
A::I g(A::I p = A::x);
A::I g(A::I p) { return 0; }
A::I A::x = 0;
template<A::I> struct A::Q { };
template<A::I> struct R { };

struct D: A::B, A { };
```

Here, all the uses of A::I are well-formed because A::f, A::x, and A::Q are members of class A and g and R are friends of class A. This implies, for example, that access checking on the first use of A::I must be deferred until it is determined that this use of A::I is as the return type of a member of class A. Similarly, the use of A::B as a *base-specifier* is well-formed because D is derived from A, so checking of *base-specifiers* must be deferred until the entire *base-specifier-list* has been seen. — end example]

8 The names in a default argument (9.3.4.7) are bound at the point of declaration, and access is checked at that point rather than at any points of use of the default argument. Access checking for default arguments in function templates and in member functions of class templates is performed as described in 13.9.2.

9 The names in a default *template-argument* (13.2) have their access checked in the context in which they appear rather than at any points of use of the default *template-argument*.

[Example 3:

```
class B { };
template <class T> class C {
protected:
    typedef T TT;
};

template <class U, class V = typename U::TT>
class D : public U { };

D <C<B> *> d;        // access error, C::TT is protected
```

— end example]

### 11.9.2 Access specifiers [class.access.spec]

1 Member declarations can be labeled by an *access-specifier* (11.7):

```
*access-specifier* : *member-specification*opt
```

An *access-specifier* specifies the access rules for members following it until the end of the class or until another *access-specifier* is encountered.

[Example 1:

```
class X {
    int a;            // X::a is private by default: class used
public:
    int b;            // X::b is public
    int c;            // X::c is public
};
```

— end example]

2 Any number of access specifiers is allowed and no particular order is required.

[Example 2:

```
struct S {
    int a;            // S::a is public by default: struct used
protected:
    int b;            // S::b is protected
private:
    int c;            // S::c is private
public:
    int d;            // S::d is public
};
```

— end example]

3 [Note 1: The effect of access control on the order of allocation of data members is specified in 7.6.9. — end note]

4 When a member is redeclared within its class definition, the access specified at its redeclaration shall be the same as at its initial declaration.

[Example 3:

```
struct S {
    class A;
    enum E : int;
private:
    class A { };        // error: cannot change access
```
