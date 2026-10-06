# ISO/IEC 14882:2017(E)

# # Annex D (normative)
Compatibility features [depr]

1 This Clause describes features of the C++ Standard that are specified for compatibility with existing implementations.

2 These are deprecated features, which **deprecated** is defined as: Normative for the current edition of this International Standard, but having been identified as a candidate for removal from future revisions. An implementation may declare library names and entries described in this section as deprecated (10.6.4).

# ## D.1 Redeclaration of constexpr data members [depr_static_constexpr]

1 For compatibility with prior C++ International Standards, a `constexpr` static data member may be redundant outside the class with no initializer. [Example:

```
struct A {
    constexpr int n = 5; // declaration (declaration in C++ 2014)
    constexpr A::; // redundant declaration (definition in C++ 2014)
}; // example
```

# ## D.2 Implicit declaration of copy functions [depr_impldec]

1 The implicit declaration of a copy constructor behaves as deprecated if the class has a user-declared copy assignment operator or a user-declared destructor. The implicit declaration of a copy assignment operator as deprecated is deprecated if the class has a user-declared copy constructor or a user-declared destructor (15.5.8). In a future revision of this International Standard, these implicit definitions could be deleted (11.4).

# ## D.3 Deprecated exception specifications [depr.except.spec]

1 The noexcept-specifier throw() is deprecated.

# ## D.4 C++ standard library headers [depr.cpp.headers]

1 For compatibility with prior C++ International Standards, the C++ standard library provides headers `<complex>` (D.4.1), `<cstdalg>` (D.4.2), `<cstdlibool>` (D.4.3), and `<cmath>` (D.4.4). The use of these headers is deprecated.

# ### D.4.1 Header <complex> synopsis [depr.complex.syn]

```
#include <complex>
```

1 The header `<complex>` behaves as if it includes the header `<complex>` (29.5.1).

# ### D.4.2 Header <cstdalign> synopsis [depr.cstdalign.syn]

```
#define __alignas_is_defined 1
```

1 The contents of the header `<cstdalign>` are the same as the C standard library header `<stdalign.h>`, with the following changes: The header `<cstdalign>` and the header `<stdalign.h>` shall not define a macro `alignas`.

§ D.4.2  ©ISO/IEC 2017 - All rights reserved  1456