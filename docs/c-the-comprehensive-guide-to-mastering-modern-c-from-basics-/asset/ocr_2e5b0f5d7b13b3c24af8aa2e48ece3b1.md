are rarely necessary. With 0xffFULL, you define 255 as an unsigned long.

| Base | Prefix | Examples | Decimal as int |
|---|---|---|---|n| 10 | | 255, -4 | 255, -4 |
| 16 | 0x | 0xff, 0xCAFE | 255, 51966 |
| 8 | 0 | 0377, 0777666 | 255, 262070 |
| 2 | 0b | 0b11111111, 0b010101 | 255, 5 |

**Table 4.7** Integer prefixes for the different number systems.

# # Operations on Integers

You can calculate arithmetically with all integer types, as you would expect: multiplication with *, addition and subtraction with + and -, and division without remainder with /. The latter means that if you calculate 20 /7, the result is 2; the decimal places are simply cut off. With %, you get the remainder modulo operation.

```
// https://godbolt.org/z/ebPcdxzvi
#include <iostream>
int main() {
std::cout << 3 * 4 + 5 + 6 << "\n"; // 29
std::cout << 20 /7 << " - Rest " << 20%%7 << "\n"; // 2 remainder 6
}
```

**Listing 4.29** Arithmetic with integers.

For more complex calculations, you must write your own functions or use floating-point numbers such as double, for which there are a large number of calculating functions in the standard library in the <cmath> header.

The bit operations have already been described in Section 4.3. The following listing is another short example.

```
// https://godbolt.org/z/jei5ExGqx
#include <iostream>
int main() {
unsigned a = 0b11110000; // 240
unsigned b = 0b00011100; // 60
std::cout << (a | b) << "\n"; // Bit-Or: 252, in bits 11111100
std::cout << (a & b) << "\n"; // Bit-And: 48, in bits 00110000
```