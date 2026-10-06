# ISO/IEC 14882:2017(E)

```
class M {
    friend void f() { // definition of global f, a friend of M
        // not the definition of a member function
};
// — end example ]
```

+   7 Such a function is an inline function (10.1.6). A friend function defined in a class is in the (lexical) scope of the class in which it is defined. A friend function defined outside the class is not (6.4.1).

+   8 No storage-class-specifier appears in the decl-friend-seq of a friend declaration.

+   9 A name nominated by a friend declaration shall be accessible in the scope of the class containing the friend declaration. The meaning of the friend declaration is same whether the friend declaration appears in the private or public (12.2) portion of the class member-specification.

+   10 Friendship is neither inherited nor transitive. [Example:

```
class A {
    friend class B;
    int a;
};
class B {
    friend class C;
};
nclass C {
    void f(A* p) {
        p->a++; // error: C is not a friend of A despite being a friend of B
    }
}
nclass D : public B {
    void f(A* p) {
        p->a++; // error: D is not a friend of A despite being derived from B
    }
}
// end example ]
```

+   11 If a friend declaration appears in a local class (12.4) and the name specified is an unqualified name, a prior declaration is looked up without considering scopes that are outside the innermost enclosing non-class scope. For a friend function declaration, if there is no prior declaration, the program is ill-formed. For a class declaration, if there is no prior declaration, the class that specified belongs to the innermost enclosing non-class scope, but if it is subsequently referenced, its name is not found by name lookup until a matching declaration is provided in the innermost enclosing non-class scope. [Example:

```
class X;
void a();
void f();
class Y {
    extern void b;
class A {
    friend class X; // OK, but X is a local class, not ::X
    friend class Y; // OK
    friend class Z; // OK, introduces local class Z
    friend void a(); // error, ::a is not considered
    friend void b(); // OK
```

§ 14.3

©ISO/IEC 2017 - All rights reserved

274