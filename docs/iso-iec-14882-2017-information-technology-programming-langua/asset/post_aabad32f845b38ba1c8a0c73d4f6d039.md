
# ISO/IEC 14882:2017(E)

```cpp
// C++ language linkage; the parameter has type "pointer to C function"

FUNC_c mf2;
// the name of the function mf2 and the function's type have
// C++ language linkage

static FUNC_c* q;
// the name of the data member q has C++ language linkage and
// the data member's type is "pointer to C function"

extern "C" {
class X {
    void mf2();
    void mf2(void(*())());
    // the name of the function mf and the function's type have
    // C++ language linkage;
    // the name of the function mf2 C++ language linkage;
    // the parameter has type "pointer to C function"
};
// end example;
```

5 if two declarations declare functions with the same name and parameter-list (11.3-5) to be members of the same namespace or declare objects with the same name to be members of the same namespace and declarations give different language linkages, the program is ill-formed; no diagnostic is required if the declarations appear in different translation units. Except for C++ language, a function without a linkage specification shall not precede the first linkage specification for that function. A function can be declared without a linkage specification unless a linkage specification has been seen; the linkage explicitly specified in the earlier declaration is not such a function declaration.

6 At most one function with a particular name can have C language linkage. Two declarations for a function with the same name and C language linkage (ignoring the names that qualify it) that appear in different namespaces refer to the same function. Two declarations for a variable with C language linkage with the same name in a global scope refer to different variables and is ill-formed unless both declarations denote the same entity; no entity shall be declared with the same name in a global scope, unless that with C language linkage shall be declared with the same name as with C language linkage (ignoring the names that qualify the respective names); no diagnostic is required if the declarations appear in different translation units. _Note: Only one definition for a given name with C language linkage may appear in the program (see 6.3); this implies that an entity must not be defined in more than one namespace scope._ end node; Example:

```cpp
int x;
namespace B {
    extern "C" int f();
    extern "C" int g() { return 1; }
    extern "C" int h();
    extern "C" int x0;
} // ill-formed: same name as global-scope object

namespace B {
    extern "C" int f();
    extern "C" int g() { return 1; } // ill-formed, the function g with C language linkage has two definitions
}

int A::f() { return 98; };
```

§ 10.5

©ISO/IEC 2017 - All rights reserved

193

# ISO/IEC 14882:2017(E)

```cpp
extern "C" int h() { return 97; } // definition for the function h with C language linkage
// A::h and h refer to the same function
// end example[]
```

- 7 A declaration directly contained in a linkage-specification is treated as if it contains the extern specifier (10.1.1) for the purpose of determining the linkage of the declared name and whether it is a definition. Such a declaration shall not specify a storage class. [Example:
extern "C" double f(); // error
static double f();
extern "C" int i; // declaration
{
} // definition
extern "C" static void g(); // error
// end example[]]

- 8 [Note: Because the linkage language is part of a function type, indirecting through a pointer to C function, the function to which the resulting value is considered a C function. — end note]
9 Link from C++ to objects defined in other languages and to objects in C++ from other languages is implementation-dependent and language-dependent. Only where the object layout strategies of two languages are similar enough can such linkage be achieved.

## 10.6 Attributes [dcl.attr]

## 10.6.1 Attribute syntax and semantics [dcl.attr.grammar]

- 1 Attributes specify additional information for various source constructs such as types, variables, names, blocks, or translation units.
attribute-specifier-seg:
attribute-specifier-seq_opt attribute-specifier
attribute-specifier:
[[ attribute-using-prefix_opt attribute-list ]]
alignment-specifier:
alignment-specifier:
alignas (type-id, ...opt)
alignas (constant-expression ...opt)
attribute-using-prefix:
using attribute-namespace :
attribute-list:
attribute-list_opt
attribute-list , attribute_opt
attribute:
attribute , ...
attribute-list , attribute ...
attribute:
attribute-token attribute-argument-clause_opt
attribute-token:
identifier
attribute-scoped-token:
attribute-scoped-token:
attribute-namespace :: identifier

attribute-namespace:
identifier

attribute-argument-clause:
balanced-token-seq-opt ]

balanced-token-seq:
balanced-token
balanced-token-seq-balanced-token

balanced-token:
 { balanced-token-seq-opt }
 { balanced-token-seq-opt }
 any other than a parenthesis, a bracket, or a brace

- 2 If an attribute-specifier contains an attribute-using-prefix, N shall not contain an attribute-scoped-token and every attribute-token in attribute-list is treated as if its identifier prefixed with N; N is the attribute-namespace specified in the attribute-using-prefix. (Note: This rule imposes no constraints on how an attribute-using-prefix affects the tokens in an attribute-clause. — end note) Example:

```cpp
using CC: opt(1), [[debug]]
void f() {
using CC: opt(1)) [[CC::debug]] // same as [[CC:opt(1)] [[CC::debug]]
using G: opt(1));
// error: cannot combine using and scoped attribute-token
}
```

- 3 For each attribute-list, an ellipsis may appear only if the form of the balanced-token-seq will be specified. — end note

- 4 In an attribute-list, an ellipsis (17.3.3). An attribute-specifier that contains no attributes has no effect. The order in which the attribute-tokens appear in an attribute-list is not significant. If a keyword (5.11) or an alternative (5.10) is considered, no lookup (6.4) is performed on any of the identifiers contained in an attribute-token, it is considered. The attribute-token determines additional requirements on the attribute-argument-clause. — end note

- 5 Each attribute-specifier is said to pertain to some entity or statement, if the attribute-specifier-seq that appertains to some entity contains an attribute alignment-specifier that is not allowed to apply to that entity, the program is ill-formed. If an attribute-specifier appears to a friend declaration (14.3), a declaration shall be made. No attribute-specifier shall pertain to an explicit instantiation (17.7.2).

- 6 For an attribute-token (including an attribute-scoped-token) not specified in this document, the behavior is implemented-defined. Any attribute-token that is not recognized by the implementation is ignored. [Note: — each implementation should choose a distinct name for the attribute-namespace in an attribute-scoped-token. — end note]

Two consecutive left square brackets shall appear only when indicating an attribute-specifier or within the balanced-token-seq. [Note: If two square brackets appear where an attribute-specifier is not allowed, the program is ill-formed]

```cpp
alignas(1) struct U {
struct alignas(16) {
 S;
};
// error: U aligns an alignment that is less strict than if the alignas(1) were omitted
```

# ISO/IEC 14882:2017(E)

```cpp
alignas(1) struct U {
struct alignas(16) {
 S;
};
// error: U aligns an alignment that is less strict than if the alignas(1) were omitted
```

## 10.6.2 Alignment specification

1 Alignment-specifier may be applied to a variable or a class, but it should not be applied to a bit-field, a function parameter, or exception-declaration (18.3).

2 When the alignment-specifier is of the form aligns(constant-expression) :
   (2.1) the constant-expression evaluates
   (2.2) if the expression does not evaluate to an alignment value (6.11), or if it extends an alignment and the implementation does not support that, the program is ill-formed.

3 An alignment-specifier of an entity of the form aligns(type-id) has the same effect as aligns(alignof(type-id)) (8.3.6).

4 The requirement of alignment of an entity is strictly the nonzero alignment specified by its alignment-specifiers, if any; otherwise, the alignment-specifiers have no effect.

5 The combined effect of all alignment-specifiers in a declaration shall not specify an alignment that is less strict than the alignment that would be required for the entity being declared if all alignment-specifiers were omitted. [Example:

```cpp
struct aligns(1) U {
struct aligns(16) {
 S;
};
// error: U aligns an alignment that is less strict than if the aligns(1) were omitted
```

6 If the definition of an entity has an alignment-specifier, any non-defining declaration of entity shall either specify equivalent alignment or no alignment-specifier. Conversely, if any declaration of an entity has an alignment-specifier, every declaration of that entity shall have an equivalent alignment. A diagnostic is required if an entity has different alignment-specifiers in different translation units. [Example:

```cpp
// Translation unit #1:
struct S { int x; } s, *p = &s;

// Translation unit #2:
struct aligns(16) S;
extern S p;
// error: definition of S lacks a definition, no diagnostic required
```

7 [Example: An aligned buffer with an alignment of A and holding N elements of type T can be declared as:

alignas(T) aligns(A) T[N]; ensures that the final requested alignment will not be weaker than alignof(T), and
