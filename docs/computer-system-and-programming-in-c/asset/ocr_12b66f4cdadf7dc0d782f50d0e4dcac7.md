# Solution

1⁸×5⁸　2⁸×4⁸　7⁸×8³　6⁸×2⁸　6⁸×8¹　2⁸×8⁰
1³×32768　2³×4096　7³×512　6³×64　6³×8　2¹
32768　8192　3584　384　48　2
Answer is 32768 + 8192 + 3584 + 384 + 48 + 2 = 44978

# Example 2

Convert (237.04)₈ to decimal form.

# Solution

| Weights | 8² | 8¹ | 8⁰ | 8⁻¹ | 8⁻² |
|---|---:|---:|---:|---:|---:|
| Weight | 64 | 8 | 1 | 0.125 | 0.015625 |
| Value |  |  |  |  |  |
| Octal Number | 2 | 3 | 7 | 0 | 4 |
| Decimal Value | 128 | 24 | 7 | 0 | 0.0625 | Total (159.0625)₁₀

# Octal to Binary Conversion

The primary application of octal numbers is representing binary numbers, as it is easier to read large numbers in octal form than in binary form. Because each octal digit can be represented by a three-bit binary number (see the following table), it is very easy to convert from octal to binary. Simply exchange each octal digit with the appropriate three-bit binary number as indicated in the examples below.

The following table shows the octal digit and the equivalent binary digit.

| Octal digit | Binary digit |
|---:|---:|
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

# Example 1

Convert (13)₈ into equivalent binary number.

# Solution

(13)₈ = (010011)₂

# Example 2

Convert (37.12)₈ into equivalent binary number.

# Solution

(37.12)₈ = (011111.001010)₂

# Example 3

Convert (127662)₈ into equivalent binary number.

1　2　7　6　6　2
001　010　111　110　110　010
This gives the binary number 001010111110110010 or 0010 1011 1110 1100 10 in our more readable format.

# Octal to Hexadecimal Conversion

This is intermediate conversion. The following steps are to be followed to implement the octal to hexadecimal conversion.
Step 1: Convert octal to binary or decimal number.
Step 2: Convert decimal/binary to hexadecimal number.

# Example

Convert (53.7)₈ into equivalent hexadecimal number system.

# Solution

The first step to convert the 537 into equivalent binary form which is as follows:

5　|　3.　|　7₈
101　|　011　|　111₂

Now group the binary digits into groups of four and add zeros where needed to complete groups; then convert the binary to hexadecimal.

0010　|　1011.　|　1110₂
　2　|　B　|　E₁₆

So the solution of: 53.7₈ equal 2B.E₁₆

# HEXADECIMAL NUMBER SYSTEM

Just like the octal number system, the hexadecimal (or base-sixteen) number system provides a convenient way to express binary numbers. The following table shows the weighting for the hexadecimal number system up to 3 decimal places before and 2 places after the hexadecimal point. Based on the