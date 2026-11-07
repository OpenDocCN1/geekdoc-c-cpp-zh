| Operator | Name | Description |
|---|---|---|
| `&` | bitwise AND | The bits in the result are set to 1 if the corresponding bits in the two operands are both 1. |
| `\|` | bitwise inclusive OR | The bits in the result are set to 1 if one or both of the corresponding bits in the two operands is 1. |
| `^` | bitwise exclusive OR | The bits in the result are set to 1 if exactly one of the corresponding bits in the two operands is 1. |
| `<<` | left shift | Shifts the bits of the first operand left by the number of bits specified by the second operand; fill from right with 0 bits. |
| `>>` | right shift with sign extension | Shifts the bits of the first operand right by the number of bits specified by the second operand; the method of filling from the left is machine dependent. |
| `~` | bitwise complement | All 0 bits are set to 1 and all 1 bits are set to 0. |

**Fig. 22.5** | Bitwise operators.

# Printing a Binary Representation of an Integral Value

When using the bitwise operators, it’s useful to illustrate their precise effects by printing values in their binary representation. The program of Fig. 22.6 prints an unsigned integer in its binary representation in groups of eight bits each.

```
```cpp
// Fig. 22.6: Fig22_06.cpp
// Printing an unsigned integer in bits.
#include <iostream>
#include <iomanip>
using namespace std;

void displayBits( unsigned ); // prototype

int main()
{
    unsigned inputValue = 0; // integral value to print in binary

    cout << "Enter an unsigned integer: ";
    cin >> inputValue;
    displayBits( inputValue );
} // end main

// display bits of an unsigned integer value
void displayBits( unsigned value )
{
    const int SHIFT = 8 * sizeof( unsigned ) - 1;
    const unsigned MASK = 1 << SHIFT;

    cout << setw( 10 ) << value << " = ";
}
```
```

**Fig. 22.6** | Printing an unsigned integer in bits. (Part 1 of 2.)