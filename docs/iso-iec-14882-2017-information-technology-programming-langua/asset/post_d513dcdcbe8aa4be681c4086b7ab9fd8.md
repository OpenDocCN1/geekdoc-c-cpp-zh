
# ISO/IEC 14882:2017(E)

3 The C++ headers <complex> (D.4.1) and <ctgmath> (D.4.4), as well as their corresponding C headers headers <complex.h> and <tgmath.h>, do not contain any of the content from the C standard library and instead include other headers from the C++ standard library.

4 The headers <iso646>, <cdstalph> (D.4.2), and <cstool> (D.4.3) are meaningless in C++, Use of the C++ headers <iso646>, <cdstalph>, <cstool>, and <ctgmath> is deprecated (D.5).

## C.5.2 Modifications to definitions [diff.mods.to.definitions]

### C.5.2.1 Types char16_t and char32_t [diff.char16]

+ 1 The types char16_t and char32_t are distinct types rather than typedef to integral types. The tokens char16_t and char32_t are keywords in this International Standard (5.11). They do not appear as macro names defined in <cuchar> (24.5.5).

### C.5.2.2 Type wchar_t [diff.wchar]

+ 1 The type wchar_t is a distinct type rather than a typedef to an integral type. The token wchar_t is a keyword in this International Standard (5.11). It does not appear as a macro name in any of <cwstype> (21.2.1), <cctype> (21.2.2), or <cwchar> (24.5.4).

### C.5.2.3 Header assert [diff.header.assert]

+ 1 The token static_assert is a keyword in this International Standard (5.11). It does not appear as a macro defined in <assert> (22.3.1).

### C.5.2.4 Header iso646 [diff.header.iso646]

+ 1 The tokens and, or, bit, bor, compl, not_eq, or_eq, xor, and xor_eq are keywords in this International Standard (5.11). They do not appear as macro names defined in <iso646>.

### C.5.2.5 Header cstdalign [diff.header.cdstalign]

+ 1 The token alias is a keyword in this International Standard (5.11). It does not appear as a macro name defined in <cdstalign> (D.4.2).

### C.5.2.6 Header cstool [diff.header.cstool]

+ 1 The tokens bool, true, and false are keywords in this International Standard (5.11). They do not appear as macro names defined in <cstool> (D.4.3).

### C.5.2.7 Macro NULL [diff.null]

+ 1 The macro NULL, defined in any of <locale> (25.5), <cdef> (21.2.1), <cstdio> (30.11.1), <cctype> (21.2.2), <cstring> (24.5.3), or <cwchar> (24.5.4), is an implementation-defined C++ pointer constant in this International Standard (21.2).

## C.5.3 Modifications to declarations [diff.mods.to.declarations]

+ 1 Header <string> (24.5.3): The following functions have different declarations:

+ (1.1) strchr
+ (1.2) strcmp
+ (1.3) strcat
+ (1.4) strstr

Subclause 24.5.3 describes the changes.

+ 2 Header <cwchar> (24.5.4): The following functions have different declarations:

+ (2.1) — wcschr
+ (2.2) — wcspbrk
+ (2.3) — wcsrchr
+ (2.4) — wcsstr
+ (2.5) — wmemchr

Subclause 24.5.4 describes the changes.
Header <stddef> (21.2.1) declares the name nullptr_t in addition to the names declared in <stddef.h> in the standard library.

## C.5.4 Modifications to behavior [diff.mods.to.behavior]

+ 1 Header <stdlib> (21.2.2): The following functions have different behavior:

+ (1.1) — exit
+ (1.2) — free
+ (1.3) abort

Subclause 21.5 describes the changes.
+ 2 Header <jmp> (21.10.2): The following functions have different behavior:

+ longjmp

Subclause 21.10.2 describes the changes.

### C.5.4.1 Macro offset(type, member-designator) [diff.offsetof]

The macro offset, defined in <stddef> (21.2.1), accepts a restricted set of type arguments in this International Standard.

### C.5.4.2 Memory allocation functions [diff.malloc]

The functions alloc, calloc, malloc, and realloc are restricted in this International Standard. Subclause 23.10 describes the changes.

# Annex D (normative)
## Compatibility features

1 This Clause describes features of the C++ Standard that are specified for compatibility with existing implementations.
2 These are deprecated features, which are defined as: Normative for the current edition of this International Standard, but having been identified as a candidate for removal from future revisions. An implementation may declare library names and entries in this section as deprecated (10.6.4).

### D.1 Redeclaration of constexpr data members [depr_static_constexpr]

1 For compatibility with prior C++ Standards, a constexpr data member may be redundant outside the class with no initializer. Example:

```cpp
struct A {
    constexpr int n = 5; // declaration in C++14
};
constexpr int A::n; // redundant declaration (definition in C++14)
```

### D.2 Implicit declaration of copy functions [depr_implec]

1 The implicit declaration of a copy constructor is deprecated if the class has a user-declared assignment operator or destructor (15.5.8). The implicit declaration of a copy assignment operator is deprecated if the class has a user-declared copy constructor or destructor. In a future revision of this International Standard, these implicit definitions could be deleted.

### D.3 Deprecated exception specifications

1 The noexcept-specifier throw() is deprecated.

### D.4 C++ library headers [depr.cpp.headers]

1 For compatibility with prior C++ Standards, the C++ standard library provides headers <complex> (D.4.1), <cstdalign> (D.4.2), <cstdlib> (D.4.3), and <cmath> (D.4.4). The use of these headers is deprecated.

### D.4.1 Header <complex> [depr.complex.syn]

```cpp
#include <complex>
```

The header <complex> behaves as if it includes the header <complex> (29.5.1).

### D.4.2 Header <cstdalign> [depr.cstdalign.syn]

```cpp
#define __alignas_is_defined 1
```

The contents of the header <cstdalign> are the same as the C standard library header <stdalign.h>, with the following changes: The header <cstdalign> and the header <stdalign.h> shall not define a macro alignas.

### D.4.3 Header <cdbool> synopsis

```cpp
#define __bool_true_false_are_defined
```

1 The contents of the header <cdbool> are the same as the C standard library header <stdool.h>, with the following changes: The header <cdbool> and <cmath.h> shall not define macros named bool, true, or false.

### D.4.4 Header <ctgmath> synopsis

```cpp
#include <complex>
#include <cmath>
```

1 The header <ctgmath> simply includes the headers <complex> (29.5.1) and <cmath> (29.9.1).

[Note: The overloads in C type-generic macros are already provided in <complex> and <cmath> by "sufficient" declarations. — end note]

## D.5 C library headers

1 For the C standard library, the C++ standard library provides the C headers shown in Table 141.

| <assert.h> | <inttypes.h> | <signal.h> | <stdio.h> | <wchar.h> |
|---|---|---|---|---|
| <complex.h> | <iso646.h> | <stdlib.h> | <stdlib.h> | <wctype.h> |
| <ctype.h> | <limits.h> | <stdarg.h> | <string.h> | |
| <errno.h> | <locale.h> | <stdbool.h> | <tgmath.h> | |
| <fenv.h> | <math.h> | <stddef.h> | <time.h> | |
| <float.h> | <setjmp.h> | <stdint.h> | <uchar.h> | |

The header <cmath> behaves as if it includes the header <complex>. The header <tgmath> behaves as if it includes the header <cmath>.

## D.6 char streams

The header <streambuf> defines two types that associate stream buffers with character arrays and assist in reading and writing objects.

### D.6.1 Class streambuf

```cpp
namespace std {
class streambuf : public basic_streambuf<char> {
```

D.6.1
