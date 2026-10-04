# Wavelets

A few of the elements of **w** are given in Equation 12.27 that follows:

```
$d_{1,1}=-\frac{1}{\sqrt{2}}x_1+\frac{1}{\sqrt{2}}x_2$,\nd_{2,1}=-\frac{1}{2}(x_1+x_2)+\frac{1}{2}(x_3+x_4),\nd_{3,1}=-\frac{1}{\sqrt{8}}(x_1+x_2+x_3+x_4)+\frac{1}{\sqrt{8}}(x_5+x_6+x_8),\ns_{3,1}=\frac{1}{\sqrt{8}}(x_1+x_2+x_3+x_4+x_5+x_6+x_8).\n(12.27)
```

To illustrate that, we use that Equations 12.24 and 12.26, the value, $x_i$, is given by

```
$x_i=-\frac{1}{\sqrt{2}}d_{1,1}-\frac{1}{2}d_{2,1}-\frac{1}{\sqrt{8}}d_{3,1},\n(12.28)
```

which can be verified using Equation 12.27 (see Problem 12.5).

# 12.3.5 Pyramid Algorithm

While the wavelet coefficients can be computed from Equation 12.22, the pyramid algorithm introduced in the wavelet setting by Mallat (1989) provides an efficient method for calculating them. The pyramid algorithm is outlined in the following for a set of length $n=2^l:

**Step 1:** Beginning with the data values $x_1, x_2, \dots, x_n$ (which is convenient to denote as $s_{0,1}, s_{0,2}, \dots, s_{0,n}$), 'down-sample' these into two sets, each containing $n/2$ values to obtain

+   $n/2$ coefficients: $d_{1,k}, k=1, \dots, n/2$
$n/2$ coefficients: $d_{1,k}, k=1, \dots, n/2$

**Step 2:** Retain $d_{1,k} k=1, \dots, n/2$ and down-sample $s_{1,k} k=1, \dots, n/2$ to obtain

+   $n/4$ coefficients: $s_{2,k}, k=1, \dots, n/4$
$n/4$ coefficients: $d_{2,k}, k=1, \dots, n/4$

**Step 3:** Retain $d_{2,k} k=1, \dots, n/4$, and down-sample $s_{2,k} k=1, \dots, n/4$ to obtain

+   $n/8$ coefficients: $s_{3,k} k=1, \dots, n/8$
$n/8$ coefficients: $d_{3,k} k=1, \dots, n/8$

...