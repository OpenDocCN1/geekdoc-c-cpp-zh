# ISO/IEC 14882:2017(E)

Example:

```
```
ttypedef void *p;
typef const int *q;
typef int **pi;
typef const int **pci;
```
```

The composite type of p and q is "pointer to const void"; the composite type of pi and pci is "pointer to const pointer to const int". — end example

# 8.1 Primary expressions

+   - primary-expression:
  - literal
  - this
  - ( expression )
  - id-expression
  - lambda-expression
  - fold-expression

# 8.1.1 Literals

A literal is a primary expression. Its type depends on its form (5.13). A string literal is an lvalue; all literals are prvalues.

# 8.1.2

The keyword names a pointer to the object for a non-static member template of a class X, or a static-data member initializer (12.2) is evaluated.

If a declaration declares a member function or member template, this expression is a prvalue of "pointer to co-qualifier-seq X" between the optional co-qualifier-seq and the end of the function-declarator, member-initializer. It should not appear before the optional co-qualifier-seq and will not appear within the declaration of a static member function (although its type and value category are defined within a static member function as they are within a static member function). [Note: This declaration matching does not occur until the complete declarator is known. — end note] Unlike the expression in other contexts, *this is not required to be of complete type for purposes of class member body. [Note: Only class members declared prior to the declaration are visible. — end note][Example:

```
```
struct A {
  char *ptr;
  template<class T> f(T t) -> decltype(g(t)) {
    return t;
  }
};
template auto A::f(int t) -> decltype(g(t));
```
```

Otherwise, if a member-declarator declares a non-static member (12.2) of a class X, the expression is a prvalue of "pointer to X" within the optional default member initializer (12.2). It should not appear in the member-declarator.

The expression this shall not appear in any other context. [Example:

```
```
class Outer {
  int a(sizeof(*this)); // error: not inside a member function
  unsigned int sz = sizeof(*this); // OK: in default member initializer

  void f() {}
```
```

©ISO/IEC 2017 - All rights reserved