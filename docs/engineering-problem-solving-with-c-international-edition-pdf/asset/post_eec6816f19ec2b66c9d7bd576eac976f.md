
### Example

143₈ = ?₂

```
1   4   3
↓   ↓   ↓
001 100 011
143₈ = 001100011₂
```

### Example

000101011011101₂ = ?₈

```
000 101 011 011 101
↘   ↘   ↘   ↘   ↘
0   5   3   3   5
000101011011101₂ = 5335₈
```

### Practice!

Convert each of the following base 10 numbers to base 2.

- 1. 921₁₀ = ?₂
- 2. 8₁₀ = ?₂
- 3. 100₁₀ = ?₂

Convert each of the following base 8 numbers to base 10.

- 4. 100₈ = ?₁₀
- 5. 247₈ = ?₁₀
- 6. 16₈ = ?₁₀

Convert each of the following numbers to the requested base.

- 7. 100₂ = ?₈
- 8. 3716₈ = ?₂
- 9. 110100111₂ = ?₁₀
- 10. 221₆ = ?₈

Hexadecimal Numbers. The hexadecimal, or base 16, number system has 16 hexadecimal digits, (0–9,A–F), and each digit in a hexadecimal number multiplies a power of 16. The decimal values of the hexadecimal digits represented by letters are (10,11,12,13,14,15) respectively.

The number 2BF₁₆ is an example of a hexadecimal number. Applying the conversion algorithm for converting from any base to 10, we can determine the equivalent decimal number, as illustrated below.

```
2BF₁₆ = ?₁₀

2 * 16^2 + F * 16^1 + B * 16^0 =
2 * 256 + 15 * 16 + 11 * 1 =
512 + 240 + 11 =
763₁₀
```

To illustrate the algorithm for converting from base ten to any other base, we will convert 763₁₀ back to base 16. The remainder of each division is a value between 0 and F.

```
763₁₀ = ?₁₆

  0  R2
16|2  R15(F)
16|16  R11(B)
16|16763
      |
Hex Digits
763₁₀ = 2FB₁₆
```

Sixteen is a power of 2, 16 = 2^4, and each of the hexadecimal digits can be represented in binary using four binary digits. This relationship can be used to quickly convert from binary to hexadecimal and hexadecimal to binary, as illustrated in the next two examples. Table 1.3 lists the binary representation of the hexadecimal digits for your convenience.

### Example

```
7BF₁₆ = ?₂

  7       B       F
  |       |       |
0111   1011   1111

7BF₁₆ = 011110111111₂
```

### Example

```
10100001101₂ = ?₁₆

  1010   000   1101
   |       |     |
   A       0     D

10100001101₂ = A0D₁₆
```

TABLE 1.3 Binary Representation of Hexadecimal Digits

| Hexadecimal Digit | Binary Representation |
|---|---|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |
| A | 1010 |
| B | 1011 |
| C | 1100 |
| D | 1101 |
| E | 1110 |
| F | 1111 |

### Practice!

Convert each of the following base 10 numbers to base 16.

- 1. 921₁₀ = ?₁₆
- 2. 8₁₀ = ?₁₆
- 3. 100₁₀ = ?₁₆

Convert each of the following base 16 numbers to base 10.

- 4. 1C0₁₆ = ?₁₀
- 5. 29E₁₆ = ?₁₀
- 6. 16₁₆ = ?₁₀

Convert each of the following numbers to the requested base.

- 7. 10010011₂ = ?₁₆
- 8. 3A1B₁₆ = ?₂
- 9. 110100111₂ = ?₁₀
- 10. 261₈ = ?₁₆

## Data Types and Storage

When data is represented in memory, it is represented as a sequence of bits. The sequence of bits may represent an instruction, a numeric value, a character, a portion of an image or digital signal, or some other type of data. If we look at the bit sequence 01000110₂, for example, it has a decimal value of 70. It also is the American National Standard Institute (ANSI) character code for the character F.

ANSI

Data representation is becoming an increasingly important and interesting field in engineering, math and computer science. The amount of data that can be generated and processed is increasing as computers become more powerful, and the use of computers in data intensive applications such as bio-computing, communications and signal processing present new challenges for defining and representing data. In this section, we will discuss the digital representation of two basic data types, integer and floating point.

### Integer Data Type.

In the previous section, we used an algorithm to convert from base 10 to base 2. This algorithm works for any base 10 integer, so in theory we can represent, exactly, all base 10 integers in base 2. In practice, we may be limited by the word size of our computing system. Integer data is often stored in memory using 4 bytes, or 32 bits. The left most bit is reserved for the sign, leaving 31 bits for the magnitude of the number.

Consider the following example that uses a word size of 8 for simplicity. The largest signed integer that can be represented in 8 bits is 2^7 - 1 or 127₁₀, as illustrated below.

```
0 1 1 1 1 1 1 1
```

The representation of data in a digital computer affects the efficiency of arithmetic and logic operations. Many computer systems store positive signed integers as illustrated above, and store negative signed integers in their 2's complement form. Storing negative integers in their 2's complement form allows for efficient execution of arithmetic operations, without checking the sign bit. First, we illustrate how to form the 2's complement of a negative number, then, we will illustrate how storing negative numbers in their 2's complement form can simplify arithmetic operations.

2's complement form

The 2's complement of a binary number is formed by negating all of the bits and adding one. Negating a bit means switching the value, or state, of a bit from 1 to 0, or from 0 to 1. Negating all the bits of a binary number forms the 1's complement of the number. Adding one to the 1's complement results in the 2's complement of the number. Using a word size of 8, the 2's complement of -127₁₀ is computed in the following example.

1's complement

#### Example Compute the 2's complement representation for the value -127₁₀.

To form the 2's complement of a negative integer, we begin with the binary representation of the unsigned value.

```
127₁₀ = 01111111₂
```

Next, we negate the bits to form the 1's complements.

```
10000000₂
```

Finally, we add 1₁₀ = 00000001₂ to form the 2's complement.

```
10000001₂.
```

Thus, the 2's complement representation for -127₁₀ is 10000001₂.

Notice what happens when we add 127₁₀ to the 2's complement of -127₁₀.

| 01111111₂ | 127₁₀ |
| --- | --- |
| + 10000001₂ | 2's complement of -127₁₀ |
| = 00000000₂ | result of addition is 0 |

The 2's complement form for representing signed integers has the property that adding a positive integer, n, to the 2's complement of n results in zero for all n. Another important property of 2's complement representation is that there is a unique representation for binary 0.

When performing addition on signed integers represented in 2's complement form, the result, if negative, will be in its 2's complement form, as shown in the following examples.

#### Example Addition of 2 binary numbers, positive result.

| 11110110 | -10₁₀ represented in 2's complement |
| --- | --- |
| + 00001101 | 13₁₀ |
| = 00000011 | 3₁₀ |

#### Example Addition of 2 binary numbers, negative result.

| 00001010 | 10₁₀ |
| --- | --- |
| + 11110011 | -13₁₀ represented in 2's complement |
| = 11111101 | -3 represented in 2's complement |

### Practice!

Find the 2's complement of the following integers:

- 1. 11001111₂
- 2. -192₁₀
- 3. -45₈

### Floating Point Data Type.

A floating point number, or real number, such as 12.25₁₀ includes a decimal point. The digits to the left of the decimal point form the integral part of the number and the digits to the right of the decimal point form the fractional part of a number. The fractional part of a decimal number can be converted to binary by repeatedly multiplying the fractional part by 2 and recording the carry bits until the fractional part becomes zero. This algorithm is illustrated in the following example.

#### Example Convert 12.25₁₀ to binary.

First, the integral part, 12₁₀ is converted to binary:

```
12 ÷ 2 = 6 R 0
6 ÷ 2 = 3 R 0
3 ÷ 2 = 1 R 1
1 ÷ 2 = 0 R 1

12₁₀ = 1100₂
```

Next we will convert the fractional part, .25₁₀ to binary by repeatedly multiplying the fractional part by 2 and recording the carry bits:

```
.25 * 2 = 0.5 C0
.5 * 2 = 1.0 C1
```

.25₁₀ = .01₂

The integral and fraction parts are now combined to form the equivalent binary value. Thus, the value 12.25₁₀ = 1100.01₂.

To convert the floating point binary number 1100.01₂ back to decimal, the binary digits to the right of the decimal point are multiplied by negative powers of 2, as shown below.

```
1100.01₂ =
1 * 2³ + 1 * 2² + 0 * 2¹ + 0 * 2⁰ + 0 * 2⁻¹ + 1 * 2⁻² =
1 * 8 + 1 * 4 + 0 + 0 + 0 * (1/2) + 1 * (1/4) =
8 + 4 + 0 + 0 + 0 + 0.25 =
12.25
```

1100.01₂ = 12.25₁₀

In the above example, we found an exact binary representation for the value 12.25₁₀. Unfortunately, many floating-point decimals have only an approximate binary representation, as illustrated in the next example.

#### Example Convert 12.6₁₀ to binary.

The integral portion, 12₁₀, has been shown to equal 1100₂. Converting the fractional portion, we repeatedly multiply by 2 and record the carry bits.

```
.6 * 2 = 1.2 C1
.2 * 2 = 0.4 C0
.4 * 2 = 0.8 C0
.8 * 2 = 1.6 C1
.6 * 2 = 1.2 C1
.2 * 2 = 0.4 C0
.4 * 2 = 0.8 C0
.8 * 2 = 1.6 C1
```
