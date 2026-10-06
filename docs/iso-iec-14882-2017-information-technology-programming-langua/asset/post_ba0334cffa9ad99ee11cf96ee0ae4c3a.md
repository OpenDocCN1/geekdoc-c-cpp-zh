
# ISO/IEC 14882:2017(E)

## 10.6.8 attribute-token noreturn

The attribute-token noreturn specifies that a function does not return. It shall appear at most once in each attribute-list and no attribute-argument-clause shall be present. The attribute may be applied to the declator-id in a function declaration. The first declaration of a function shall specify the noreturn attribute if any declaration of that function specifies the noreturn attribute. If a function is declared without the noreturn attribute in either translation unit, the program is ill-formed, no diagnostic required.

If a function f is called where f was previously declared with the noreturn attribute and f eventually returns, the behavior is undefined. [Note: The function may terminate by throwing an exception.] — end note|if a function marked [noreturn] might return. — end note

[Note: Implementations should issue a warning if a function marked [noreturn] might return. — end note

+ 3 [Example:]

```cpp
[[noreturn]] void f() {
    throw "error";
    // OK
}

[[noreturn]] void q(int i) {
    // behavior is undefined if called with an argument <= 0
    if (i > 0)
        throw "positive";
}
```
— end example

# ISO/IEC 14882:2017(E)

## 11 Declarators [dcl.decl]

A declarator declares a single variable, function, or type, within a declaration. The *init-declarator-list* appearing in a declaration is a comma-separated sequence of declarators, each of which can have an initializer.

- *init-declarator-list:*
  - *init-declarator*
  - *init-declarator-list*, *init-declarator*
  - *init-declarator:*
    - *declarator initializer-opt*

The three components of a *simple-declaration* are (10.6), the specifiers (*dcl-specifier-seq*; 10.1) and the declarators (*init-declarator-list*). The specifiers indicate the type, storage class or other properties of the entities being declared. The declarators specify names with operators such as * (pointer) to () (function returning). Initial values can also be specified in a declarator; initializers are in 11.6 and 15.6.

Each *init-declarator* in a declaration is analyzed separately as if it was in a declaration by itself. [Note: A declarator with several declarators is usually equivalent to the corresponding sequence of declarations each with a single declarator.

```
T D1, D2; ... Dn;
```
is usually equivalent to
```
T D1; D2; ... Dn;
```

Where T is a *dcl-specifier-seq* and D Di is an *init-declarator*. One exception is when a name introduced by one of the *declarators* has a type name used by the *dcl-specifiers*, so that when the same *dcl-specifiers* are used in a consequent declaration, they do not have the same meaning, as in

```cpp
struct S { ... };
S, T; // two instances of struct S
```

which is not equivalent to

```cpp
struct S { ... };
S;
T; // error
```

Another exception is when T is auto (10.1.7.4), for example:

```cpp
auto i = 1; j = 2.0;      // error: deduced types for i and j do not match
as opposed to
auto i = 1;                     // OK: i deduced to have type int
auto j = 2.0;                    // OK: j deduced to have type double
```

4 Declarators have the syntax

- *declarator:*
  - *ptr-declarator*
  - *nptr-declarator parameters-and-qualifiers trailing-return-type*

- *ptr-declarator:*
  - *nptr-declarator*
  - *ptr-operator ptr-declarator*

# ISO/IEC 14882:2017(E)

noptr-declarator:
declarator-id attribute-specifier-seq_opt
noptr-declarator parameters-and-qualifiers
noptr-declarator [ constant-expression_opt ] attribute-specifier-seq_opt
( ptr-declarator-qualifiers ):

parameters-and-qualifiers:
( parameter-declaration-clause ) cv-qualifier-seq_opt
ref-qualifier-specifier cv-qualifier attribute-specifier-specifier

trailing-return-type:
-> type-id

- *ptr-operator:*
  - * attribute-specifier-seq_opt cv-qualifier-seq_opt
  - & attribute-specifier-seq_opt
  - && attribute-specifier-seq_opt
  - nested-name-specifier * attribute-specifier-seq_opt cv-qualifier-seq_opt

cv-qualifier-seq:
cv-qualifier cv-qualifier-seq_opt

cv-qualifier:
const
volatile

ref-qualifier:
&

declarator-id:
... opt id-expression

## 11.1 Type names [dcl.name]

1 To specify type conversions, and as an argument of sizeof, alignof, new, or type, the name of a type should be specified. This can be done with a type-id, which is syntactically a declaration for a variable or function that types the name of the entity.

type-id:
type-specifier-seq abstract-declarator_opt

defining-type-id:
defining-type-specifier-seq abstract-declarator_opt

abstract-declarator:
ptr-declarator noptr-declarator_opt parameters-and-qualifiers trailing-return-type

ptr-declarator:
noptr-declarator ptr-operator abstract-declarator_opt

noptr-declarator:
noptr-declarator [ constant-expression_opt ] attribute-specifier-seq_opt

abstract-pack-declarator:
noptr-abstract-pack-declarator ptr-operator abstract-pack-declarator( )

# ISO/IEC 14882:2017(E)

noptr-abstract-pack-declarator:
noptr-abstract-pack-declarator parameters-and-qualifiers [ constant-expression_opt ] attribute-specifier-seq_opt

It is possible to uniquely identify the location in the abstract-declarator where the identifier would appear if the construction was a declaration. A name is then the same as the type of the identifier. [Example:

```cpp
int                         // int
int *                        // int *
int *[3]                   // int *[3]
int (*)                    // int (*)
int (*double)              // int (*double)
```
names the type "int", "pointer to int", "array of 3 pointers to int", "function of (no parameters) mentioned in 9.8, and "pointer to function of (double) returning to int"

2 A type can be named (often easily) using a type-id (10.1.3).

## 11.2 Ambiguity resolution [dcl.ambig]

The ambiguity arising from the similarity between a function-style cast and a declaration in 9.8 can also occur in the context of a declaration. In that context, the closure is between a function declaration with a redundant set of parameters around a name and an object declaration with a function-style cast—just as for the ambiguities in 9.8, the resolution is to consider any construct that could possibly be declaration. [Note: A declaration can be explicitly disambiguated by adding parameters around the argument. The ambiguity can be avoided by use of copy-initialization or by use of a function-style cast. — end note [Example:

```cpp
struct S {
S(int);
};

void foo(double a) {
    S x();                     // function declaration
    S y();                     // function declaration
    y(int(a));              // object declaration
    z(int(a));               // object declaration
    z = int(a);               // object declaration
}
```
— end example

2 An ambiguity can arise from the similarity between a function-style cast and a type-id. The resolution of that construct could possibly be a type-id in its syntactic context shall be considered a type-id. [Example:

```cpp
template <class T> struct X {
template <int N> struct Y {
    X<int> a;                  // type-id
    X<int>() b;                // expression (ill-formed)
    X<int>(1) c;               // type-id (ill-formed)
    Y(int) d;                  // expression
    Y<int>(1) d;               // expression
};
```

```cpp
void foo(signed char a) {
    sizeof(int); // type-id (ill-formed)
}
```

```cpp
sizeof(int a);           // expression
sizeof(int(unsigned a)); // type-id (ill-formed)

(int)0;                   // type-id (ill-formed)
int(a)+1;                // expression
int(unsigned a))+1;      // type-id (ill-formed)
}
```
--- end example

3 Another ambiguity arises in a parameter-declaration-clause when a type-name is nested in parentheses. In this case, the choice is between the declaration of a parameter type pointer to function and the declaration of a parameter with redundant parentheses around the declarator-id. The resolution is to consider the type-name as a simple-type-specifier rather than a declarator-id. [Example:

```cpp
class C {
    void f(int C) {}
    void f(*fp)(C* p_param) { // not: void f(int C) {}
};
int g(C);
void foo() {
    f(1);
    // error: cannot convert 1 to function pointer
    f(g);
    // OK
}
```

For another example,

```cpp
class C {
    void h(int *C[10]);
    void h(*fp)(int* _C[10]);
    // not: void h(int *C[10]);
}
```
--- end example

[dcl.meaning]

## 11.3 Meaning of declarators

1 A declarator contains one declarator-id, it names the identifier that is declared. An unqualified-id occurring in a declarator shall be a simple identifier for the declaration of special functions (15.1, 15.3, 15.4, 16.6) and for the declaration of template specializations or partial specializations (17.7). When the declarator-id is qualified, the declaration shall refer to a previously declared member of the class or namespace to which the qualifier-id refers (10.3.1) or to a specifier-prefix through which the member shall not merely have been introduced by a scope-specifier of the class namespace de-id. The nested-name-specifier of a qualified declarator shall not begin with a decltype-specifier. Note: If the qualifier is the global : resolution operator, the declarator-id refers to a name declared in the global namespace scope. — end The optional attribute-specifier following a declarator-id is

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
