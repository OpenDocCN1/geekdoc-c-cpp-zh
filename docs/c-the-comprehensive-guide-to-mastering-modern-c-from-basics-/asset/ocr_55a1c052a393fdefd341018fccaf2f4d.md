| Operation | Binary | Decimal |
| --- | --- | --- |
| Not ~b | 1100 | 12 |

**Table 4.2** Bitwise arithmetic with a (hypothetical) four-bit-wide unsigned int.

The << and >> operators should no longer scare you: simply shift the bit representation of the first operand to the left or right by the number of bits of the second operand. In the computer, it is the same as if you were multiplying or dividing by two just as often:

+   * 345 << 3 is like 345*2*2 and results in 2760.
* 345 >> 3 is like 345/2/2 and gives 43.

As soon as you need such number magic, you will have to deal with the number representation in the computer again, for example in Section 4.4.3. Until then, remember that C++ has these operations.

So the use of this in the real world is limited to the view of numbers as a series of bits; otherwise *2 and /2 make much more sense. So that you can see this, the following code reverses the bits of an unsigned short.

```
// https://godbolt.com/z/qdY1d5a9
#include <iostream>
#include <bitset>
constexpr unsigned n bits = sizeof(unsigned short); // 8 bits per char
auto reverse_bits(unsigned val) -> unsigned short {
  for (unsigned i = 0; i < n bits; ++i) {
    ret = (ret << 1) | (val & 1); // one to the side, set lowest bit
    val >>= 1; // one in the other direction
  }
  return ret;
}
void tell(unsigned val) {
```