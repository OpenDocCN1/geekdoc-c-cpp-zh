
determines whether a 1 or a 0 should be printed for the current leftmost bit of variable value. When value and displayMask are combined using & all the bits except the high-order bit in variable value are "masked off" (hidden), because any bit "ANDed" with 0 yields 0. If the leftmost bit is 1, value & displayMask evaluates to a nonzero (true) value and 1 is printed—otherwise, 0 is printed. Variable value is then left shifted one bit by the expression value <<= 1 (this is equivalent to value = value << 1). These steps are repeated for each bit in unsigned variable value. Figure 10.8 summarizes the results of combining two bits with the bitwise AND operator.

### Common Programming Error 10.10

Using the logical AND operator (&&) for the bitwise AND operator (&)—and vice versa—is an error.

| Bit 1 | Bit 2 | Bit 1 & Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Fig. 10.8 | Results of combining two bits with the bitwise AND operator &.

## 10.9.2 Making Function displayBits More Generic and Portable

In line 21 of Fig. 10.7, we hard coded the integer 31 to indicate that the value 1 should be shifted to the leftmost bit in the variable displayMask. Similarly, in line 26, we hard coded the integer 32 to indicate that the loop should iterate 32 times—once for each bit in variable value. We assumed that unsigned ints are always stored in 32 bits (four bytes) of memory. Today's popular computers generally use 32-bit or 64-bit word hardware architectures. As a C programmer, you'll tend to work across many hardware architectures, and sometimes unsigned ints will be stored in smaller or larger numbers of bits.

### Portability Tip 10.7

Figure 10.7 can be made more generic and portable by replacing the integers 31 (line 21) and 32 (line 26) with expressions that calculate these integers, based on the size of an unsigned int for the platform on which the program executes. The symbolic constant CHAR_BIT (defined in `<limits.h>`) represents the number of bits in a byte (normally 8). Recall sizeof determines the number of bytes used to store an object or type. The expression sizeof(unsigned int) evaluates to 4 for 32-bit unsigned ints and 8 for 64-bit unsigned ints. You can replace 31 with CHAR_BIT * sizeof(unsigned int) - 1 and replace 32 with CHAR_BIT * sizeof(unsigned int). For 32-bit unsigned ints, these expressions evaluate to 31 and 32, respectively. For 64-bit unsigned ints, they evaluate to 63 and 64.

## 10.9.3 Using the Bitwise AND, Inclusive OR, Exclusive OR and Complement Operators

Figure 10.9 demonstrates the use of the bitwise AND operator, the bitwise inclusive OR operator, the bitwise exclusive OR operator and the bitwise complement operator. The program uses function displayBits (lines 46–64) to print the unsigned int values. The output is shown in Fig. 10.10.

```c
// Fig. 10.9: fig10_09.c
// Using the bitwise AND, bitwise inclusive OR, bitwise
// exclusive OR and bitwise complement operators
#include <stdio.h>

void displayBits(unsigned int value); // prototype

int main(void)
{
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
    puts("\nThe one's complement of");
    displayBits(number1);
    puts("is");
    displayBits(~number1);
}
```

Fig. 10.9 | Using the bitwise AND, bitwise inclusive OR, bitwise exclusive OR and bitwise complement operators. (Part 1 of 2.)

```c
// display bits of an unsigned int value
void displayBits(unsigned int value)
{
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

Fig. 10.9 | Using the bitwise AND, bitwise inclusive OR, bitwise exclusive OR and bitwise complement operators. (Part 2 of 2.)

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

The one's complement of
21845 = 00000000 00000000 01010101 01010101
is
4294945450 = 11111111 11111111 10101010 10101010
```

Fig. 10.10 | Output for the program of Fig. 10.9.

### Bitwise AND Operator (&)

In Fig. 10.9, integer variable number1 is assigned value 65535 (00000000 00000000 11111111 11111111) in line 11 and variable mask is assigned the value 1 (00000000 00000000 00000000 00000001) in line 12. When number1 and mask are combined using the bitwise AND operator (&) in the expression number1 & mask (line 17), the result is 00000000 00000000 00000000 00000001. All the bits except the low-order bit in variable number1 are "masked off" (hidden) by "ANDing" with variable mask.

### Bitwise Inclusive OR Operator (|)

The bitwise inclusive OR operator (|) is used to set specific bits to 1 in an operand. In Fig. 10.9, variable number1 is assigned 15 (00000000 00000000 00000000 00001111) in line 20, and variable setBits is assigned 241 (00000000 00000000 00000000 11110001) in line 21. When number1 and setBits are combined using the bitwise inclusive OR operator in the expression number1 | setBits (line 26), the result is 255 (00000000 00000000 00000000 11111111). Figure 10.11 summarizes the results of combining two bits with the bitwise inclusive OR operator.

| Bit 1 | Bit 2 | Bit 1 \| Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Fig. 10.11 | Results of combining two bits with the bitwise inclusive OR operator |.

### Bitwise Exclusive OR Operator (^)

The bitwise exclusive OR operator (^) sets each bit in the result to 1 if exactly one of the corresponding bits in its two operands is 1. In Fig. 10.9, variables number1 and number2 are assigned the values 139 (00000000 00000000 00000000 10001011) and 199 (00000000 00000000 00000000 11000111) in lines 29–30. When these variables are combined with the bitwise exclusive OR operator in the expression number1 ^ number2 (line 35), the result is 00000000 00000000 00000000 01001100. Figure 10.12 summarizes the results of combining two bits with the bitwise exclusive OR operator.

| Bit 1 | Bit 2 | Bit 1 ^ Bit 2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Fig. 10.12 | Results of combining two bits with the bitwise exclusive OR operator ^.

### Bitwise Complement Operator (~)

The bitwise complement operator (~) sets all 1 bits in its operand to 0 in the result and sets all 0 bits to 1 in the result—otherwise referred to as "taking the one's complement of the
