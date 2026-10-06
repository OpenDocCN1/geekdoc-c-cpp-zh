# ISO/IEC 14882:2017(E)

```
sizeof(int a);           // expression
sizeof(int(unsigned a)); // type-id (ill-formed)

(int)0;                   // type-id (ill-formed)
int(a)+1;                // expression
int(unsigned a))+1;      // type-id (ill-formed)
}
// --- end example
```

3 Another ambiguity arises in a parameter-declaration-clause when a type-name is nested in parentheses. In this case, the choice is between the declaration of a parameter type pointer to function and the declaration of a parameter with redundant parentheses around the declarator-id. The resolution is to consider the type-name as a simple-type-specifier rather than a declarator-id. [Example:

```
Class C {
void f(int C) {}
void f(*fp)(C* p_param) { //n// not: void f(int C) {}
}
int g(C);
void foo() {
f(1);
// error: cannot convert 1 to function pointer
f(g);
// OK
}
```

For another example,

```
Class C {
void h(int *C[10]);
void h(*fp)(int* _C[10]);
// not: void h(int *C[10]);
}
// --- end example
```

[dcl.meaning]

# 11.3 Meaning of declarators

1 A declarator contains one declarator-id, it names the identifier that is declared. An unqualified-id occurring in a declarator shall be a simple identifier for the declaration of special functions (15.1, 15.3, 15.4, 16.6) and for the declaration of template specializations or partial specializations (17.7). When the declarator-id is qualified, the declaration shall refer to a previously declared member of the class or namespace to which the qualifier-id refers to (10.3.1) or to a specifier-prefix through which the member shall not merely have been introduced by a scope-specifier of the class or namespace de-id. The nested-name-specifier of a qualified declarator shall not begin with a decltype-specifier. Note: If the qualifier is the global : scope resolution operator, the declarator-id refers to a name declared in the global namespace scope. — end] The optional attribute-specifier following a declarator-id is

2 A static, thread_local, extern, mutable, friend, inline, virtual, constexpr, explicit, or typedef specifier applies directly to each declarator-id in an init-declarator-list or member-declarator-list; the type specified for each declarator-id depends on which decl-specifier-seq and its declarator.

3 Thus, a declaration of a particular declarator has the form

```
T

where T is the form of attribute-specifier-seq_out decl-specifier-seq and D is a declarator. Following is a recursive procedure for determining the type specifier for the contained declarator-id by such a declaration.
```

4 First, the decl-specifier-seq determines a type. In a declaration

```
T
```

© ISO/IEC 2017 — All rights reserved

204