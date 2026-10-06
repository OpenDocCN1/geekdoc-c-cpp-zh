# ISO/IEC 14882:2017(E)

```
Y y3 = (Y)z;
// OK: cast notation
}

void g(X a, &b) {
  int i = (a)? ? i*a : 0;
  int j = (a&&b) ? a+b : i;
  if (a) {
  n}
```

// end example
The conversion-type-id does not represent a function type nor an array type. The conversion-type-id in a conversion-function-id is the longest sequence of tokens that could form a conversion-type-id. [Note: This prevents ambiguities between the declarator operator and its expression counterparts.] [Example:

```
&ac.operator*int; // syntax error
  parsed as (&ac.operator)*i
  not as &(ac.operator*i)
```

The * is the pointer declarator and not the multiplication operator. // end example] This rule prevents ambiguities for attributes. [Example:

```
operator int [[noreturn]] O(); // error: noreturn attribute applied to a type
// end example; // end note]
```

+   Conversion functions are inherited.

+   Conversion functions can be virtual.

A conversion function template should not have a deduced return type (10.1.7.4). [Example:

```
struct S {
  operator auto() const { return 10; } // OK
  template<class T>
  operator auto() const { return 1; }; // error: conversion function template
};
 end example]
```

# 15.4 Destructors

+   In a declaration of the declarator, the declarator is a function declarator (11.3.5) of the form ptv-declarator (parameter-declaration-clause) noexcept-specifier-opt attribute-specifier-seq-opt where the ptv-declarator consists of only one id-declarator, an optional attribute-specifier-seq, and optional surrounding parentheses, and one of the following:

+   (1.1) in a member-declaration that belongs to the member-specification of a class but is not a friend declaration (14.3), the id-expression is ~class-name and the class-name is the injected-class-name (Clause 12) of the immediately enclosing class:

+   (1.2) in a member-declaration that belongs to the member-specification of a class template but is not a friend declaration, the id-expression is ~class-name and the class-name make the current instantiation (17.6.2.1) of the immediately enclosing class template;

+   (1.3) in a namespace scope or in a friend declaration, the id-expression is nested-specifier ~class-name and the class-name names the same class as the nested-specifier.

The class-name shall not be a typedef-name. A destructor takes no arguments (11.3.5). Each decl-specifier of the decl-specifier-seq of a destructor declaration (if any) should be friend, inline, or virtual.