Examples:

`EXP[-2]`    (Returns 0.1353353)
`EXP[0]`     (Returns 1.000)
`EXP[2]`     (Returns 7.3890561)
`EXP[110.25]` (Overflow error)

# Arbitrary Exponent of a Number

No standard function is available to evaluate an expression in the form x^x. It can, however, be calculated in an indirect manner, using the formula

x^x = e^(x ln x), that is, EXP[y = LN[x]]

Examples:

`EXP[4 * LN[3]]`  (Equivalent to 3^4, which returns 81.000)
`EXP[4 * LN[10]]` (Equivalent to 10^4, which returns 10000.000)

# 4.6  Logical Functions

The available logical functions are AND, OR, and XOR. These can be used in two different manners, as

+   - Bitwise functions
+   - Boolean functions

# Bitwise Functions

When used as bitwise functions, all the corresponding bits of the binary representations of the two numbers (on which these function are operated) are individually compared, and the resulting answer in the binary format is converted back to the decimal format. Table 4.1 is the truth table for the three functions. Bit-1 and bit-2 are the corresponding bits of the two numbers.

Figure 4.2 gives the Venn diagram representations of these functions. In this figure, the circular area corresponding to a bit represents a binary value of 1, and the area lying outside the circle represents binary value 0. The shaded area represents the result (binary value 1) of the specified logical operation. This figure also indicates that all the

| Bit-1 | Bit-2 | AND | OR | XOR |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

**TABLE 4.1**  Truth Table for Bitwise AND, OR, and XOR