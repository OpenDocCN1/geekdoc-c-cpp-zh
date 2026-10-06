# ISO/IEC 14882:2017(E)

# C.2.15 Clause 29: numerics library [diff.cpp03.numerics]

29.5

Change: Specified representation of complex numbers.
Rationale: Compatibility with C99.
Effect on original feature: Valid C++ 2003 code that uses implementation-specific knowledge about the binary representation of the required template specializations of std::complex may not be compatible with this International Standard.

# C.2.16 Clause 30: input/output library [diff.cpp03.input.output]

30.7.4.1,30.5.5.1,30.5.5.4,

Change: Specify use of explicit in existing boolean conversion functions.
Rationale: Clarify intentions.
Effect on original feature: Valid C++ 2003 code that relies on implicit boolean conversions will fail to comply with this International Standard. Such conversions occur in the following conditions:

+   - passing a value to a function that takes an argument of type bool;
- using operator== to false or true;
- returning a value from a function with return type bool;
- initializing members of type bool via aggregate initialization;
- initializing a const bool would bind to a temporary.

30.5.3.1

Change: Base class of std::ios_base::failure.
Rationale: More detailed error messages.
Effect on original feature: std::ios_base::failure is no longer derived from std::exception, but is now derived from std::runtime_error. Valid C++ 2003 code assumes that std::ios_base::failure is derived directly from std::exception may except efficiently in this International Standard.

30.5.2

Change: Flag types in std::ios_base are now bitmasks with values defined as constexpr static members.
Rationale: For new features.
Effect on original feature: Valid C++ 2003 code that relies on std::ios_base flag types being represented as std::bitset or as an integer type may fail to comply with this International Standard. For example:

```
#include <iostream>

int main() {
  int flag = std::ios_base::hex;
  std::cout.setf(flag); // setf does not take argument of type int
```

# C.3 C++ and ISO C++ 2011 [diff.cpp111]

This subclause lists the differences between C++ and ISO C++ 2011 (ISO/IEC 14882:2011, Programming Languages - C++), by the characters of this document.

# C.3.1 Lexical conventions [diff.cpp11.lex]

Change: pp-number can contain one or more quotes.
Rationale: Necessary to enable quotes as digit separators.
Effect on original feature: Valid C++ 2011 code may fail to comply or change meaning in this International Standard. For example, the following code is both in C++ 2011 and in this International

§ C.3.1