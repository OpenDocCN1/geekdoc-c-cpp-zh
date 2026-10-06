As mentioned before, data information in computers is represented in binary code.
Since a number can be positive or negative, how does one signify the sign of a number in computers? Generally, the leftmost bit of the number indicates the sign of the value represented, where "0" indicates the positive sign and "1" indicates the negative sign.
For example:
An 8-bit number $A = (+1011011)$ and $B = (-1011011)$ can be represented in a computer as:

| A | 0 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |
| B | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |

The leftmost bit is the sign; it forms the number together with the rest of the bits.
Once the data information has been digitized, it can be recognized and represented by a computer. In order to simplify the computation of signed numbers and make ALU simpler, people have invented binary-coding methods, whose substantial difference lies in the coding methods of **negative numbers**.
Now we will introduce some common coding methods: true code, ones-complement code, and complement code.

#  1. True Code

True code makes the separate bit 0 or 1 and combines the absolute value of the number with the other bits to achieve the coding. It is also called "sign-absolute value represented" coding.
Firstly we will show how to represent a signed integer in true code:
Suppose we use one bit in memory to store an integer, and its true code is this:

```
$X = +1011011 \quad [X]_{true} = 00101011$
$X = -1011011 \quad [X]_{true} = 10101011$
```

Here $[X]_{true}$ are the machine number, and $X$ is called its true value.
For decimal fraction, the sign bit in true code is the one to the left of the decimal point. For example:

```
$X = 0.10111 \quad [X]_{true} = 0.10111$
$X = -0.10111 \quad [X]_{true} = 1.10111$
```

True code is simple and intuitive, and the conversion between it and its true value is convenient. However, true code has several shortcomings:
Firstly, the true code representation for 0 is not unique, since:

```
$+[0]_{true} = 000 \dots 0 \quad -[0]_{true} = 100 \dots 0$
```

The ambiguity of 0 can cause trouble when computer makes verdicts on 0.
Secondly, when we use true code to do arithmetic operations, the sign bit should be handled independently and the operation rule is complicated. Take addition as an