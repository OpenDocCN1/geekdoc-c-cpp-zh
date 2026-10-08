
MUL    A, B, R1        ;       R1 ← A * B
MUL    C, D, R2        ;       R2 ← C * D
MUL    E, F, R3        ;       R3 ← E * F
ADD    R1, R2, R1      ;       R1 ← R1 + R2
SUB    R1, R3, Z       ;       Z ← R1 - R3

This sequence implements the statement Z = A * B + C * D - E * F. The three-address format, in addition to the other formats, is normally used by typical microcontrollers such as the PIC18F.

If we drop the third address from the three-address format, we obtain the two-address format, whose general form is
<op-code> Addr1, Addr2
Some typical two-address instructions are

MOV    A, R1           ;       R1 ← A
ADD    C, R2           ;       R2 ← R2 + C
SUB    R1, R2          ;       R2 ← R2 - R1

In this format, the addresses Addr1 and Addr2 represent source and destination addresses, respectively.

The following sequence of two-address instructions is equivalent to the program using three-address format presented earlier:

MOV    A, R1           ;       R1 ← A
MUL    B, R1           ;       R1 ← R1 * B
MOV    C, R2           ;       R2 ← C
MUL    D, R2           ;       R2 ← R2 * D
MOV    E, R3           ;       R3 ← E
MUL    F, R3           ;       R3 ← R3 * F
ADD    R2, R1          ;       R1 ← R1 + R2
SUB    R3, R1          ;       R1 ← R1 - R3
MOV    R1, Z           ;       Z ← R1

Some typical one-address instructions are

LDA    B               ;       Acc ← B
ADD    C               ;       Acc ← Acc + C
MUL    D               ;       Acc ← Acc * D
STA    E               ;       E   ← Acc

Note that Acc means the accumulator.
The following program illustrates how we can translate the C language statement, z = (a * b) + (c * d) - (e * f);, into a sequence of one-address instructions:

lda    e               ;       Acc ← e
mul    f               ;       Acc ← e * f
sta    t1              ;       t1 ← Acc
lda    c               ;       Acc ← c
mul    d               ;       Acc ← c * d
sta    t2              ;       t2 ← Acc
lda    a               ;       Acc ← a
mul    b               ;       Acc ← a * b
add    t2              ;       Acc ← Acc + t2
sub    t1              ;       Acc ← Acc - t1
sta    z               ;       Z ← Acc

In this program, t1 and t2 represent the addresses of memory locations used to store temporary results. Instructions that do not require any addresses are called zero-address instructions. All microcontrollers include some zero-address instructions in the instruction set. Typical examples of zero-address instructions are CLC (clear carry) and NOP (No operation).

## 4.3.6 Typical Instruction Set

An instruction set of a specific microcontroller consists of all the instructions that it can execute. The capabilities of a microcontroller are determined to some extent by the types of instructions it is able to perform. Each microcontroller has a unique instruction set designed by its manufacturer to do a specific task. We discuss some of the instructions that are common to all microcontrollers. We group together chunks of these instructions which have similar functions. These instructions typically include:

- Arithmetic Instructions: Typical arithmetic instructions include ADD, SUBTRACT, COMPARE, MULTIPLY, and DIVIDE. Note that the SUBTRACT instruction provides the result and also affects the status flags, whereas the COMPARE instruction performs subtraction without any result and affects the flags based on the result.

Typical microcontrollers utilize common hardware to perform addition and subtraction operations for both unsigned and signed numbers. The instruction set for a microprocessor typically includes the same ADD and SUBTRACT instructions for both unsigned and signed numbers. The interpretations of unsigned and signed ADD and SUBTRACT operations are performed by the programmer. For example, consider adding two 8-bit numbers, A and B (A = FF₁₆ and B = FF₁₆), using the ADD instruction by a microprocessor as follows:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_79_0.png)

When the addition above is interpreted by the programmer as an unsigned operation, the result will be A + B = FF₁₆ + FF₁₆ = 255₁₀ + 255₁₀ = 510₁₀ which is FE₁₆ with a carry, as shown above. However, if the addition is interpreted as a signed operation, then A + B = FF₁₆ + FF₁₆ = (-1₁₀) + (-1₁₀) = -2₁₀ which is FE₁₆ as shown above, and the final carry must be discarded by the programmer. Similarly, the unsigned and signed subtraction can be interpreted by the programmer.

The unsigned and signed multiplication and division algorithms will be discussed in the following.

### Unsigned Multiplication

Several unsigned multiplication algorithms are available. Multiplication of two unsigned numbers can be accomplished via repeated addition. For example, to multiply 4₁₀ by 3₁₀, the number 4₁₀ can be added twice to itself to obtain the result, 12₁₀.

### Signed Multiplication

Signed multiplication can be performed using various algorithms. A simple algorithm follows. Assume that M (multiplicand) and Q (multiplier) are in two's-complement form. Assume that Mₙ and Qₙ are the most significant bits (sign bits) of the multiplicand (M) and the multiplier (Q), respectively. The sign bit of the product is determined as Mₙ ⊕ Qₙ, where Mₙ and Qₙ are the most significant bits (sign bits) of the multiplicand (M) and the multiplier (Q), respectively. To perform signed multiplication, proceed as follows:

1. If $M_n = 1$, compute the two's complement of $M$.
2. If $Q_n = 1$, compute the two's complement of $Q$.
3. Multiply the $n - 1$ bits of the multiplier and the multiplicand using unsigned multiplication.
4. The sign of the result, $S_n = M_n \oplus Q_n$.
5. If $S_n = 1$, compute the two's-complement of the result obtained in step 3.

Next, consider a numerical example. Assume that $M$ and $Q$ are two's-complement numbers. Suppose that $M = 1100_2$ and $Q = 011_2$. Because $M_n = 1$, take the two's-complement of $M$ to be $0100_2$; because $Q_n = 0$, do not change $Q$. Multiply $011_2$ and $0100_2$ using the unsigned multiplication method discussed before. The product is $00011100_2$. The sign of the product $S_n = M_n \oplus Q_n = 1 \oplus 0 = 1$. Hence, take the two's-complement of the product $00011100_2$ to obtain $11100100_2$, which is the final answer: $-28_{10}$.

### Unsigned Division

Unsigned division can be accomplished via repeated subtraction. For example, consider dividing $7_{10}$ by $3_{10}$ as follows:

| Dividend | Divisor | Subtraction Result | Counter |
| :---: | :---: | :---: | :---: |
| $7_{10}$ | $3_{10}$ | $7 - 3 = 4$ | 1 |
| | | $4 - 3 = 1$ | $1 + 1 = 2$ |

Quotient = counter value = 2
Remainder = subtraction result = 1

Here, 1 is added to a counter whenever the subtraction result is greater than the divisor. The result is obtained as soon as the subtraction result is smaller than the divisor.

### Signed Division

Signed division can be performed using various algorithms. A simple algorithm follows. Assume that DV (Dividend) and DR (Divisor) are in two's-complement form. For the first case, perform unsigned division using repeated subtraction of the magnitudes without the sign bits. The sign bit of the quotient is determined as $DV_n \oplus DR_n$ where $DV_n$ and $DR_n$ are the most significant bits (sign bits) of the dividend (DV) and the divisor (DR) respectively. To perform signed division, proceed as follows:

1. If $DV_n = 1$, compute the two's complement of DV, else keep DV unchanged.
2. If $DR_n = 1$, compute the two's complement of DR, else keep DR unchanged.
3. Divide the $n - 1$ bits of the dividend by the divisor using unsigned division algorithm (repeated subtraction).
4. The sign of the Quotient $Q_s = DV_n \oplus DR_n$. The sign of the remainder is the same as the sign of the dividend unless the remainder is zero. The following numerical examples illustrate this:

The general equation for division can be used for signed division. Note that the general equation for division is $dividend = quotient * divisor + remainder$. For example, consider dividend = -9, divisor = 2. Three possible solutions are shown below:

- (a) -9 = -4 * 2 - 1, Quotient = -4, Remainder = -1.
- (b) -9 = -5 * 2 + 1, Quotient = -5, Remainder = +1.
- (c) -9 = -6 * 2 + 3, Quotient = -6, Remainder = +3.

However, the correct answer is shown in (a), in which the Quotient = -4 and the remainder = -1. Hence, for signed division, the sign of the remainder is the same as the sign of the dividend, unless the remainder is zero.

5. If $Q_n = 1$, compute the two's-complement of the quotient obtained in step 3, else keep the quotient unchanged.
