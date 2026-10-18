
## 7.1.6 Representing Fractions

Figure 7.1 showed a byte structure. As indicated, by associating a weight \(w_i = 2^i\) with each \(i\)th bit position, we can precisely represent integer values in the range [0...255]. However, assigning different weights lets us represent a different range of values. For example, if fractional weights are assumed, then fractions can be represented, as shown in Figure 7.2.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_509_0.png)

**Figure 7.2** Fractional value representation of a byte by assigning weights \(w_i\) as consecutive values of \(2^{-i}\). Unlike integer values, not all decimal fractions can be precisely represented.

More precisely, changing the weight definition \(w_i\) in Eq. (7.3) for \(B = 2\) as follows

\[
w_i = 2^{-(i+1)}
\tag{7.12}
\]

and inserting it into Eq. (7.2) yields

\[
D_{FB} = \sum_{i=0}^{N-1} b_i 2^{-(i+1)}
\tag{7.13}
\]

where FB stands for fraction-binary. Comparing Figure 7.1 with Figure 7.2, notice that bit numbering is symmetrical. In this assumption, the MSB for the integer part corresponds to \(i = N - 1\), whereas for the fraction, the MSB is placed at \(i = 0\). Note also that in both representations, there is a fixed number of digits for an integer, as well as fractional parts. Therefore these are *fixed-point* (FX) representations, as opposed to *floating-point* (FP) representations, which will be discussed in Section 7.4.

For example, let’s consider the following bit assignment, which served as an example at the beginning of Section 7.1:

| \(b_0\) | \(b_1\) | \(b_2\) | \(b_3\) | \(b_4\) | \(b_5\) | \(b_6\) | \(b_7\) |
|---|---|---|---|---|---|---|---|
| 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 |

For an integer representation, we used Eq. (7.1). But to compute a fraction, we need to use Eq. (7.13) instead, as follows:

\[
D = 2^{-1}\cdot 0 + 2^{-2}\cdot 1 + 2^{-3}\cdot 0 + 2^{-4}\cdot 1 + 2^{-5}\cdot 0 + 2^{-6}\cdot 1 + 2^{-7}\cdot 1 + 2^{-8}\cdot 1
\]

\[
= 2^{-2} + 2^{-4} + 2^{-6} + 2^{-7} + 2^{-8} = 0.33984375
\]

In other words, we can write that \(01010111_2 = 0.33984375_{10}\).

We see that the same bit assignments do lead to different values. They depend on the weight definitions. Recall that in the integer representation, the LSB value was 1, so all intermediate values could be precisely represented. But in the case of a fraction, the LSB value is \(2^{-8} = 0.00390625\), and we can operate in multiples of it. When we divide the value of our example number by the LSB, we get the following:

\[
0.33984375 / 0.00390625 = 87
\]

Is this a surprise? Not necessarily, if we recall that the integer value of the same bit representation is exactly 87. In other words, a fractional representation means *rescaling* an integer value by the fractional value of the LSB. Formally, a given integer binary value \(D_{IB}\) from Eq. (7.5) can be rescaled to a new value as follows:

\[
\hat{D} = s \cdot D_{IB} + f
\tag{7.14}
\]

where \(s\) denotes scaling and \(f\) is an offset value. In our example, we had \(D_{IB} = 87\), \(s = 2^{-8}\), and \(f = 0\). This also means the same C2 encoding can be used to represent a negative fractional value, as discussed in Section 7.1.4.

An important question is how precise the representation in Eq. (7.13) is for real fractions. Notice that the precision \(P\) is related to the lowest possible value that can be represented in the LSB:

\[
P = B^{-N} = 2^{-N}
\tag{7.15}
\]

For a byte, \(P = 2^{-8} = 0.00390625\). This means all values less than that will be represented as 0—i.e. they will be disregarded. On the other hand, the maximum representable value is \(1.0 - P\), which in our case is \(0.99609375\). Moreover, operating in multiples of \(P\) means not all decimal fractions can be precisely represented in a binary form. We will see that even increasing the number of bits only helps somewhat; doing so limits the representation error but in some cases never leads to a fully precise representation. This is an important observation that explains imprecision in computations due to *rounding error*. We discuss rounding methods in the context of floating-point values in Section 7.4.4.

Let’s now devise an algorithm for converting a decimal fraction into the closest binary representation. A value expressed by Eq. (7.13) is less than 1. If it is multiplied by 2, the result is as follows:

\[
2 \cdot D_{FB} = b_0 + \sum_{i=1}^{N-1} b_i 2^{-i}
\tag{7.16}
\]

Notice that when a fraction \(D\) is multiplied by 2, we get two values: an integer 0 or 1 and a fraction less than 1. The former immediately provides the first bit \(b_0\) from the fractional representation. To find consecutive bits, the second term from Eq. (7.16) is multiplied by 2, and the entire procedure repeats. This continues until one of the following conditions is met: either the fraction is exactly 0, or the maximum number of \(N\) bits is reached. However, as we pointed out earlier, for some fractions the bit representation is only an approximation of the real value. Let’s verify this procedure, first in the decimal domain with \(B = 10\) and a value \(D = 0.35\). We get the following series of integers (\(I\)) and fractions (\(F\)):

|   | I | F |
|---|---:|---:|
| 0.35 · 10 | **3** | 0.5 |
| 0.5 · 10 | **5** | 0 |

Reading out the values of \(I\), we immediately obtain 0.35. Let’s now change to the binary base: \(B = 2\), and the same value \(D = 0.35\). For \(N = 8\), we get the following:

| \(i\) |   | \(I\) | \(F\) |
|---:|---|---:|---:|
| 0 | 0.35 · 2 | **0** | 0.7 |
| 1 | 0.7 · 2 | **1** | 0.4 |
| 2 | 0.4 · 2 | **0** | 0.8 |
| 3 | 0.8 · 2 | **1** | 0.6 |
| 4 | 0.6 · 2 | **1** | 0.2 |
| 5 | 0.2 · 2 | **0** | 0.4 |
| 6 | 0.4 · 2 | **0** | 0.8 |
| 7 | 0.8 · 2 | **1** | 0.6 |
| 8 | 0.6 · 2 | **1** | 0.2 |

Knowing the scaling properties from Eq. (7.14), we can obtain the same result as follows:

1. Multiply \(0.35 \cdot 2^8 = 89.6\).
2. Take the integer part of the previous result and convert it into a binary representation: \(89_{dec} = 01011001_{bin}\).

We see that either way, the value \(0.35_{dec} \approx 01011001_{bin}\) is obtained. However, this is only an approximation of 0.35, since the value \(0.6 \cdot 2^{-8} = 0.00234375\) was left out. In other words, a rounding error has been generated:

\[
\Delta_0 = |0.35_{dec} - 01011001_{bin}| = |0.35 - 0.34765625| = 0.00234375
\]

Whether this is an acceptable error depends on the application. But we can do better than this. If we consider the eighth bit of the previous series and add it to the seventh, then \(0.35_{dec} \approx 01011010_{bin}\), with the following error:

\[
\Delta_1 = |0.35_{dec} - 01011010_{bin}| = |0.35 - 0.3515625| = 0.0015625
\]

Notice that \(\Delta_1 < \Delta_0\). So what we did was choose a different rounding algorithm—rounding to the nearest number instead of rounding toward 0. Here we see how important proper rounding is; this will be discussed further in Section 7.4.4. Also, \(\Delta_1 < \frac{1}{2}P = 2^{-9} = 0.001953125\). In an FX representation, the maximum rounding error is fixed to the constant value of \(\pm \frac{1}{2}P\), as shown in Figure 7.3.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_512_0.png)

**Figure 7.3** The maximum rounding error in the fixed-point representation is limited to \(\pm \frac{1}{2}P = 2^{-N-1}\). Real values \(x_1\) and \(x_2\) are represented by the closest fixed-point value. \(\bar{x}_n = D_{FB}(n)\) denotes the \(n\)th fixed-point value, \(0 \le n < 2^N\). Values out of range lead to overflow, which for unsigned numbers results in the value being wrapped around.

### Things to Remember

- Unlike integers, the binary representation of some real fractions cannot be precise. The absolute value of the difference is called rounding error.
- The maximum rounding error in an FX representation with \(N\) fraction bits is \(\pm \frac{1}{2}P = 2^{-N-1}\).
- To convert a decimal fraction into its binary representation, the fraction is multiplied by 2, and the integer part of the result provides a consecutive representation bit. Then the procedure is repeated for the remaining consecutive fractions until \(N\) bits are obtained.

## 7.2 Binary Shift Operations

From daily observations, we know that multiplication and division by 10 are straightforward—we simply shift the decimal point one position to the right or to the left. For example, \(-12.34\), after we shift the decimal point one position to the right, becomes \(-123.4\). Hence, it has been multiplied by 10. On the other hand, when we shift the decimal point one position to the left, the new value is \(-1.234\). In this case, the original value has been divided by 10. Thus a right shift by one digit position multiplies the value by the base, whereas a shift to the left divides it by the base. This is true for any base, including binary.

The rules are simple in principle; but as always, there are further details—for example, after the shift, what value should be placed in the vacant position? For example, if we shift bits to the left, then the vacant rightmost bit can be set to 0. However, what will we do with the leftmost bit if the value is signed? If we throw it away, then it can appear that a negative value becomes a positive one or vice versa. Otherwise, can we do a bit rotation—that is, move the leftmost bit into the rightmost position? There are many options, and the possible rules are summarized in Table 7.3.

Shift operations are very efficient ways to manipulate bits. Frequently, integer multiplication or division by 2 and its multiples is faster when implemented using bit-shift operators than with the corresponding arithmetic multiplication or division.
