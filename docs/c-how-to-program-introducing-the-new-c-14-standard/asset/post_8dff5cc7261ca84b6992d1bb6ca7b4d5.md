
```cpp
// display bits of an unsigned integer value
void displayBits(unsigned value) {
    const unsigned SHIFT{8 * sizeof(unsigned) - 1};
    const unsigned MASK{static_cast<const unsigned>(1 << SHIFT)};

    cout << setw(10) << value << " = ";

    // display bits
    for (unsigned j{1}; j <= SHIFT + 1; ++j) {
        cout << (value & MASK ? '1' : '0');
        value <<= 1; // shift value left by 1

        if (j % 8 == 0) { // output a space after 8 bits
            cout << ' ';
        }
    }

    cout << endl;
}
```

```text
The result of combining the following
2179876355 = 10000001 11101110 01000110 00000011
             1 = 00000000 00000000 00000000 00000001
using the bitwise AND operator & is
             1 = 00000000 00000000 00000000 00000001

The result of combining the following
            15 = 00000000 00000000 00000000 00001111
           241 = 00000000 00000000 00000000 11110001
using the bitwise inclusive OR operator | is
           255 = 00000000 00000000 00000000 11111111

The result of combining the following
           139 = 00000000 00000000 00000000 10001011
           199 = 00000000 00000000 00000000 11000111
using the bitwise exclusive OR operator ^ is
            76 = 00000000 00000000 00000000 01001100

The one's complement of
         21845 = 00000000 00000000 01010101 01010101
4294945450 = 11111111 11111111 10101010 10101010
```

**Fig. 22.8 Bitwise AND, inclusive OR, exclusive OR and complement operators.**

## Bitwise AND Operator (&)

In **Fig. 22.8**, line 12 uses `2179876355 (10000001 11101110 01000110 00000001)` to initialize variable `number1`, and line 14 uses `1 (00000000 00000000 00000000 00000001)` to initialize variable `mask`. When `mask` and `number1` are combined using the *bitwise AND operator* (`&`) in the expression `number1 & mask` (line 18), the result is `00000000 00000000 00000000 00000001`. All the bits except the low-order bit in variable `number1` are “masked off” (hidden) by “ANDing” with constant `MASK`.

### Bitwise Inclusive OR Operator (|)

The *bitwise inclusive OR operator* is used to set specific bits to 1 in an operand. In **Fig. 22.8**, line 21 assigns `15 (00000000 00000000 00000000 00001111)` to variable `number1`, and line 22 uses `241 (00000000 00000000 00000000 11110001)` to initialize variable `setBits`. When `number1` and `setBits` are combined using the *bitwise inclusive OR operator* in the expression `number1 | setBits` (line 27), the result is `255 (00000000 00000000 00000000 11111111)`. **Figure 22.9** summarizes the results of combining two bits with the *bitwise inclusive-OR operator*.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2555_0.png)

### Common Programming Error 22.3

*Using the logical OR operator* (`||`) for the bitwise OR operator (`|`) and vice versa is a logic error.

**Fig. 22.9 Combining two bits with the bitwise inclusive-OR operator (|).**

| Bit 1 | Bit 2 | Bit 1 \| Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 1 |

## Bitwise Exclusive OR (^)

The *bitwise exclusive OR operator (^)* sets each bit in the result to 1 if exactly one of the corresponding bits in its two operands is 1. In *Fig. 22.8*, lines 30–31 give variables `number1` and `number2` the values `139` (`00000000 00000000 00000000 10001011`) and `199` (`00000000 00000000 00000000 11000111`), respectively. When these variables are combined with the *bitwise exclusive OR operator* in the expression `number1 ^ number2` (line 36), the result is `00000000 00000000 00000000 01001100`. **Figure 22.10** summarizes the results of combining two bits with the *bitwise exclusive OR operator*.

**Fig. 22.10 Combining two bits with the bitwise exclusive OR operator (^).**

| Bit 1 | Bit 2 | Bit 1 ^ Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

## Bitwise Complement (~)

The *bitwise complement operator* (`~`) sets all `1` bits in its operand to `0` in the result and sets all `0` bits to `1` in the result—otherwise referred to as “taking the *one’s complement* of the value.” In **Fig. 22.8**, line 39 assigns variable `number1` the value `21845` (`00000000 00000000 01010101 01010101`). When the expression `~number1` evaluates, the result is (`11111111 11111111 10101010 10101010`).

## Bitwise Shift Operators

**Figure 22.11** demonstrates the *left-shift operator* (`<<`) and the *right-shift operator* (`>>`). Function `displayBits` (lines 26–43) prints the `unsigned` integer values.

```cpp
// Fig. 22.11: fig22_11.cpp
// Using the bitwise shift operators.
#include <iostream>
#include <iomanip>
using namespace std;

void displayBits(unsigned); // prototype

int main() {
   unsigned number1{960};

   // demonstrate bitwise left shift
   cout << "The result of left shifting\n";
   displayBits(number1);
   cout << "8 bit positions using the left-shift operator is\n";
   displayBits(number1 << 8);

   // demonstrate bitwise right shift
   cout << "\nThe result of right shifting\n";
   displayBits(number1);
   cout << "8 bit positions using the right-shift operator is\n";
   displayBits(number1 >> 8);
}

// display bits of an unsigned integer value
void displayBits(unsigned value) {
   const unsigned SHIFT{8 * sizeof(unsigned) - 1};
   const unsigned MASK{static_cast<unsigned>(1) << SHIFT};

   cout << setw(10) << value << " = ";

   // display bits
   for (unsigned i{1}; i <= SHIFT + 1; ++i) {
       cout << (value & MASK ? '1' : '0');
       value <<= 1; // shift value left by 1

       if (i % 8 == 0) { // output a space after 8 bits
           cout << ' ';
       }
   }

   cout << endl;
}
```

```text
The result of left shifting
        960 = 00000000 00000000 00000011 11000000
8 bit positions using the left-shift operator is
     245760 = 00000000 00000011 11000000 00000000

The result of right shifting
        960 = 00000000 00000000 00000011 11000000
8 bit positions using the right-shift operator is
          3 = 00000000 00000000 00000000 00000011
```

**Fig. 22.11 Bitwise shift operators.**

### Left-Shift Operator

The *left-shift operator* (`<<`) shifts the bits of its left operand to the left by the number of bits specified in its right operand. Bits vacated to the right are replaced with `0`s; bits shifted off the left are lost. In Fig. 22.11, line 10 initializes variable `number1` with the value `960` (`00000000 00000000 00000011 11000000`). The result of left-shifting variable `number1` eight bits in the expression `number1 << 8` (line 16) is `245760` (`00000000 00000011 11000000 00000000`).

### Right-Shift Operator

The *right-shift operator* (`>>`) shifts the bits of its left operand to the right by the number of bits specified in its right operand. Performing a right shift on an `unsigned` integer causes the vacated bits at the left to be replaced by 0s; bits shifted off the right are lost. In the program of **Fig. 22.11**, the result of right-shifting `number1` in the expression `number1 >> 8` (line 22) is `3` (`00000000 00000000 00000000 00000011`).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2560_0.png)

### Common Programming Error 22.4

*The result of shifting a value is undefined if the right operand is negative or if the right operand is greater than or equal to the number of bits in which the left operand is stored.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2560_1.png)

### Portability Tip 22.3

*The result of right-shifting a signed value is machine dependent. Some machines fill with zeros and others use the sign bit.*

## Bitwise Assignment Operators

Each bitwise operator (except the bitwise complement operator) has a corresponding assignment operator. These `bitwise assignment operators` are shown in **Fig. 22.12**; they’re used in a similar manner to the arithmetic assignment operators introduced in **Chapter 4**.

**Fig. 22.12 Bitwise assignment operators.**

| Bitwise assignment operator | Description |
|---|---|
| `&=` | Bitwise AND assignment operator. |
| `|=` | Bitwise inclusive OR assignment operator. |
| `^=` | Bitwise exclusive OR assignment operator. |
| `<<=` | Left-shift assignment operator. |
| `>>=` | Right-shift with sign extension assignment operator. |

## Operator Precedence

**Figure 22.13** shows the precedence and associativity of the operators introduced up to this point in the text. They’re shown top to bottom in decreasing order of precedence.

**Fig. 22.13 Operator precedence and associativity.**

| Operators | Associativity | Type |
|---|---|---|
| `++ --` (unary; right to left) | left to right | primary |
| `* / %` (binary; left to right)<br>`()` (grouping parentheses) | *[See caution in Fig. 2.10 regarding grouping parentheses.]* |  |
