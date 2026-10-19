
variables as doubles and not as floats. While Python eliminates single-precision floats, it adds a new data type complex for dealing with complex numbers. Complex numbers are stored as pairs of doubles and are quite useful in science.

The details of how closely Python adheres to the IEEE 754 standard depend upon the details of Python’s use of the C or Java language to power the Python interpreter. In particular, with the recent 64 bits architectures for CPUs, the range may even be greater than the IEEE standard, and the abnormal numbers (±INF, NaN) may differ. Likewise, the exact conditions for overflows and underflows may also differ. That being the case, the exploratory exercises to follow become all that more interesting because we cannot say that we know what results you should obtain!

## 2.4.3

## Over and Underflow Exercises

- 1. Consider the 32-bit single-precision floating-point number A:

|  | s | e | f |
|---|---|---|---|
| Bit position | 31 | 30 23 | 22 0 |
| Value | 0 | 0000 1110 | 1010 0000 0000 0000 0000 000 |

- a) What are the (binary) values for the sign s, the exponent e, and the fractional mantissa f? (Hint: e10 = 14.)
- b) Determine decimal values for the biased exponent e and the true exponent p.
- c) Show that the mantissa of A equals 1.625 000.
- d) Determine the full value of A.

- 2. Write a program that determines the underflow and overflow limits (within a factor of 2) for Python on your computer. Here is a sample pseudocode

```
under = 1.
over = 1.
begin do N times
    under = under/2.
    over = over * 2.
    write out: loop number, under, over
end do
```

You may need to increase N if your initial choice does not lead to underflow and overflow. (Notice that if you want to be more precise regarding the limits of your computer, you may want to multiply and divide by a number smaller than 2.)

- a) Check where under- and overflow occur for double-precision floating-point numbers (floats). Give your answer in decimal.
- b) Check where under- and overflow occur for double-precision floating-point numbers.
- c) Check where under- and overflow occur for integers. Note: There is no exponent stored for integers, so the smallest integer corresponds to the most

negative one. To determine the largest and smallest integers, you must observe your program's output as you explicitly pass through the limits. You accomplish this by continually adding and subtracting 1. (Because integer arithmetic uses two's complement arithmetic, you should expect some surprises.)

## 2.4.4

## Machine Precision (Model)

A major concern of computational scientists is that the floating-point representation used to store numbers is of limited precision. As we have shown for a 32-bit-word machine, single-precision numbers are good to 6–7 decimal places, while doubles are good to 15–16 places. To see how limited precision affects calculations, consider the simple computer addition of two single-precision numbers:

7 + 1.0 × 10⁻⁷ = ?
(2.19)

The computer fetches these numbers from memory and stores the bit patterns

7 = 0 1000 0010 1110 0000 0000 0000 0000 000 ,
(2.20)

10⁻⁷ = 0 0110 0000 1101 0110 1011 1111 1001 010 ,
(2.21)

in working registers (pieces of fast-responding memory). Because the exponents are different, it would be incorrect to add the mantissas, and so the exponent of the smaller number is made larger while progressively decreasing the mantissa by shifting bits to the right (inserting zeros) until both numbers have the same exponent:

10⁻⁷ = 0 01100001 0110 1011 0101 1111 1100 101 (0)
= 0 0110 0010 0011 0101 1010 1111 1110 010 (10)
...
(2.22)
= 0 1000 0010 0000 0000 0000 0000 0000 000 (0001 101 ... 0)
⇒ 7 + 1.0 × 10⁻⁷ = 7 .
(2.23)

Because there is no room left to store the last digits, they are lost, and after all this hard work the addition just gives 7 as the answer (truncation error in Figure 2.3). In other words, because a 32-bit computer stores only 6 or 7 decimal places, it effectively ignores any changes beyond the sixth decimal place.

The preceding loss of precision is categorized by defining the machine precision εₘ as the maximum positive number that, on the computer, can be added to the number stored as 1 without changing that stored 1:

1_c + ε_m ≜ 1_c ,
(2.24)

where the subscript c is a reminder that this is a computer representation of 1. Consequently, an arbitrary number x can be thought of as related to its floating-point representation x_c by

x_c = x(1 ± ε),   |ε| ≤ ε_m , (2.25)

where the actual value for ε is not known. In other words, except for powers of 2 that are represented exactly, we should assume that all single-precision numbers contain an error in the sixth decimal place and that all doubles have an error in the 15th place. And as is always the case with errors, we must assume that we really do not know what the error is, for if we knew, then we would eliminate it! Consequently, the arguments we are about to put forth regarding errors should be considered approximate, but that is to be expected for unknown errors.

## 2.4.5

## Experiment: Your Machine's Precision

Write a program to determine the machine precision ε_m of your computer system within a factor of 2. A sample pseudocode is

```
eps = 1.
begin do N times
    eps = eps/2.                # Make smaller
    one = 1. + eps              # Write loop number, one, eps
end do
```

A Python implementation is given in Listing 2.4, while a more precise one is ByteLimit.py on the instructor's guide.

## Listing 2.4 Limits.py determines machine precision within a factor of 2.

```
# Limits.py: determines approximate machine precision

N = 10
eps = 1.0

for i in range(N):
    eps = eps/2
    one_Plus_eps = 1.0 + eps
    print('eps = ', eps, ', one + eps = ', one_Plus_eps)
```

- 1. Determine experimentally the precision of double-precision floats.
- 2. Determine experimentally the precision of complex numbers.

To print out a number in the decimal format, the computer must convert from its internal binary representation. This not only takes time, but unless the number is an exact power of 2, leads to a loss of precision. So if you want a truly precise indication of the stored numbers, you should avoid conversion to decimals and instead print them out in octal or hexadecimal format (\0NNN).

## 2.5 Problem: Summing Series

A classic numerical problem is the summation of a series to evaluate a function. As an example, consider the infinite series for sin x:

```
sin x = x - x^3/3! + x^5/5! - x^7/7! + ⋯ (exact).
```

Your problem is to use just this series to calculate sin x for x < 2π and x > 2π, with an absolute error in each case of less than 1 part in 10^8. While an infinite series is exact in a mathematical sense, it is not a good algorithm because errors tend to accumulate and because we must stop summing at some point. An algorithm would be the finite sum sin x ≈ ∑_{n=1}^N (-1)^{n-1} x^{2n-1} / (2n-1)! (algorithm).

But how do we decide when to stop summing? (Do not even think of saying, "When the answer agrees with a table or with the built-in library function.") One approach would be to stop summing when the next term is smaller than the precision desired. Clearly then, if x is large, this would require large N as well. In fact, for really large x, one would have to go far out in the series before the terms start decreasing.

Never mind that the algorithm (2.27) indicates that we should calculate (-1)^{n-1}x^{2n-1} and then divide it by (2n-1)! This is not a good way to compute. On the one hand, both (2n-1)! and x^{2n-1} can get very large and cause overflows, despite the fact that their quotient may not be large. On the other hand, powers and factorials are very expensive (time-consuming) to evaluate on the computer. Consequently, a better approach is to use a single multiplication to relate the next term in the series to the previous one:

```
(-1)^{n-1} x^{2n-1} / (2n-1)! = -x^2 / ((2n-1)(2n-2)) * (-1)^{n-2} x^{2n-3} / (2n-3)! 
⇒ nth term = -x^2 / ((2n-1)(2n-2)) × (n-1)th term. (2.28)
```

While we want to establish absolute accuracy for sin x, that is not so easy to do. What is easy to do is to assume that the error in the summation is approximately the last term summed (this assumes no round-off error, a subject we talk about in Chapter 3). To obtain a relative error of 1 part in 10^8, we then stop the calculation when |nth term / sum| < 10^{-8}, (2.29)
