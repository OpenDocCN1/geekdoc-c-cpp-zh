
## 12.9
The Fast Fourier Transform Algorithm

We have seen in (12.37) that a discrete Fourier transform can be written in the compact form as

$$Y_n = \frac{1}{\sqrt{2\pi}} \sum_{k=1}^{N} Z^{nk} y_k \;,\quad Z = e^{-2\pi i / N} \;,\quad n = 0,1,\dots,N-1.\tag{12.81}$$

Even if the signal elements $y_k$ to be transformed are real, $Z$ is complex, and therefore we must process both real and imaginary parts when computing transforms. Because both $n$ and $k$ range over $N$ integer values, the $(Z^n)^k y_k$ multiplications in (12.81) require some $N^2$ multiplications and additions of complex numbers. As $N$ gets large, as happens in realistic applications, this geometric increase in the number of steps leads to long computation times.

In 1965, Cooley and Tukey discovered an algorithm⁷ that reduces the number of operations necessary to perform a DFT from $N^2$ to roughly $N \log_2 N$ (Cooley, 1965; Donnelly and Rust, 2005). Although this may not seem like such a big difference, it represents a 100-fold speedup for 1000 data points, which changes a full day of processing into 15 min of work. Because of its widespread use (including cell phones), the fast Fourier transform algorithm is considered one of the 10 most important algorithms of all time.

The idea behind the FFT is to utilize the periodicity inherent in the definition of the DFT (12.81) to reduce the total number of computational steps. Essentially, the algorithm divides the input data into two equal groups and transforms only one group, which requires $\sim (N/2)^2$ multiplications. It then divides the remaining (nontransformed) group of data in half and transforms them, continuing the process until all the data have been transformed. The total number of multiplications required with this approach is approximately $N \log_2 N$.

Specifically, the FFT's time economy arises from the computationally expensive complex factor $Z^{nk} [= (Z^n)^k]$ having values that are repeated as the integers $n$ and $k$ vary sequentially. For instance, for $N = 8$,

$Y_0 = Z^0 y_0 + Z^0 y_1 + Z^0 y_2 + Z^0 y_3 + Z^0 y_4 + Z^0 y_5 + Z^0 y_6 + Z^0 y_7$, 
$Y_1 = Z^0 y_0 + Z^1 y_1 + Z^2 y_2 + Z^3 y_3 + Z^4 y_4 + Z^5 y_5 + Z^6 y_6 + Z^7 y_7$, 
$Y_2 = Z^0 y_0 + Z^2 y_1 + Z^4 y_2 + Z^6 y_3 + Z^8 y_4 + Z^{10} y_5 + Z^{12} y_6 + Z^{14} y_7$, 
$Y_3 = Z^0 y_0 + Z^3 y_1 + Z^6 y_2 + Z^9 y_3 + Z^{12} y_4 + Z^{15} y_5 + Z^{18} y_6 + Z^{21} y_7$, 
$Y_4 = Z^0 y_0 + Z^4 y_1 + Z^8 y_2 + Z^{12} y_3 + Z^{16} y_4 + Z^{20} y_5 + Z^{24} y_6 + Z^{28} y_7$, 
$Y_5 = Z^0 y_0 + Z^5 y_1 + Z^{10} y_2 + Z^{15} y_3 + Z^{20} y_4 + Z^{25} y_5 + Z^{30} y_6 + Z^{35} y_7$, 
$Y_6 = Z^0 y_0 + Z^6 y_1 + Z^{12} y_2 + Z^{18} y_3 + Z^{24} y_4 + Z^{30} y_5 + Z^{36} y_6 + Z^{42} y_7$, 
$Y_7 = Z^0 y_0 + Z^7 y_1 + Z^{14} y_2 + Z^{21} y_3 + Z^{28} y_4 + Z^{35} y_5 + Z^{42} y_6 + Z^{49} y_7$,

> 7) Actually, this algorithm has been discovered a number of times, for instance, in 1942 by Danielson and Lanczos (Danielson and Lanczos, 1942), as well as much earlier by Gauss.

where we include Z⁰ (≡ 1) for clarity. When we actually evaluate these powers of Z, we find only four independent values:

Z⁰ = exp(0) = +1 ,          Z¹ = exp(-2π/8) = + √2/2 - i √2/2 ,
Z² = exp(-2·2iπ/8) = -i ,      Z³ = exp(-2π·3i/8) = - √2/2 - i √2/2 ,
Z⁴ = exp(-2π·4i/8) = -Z⁰ ,      Z⁵ = exp(-2π·5i/8) = -Z¹ ,
Z⁶ = exp(-2·6iπ/8) = -Z² ,      Z⁷ = exp(-2·7iπ/8) = -Z³ ,
Z⁸ = exp(-2π·8i/8) = +Z⁰ ,      Z⁹ = exp(-2π·9i/8) = +Z¹ ,
Z¹⁰ = exp(-2π·10i/8) = +Z² ,    Z¹¹ = exp(-2π·11i/8) = +Z³ ,
Z¹² = exp(-2π·11i/8) = -Z⁰ ,    ...    (12.82)

When substituted into the definitions of the transforms, we obtain

Y₀ = Z⁰ y₀ + Z⁰ y₁ + Z⁰ y₂ + Z⁰ y₃ + Z⁰ y₄ + Z⁰ y₅ + Z⁰ y₆ + Z⁰ y₇ ,    (12.83)
Y₁ = Z⁰ y₀ + Z¹ y₁ + Z² y₂ + Z³ y₃ - Z⁰ y₄ - Z¹ y₅ - Z² y₆ - Z³ y₇ ,    (12.84)
Y₂ = Z⁰ y₀ + Z² y₁ - Z⁰ y₂ - Z² y₃ + Z⁰ y₄ + Z² y₅ - Z⁰ y₆ - Z² y₇ ,    (12.85)
Y₃ = Z⁰ y₀ + Z³ y₁ - Z² y₂ + Z¹ y₃ - Z⁰ y₄ - Z³ y₅ + Z² y₆ - Z¹ y₇ ,    (12.86)
Y₄ = Z⁰ y₀ - Z⁰ y₁ + Z⁰ y₂ - Z⁰ y₃ + Z⁰ y₄ - Z⁰ y₅ + Z⁰ y₆ - Z⁰ y₇ ,    (12.87)
Y₅ = Z⁰ y₀ - Z¹ y₁ + Z² y₂ - Z³ y₃ - Z⁰ y₄ + Z¹ y₅ - Z² y₆ + Z³ y₇ ,    (12.88)
Y₆ = Z⁰ y₀ - Z² y₁ - Z⁰ y₂ + Z² y₃ + Z⁰ y₄ - Z² y₅ - Z⁰ y₆ + Z² y₇ ,    (12.89)
Y₇ = Z⁰ y₀ - Z³ y₁ - Z² y₂ - Z¹ y₃ - Z⁰ y₄ + Z³ y₅ + Z² y₆ + Z¹ y₇ ,    (12.90)
Y₈ = Y₀ .    (12.91)

We see that these transforms now require 8 × 8 = 64 multiplications of complex numbers, in addition to some less time-consuming additions. We place these equations in an appropriate form for computing by regrouping the terms into sums and differences of the y's:

Y₀ = Z⁰(y₀ + y₄) + Z⁰(y₁ + y₅) + Z⁰(y₂ + y₆) + Z⁰(y₃ + y₇) ,    (12.92)
Y₁ = Z⁰(y₀ - y₄) + Z¹(y₁ - y₅) + Z²(y₂ - y₆) + Z³(y₃ - y₇) ,    (12.93)
Y₂ = Z⁰(y₀ + y₄) + Z²(y₁ + y₅) - Z⁰(y₂ + y₆) - Z²(y₃ + y₇) ,    (12.94)
Y₃ = Z⁰(y₀ − y₄) + Z³(y₁ − y₅) − Z²(y₂ − y₆) + Z¹(y₃ − y₇),  (12.95)
Y₄ = Z⁰(y₀ + y₄) − Z⁰(y₁ + y₅) + Z⁰(y₂ + y₆) − Z⁰(y₃ + y₇),  (12.96)
Y₅ = Z⁰(y₀ − y₄) − Z¹(y₁ − y₅) + Z²(y₂ − y₆) − Z³(y₃ − y₇),  (12.97)
Y₆ = Z⁰(y₀ + y₄) − Z²(y₁ + y₅) − Z⁰(y₂ + y₆) + Z²(y₃ + y₇),  (12.98)
Y₇ = Z⁰(y₀ − y₄) − Z³(y₁ − y₅) − Z²(y₂ − y₆) − Z¹(y₃ − y₇),  (12.99)
Y₈ = Y₀ .  (12.100)

Note the repeating factors inside the parentheses, with combinations of the form yₚ ± y_q. These symmetries are systematized by introducing the butterfly operation (Figure 12.8). This operation takes the yₚ and y_q data elements from the left wing and converts them to the yₚ + Zy_q elements in the right wings. In Figure 12.9 we show what happens when we apply the butterfly operations to an entire FFT process, specifically to the pairs (y₀, y₄), (y₁, y₅), (y₂, y₆), and (y₃, y₇). Note how the number of multiplications of complex numbers has been reduced: For the first butterfly operation there are 8 multiplications by Z⁰; for the second butterfly operation there are 8 multiplications, and so forth, until a total of 24 multiplications are made in four butterflies. In contrast, 64 multiplications are required in the original DFT (12.91).

![](img/bccda43674e4a93dee81c749eba8d2f7_324_0.png)

Figure 12.8 The basic butterfly operation in which elements y_p and y_q on the left are transformed into y_p + Zy_q and y_p − Zy_q on the right.

### 12.9.1
Bit Reversal

The reader may have observed in Figure 12.9 that we started with eight data elements in the order 0–7 and that after three butterfly operators we obtained transforms in the order 0, 4, 2, 6, 1, 5, 3, 7. The astute reader may further have observed that these numbers correspond to the bit-reversed order of 0–7. Let us look into this further. We need 3 bits to give the order of each of the 8 input data elements (the numbers 0–7). Explicitly, on the left in Table 10.1 we give the binary representation for decimal numbers 0–7, their bit reversals, and the corresponding

## Table 12.1 Reordering for 16 data complex points.

| Order | Input data | New order | Order | Input data | New order |
|---|---|---|---|---|---|
| 0 | 0.0 + 0.0i | 0.0 + 0.0i | 8 | 8.0 + 8.0i | 1.0 + 1.0i |
| 1 | 1.0 + 1.0i | 8.0 + 8.0i | 9 | 9.0 + 9.0i | 9.0 + 9.0i |
| 2 | 2.0 + 2.0i | 4.0 + 4.0i | 10 | 10.0 + 10.0i | 5.0 + 5.0i |
| 3 | 3.0 + 3.0i | 12.0 + 12.0i | 11 | 11.0 + 11.0i | 13.0 + 13.0i |
| 4 | 4.0 + 4.0i | 2.0 + 2.0i | 12 | 12.0 + 12.0i | 3.0 + 3.0i |
| 5 | 5.0 + 5.0i | 10.0 + 10.0i | 13 | 13.0 + 13.0i | 11.0 + 11.0i |
| 6 | 6.0 + 6.0i | 6.0 + 6.0i | 14 | 14.0 + 14.0i | 7.0 + 7.0i |
| 7 | 7.0 + 7.0i | 14.0 + 14.0i | 15 | 15.0 + 15.0i | 15.0 + 15.0i |

| Dec | Bin | Rev | Dec Rev | Binary-Reversed 0–7 | Binary-Reversed 0–16 |
|---|---|---|---|---|---|
|  |  |  |  | Rev | Dec Rev |
| 0 | 000 | 000 | 0 | 0000 | 0 |
| 1 | 001 | 100 | 4 | 1000 | 8 |
| 2 | 010 | 010 | 2 | 0100 | 4 |
| 3 | 011 | 110 | 6 | 1100 | 12 |
| 4 | 100 | 001 | 1 | 0010 | 2 |
| 5 | 101 | 101 | 5 | 1010 | 10 |
| 6 | 110 | 011 | 3 | 0110 | 6 |
| 7 | 111 | 111 | 7 | 1110 | 14 |
| 8 | 1000 | — | — | 0001 | 1 |
| 9 | 1001 | — | — | 1001 | 9 |
| 10 | 1010 | — | — | 0101 | 5 |
| 11 | 1011 | — | — | 1101 | 13 |
| 12 | 1100 | — | — | 0011 | 3 |
| 13 | 1101 | — | — | 1011 | 11 |
| 14 | 1110 | — | — | 0111 | 7 |
| 15 | 1111 | — | — | 1111 | 15 |

## 12.10
FFT Implementation

The first FFT program we are aware of was written in Fortran IV by Norman Brenner at MIT’s Lincoln Laboratory (Higgins, 1976) and was hard for us to follow. Our (easier-to-follow) Python version is in Listing 12.3. Its input is N = 2^n data to be transformed (FFTs always require that the number of input data are a power of 2). If the number of your input data is not a power of 2, then you can make it so by concatenating some of the initial data to the end of your input until a power of
