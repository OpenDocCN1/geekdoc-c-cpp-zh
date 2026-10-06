
# ISO/IEC 14882:2017(E)

has a virtual base class of type V. Given the class C defined above, an object of class C will have one subobject of V, as shown in Figure 4.

- 7 [Note: A class can have both virtual and non-virtual base classes of a given type.

```cpp
class B { / ... / };
class X : virtual public B { / ... / };
class Y : virtual public B { / ... / };
class Z : public B { / ... / };
class AA : public X, public Z { / ... / };
```

For an object of class AA, all virtual occurrences of base B in the lattice of AA correspond to a single B subobject within the type of AA, and every other occurrence of a (non-virtual) base class B in the lattice of AA one-to-one with a distinct B subobject within the type of AA. Given the class AA defined above, class AA has two subobjects of B: Z and the virtual B shared by X and Y, as shown in Figure 5.

![](img/feea898746c6066176386930de01055d_269_0.png)

end note Figure 5 Virtual and non-virtual base class]

## 13.2 Member lookup [class.member.lookup]

- 1 Member name lookup determines the name of a (id-expression) in class (6.3.7). Name lookup can result in an ambiguity, in which case the program is ill-formed. For an id-expression, name lookup begins in the scope of the thing; for a qualified-id, name lookup begins in the scope of the nested-name-specifier. Name lookup takes precedence before access (6.4, 14.4).

- 2 The following steps define the set of name lookup for member f in a class C.

- 3 The lookup set for f in C, S(f,C), consists of two component sets: the declarations set (possibly including using-declarations) f; the subobject set, a set of subsets where declarations of these members are overridden. In the declaration set, using-declarations are replaced by those of designated declarations that are not hidden or overridden (10.3.3), and type declarations (including nested-class declarations). S(f,C) is calculated as follows:

- 4 If C contains a declaration of name f, the declaration set contains every declaration of f declared in C that satisfies the requirements of the language construct in which the lookup occurs. Note: Looking up in an elaborated-type-specifier (6.4.4) or base-specifier (10.3), for instance, ignores all non-type declarations, while looking up a name in a nested-name-specifier (6.4.3) ignores function, variable, and enumerator declarations. As an example, looking up a name in a using-declaration (10.33) includes the declaration of a class or enumeration that would ordinarily be hidden by another declaration of name in the same scope. end note] If the resulting declaration set is not empty, the subobject contains C itself, and calculation is complete.

- 5 Otherwise (i.e., C does not contain a declaration of f or the resulting declaration set is empty), S(f,C) is initially empty. If C has base classes, the lookup set for f in each direct base class subobject B, and merge each lookup set S(f,B) into S(f,C).

- 6 The following steps define the result of merging lookup $S(f, B_i)$ into the intermediate $S(f, C)$:

- (6.1) If each of the subject members of $S(f, B_i)$ is a base class subobject of at least one of the subject members of $S(f, C)$, or if $S(f, B_i)$ is empty, $S(f, C)$ is unchanged and the merge is aborted. Conversely, if each of the subject members of $S(f, C)$ is a base class subobject of at least one of the subject members of $S(f, B_i)$, or if $S(f, C)$ is empty, the new $S(f, C)$ is a copy of $S(f, B_i)$.

- (6.2) Otherwise, if the declaration sets of $S(f, B_i)$ and $S(f, C)$ differ, the merge is ambiguous: the new $S(f, C)$ is a lookup with an invalid declaration and the union of the subobject sets. In subsequent merges, an invalid declaration is considered different from other.

- (6.3) Otherwise, the new $S(f, C)$ is a lookup set with shared declarations and the union of the subject sets.

- 7 The result of name lookup for $f$ in $C$ is the declaration defined in $S(f, C)$. If it is an invalid, the program is ill-formed. [Example]:

```cpp
struct A {
  int x;
};
struct B {
  float x;
};
struct C : public A, B {};
struct D : public virtual C {
  char x;
};
struct E : public virtual C {};
struct F : public D, E {};
int main() {
  int f;
  f;
}
```

- 8 If the name of overloaded function is found, overload resolution (6.3) takes place before access. Ambiguities can be resolved by qualifying with its class. [Example]:

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
struct V {
  int v;
};
struct A {
  int a;
  static int s;
  enum { e };
};
struct B : A, virtual V {};
```

- 9 [Note: A static member, a nested type or enumerator can be found if an object has more than one class subobject of type T. Two class subobjects share the non-static member objects of their common base classes. [Example]:

```cpp
struct C : A, virtual V {};
struct D : B, C {};
void f(D* pd) {
    pd->v++; // OK: one v (virtual)
    pd->s++; // OK: one s (static)
    int i = pd->e; // OK: one e (enumerator)
    pd->d++; // error, ambiguous: two in D
}
```

- 10 Note: When virtual base classes are used, a hidden declaration can be reached along a path that does not pass through the hiding declaration. This is not an ambiguity. The identical use with non-virtual base classes is an ambiguity; in case there is no instance of the name that hides others. [Example]:

```cpp
struct V { int f0(); int x; };
struct W { int g0(); int y; };
struct B : virtual V, W {
    int f0(); int x;
    int g0(); int y;
};
struct C : virtual V, W {};
struct D : B, C { void glorp(); };
```

![](img/feea898746c6066176386930de01055d_271_0.png)

Figure 6 — Name lookup

The names declared in V and the left-hand instance of W are hidden by those in B, but the names declared in the right-hand instance of W are not hidden at all.

```cpp
void D::glorp() {
    x++; // OK: B::x hides V::x
    f0(); // OK: B::f hides V::f()
    y++; // error: B::y and C's W::y
    g0(); // error: B::g0() and C's W::g0()
}
```

- 11 An explicit or implicit conversion from a pointer to an expression designating an object of a derived class to a pointer or reference to one of its base classes shall unambiguously refer to a unique object representing the base class. [Example]:

```cpp
struct V {};
struct A {};
struct B : A, virtual V {};
struct C : A, virtual V {};
```

```cpp
struct D : B, C {
  void g() {
    D d;
    B* pb = &d;
    A* pa = &d;
    V* pv = &d; // error, ambiguous: C's A or B's A?
    // OK: only one V subobject
  }
};
```

- [Note: Even if the result of name lookup is unambiguous, a name found in multiple subobjects might still be ambiguous (7.12, 8.2.5, 14.2). [Example]:

```cpp
struct B1 {
  void f();
  static void f(int);
  int i;
};
struct B2 {
  void f(double);
};
struct I1 : B1 {};
struct I2 : B1 {};

struct D : I1, I2, B2 {
  using B1::f;
  using B2::f;
  void g() {
    f(); // Ambiguous conversion of this
    f(0); // Unambiguous (static)
    f(0.0); // Unambiguous (only one B2)
    int I1::i = &d; // Unambiguous
    int D::i = &d; // Ambiguous conversion
  }
};
```

## 13.3 Virtual functions

- 1 [Note: Virtual functions support dynamic binding and object-oriented programming. — end note] A class that declares a virtual function is called a polymorphic class.

- 2 If a virtual function vf is declared in a class Base and in a class Derived, derived directly or indirectly from Base, a member function with the same name, parameter-list (11.3.5), cv-qualification, and ref-qualifier (or absence of same) as Base::vf is then, declared: vf is virtual (whether or not it is declared) and overrides any virtual function of it. A virtual member function C::vf of a class S is a final overrider unless the derived class (4.5) of S is a base subclass (if) declares or inherits another member function that overrides vf. [Example]:

```cpp
struct A {
  void f();
}
```
