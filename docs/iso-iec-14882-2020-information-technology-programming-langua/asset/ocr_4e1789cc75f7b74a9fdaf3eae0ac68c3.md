# ISO/IEC 14882:2020(E)

17 In a using-declarator that does not name a constructor, all members of the set of introduced declarations shall be accessible. In a using-declarator that names a constructor, no access check is performed. In particular, if a derived class uses a using-declarator to access a member of a base class, the member name shall be accessible. If the name is that of an overloaded member function, then all functions named shall be accessible. The base class members mentioned by a using-declarator shall be visible in the scope of at least one of the direct base classes of the class where the using-declarator is specified.

18 [Note 8: Because a using-declarator designates a base class member (and not a member subobject or a member function of a base class subobject), a using-declarator cannot be used to resolve inherited member ambiguities.

[Example 13:

```
struct A { int x(); };
struct B : A {};
struct C : A {
    using A::x;
    int x(int);
};

struct D : B, C {
    using C::x;
    int x(double);
};
int f(D* d) {
    return d->x();    // error: overload resolution selects A::x, but A is an ambiguous base class
}
```

— end example]

— end note]

19 A synonym created by a using-declaration has the usual accessibility for a member-declaration. A using-declarator that names a constructor does not create a synonym; instead, the additional constructors are accessible if they would be accessible when used to construct an object of the corresponding base class, and the accessibility of the using-declaration is ignored.

[Example 14:

```
class A {
    private:
        void f(char);
    public:
        void f(int);
    protected:
        void g();
};

class B : public A {
    using A::f;        // error: A::f(char) is inaccessible
    public:
    using A::g;        // B::g is a public synonym for A::g
};
```

— end example]

20 If a using-declarator uses the keyword typename and specifies a dependent name (13.8.3), the name introduced by the using-declaration is treated as a typedef-name (9.2.4).

# 9.10 The asm declaration [dcl.asm]

1 An asm declaration has the form

```
asm-declaration:
    attribute-specifier-seq_opt asm ( string-literal ) ;
```

The asm declaration is conditionally-supported; its meaning is implementation-defined. The optional attribute-specifier-seq in an asm-declaration appertains to the asm declaration.

> [Note 1: Typically it is used to pass information through the implementation to an assembler. — end note]