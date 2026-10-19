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
— end example
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

![](bbox=[0.38, 0.52, 0.65, 0.61])

Figure 6: Name lookup  [fig:class.lookup]

As illustrated in Figure 6, the names declared in V and the left-hand instance of W are hidden by those in B, but the names declared in the right-hand instance of W are not hidden at all.

```
void D::glorp() {
    x++;
    f();
    y++;
    g();
}
— end example
```

11 An explicit or implicit conversion from a pointer to or an expression designating an object of a derived class to a pointer or reference to one of its base classes shall unambiguously refer to a unique object representing the base class.