

## PROBLEMS

- 1. Give the entire count sequence of binary patterns for 3-bit unsigned integers.

- 2. What is the decimal value represented by the 8-bit binary number 11001001.0101₂ when interpreted as:
  - (a) An unsigned number?
  - (b) A 2's-complement number?

- 3. What is the decimal value represented by the binary number 10001101₂ when interpreted as:
  - (a) A sign + magnitude number?
  - (b) A 2's-complement number?

- 4. Use polynomial evaluation to:
  - (a) Convert 101101₂ to base 10.
  - (b) Convert DEAF₁₆ to base 10.
  - (c) Convert 0.325₄ to base 10.

- 5. Use repeated division to:
  - (a) Convert 150₁₀ to base 2.
  - (b) Convert 1500₁₀ to base 16.
  - (c) Convert 400₁₀ to base 7

- 6. Use repeated multiplication to⁵:
  - (a) Convert 0.9₁₀ to base 2.
  - (b) Convert 0.9₁₀ to base 16.
  - (c) Convert 0.9₁₀ to base 3.

- 7. Use shortcuts based on power relationships to:
  - (a) Convert ACE₁₆ to base 2.
  - (b) Convert FACE₁₆ to base 8.
  - (c) Convert 1011.0111₂ to base 8.
  - (d) Convert 2321.1₈ to base 8.
  - (e) Convert 176₈ to base 3

- 8. Perform the indicated conversions:
  - (a) Convert FA₁₆.E₈ to base 2 (binary).
  - (b) Convert 101011.01101₂ to base 16 (hexadecimal).
  - (c) Convert 56.23₁₀ to base 2 (binary).
  - (d) Convert 1101.101101₂ to base 10 (decimal).
  - (e) Convert 12.34₈ to base 7

- 9. Convert the decimal number -371₁₀ to 16-bit 2's-complement binary, with 8 bits of integer part and 8 bits of fractional part.

⁵ If the process repeats indefinitely, calculate as few digits as necessary to provide same or better resolution.

- 10. What is the 2's-complement 8-bit representation of -10010₂?

- 11. Give the 2's-complement 8-bit representation of -77₁₀, with the binary point in the middle (e.g., bbbb.bbbb).

- 12. For each of the following 2's-complement numbers, give the corresponding 8-bit representation of the negative of its value:
  - (a) 01010101
  - (b) 10101010
  - (c) 10000001
  - (d) 01111110

- 13. Consider a 2's-complement number represented by n bits, with the binary point placed between the two most significant bits (e.g., bbb ... b).
  - (a) Give an algebraic expression in terms of n for the positive value that has the smallest nonzero magnitude.
  - (b) Give the binary representation of (a), where n is 8.
  - (c) Give an algebraic expression in terms of n for the negative value that has the smallest nonzero magnitude.
  - (d) Give the binary representation of (c), where n is 8.

- 14. Give the 32-bit binary representation of the floating-point value -25.1:

| 31 | 30 | ... | 23 | 22 | ... | 0 |
|---|---|---|---|---|---|---|
| | | | | | | |

- 15. The ASCII code for the symbol "0" is 30₁₆. Use this fact to determine the hex constants that would be stored in memory, starting at address N, for the C character string "12345":

| Address | N+1 | N+2 | N+3 | N+4 | N+5 | N+6 | ... |
|---|---|---|---|---|---|---|---|
| N | | | | | | | |

- 16. Perform the indicated addition on the following 4-bit operands, filling in all the indicated fields:

| | | | | | 0 | Carries |
|---|---|---|---|---|---|---|
| 1 | 0 | 1 | | 1 | | Addend |
| + | 0 | 1 | 1 | | 0 | Augend |
| | | | | | | Sum Bits |

- 17. Perform the indicated subtraction on the following 4-bit operands, filling in all the indicated fields:

| | | | | | 0 | Borrows |
|---|---|---|---|---|---|---|
| 1 | 0 | 1 | | 1 | | Minuend |
| - | 0 | 1 | 1 | | 0 | Subtrahend |
| | | | | | | Difference Bits |

- 18. If the operands are unsigned, then does an overflow occur:
  - (a) In problem 16?
  - (b) In problem 17?

- 19. If the operands are signed, then does an overflow occur:
  - (a) In problem 16?
  - (b) In problem 17?

- 20. Find the indicated sum of the following signed 8-bit 2's-complement numbers and indicate which cause an arithmetic overflow to occur:
  - (a) 00111101 +01101100
  - (b) 00101101 +10110101
  - (c) 11101011 +11110100

- 21. Find the indicated difference of the following signed 8-bit 2's-complement numbers and indicate which cause an arithmetic overflow to occur:
  - (a) 00101100 +01010100
  - (b) 00101110 +01101011
  - (c) 11000100 +1010101

- 22. Assume that the C assignment statement "s = a + b" has just been executed, where all variables are declared as signed ints. Write a C expression that is true if and only if the addition results in an overflow.

- 23. Repeat problem 22 for the C assignment statement "s = a - b"

- 24. What is the most positive decimal value of a 6-bit 2's-complement number?

- 25. What is the most negative decimal value of a 6-bit 2's-complement number?

- 26. What is the minimum decimal value of a 6-bit unsigned number?

- 27. What is the maximum decimal value of a 6-bit unsigned number?

- 28. The exact binary representation of one-sixth (1/6) requires an infinite number of digits. Truncating it (discarding extra bits) to make it fit within a fixed-precision representation creates a representation error. What is the absolute error that results from storing one-sixth without rounding using 8 fractional bits?

## True/False:

- 29. Overflow is impossible when subtracting one unsigned number from another.

- 30. Overflow is impossible when subtracting two signed operands of the same sign.

- 31. There are two representations of zero in 2's complement.

- 32. If rollover occurs when incrementing an integer, there is an overflow.

- 33. In 2's complement, the absolute values of full-scale negative and full-scale positive are identical.

## Implementing Arithmetic

### 3.1 2'S-COMPLEMENT AND HARDWARE COMPLEXITY

Computers manipulate bit patterns. *How* those patterns are assigned to the values they represent has a big effect on hardware complexity. For example, both the sign-plus-magnitude and the 2's-complement representation allow us to recognize whether a number is positive or negative simply by looking at the most significant bit. However, wouldn't it be great if patterns were assigned to values in such a way that the same hardware could be used to perform integer arithmetic regardless of whether the operands were signed or unsigned? That is exactly what the 2's-complement representation is intended to do!

For example, suppose we were to add the two *unsigned* decimal values 9 and 3. The computer would be given their binary equivalents, 1001 and 0011. The correct decimal result is 12, so the hardware that performs addition is designed to produce the binary equivalent, 1100. But what happens if those same binary patterns are interpreted instead as *signed* numbers according to the 2's-complement scheme shown in Figure 3-1? Then, the operands would be -7 and +3, and the same binary result of 1100 produced by the hardware would correctly be interpreted as -4.

The fundamental characteristic of 2's-complement representation that makes this work is that it follows a count sequence¹ from full-scale negative to full-scale positive (with a rollover to zero), in much the same way that the representation of unsigned numbers follows a count sequence from the smallest magnitude (zero) to the largest. The sign-plus-magnitude representation does not share this characteristic.

¹ The sequence of numeric values represented by the sequence of patterns is monotonically increasing, meaning that it increases by one at each step.

In a similar manner, using the 2's-complement representation permits one hardware subtractor for both signed and unsigned integers. However, it also turns out that we do not even need separate hardware for addition and subtraction! All we need to do in order to compute the difference A - B is to *add* the negative of B to A, as in A + (-B). In other words, we simply need to add some hardware to form the 2's complement of B.

All hardware adders accept an initial “carry-in” that can be used to add a constant of 0 or 1 to the sum. Normally, this input is set to 0. However, if we set it to 1 and invert all the bits of B, the net effect will be the same as adding -B instead of B. We can

![](img/f0b8aa873b11dc585ed698a10d04e7a7_54_0.png)

FIGURE 3-1 One adder for both unsigned and 2's-complement signed numbers.

then implement a single circuit with one control input that will compute either A + B or A – B by simply using a set of exclusive-OR gates as a controlled inverter that passes either B or its inverse to the adder, as shown in Figure 3-2.

There are minor differences, however, in how other operations are implemented. Suppose, for example, that we need to compare two integers X and Y. Knowing their bit patterns is not sufficient to determine which represents the greater value. For example, 1001 is not always greater than 0011. That is true only if these patterns represent unsigned integers. If they represent signed integers, then 0011 represents the greater value.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_54_1.png)

FIGURE 3-2 Modified adder performs both addition and subtraction.

