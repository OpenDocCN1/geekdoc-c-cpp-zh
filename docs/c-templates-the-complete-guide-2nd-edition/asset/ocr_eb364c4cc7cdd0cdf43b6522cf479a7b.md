```
auto a = t[CTValue<unsigned, 2>{}];
auto b = t[CTValue<unsigned, 3>{}]; a and b will be initialized by
the type and value of the third and fourth values in the Tuple t.
```

To make the usage of constant indices more convenient, we can implement the literal operator with constexpr to compute the numeric compile-time literals directly from ordinary literals with the suffix _c: Click here to view code image

# tuples/literals.hpp

```
#include "ctvalue.hpp"
#include <cassert>
#include <cstddef>

// convert single char to corresponding int value at compile time:
constexpr int toInt(char c) {
// hexadecimal letters:
if (c >= 'A' && c <= 'F') {
return static_cast<int>(c) - static_cast<int>('A') + 10;
}
if (c >= 'a' && c <= 'f') {
return static_cast<int>(c) - static_cast<int>('a') + 10;
}
// other (disable '.' for floating-point literals):
assert(c >= '0' && c <= '9');
return static_cast<int>(c) - static_cast<int>('0');
}
// parse array of chars to corresponding int value at compile time:
template<std::size_t N>
constexpr int parseInt(char const (&arr)[N]) {
int base = 10; // to handle base (default: decimal)
int offset = 0; // to skip prefixes like 0x
if (N > 2 && arr[0] == '0') {
switch (arr[1]) {
case 'x': //prefix 0x or 0X, so hexadecimal
case 'X':
base = 16;
offset = 2;
break;
case 'b': //prefix 0b or 0B (since C++14), so binary
case 'B':
base = 2;
offset = 2;
break;
default: //prefix 0, so octal
base = 8;
offset = 1;
break;
}
}
// iterate over all digits and compute resulting value:
```