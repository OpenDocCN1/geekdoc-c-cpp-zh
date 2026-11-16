
![](img/f0b8aa873b11dc585ed698a10d04e7a7_63_0.png)

FIGURE 3-6 Using integer multiplication to produce a fixed-point product.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_63_1.png)

FIGURE 3-7 Using integer division to produce a fixed-point quotient.

Again, what is needed is a result with a scale factor of 2^16 (not 2^0)! Rather than shifting the quotient left by 16 bits, however, it is better to left-shift the dividend because division with a 64-bit dividend and a 32-bit divisor produces a 32-bit quotient. Given the extra dividend bits, it is better to pre-shift the sign-extended dividend left by 16 bits, as shown in Figure 3-7.

Fixed-point multiplication and division are typically implemented as functions written in assembly language, to take advantage of the double-length products and dividends available with the integer instruction set of most processors. This makes implementation of multiplication and division of fixed-point numbers in 16.16 format rather straightforward in assembler and on a 32-bit processor. Implementation in a high-level language (such as C), however, is problematic, because a single data type (and thus word size) is used for both the operands and the result.

## 3.3.2 Fixed-Point Using a Universal 32.32 Format

The range of the 16.16 format is limited to approximately ±32767 with a precision of about five decimal digits to the right of the radix point. When memory space is not an issue, a significant improvement in range and precision can be obtained by using 64 bits for all fixed-point numbers, with 32 bits in both the whole and the fractional parts (Figure 3-8).5

## 3.3.3 Multiplication of 32.32 Fixed-Point Reals

By now, you can guess that the 32.32 format would be most easily implemented on a 64-bit processor. Unfortunately, 64-bit processors are generally considered too expensive for almost all embedded applications. As an example of how 32.32 fixed-point arithmetic can be implemented on a 32-bit processor, let us consider multiplication. Since multiplication is such a fundamental operation, our objective will be to maximize performance by devising an algorithm that can be coded in assembler, using regular 32-bit integer operations, and without using any loops or branching.

Our strategy will be to consider first how to compute the 128-bit product of two 64-bit unsigned integers and then to modify that result to handle signed integers. Next, we use our 32.32 scaling to select which 64 bits of the 128-bit product to keep, and note how discarding the rest simplifies the computation.

Consider a 64-bit integer A, with the bits numbered in little endian format (A63A62...A0). The unsigned value of A can be expressed, via polynomial evaluation, as:

```
A_u = 2^63 A_63 + 2^62 A_62 + ... + 2^0 A_0
```

Separating the first term from the rest, we have

```
A_u = 2^63 A_63 + (2^62 A_62 + ... + 2^0 A_0)
= 2^63 A_63 + A_62..0 (where A_62..0 = 2^62 A_62 + ... + 2^0 A_0)
```

Thus, the 128-bit product of two 64-bit unsigned integers is

```
A_u B_u = (2^63 A_63 + A_62..0) x (2^63 B_63 + B_62..0)
= 2^126 A_63 B_63 + 2^63 A_63 B_62..0 + 2^63 B_63 A_62..0 + A_62..0 B_62..0
```

5 This approach was used in the Sony PlayStation, whose MIPS processor has no floating-point unit.

Now, consider what happens when the bits are interpreted as a 64-bit signed integer. First, note that the signed value of A can be expressed as

$A_s = -2^{63} A_{63} + (2^{62} A_{62} + \cdots + 2^0 A_0) = -2^{63} A_{63} + A_{62..0}$

Thus, the 128-bit product of two 64-bit signed integers is

$A_s B_s = (-2^{63} A_{63} + A_{62..0}) \times (-2^{63} B_{63} + B_{62..0}) = 2^{126} A_{63} B_{63} - 2^{63} (A_{63} B_{62..0} + B_{63} A_{62..0}) + A_{62..0} B_{62..0}$

This differs from $A_u B_u$ only in the sign of the middle term, so we can simply compute $A_s B_s$ as:

$A_s B_s = A_u B_u - 2 \times 2^{63} (A_{63} B_{62..0} + B_{63} A_{62..0}) = A_u B_u - 2^{64} A_{63} B_{62..0} - 2^{64} B_{63} A_{62..0}$

Graphically, the product $A_s B_s$ is computed as shown in Figure 3-9.

Remember that the 0's shown in the most significant bits of the last two partial products in Figure 3-9 occur because $A_{62..0}$ and $B_{62..0}$ are 63-bit (not 64-bit) unsigned values.

A and B hold fixed-point real numbers in a 32.32 format; given that $A_s B_s$ is to be stored in the same format, then we must discard 32 bits from both ends of the partial products, to preserve the proper 32.32 scaling, as is shown in Figure 3-10.

Computing the middle 64 bits of the product $A_u B_u$ (the first of the three terms shown above) using integer multiplication on a 32-bit processor is accomplished by breaking each 64-bit operand into two 32-bit halves (i.e., $A_u = 2^{32} A_{hi} + A_{lo}$ and $B_u = 2^{32} B_{hi} + B_{lo}$) and then combining the cross-products:

$A_u B_u = (2^{32} A_{hi} + A_{lo}) \times (2^{32} B_{hi} + B_{lo}) = 2^{64} A_{hi} B_{hi} + 2^{32} (A_{hi} B_{lo} + A_{lo} B_{hi}) + A_{lo} B_{lo}$

![](img/f0b8aa873b11dc585ed698a10d04e7a7_65_0.png)

FIGURE 3-9 Computing a signed fixed-point product from an unsigned product.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_66_0.png)

FIGURE 3-10 Converting from 64.64 to 32.32 fixed-point format.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_66_1.png)

FIGURE 3-11 Computing the 32.32 unsigned fixed-point product.

We are going to keep only the middle 64 bits, so we can discard the 32-bit upper half of A_hi B_hi and the 32-bit lower half of A_lo B_lo as shown in Figure 3-11.

All that remains (to compute the signed product A_s B_s) is to conditionally subtract the lower halves of A_62..0 and B_62..0 from the upper half of the unsigned product A_u B_u (see Figure 3-11). Note that the only difference between A and A_62..0 and between B and B_62..0 is the most significant bit position; this is irrelevant since we used only their lower halves in the subtractions. Thus, to convert the unsigned product into a signed product, simply subtract the lower half of B from the upper half of the unsigned product A_u B_u if A is negative (A_63 = 1) and subtract the lower half of A if B is negative (B_63 = 1).6

6 Note that changing the unsigned product to a signed product by adjusting the upper half is related to the earlier discussion about the difference between signed and unsigned multiplication.

## 3.3.4 Example: Multiplying Two 4.4 Fixed-Point Reals

To illustrate the total algorithm, consider the problem of multiplying two numbers A and B, each represented as a 2's-complement 4.4 fixed-point real. To simplify the example, let us assume that this is to be implemented on a 4-bit microprocessor whose unsigned multiply instruction produces an 8-bit product from two 4-bit operands.

Let A = -1.50₁₀ = 1110.1000₂ Note: As an unsigned integer, Aᵤ = 11101000₂ = 232₁₀

Let B = +2.75₁₀ = 0010.1100₂ Note: As an unsigned integer, Bᵤ = 00101100₂ = 44₁₀

The 16-bit product AᵤBᵤ should be 232 x 44 = 10208₁₀. The following expression shows how it would be calculated on a 4-bit CPU:

AᵤBᵤ = 2⁸AₕBₕ + 2⁴(AₕBₗ + AₗBₕ) + AₗBₗ
= 2⁸(1100 x 0010) + 2⁴((1100 x 1100 + 1000 x 0010) + (1000 x 1100)
= 2⁸(00011000) + 2⁴(10101000 + 00010000) + 01100000

The powers of 2 simply determine how the various 8-bit partial products should be aligned:

![](img/f0b8aa873b11dc585ed698a10d04e7a7_67_0.png)

Remember that of this, we really only need the middle 8 bits (01111110). All that is left is to conditionally subtract the lower halves of A and B, depending (respectively) on the signs of B and A. Since only A is negative, we simply subtract the lower half of B from the upper half of the 8-bits calculated above:

![](img/f0b8aa873b11dc585ed698a10d04e7a7_67_1.png)

Inserting the binary point and converting to decimal to check, we get:

1011.1110₂ = -0100.0010₂ = -4.125₁₀ (which is correct!)

With a little ingenuity, this algorithm for multiplication of two signed 32.32 fixed-point real numbers can be implemented as straight-line code (without any loops or branching). Unfortunately, the algorithm for signed division is much more difficult. In practice, however, most divisions use a constant divisor, and so may be rewritten as an equivalent multiplication by the inverse of the constant. True division of fixed-point reals is only required when the divisor is a variable.
