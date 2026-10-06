# ISO/IEC 14882:2017(E)

**Rationale**: In C++, implicit creates several opportunities for ambiguity between expressions involving function-like casts and declarations. Explicit declaration is increasingly considered to be proper style. Liaison with WG14 indicated support for (at least) deprec implicit int in the next revision of C.
**Effect on original feature**: Deletion of semantically well-defined feature.
**Difficulty of converting**: Syntactic transformation. Could be automated.
**How widely used**: Common.

10.1.7.4

**Change**: The auto keyword cannot be used as a storage class classifier.

```
void f() {
    auto int x; // invalid C, invalid C++
}
```

**Rationale**: Allowing the use of auto to deduce the type of a variable from its initializer results in undesired interpretations of auto as a storage class in certain contexts.
**Effect on original feature**: Deletion of semantically well-defined feature.
**Difficulty of converting**: Syntactic transformation.
**How widely used**: Rare.

10.2

**Change**: In C++, objects of enumeration type can only be assigned values of the same enumeration type. In C, objects of enumeration type can be assigned values of any integral type.

Example:

```
enum color { red, blue, green };
enum color c = 1; // valid C, invalid C++
```

**Rationale**: The type-safe nature of C++.
**Effect on original feature**: Deletion of semantically well-defined feature.
**Difficulty of converting**: Syntactic transformation. (The type error produced by the assignment can be automatically corrected by applying an explicit cast.)
**How widely used**: Common.

10.2

**Change**: In C++, the type of the enumerator is its enumeration. In C, the type of an enumerator is int.

Example:

```
enum { A };
size_t sizeof(A) == sizeof(int) // in C
sizeof(A) == sizeof(int)      // in C++
/* and int is not necessarily equal to sizeof(A) * /
```

**Rationale**: In C++, an enumerator is a distinct type.
**Effect on original feature**: Change to semantics of well-defined feature.
**Difficulty of converting**: Syntactic transformation.
**How widely used**: Seldom. The only time this affects existing C is when the size of the enumerator is int. Taking the size of an enumerator is not a common C coding practice.

# C.1.7 Clause 11: declarators

11.3.5

**Change**: In C++, a function declared with an empty parameter list takes no arguments. In C, an empty

§ C.1.7

©ISO/IEC 2017 - All rights reserved

1437