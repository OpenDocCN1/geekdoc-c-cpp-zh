# 20 1 Introduction

The specific format of floating-point number varies among different computers. Suppose we have a 16-bit machine; then a binary number may have 4 bits for its exponent and 12 bits for its mantissa.

| 15 14 exponent | 12 11 10 mantissa | 0 |
| --- | --- | --- |
| sign sign | decimal point |

Here is a practical example, where the exponent and the mantissa are represented by complement code and true code respectively.

| 0 0 1 0 | 110.......0 | represents $(-0.11 \times 10^{10})_2 |
| 1 1 0 1 | 110.......0 | represents (0.11 \times 10^{-11})_2 |

# 1.4.6 The Number Range that can be Represented

The number range can be represented in a computer depends on the data bits and the representation used. An $M$ bit integer (including the sign bit) can be as large as $2^{M-1}-1$ and as small as $(-2^{M-1}-1)$ when represented by complement code or true code; if it can range from $-2^{M-1}$ to $2^{M-1}-1$.

One thing mentioned is that the representation of 0 by complement code is unique, so $[X]_{complement} = 100\dots0$ corresponds to the original value of $-2^{M-1}$ (note that the complement code 0 is a special case, the value 1 on the bit that has weight $2^{M-1}$ represents both sign and value). Here we do not prove the number range that complement code can represent, but you can prove it if interested.

For example, $M=8$, the number range that true code can represent is $-127 \sim +127$. The range in complement-code is $-128 \sim +127$. For an $n$-bit fixed point decimal, the bit to the left of the decimal point is the sign. The number range that true code or complement code represents is $(-1-2^{-n}) \sim (1-2^{-n})$, while for complement code is $-1 \sim (1-2^{-n})$.

The range of a floating-point number that can be represented on the number of bits in the exponent and mantissa.

Suppose the exponent is an $R$-bit integer (represented by complement code), and the mantissa is an $n$-bit fixed point decimal (represented by true code); the range of floating-point number is:

```
$-(1-2^{-n}) \times 2^{(2^{R-1}-1)} \sim +(1-2^{-n}) \times 2^{(2^{R-1}-1)}$
```

If we want to enlarge the number range that can be represented, we should increase the number of bits in the exponent. Each 1-bit increase in the exponent will double the number range. If we want to increase the precision, we should increase the number of