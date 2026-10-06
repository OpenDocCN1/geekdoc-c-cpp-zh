# ISO/IEC 14882:2017(E)

the member ec of the return value is equal to errc::result_out_of_range. Otherwise, value is set to the parsed value and the member ec is set such that the conversion to bool yields false.

```
from_char_result from_chars(const char* first, const char* last,
                                                                see below\n& value, int base = 10);
```

+   3 Requires: base has a value between 2 and 3 (inclusive).

+   4 Effects: The pattern is the expected form of the subject sequence in the "C" for the nonzero base, based on strtol, that no "Ox" or "OX" shall appear if the value of base is 16, and that a minus is the only sign that may appear, and only if value has a signed type.

+   5 Throws: Nothing.

+   Remarks: The implementation shall provide overload for all signed and unsigned integer types and char as the referenced type of the parameter value.

```
from_char_result from_chars(const char* first, const char* last, float& value,
                                                              chars_format fmt = chars_format::general);
from_char_result from_chars(const char* first, const char* last, double& value,
                                                              chars_format fmt = chars_format::general);
from_char_result from_chars(const char* first, const char* last, double& value,
                                                              chars_format fmt = chars_format::general);
```

+   6 Requires: fmt has the value expected form of the enumerators of format.

+   (7.1) the only sign that may appear is a minus:
The pattern is the expected form of the subject sequence in the "C", as described for strtol, except that

+   (7.2) if fmt has chars_format::scientific set not chars_format::fixed, the optional exponent part shall appear

+   (7.3) if fmt is chars_format::fixed set not chars_format::scientific, the optional
\xponent
part should not appear; or

+   if it is chars_format::hex, the prefix "Ox" or "OX" is assumed. The string Ox123 is parsed to have the value 0 with remaining characters x123. end example

In any case, the resulting value is one of at most two floating-point values closest to the value of the string matching the pattern.

+   8 Throws: Nothing.

SEE ALSO: ISO C 7.22.1.3, 7.22.1.4

# 23.3 Compile-time integer sequences

```
[intseq]
```

# 23.3.1 In general

The library provides a class template that can represent an integer sequence. When used as a function template the parameter packing can be deduced and used in a pack expansion.
[Note: The index_sequence alias is provided for the common case of an integer sequence of size_t; see also 23.3.5.5. — end note]

# 23.3.2 Class template integer_sequence

```
[intseq::intseq]
```

```
namespace std {
template<class T, T... I>
struct integer_sequence {
  using value_type = T;
  static constexpr size_t size() noexcept { return sizeof(I); };
};
```

©ISO/IEC 2017 - All rights reserved

536