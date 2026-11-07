
and replace 32 with `CHAR_BIT * sizeof(unsigned int)`

For 32-bit unsigned ints, these expressions evaluate to 31 and 32. For 64-bit unsigned ints, they evaluate to 63 and 64.

## 10.9.3 Using the Bitwise AND, Inclusive OR, Exclusive OR and Complement Operators

Figure 10.5 demonstrates the bitwise AND, the bitwise inclusive OR, the bitwise exclusive OR and the bitwise complement operators. The program uses function displayBits (lines 45–62) to display the unsigned int values.

```c
// fig10_05.c
// Using the bitwise AND, bitwise inclusive OR, bitwise
// exclusive OR and bitwise complement operators
#include <stdio.h>

void displayBits(unsigned int value); // prototype

int main(void) {
   // demonstrate bitwise AND (&)
   unsigned int number1 = 65535;
   unsigned int mask = 1;
   puts("The result of combining the following");
   displayBits(number1);
   displayBits(mask);
   puts("using the bitwise AND operator & is");
   displayBits(number1 & mask);

   // demonstrate bitwise inclusive OR (|)
   number1 = 15;
   unsigned int setBits = 241;
   puts("\nThe result of combining the following");
   displayBits(number1);
   displayBits(setBits);
   puts("using the bitwise inclusive OR operator | is");
   displayBits(number1 | setBits);

   // demonstrate bitwise exclusive OR (^)
   number1 = 139;
   unsigned int number2 = 199;
   puts("\nThe result of combining the following");
   displayBits(number1);
   displayBits(number2);
   puts("using the bitwise exclusive OR operator ^ is");
   displayBits(number1 ^ number2);

   // demonstrate bitwise complement (~)
   number1 = 21845;
   puts("\nThe one");
   displayBits(number1);
   puts("is");
   displayBits(~number1);
}

// display bits of an unsigned int value
void displayBits(unsigned int value) {
  // declare displayMask and left shift 31 bits
  unsigned int displayMask = 1 << 31;

  printf("%10u = ", value);

  // loop through bits
  for (unsigned int c = 1; c <= 32; ++c) {
    putchar(value & displayMask ? '1' : '0');
    value <<= 1; // shift value left by 1

    if (c % 8 == 0) { // output a space after 8 bits
      putchar(' ');
    }
  }

  putchar('\n');
}
```

**Fig. 10.5** | Using the bitwise AND, bitwise inclusive OR, bitwise exclusive OR and bitwise complement operators. (Part 1 of 2.)

```text
The result of combining the following
65535 = 00000000 00000000 11111111 11111111
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

The one
21845 = 00000000 00000000 01010101 01010101
is
4294945450 = 11111111 11111111 10101010 10101010
```

Fig. 10.5 | Using the bitwise AND, bitwise inclusive OR, bitwise exclusive OR and bitwise complement operators. (Part 2 of 2.)

### Bitwise AND Operator (&)

Line 10 assigns the value 65535 `00000000 00000000 11111111 11111111` to the integer variable number1, and line 11 assigns the value 1 `00000000 00000000 00000000 00000001` to the variable mask. When you combine number1 and mask using the bitwise AND operator (&) in the expression number1 & mask (line 16), the result is `00000000 00000000 00000000 00000001`.

All the bits except the low-order bit in number1 are “masked off” (hidden) by “AND-ing” with variable mask.

### Bitwise Inclusive OR Operator (|)

The bitwise inclusive OR operator sets specific bits to 1 in an operand. Line 19 assigns 15 `00000000 00000000 00000000 00001111` to the variable number1 and line 20 assigns 241 `00000000 00000000 00000000 11110001` to the variable setBits. When you combine number1 and setBits with the bitwise inclusive OR operator in the expression number1 | setBits (line 25), the result is 255 `00000000 00000000 00000000 11111111`.

The following table summarizes the results of combining two bits with the bitwise inclusive OR operator.

| Bit 1 | Bit 2 | Bit 1 \| Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Bitwise Exclusive OR Operator (^)

The bitwise exclusive OR operator (^) sets each bit in the result to 1 if exactly one of the corresponding bits in its two operands is 1. Line 28 assigns number1 the value 139 `00000000 00000000 00000000 10001011` and line 29 assigns number2 the value 199 `00000000 00000000 00000000 11000111`. When you combine these variables with the bitwise exclusive OR operator in the expression number1 ^ number2 (line 34), the result is `00000000 00000000 00000000 01001100`.

The following table summarizes the results of combining two bits with the bitwise exclusive OR operator.

| Bit 1 | Bit 2 | Bit 1 ^ Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Bitwise Complement Operator (~)

The bitwise complement operator (~) sets all 1 bits in its operand to 0 in the result and sets all 0 bits to 1. This is otherwise referred to as "taking the one’s complement of the value." Line 37 assigns number1 the value 21845 `00000000 00000000 01010101 01010101`. The expression ~number1 (line 41) toggles all the bits producing `11111111 11111111 10101010 10101010`.

## 10.9.4 Using the Bitwise Left- and Right-Shift Operators

Figure 10.6 demonstrates the left-shift (<<) and right-shift (>>) operators. Again, we use the function displayBits to display the unsigned int values.

```c
// fig10_06.c
// Using the bitwise shift operators
#include <stdio.h>

void displayBits(unsigned int value); // prototype

int main(void) {
    unsigned int number1 = 960; // initialize number1

    // demonstrate bitwise left shift
    puts("\nThe result of left shifting");
    displayBits(number1);
    puts("8 bit positions using the left shift operator << is");
    displayBits(number1 << 8);

    // demonstrate bitwise right shift
    puts("\nThe result of right shifting");
    displayBits(number1);
    puts("8 bit positions using the right shift operator >> is");
    displayBits(number1 >> 8);
}

// display bits of an unsigned int value
void displayBits(unsigned int value) {
    // declare displayMask and left shift 31 bits
    unsigned int displayMask = 1 << 31;

    printf("%10u = ", value);

    // loop through bits
    for (unsigned int c = 1; c <= 32; ++c) {
        putchar(value & displayMask ? '1' : '0');
        value <<= 1; // shift value left by 1

        if (c % 8 == 0) { // output a space after 8 bits
            putchar(' ');
        }
    }

    putchar('\n');
}
```

```text
The result of left shifting
960 = 00000000 00000000 00000011 11000000
8 bit positions using the left shift operator << is
245760 = 00000000 00000011 11000000 00000000

The result of right shifting
960 = 00000000 00000000 00000011 11000000
8 bit positions using the right shift operator >> is
3 = 00000000 00000000 00000000 00000011
```

Fig. 10.6 | Using the bitwise shift operators. (Part 2 of 2.)

### Left-Shift Operator (<<)

The left-shift operator (<<) shifts the bits of its left operand to the left by the number of bits specified in its right operand. Bits vacated to the right are replaced with 0s. Bits shifted off the left are lost. Line 8 assigns the variable number1 the value 960 `00000000 00000000 00000011 11000000`.

Left-shifting number1 eight bits with the expression number1 << 8 (line 14) results in the value 245760 `00000000 00000011 11000000 00000000`.

### Right-Shift Operator (>>)

The right-shift operator (>>) shifts the bits of its left operand to the right by the number of bits specified in its right operand. Right-shifting an unsigned int replaces the vacated bits at the left with 0s. Bits shifted off the right are lost. The result of right-shifting number1 with the expression number1 >> 8 (line 20) is 3 `00000000 00000000 00000000 00000011`.
