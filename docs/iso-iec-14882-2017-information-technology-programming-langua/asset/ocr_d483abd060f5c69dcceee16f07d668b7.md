# ISO/IEC 14882:2017(E)

# 20.5.5 Conforming implementations

# 20.5.5.1 Overview

This section describes the constraints on, and latitude of, implementations is discussed in 20.5.2; its use of macros in 20.5.3, non-member functions in 20.5.4, member functions in 20.5.5.5, data race avoidance in 20.5.5.9, class specifiers in 20.5.5.10, class derivation in 20.5.5.11, and exceptions in 20.5.5.12.

+   A C++ header may include other C+ headers. A C++ header shall include only its corresponding declarations and definitions that appear in its syntax. A C++ header shown in its includes including any other C++ headers shall provide the declarations and definitions that appear in those of other headers.

+   Certain types and macros are defined in more than one header. Every entity shall be defined such that any header that defines it may be included after any other header that defines it (6.2).

+   The C standard library headers (D.5) shall define C++ standard library header, as described in 20.5.1.2.

# 20.5.5.3 Restrictions on macro functions

+   The names and global functions defined in 20.5.1.1 shall be reserved to the implementation.

+   All object-like macros defined by the C standard library and described in this class as expanding to include constant expressions are also suitable for #if directives, unless explicitly stated otherwise.

# 20.5.5.4 Non-member functions

It is specified whether any non-member functions in the C++ standard library are defined as inline [10.1.6).

A call to a non-member function signature declared in Clauses 21 through 33 and Annex D shall be allowed if the implementation declared no additional non-member function signatures. [18].

An implementation shall not declare a non-member function signature with default arguments. Unless otherwise specified, calls made by functions in the standard library to non-operator, non-member functions do use functions from another namespace which are found through argument-dependent lookup (20.5.3.2). The exception for argument-dependent lookup allows cases such as the swappable with requirements (20.5.3.2); operator:: (27.6.2.2) in cases where out_iterator_.

```
Effects:
*out_stream << value;
*if (delim != 0)
  *out_stream << delim;
  return true;
```

# 20.5.5.5 Member functions

It is specified whether any member functions in the C++ standard library are defined as inline [10.1.6).

For a non-virtual member function signature described in the C++ standard, an implementation may declare a different set of member function signatures, provided that any call to the member function that would select an overload from the set of declarations in this document behaves as if overload were selected. [4 Note: For instance, an implementation may add parameters with default values, or replace a

+   1) A valid C++ program always calls the expected non-member function. An implementation may also add additional non-member functions that would otherwise not be called by a valid C++ program.