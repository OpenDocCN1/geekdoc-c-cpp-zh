# 16.4.6.4 Non-member functions [global.functions]

1 It is unspecified whether any non-member functions in the C++ standard library are defined as inline (9.2.8).

2 A call to a non-member function signature described in Clause 17 through Clause 32 and Annex D shall behave as if the implementation declared no additional non-member function signatures.182

3 An implementation shall not declare a non-member function signature with additional default arguments.

4 Unless otherwise specified, calls made by functions in the standard library to non-operator, non-member functions do not use functions from another namespace which are found through argument-dependent name lookup (6.5.3).

> [Note 1: The phrase “unless otherwise specified” applies to cases such as the swappable with requirements (16.4.4.3). The exception for overloaded operators allows argument-dependent lookup in cases like that of ostream_::operator= (23.6.3.3):
> Effects:
> *out_stream << value;
> if (delim != 0)
>   *out_stream << delim;
> return *this;
> — end note]

```
*out_stream << value;
if (delim != 0)
  *out_stream << delim;
return *this;
```

# 16.4.6.5 Member functions [member.functions]

1 It is unspecified whether any member functions in the C++ standard library are defined as inline (9.2.8).

2 For a non-virtual member function described in the C++ standard library, an implementation may declare a different set of member function signatures, provided that any call to the member function that would select an overload from the set of declarations described in this document behaves as if that overload were selected.

> [Note 1: For instance, an implementation can add parameters with default values, or replace a member function with default arguments with two or more member functions with equivalent behavior, or add additional signatures for a member function name. — end note]

# 16.4.6.6 Friend functions [hidden.friends]

1 Whenever this document specifies a friend declaration of a function or function template within a class or class template definition, that declaration shall be the only declaration of that function or function template provided by an implementation.

> [Note 1: In particular, an implementation is not allowed to provide an additional declaration of that function or function template at namespace scope. — end note]

> [Note 2: Such a friend function or function template declaration is known as a hidden friend, as it is visible neither to ordinary unqualified lookup (6.5.2) nor to qualified lookup (6.5.4). — end note]

# 16.4.6.7 Constexpr functions and constructors [constexpr.functions]

1 This document explicitly requires that certain standard library functions are constexpr (9.2.6). An implementation shall not declare any standard library function signature as constexpr except for those where it is explicitly required. Within any header that provides any non-defining declarations of constexpr functions or constructors an implementation shall provide corresponding definitions.

# 16.4.6.8 Requirements for stable algorithms [algorithm.stable]

1 When the requirements for an algorithm state that it is “stable” without further elaboration, it means:

+   (1.1) — For the sort algorithms the relative order of equivalent elements is preserved.
+   (1.2) — For the remove and copy algorithms the relative order of the elements that are not removed is preserved.
+   (1.3) — For the merge algorithms, for equivalent elements in the original two ranges, the elements from the first range (preserving their original order) precede the elements from the second range (preserving their original order).

# 16.4.6.9 Reentrancy [reentrancy]

1 Except where explicitly specified in this document, it is implementation-defined which functions in the C++ standard library may be recursively reentered.