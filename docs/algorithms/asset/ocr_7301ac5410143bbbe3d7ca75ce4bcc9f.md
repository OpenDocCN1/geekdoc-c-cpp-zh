# 68

# 2.6 The fast Fourier transform

leads to the definitive FFT algorithm of Figure 2.9, whose running time is T(n)
= 2T(n/2) + O(n) = O(n \log n).

# Figure 2.9 The fast Fourier transform

```
function FFT(a, w)
Input: An array a = (a_0, a_1, \dots, a_{n-1}), for n a power of 2
A primitive nth root of unity, \omega
Output: M_n(\omega)
```

```
if \omega = 1: return a
(s_0, s_1, \dots, s_{n/2-1}) = FFT((a_0, a_2, \dots, a_{n-2}), \omega^2)
(s_0, s_1, \dots, s_{n/2-1}) = FFT((a_1, a_3, \dots, a_{n-1}), \omega^2)
for j = 0 to n/2 - 1:
r_j = s_j + \omega^j s'_j
r_{j+n/2} = s_j - \omega^j s'_j
return (r_0, r_1, \dots, r_{n-1})
```

# The fast Fourier transform unraveled

Throughout our discussions, the fast Fourier transform has remained tightly
coconed within a divide-and-conquer formalism. To fully expose its structure,
we now unravel the recursion.

The divide-and-conquer step of the FFT can be drawn as a simple circuit. Here
is how a problem of size n is reduced to two subproblems of size n/2 (for clarity,
one pair of outputs (j, j + n/2) is singled out):

```
FFT_n (input: a_0, \dots, a_{n-1}, output: r_0, \dots, r_{n-1})
```

| a_0 |
| a_1 |
| :--- |
| FFT_{n/2} | r_j |
| a_{n-2} | |
| a_1 |
| a_3 |
| :--- |
| FFT_{n/2} | r_{j+n/2} |
| a_{n-1} |

Using a particular shorthand: the edges are wiring complex numbers
from left to right. A weight of j means "multiply the number on this wire by \omega^j." And
when two wires come into a junction from the left, the numbers are carrying
added up. The two outputs depicted are executing the commands

```
r_j = s_j + \omega^j s'_j
r_{j+n/2} = s_j - \omega^j s'_j
```