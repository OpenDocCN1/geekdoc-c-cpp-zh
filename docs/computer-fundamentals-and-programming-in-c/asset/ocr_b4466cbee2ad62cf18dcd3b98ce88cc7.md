|  | In groups of 3 bits |
|---|---|
| 1 | 001 |
| 2 | 010 |
| 4 | 111 |
| 7 | 111 |
| 3 | 011 |
| 2 | 010 |
| 4 | 100 |
| 4 | 100 |

The binary number is regrouped as four-bit binary numbers that are replaced with hexadecimal symbols.

| In groups of 4 bits | Equivalent hexadecimal |
|---|---|
| 0010 | 2 |
| 1011 | B |
| 1111 | F |
| 0110 | 6 |
| 1010 | A |
| 0100 | 4 |

Therefore, we see that 127324₈ = 2BF6A₁₆.

However, there are easier conversion methods. Some ways to perform conversion between the bases are as follows.

**Any base to decimal** — Use expanded notation. Write down each digit as a product of a power of the base and add them all.

**Decimal to any base** — Use the division method. Divide the decimal number repeatedly with the base, writing down the remainder at each step. When the quotient becomes zero, the string of remainders is the number in the new base.

**Octal to hexadecimal or vice versa** — Use binary as an intermediate form.

# 2.5.2 Working with Fractional Numbers

One is familiar with the decimal (base-10) number system. Each digit within any given decimal number is associated with a weight. Furthermore, the value of that number is the sum of the digits after each has been multiplied by its weight. To illustrate, let us consider Table 2.5 and assume that the number 654.52, written as (654.52)₁₀ to specify base-10, is being represented. Note that the digits range from 0 to 9.

Table 2.5  Decimal number system

|  | Hundreds | Tens | Units | One-tenth | One-hundredth |  |
|---|---:|---:|---:|---:|---:|---:|
| Weights | 10² | 10¹ | 10⁰ | 10⁻¹ | 10⁻² |  |
| Symbols | 6 | 5 | 4 | 5 | 2 |  |
| Weighted value | 600 | 50 | 4 | 0.5 | 0.02 | Total 654.52 |

Just as the decimal system with its ten digits is a base-10 system, the binary number system with its two digits, 0 and 1, is a base-2 system. Table 2.6 shows the weighting for the binary number system up to two decimal places after and three places before the binary point (.). Note the similarity with the decimal system.

Table 2.6  Binary weights

| Weights | 2² | 2¹ | 2⁰ | 2⁻¹ | 2⁻² |

The least significant bit (LSB) is the rightmost binary digit, which has the lowest binary weight of a given number. The most significant bit (MSB) is the leftmost binary digit, which has the highest binary weight of a given number.

Counting in binary is similar to the decimal number system. The LSB begins with zero (0) and is incremented until the maximum digit value is reached. The adjacent bit positions are then filled appropriately as the iterative counting process continues.

# Note

+   - For conversion from any number base system to decimal use expanded notation.
+   - For conversion from decimal number system to any base use the division method.
+   - While converting octal number to hexadecimal number or vice versa use binary as an intermediate form.
+   - It is important to note that many decimal fractions do not have an exact representation in binary.

# Conversion from decimal fractions to binary

When converting a fractional decimal value to binary, a slightly different approach is needed. Instead of dividing by 2, the decimal fraction is multiplied by 2. If the result is greater than or equal to 1, then 1 is to be put as the quotient. If the result is less than 1, then 0 is put as the quotient.

EXAMPLE

Converting (0.375)₁₀ to binary.

0.375 × 2 = 0.750  0
0.750 × 2 = 1.500  1
0.500 × 2 = 1.000  1
done.

Note that the last operation is complete when the fraction part equals zero. It is rarely possible to accurately represent a fractional value in binary. The answer to this problem is: .011

It is important to note that many decimal fractions do not have an exact representation in binary. This is illustrated in the following example.