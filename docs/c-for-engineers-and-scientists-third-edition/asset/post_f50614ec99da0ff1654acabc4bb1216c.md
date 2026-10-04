
# Chapter 15

## 793 The Exclusive OR Operator

A sample run of Program 15.4 follows:

```
Enter a string of both uppercase and lowercase letters:
ababcdefghijklmnopqrstuvwxyz
The string of letters you entered is:
ababcdefghijklmnopqrstuvwxyz
This string, in lowercase letters, is:
ababcdefghijklmnopqrstuvwxyz
```

Reviewing Program 15.4, first notice that the input string has been stored and passed to lower() as a C-string, which is an array of characters. This permits the called function to receive and process the original character values instead of a copy of the values. Second, notice that uppercase characters are converted to lowercase and letters remain unaltered. This result happens because the first of all lowercase letters is 1, so forcing this bit to 1 has no effect. When this bit is 0, for uppercase letters, this is the input character altered.

### 15.3 The Exclusive OR Operator

The exclusive OR operator performs a bit-by-bit comparison of its operands. The result of the comparison is determined by the following rule: The result of the comparison is 1 if one, and only one, of the bits being compared is 1; otherwise, the result is 0. As shown in the following example of an exclusive OR operation, when both bits are compared the same value (both 1 or both 0), the result is 0. When both bits have different values (one 1 and the other 0) the result is 1. Again, each pair of bit comparison is independent of any other bit comparison.

```
0 0 1 1 0 0 1
^ 1 1 0 1 0 1 1
- - - - - - -
0 1 1 0 1 1 0
```

An OR operation can be used to create the opposite value, or complement, of any bit in a variable. The reason is that exclusive OR any bit (1 or 0) with 1 forces the resulting bit to be the opposite value of its original state, and exclusive OR any bit (1 or 0) with 0 leaves the original unchanged. For example, the variable op1 has the pattern x x x x x x x; each can be 1 or 0, independent of any other x in the number. Using the notation that x is the (opposite) value of x, the result of exclusive ORing with the binary number 0 1 0 1 0 1 0 1 is as follows:

```
op1 = x x x x x x x
op2 = 0 1 0 1 0 1 0 1
```

```
Result = x x x x x x x
```

As you can see in this example, the 1s in op2 force the resulting bits to be the complement of their original bit values, and the 0s in op2 filter the bits in op1 through no change in their values.

## 794 Bit Operations

Many encryption methods use the exclusive OR operation to code data by exclusive ORing each character with a mask value. The choice of the mask value, which is referred to as the encryption key, is arbitrary, and any key value can be used. Program 15.5 uses an encryption key of 52 to code a user-entered message.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_813_0.png)

### Program 15.5

```cpp
#include <iostream>
using namespace std;

void encrypt(char *); // function prototype

int main()
{
    char message[81]; // enough storage for a complete line
    cout << "\nEnter a sentence:\n";
    cin.getline(message,80,'\n');
    cout << "\nThe sentence just entered is:\n";
    cout << message << endl;
    encrypt(message);
    cout << "\nThe encrypted version of this sentence is:\n";
    cout << message << endl;
    return 0;
}

void encrypt(char *message)
{
    while (*message != '\0')
        *message++ ^= 52;
}
```

Following is a sample run of Program 15.5:

```
Enter a sentence:
Good morning
The sentence just entered is:
Good morning
The encrypted version of this sentence is:
s[P|Y[FZ]ZS
```

## Different-Size Data Items

Decoding an encrypted message requires ORing the coded message with the original encryption key, which is left for you to try as an exercise (see Programming Practice for Chapter 15, Exercise 12, at the end of the chapter).

### 15.4 The Complement Operator

The complement operator, ~, is a unary operator that changes each 1 bit in its operand to 0 and each 0 bit to 1. For example, if the variable op1 contains the binary number 11001010, ~op1 replaces this binary number with the number 00110101. The complement operator is used to force any bit in an operand to 0, independent of the actual number of bits used to store the number. For example,

```cpp
op1 = op1 & ~07; // 07 is an octal
```

or its shorter form sets the last three bits of op1 to 0, regardless of how op1 is stored in the computer. Either statement, of course, is replaced by AND the last three bits of op1 with 0s, if the number of bits used to store the number. In a computer that uses 16 bits to store integers, the AND operation is

```cpp
op1 = op1 & ~077; // in octal
```

```cpp
op1 = op1 & ~0xFFFF; // in hexadecimal
```

For a computer that uses 32 bits to store integers, the preceding AND sets the leftmost 16 bits to the left, which is an unintended result. The following is the correct statement for 32 bits:

```cpp
op1 = op1 & ~0777777; // in octal
```

```cpp
op1 = op1 & ~xFFFFFF; // in hexadecimal
```

Using the complement operator in this situation frees the programmer from having to determine the operand's size, and more importantly makes the program portable between machines.

### 15.5 Different-Size Data Items

When the operators & and ^ are used with operands of different sizes, the shorter operand is always increased in size to match the larger operand's size. Figure 15.1 illustrates adding a 16-bit unsigned integer to a 32-bit number. As the figure shows, the additional bits are added to the left of the original number and filled with 0s. This is the equivalent of adding leading 0s to the number, which has no effect on the number's value.

## 796 Bit Operations

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_815_0.png)

When extending signed numbers, the original leftmost bit is reproduced in the extra bits added to the number. As illustrated in Figure 15.2, if the leftmost bit is 0, corresponding to a positive number, 0 is placed in each of the additional bit positions. If the leftmost bit is 1, which corresponds to a negative number, 1 is placed in the additional bit positions. In either case, the resulting binary number has the same sign and magnitude as the original number.

Figure 15.1 Extending 16-bit unsigned data to 32 bits

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_815_1.png)

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_815_2.png)

Figure 15.2 Extending 16-bit signed data to 32 bits

### 15.6 The Shift Operators

The left shift operator, <<, causes bits in an operand to be shifted to the left by a given amount. For example, the statement

```cpp
op1 << 4;
```

causes the bits in op1 to be shifted four bits to the left, filling any vacated bits with a 0. Figure 15.3 illustrates the effect of shifting the binary number 1111000010101011 to the left by four bit positions.

## 797 The Shift Operators

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_816_0.png)

Figure 15.3 An example of a left shift

For unsigned integers, each left shift corresponds to multiplication by two. This is also true for signed numbers using complement representation, as long as the leftmost bit doesn't switch values. Because a change in the leftmost bit of a two's complement number represents a change in both the sign and magnitude represented by the bit, this shift doesn't represent a simple multiplication by two.

The right shift operator, >> causes the bits in an operand to be shifted to the right by three bit positions for a given amount. For example, the statement

```cpp
op2 = op1 >> 3;
```

causes the bits in op1 to be shifted to the right by binary number 11110000101011. Figure 15.4a illustrates the right shift of the unsigned binary bits are shifted 'off the end' and are lost. As shown, the three rightmost bits are shifted three bit positions.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_816_1.png)

Figure 15.4a An unsigned arithmetic right shift

## Bit Operations

For unsigned numbers, the leftmost bit isn't used as a sign bit. For this type of number, the vacated leftmost bits are always filled with 0s, as shown in Figure 15.4a. For signed numbers, what's filled in the vacated bits depends on the computer. Most computers reproduce the number's original sign bit. Figure 15.4b illustrates the right shift of a negative binary number by bit positions, and the sign bit is reproduced in the vacated bits. Figure 15.4c illustrates the equivalent right shift of a positive binary number.

The sign bit is a 1

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_817_0.png)

Vacated bit positions are filled with 1s

Figure 15.4b The right shift of a negative binary number

The sign bit is a 0

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_817_1.png)

Vacated bit positions are filled with 0s

Figure 15.4c The right shift of a positive binary number
