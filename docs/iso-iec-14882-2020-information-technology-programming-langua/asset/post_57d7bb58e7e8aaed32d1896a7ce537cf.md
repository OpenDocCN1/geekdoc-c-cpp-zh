
# ISO/IEC 14882:2020(E)

(5.5) — all forms of list::merge

Valid C++ 2003 code that uses these functions may fail to compile with this revision of C++.

6 Affected subclauses: 22.2.3 and 22.2.6

Change: Signature changes: resize.

Rationale: Performance, compatibility with move semantics.

Effect on original feature: For vector, deque, and list the fill value passed to resize is now passed by reference instead of by value, and an additional overload of resize has been added. Valid C++ 2003 code that uses this function may fail to compile with this revision of C++.

# C.4.13 Clause 25: algorithms library [diff.cpp03.algorithms]

1 Affected subclause: 25.1

Change: Result state of inputs after application of some algorithms.

Rationale: Required by new feature.

Effect on original feature: A valid C++ 2003 program may detect that an object with a valid but unspecified state has a different valid but unspecified state with this revision of C++. For example, std::remove and std::remove_if may leave the tail of the input sequence with a different set of values than previously.

# C.4.14 Clause 26: numerics library [diff.cpp03.numerics]

1 Affected subclause: 26.4

Change: Specified representation of complex numbers.

Rationale: Compatibility with C99.

Effect on original feature: Valid C++ 2003 code that uses implementation-specific knowledge about the binary representation of the required template specializations of std::complex may not be compatible with this revision of C++.

# C.4.15 Clause 29: input/output library [diff.cpp03.input.output]

1 Affected subclauses: 29.7.4.2.4, 29.7.5.2.4, and 29.5.5.4

Change: Specify use of explicit in existing boolean conversion functions.

Rationale: Clarify intentions, avoid workarounds.

Effect on original feature: Valid C++ 2003 code that relies on implicit boolean conversions will fail to compile with this revision of C++. Such conversions occur in the following conditions:

+   - passing a value to a function that takes an argument of type bool;
+   - using operator== to compare to false or true;
+   - returning a value from a function with a return type of bool;
+   - initializing members of type bool via aggregate initialization;
+   - initializing a const bool& which would bind to a temporary object.

2 Affected subclause: 29.5.3.2.1

Change: Change base class of std::ios_base::failure.

Rationale: More detailed error messages.

Effect on original feature: std::ios_base::failure is no longer derived directly from std::exception, but is now derived from std::system_error, which in turn is derived from std::runtime_error. Valid C++ 2003 code that assumes that std::ios_base::failure is derived directly from std::exception may execute differently in this revision of C++.

3 Affected subclause: 29.5.3

Change: Flag types in std::ios_base are now bitmasks with values defined as constexpr static members.

Rationale: Required for new features.

Effect on original feature: Valid C++ 2003 code that relies on std::ios_base flag types being represented as std::bitset or as an integer type may fail to compile with this revision of C++. For example:

```
#include <iostream>

int main() {
    int flag = std::ios_base::hex;
    std::cout.setf(flag);    // error: setf does not take argument of type int
}
```

is valid in C, invalid in C++. This makes it impossible to define mutually referential file-local objects with static storage duration, if initializers are restricted to the syntactic forms of C. For example,

```
struct X { int i; struct X* next; };
```

```
static struct X a;
static struct X b = { 0, &a };
static struct X a = { 1, &b };
```

**Rationale:** This avoids having different initialization rules for fundamental types and user-defined types.
**Effect on original feature:** Deletion of semantically well-defined feature.
**Difficulty of converting:** Semantic transformation. In C++, the initializer for one of a set of mutually-referential file-local objects with static storage duration must invoke a function call to achieve the initialization.
**How widely used:** Seldom.

2 **Affected subclause:** 6.4
**Change:** A struct is a scope in C++, not in C.
**Rationale:** Class scope is crucial to C++, and a struct is a class.
**Effect on original feature:** Change to semantics of well-defined feature.
**Difficulty of converting:** Semantic transformation.
**How widely used:** C programs use struct extremely frequently, but the change is only noticeable when struct, enumeration, or enumerator names are referred to outside the struct. The latter is probably rare.

3 **Affected subclause:** 6.6 [also 9.2.9]
**Change:** A name of file scope that is explicitly declared const, and not explicitly declared extern, has internal linkage, while in C it would have external linkage.
**Rationale:** Because const objects may be used as values during translation in C++, this feature urges programmers to provide an explicit initializer for each const object. This feature allows the user to put const objects in source files that are included in more than one translation unit.
**Effect on original feature:** Change to semantics of well-defined feature.
**Difficulty of converting:** Semantic transformation.
**How widely used:** Seldom.

4 **Affected subclause:** 6.9.3.1
**Change:** The main function cannot be called recursively and cannot have its address taken.
**Rationale:** The main function may require special actions.
**Effect on original feature:** Deletion of semantically well-defined feature.
**Difficulty of converting:** Trivial: create an intermediary function such as mymain(argc, argv).
**How widely used:** Seldom.

5 **Affected subclause:** 6.8
**Change:** C allows “compatible types” in several places, C++ does not.
For example, otherwise-identical struct types with different tag names are “compatible” in C but are distinctly different types in C++.
**Rationale:** Stricter type checking is essential for C++.
**Effect on original feature:** Deletion of semantically well-defined feature.
**Difficulty of converting:** Semantic transformation. The “typesafe linkage” mechanism will find many, but not all, of such problems. Those problems not found by typesafe linkage will continue to function properly, according to the “layout compatibility rules” of this document.
**How widely used:** Common.

# C.5.4 Clause 7: expressions [diff.expr]

1 **Affected subclause:** 7.3.12
**Change:** Converting void* to a pointer-to-object type requires casting.

```
char a[10];
void* b=a;
void foo() {
    char* c=b;
}
```

ISO C will accept this usage of pointer to void being assigned to a pointer to object type. C++ will not.
**Rationale:** C++ tries harder than C to enforce compile-time type safety.
**Effect on original feature:** Deletion of semantically well-defined feature.

5 Affected subclause: 9.2.9
Change: Banning implicit int.

In C++ a decl-specifier-seq must contain a type-specifier, unless it is followed by a declarator for a constructor, a destructor, or a conversion function. In the following example, the left-hand column presents valid C; the right-hand column presents equivalent C++:

```
void f(const parm);
const n = 3;
main()
    /* ... */

void f(const int parm);
const int n = 3;
int main()
    /* ... */
```

Rationale: In C++, implicit int creates several opportunities for ambiguity between expressions involving function-like casts and declarations. Explicit declaration is increasingly considered to be proper style. Liaison with WG14 (C) indicated support for (at least) deprecating implicit int in the next revision of C.

Effect on original feature: Deletion of semantically well-defined feature.

Difficulty of converting: Syntactic transformation. Can be automated.

How widely used: Common.

6 Affected subclause: 9.2.9.6
Change: The keyword auto cannot be used as a storage class specifier.

```
void f() {
    auto int x;    // valid C, invalid C++
}
```

Rationale: Allowing the use of auto to deduce the type of a variable from its initializer results in undesired interpretations of auto as a storage class specifier in certain contexts.

Effect on original feature: Deletion of semantically well-defined feature.

Difficulty of converting: Syntactic transformation.

How widely used: Rare.

7 Affected subclause: 9.3.4.6
Change: In C++, a function declared with an empty parameter list takes no arguments. In C, an empty parameter list means that the number and type of the function arguments are unknown.

Example:

```
int f();
    // means int f(void) in C++
    // int f( unknown ) in C
```

Rationale: This is to avoid erroneous function calls (i.e., function calls with the wrong number or type of arguments).

Effect on original feature: Change to semantics of well-defined feature. This feature was marked as “obsolescent” in C.

Difficulty of converting: Syntactic transformation. The function declarations using C incomplete declaration style must be completed to become full prototype declarations. A program may need to be updated further if different calls to the same (non-prototype) function have different numbers of arguments or if the type of corresponding arguments differed.

How widely used: Common.

8 Affected subclause: 9.3.4.6 [see 7.6.2.5]
Change: In C++, types may not be defined in return or parameter types. In C, these type definitions are allowed.

Example:

```
void f( struct S { int a; } arg ) {}    // valid C, invalid C++
enum E { A, B, C } f() {}              // valid C, invalid C++
```

Rationale: When comparing types in different translation units, C++ relies on name equivalence when C relies on structural equivalence. Regarding parameter types: since the type defined in a parameter list would be in the scope of the function, the only legal calls in C++ would be from within the function itself.

Effect on original feature: Deletion of semantically well-defined feature.

Difficulty of converting: Semantic transformation. The type definitions must be moved to file scope, or in header files.

How widely used: Seldom. This style of type definition is seen as poor coding style.
