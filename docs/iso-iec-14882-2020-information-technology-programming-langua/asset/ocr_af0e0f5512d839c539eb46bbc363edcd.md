[Example 2:

```
void f(int n) {
    [] { n = 1; };                // error: n is not odr-usable due to intervening lambda-expression
    struct A {
        void f() { n = 2; }         // error: n is not odr-usable due to intervening function definition scope
    };
    void g(int = n);               // error: n is not odr-usable due to intervening function parameter scope
    [=](int k = n) {};             // error: n is not odr-usable due to being
                                   // outside the block scope of the lambda-expression
    [&] { [n]{ return n; }; };     // OK
}
```

— end example

10 Every program shall contain exactly one definition of every non-inline function or variable that is odr-used in that program outside of a discarded statement (8.5.2); no diagnostic required. The definition can appear explicitly in the program, it can be found in the standard or a user-defined library, or (when appropriate) it is implicitly defined (see 11.4.5.2, 11.4.5.3, 11.4.7, and 11.4.6).

[Example 3:

```
auto f() {
    struct A {};
    return A{};
}
decltype(f()) g();
auto x = g();
```

A program containing this translation unit is ill-formed because g is odr-used but not defined, and cannot be defined in any other translation unit because the local class A cannot be named outside this translation unit. — end example

11 A definition domain is a private-module-fragment or the portion of a translation unit excluding its private-module-fragment (if any). A definition of an inline function or variable shall be reachable from the end of every definition domain in which it is odr-used outside of a discarded statement.

12 A definition of a class shall be reachable in every context in which the class is used in a way that requires the class type to be complete.

[Example 4: The following complete translation unit is well-formed, even though it never defines X:

```
struct X;          // declare X as a struct type
struct X* x1;      // use X in pointer formation
X* x2;             // use X in pointer formation
```

— end example

[Note 3: The rules for declarations and expressions describe in which contexts complete class types are required. A class type T must be complete if:

+   (12.1) — an object of type T is defined (6.2), or
+   (12.2) — a non-static class data member of type T is declared (11.4), or
+   (12.3) — T is used as the allocated type or array element type in a new-expression (7.6.2.8), or
+   (12.4) — an lvalue-to-rvalue conversion is applied to a glvalue referring to an object of type T (7.3.2), or
+   (12.5) — an expression is converted (either implicitly or explicitly) to type T (7.3, 7.6.1.4, 7.6.1.7, 7.6.1.9, 7.6.3), or
+   (12.6) — an expression that is not a null pointer constant, and has type other than cv void*, is converted to the type pointer to T or reference to T using a standard conversion (7.3), a dynamic_cast (7.6.1.7) or a static_cast (7.6.1.9), or
+   (12.7) — a class member access operator is applied to an expression of type T (7.6.1.5), or
+   (12.8) — the typeid operator (7.6.1.8) or the sizeof operator (7.6.2.5) is applied to an operand of type T, or
+   (12.9) — a function with a return type or argument type of type T is defined (6.2) or called (7.6.1.3), or
+   (12.10) — a class with a base class of type T is defined (11.7), or
+   (12.11) — an lvalue of type T is assigned to (7.6.19), or
+   (12.12) — the type T is the subject of an alignof expression (7.6.2.6), or
+   (12.13) — an exception-declaration has type T, reference to T, or pointer to T (14.4).

— end note