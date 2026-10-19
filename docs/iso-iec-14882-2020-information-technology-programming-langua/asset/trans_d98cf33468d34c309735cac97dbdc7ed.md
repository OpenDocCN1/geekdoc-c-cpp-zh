

```
A* pa = &bobj;
B bobj;

// undefined behavior: upcast to a base class type
// definition of bobj
```

```
extern X xobj;
int* p3 = &xobj.i;
X xobj;

// OK, X is a trivial class
```

For another example,

```
struct W { int j; };
struct X : public virtual W { };
struct Y {
    int* p;
    X x;
    Y() : p(&x.j) {  // undefined, x is not yet constructed
    }
};
```
— end example

2 During the construction of an object, if the value of the object or any of its subobjects is accessed through a glvalue that is not obtained, directly or indirectly, from the constructor’s this pointer, the value of the object or subobject thus obtained is unspecified.

[Example 2:

```
struct C;
void no_opt(C*);

struct C {
    int c;
    C() : c(0) { no_opt(this); }
};

const C cobj;
```

```
void no_opt(C* cptr) {
    int i = cobj.c * 100;      // value of cobj.c is unspecified
    cptr->c = 1;
    cout << cobj.c * 100       // value of cobj.c is unspecified
         << '\n';
}
```

```
extern struct D d;
struct D {
    D(int a) : a(a), b(d.a) {}
    int a, b;
};
D d = D(1);    // value of d.b is unspecified
```
— end example

3 To explicitly or implicitly convert a pointer (a glvalue) referring to an object of class X to a pointer (reference) to a direct or indirect base class B of X, the construction of X and the construction of all of its direct or indirect bases that directly or indirectly derive from B shall have started and the destruction of these classes shall not have completed, otherwise the conversion results in undefined behavior. To form a pointer to (or access the value of) a direct non-static member of an object obj, the construction of obj shall have started and its destruction shall not have completed, otherwise the computation of the pointer value (or accessing the member value) results in undefined behavior.

[Example 3:

```
struct A { };
struct B : virtual A { };
struct C : B { };
struct D : virtual A { D(A*); };
struct X { X(A*); };
```

## ISO/IEC 14882:2020(E)

```
Thing(Thing&&);
private:
    Thing(const Thing&);
};

Thing f(bool b) {
    Thing t;
    if (b)
        throw t;        // OK: Thing(Thing&&) used (or elided) to throw t
    return t;           // OK: Thing(Thing&&) used (or elided) to return t
}

Thing t2 = f(false);    // OK: no extra copy/move performed, t2 constructed by call to f
```

```
struct Weird {
    Weird();
    Weird(Weird&);
};

Weird g() {
    Weird w;
    return w;           // OK: first overload resolution fails, second overload resolution selects Weird(Weird&)
}
— end example
```

5 [Example 3:

```
template<class T> void g(const T&);

template<class T> void f() {
    T x;
    try {
        T y;
        try { g(x); }
        catch (...) {
            if (/*...*/)
                throw x;        // does not move
            throw y;            // moves
        }
        g(y);
    } catch(...) {
        g(x);
        g(y);                   // error: y is not in scope
    }
}
— end example
```

## 11.11 Comparisons [class.compare]

### 11.11.1 Defaulted comparison operator functions [class.compare.default]

1 A defaulted comparison operator function (12.6.3) for some class C shall be a non-template function that is

- (1.1) — a non-static const non-volatile member of C having one parameter of type const C& and either no ref-qualifier or the ref-qualifier &, or
- (1.2) — a friend of C having either two parameters of type const C& or two parameters of type C.

A comparison operator function for class C that is defaulted on its first declaration and is not defined as deleted is implicitly defined when it is odr-used or needed for constant evaluation. Name lookups in the defaulted definition of a comparison operator function are performed from a context equivalent to its function-body. A definition of a comparison operator as defaulted that appears in a class shall be the first declaration of that function.

2 A defaulted <=> or == operator function for class C is defined as deleted if any non-static data member of C is of reference type or C has variant members (11.5.2).

## ISO/IEC 14882:2020(E)

3 A binary operator expression a @ b is usable if either

- (3.1) — a or b is of class or enumeration type and overload resolution (12.4) as applied to a @ b results in a usable candidate, or
- (3.2) — neither a nor b is of class or enumeration type and a @ b is a valid expression.

4 A defaulted comparison function is constexpr-compatible if it satisfies the requirements for a constexpr function (9.2.6) and no overload resolution performed when determining whether to delete the function results in a usable candidate that is a non-constexpr function.

> [Note 1: This includes the overload resolutions performed:
> - (4.1) — for an operator<=> whose return type is not auto, when determining whether a synthesized three-way comparison is defined,
> - (4.2) — for an operator<=> whose return type is auto or for an operator==, for a comparison between an element of the expanded list of subobjects and itself, or
> - (4.3) — for a secondary comparison operator @, for the expression x @ y.
> — end note

5 If the member-specification does not explicitly declare any member or friend named operator==, an == operator function is declared implicitly for each three-way comparison operator function defined as defaulted in the member-specification, with the same access and function-definition and in the same class scope as the respective three-way comparison operator function, except that the return type is replaced with bool and the declarator-id is replaced with operator==.

> [Note 2: Such an implicitly-declared == operator for a class X is defined as defaulted in the definition of X and has the same parameter-declaration-clause and trailing requires-clause as the respective three-way comparison operator. It is declared with friend, virtual, constexpr, or consteval if the three-way comparison operator function is so declared. If the three-way comparison operator function has no noexcept-specifier, the implicitly-declared == operator function has an implicit exception specification (14.5) that can differ from the implicit exception specification of the three-way comparison operator function. — end note]

> [Example 1:
```
template<typename T> struct X {
  friend constexpr std::partial_ordering operator<=>(X, X) requires (sizeof(T) != 1) = default;
  // implicitly declares: friend constexpr bool operator==(X, X) requires (sizeof(T) != 1) = default;

  [[nodiscard]] virtual std::strong_ordering operator<=>(const X&) const = default;
  // implicitly declares: [[nodiscard]] virtual bool operator==(const X&) const = default;
};
```
— end example

> [Note 3: The == operator function is declared implicitly even if the defaulted three-way comparison operator function is defined as deleted. — end note]

6 The direct base class subobjects of C, in the order of their declaration in the base-specifier-list of C, followed by the non-static data members of C, in the order of their declaration in the member-specification of C, form a list of subobjects. In that list, any subobject of array type is recursively expanded to the sequence of its elements, in the order of increasing subscript. Let xi be an lvalue denoting the ith element in the expanded list of subobjects for an object x (of length n), where xi is formed by a sequence of derived-to-base conversions (12.4.4.2), class member access expressions (7.6.1.5), and array subscript expressions (7.6.1.2) applied to x.

### 11.11.2 Equality operator [class.eq]

1 A defaulted equality operator function (12.6.3) shall have a declared return type bool.

2 A defaulted == operator function for a class C is defined as deleted unless, for each xi in the expanded list of subobjects for an object x of type C, xi == xi is usable (11.11.1).

3 The return value V of a defaulted == operator function with parameters x and y is determined by comparing corresponding elements xi and yi in the expanded lists of subobjects for x and y (in increasing index order) until the first index i where xi == yi yields a result value which, when contextually converted to bool, yields false. If no such index exists, V is true. Otherwise, V is false.

4 [Example 1:

