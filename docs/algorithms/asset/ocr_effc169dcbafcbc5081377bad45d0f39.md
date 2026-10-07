# Chapter 2

# Algorithms 57

Matrix multiplication is particularly easy to break into subproblems, because it can be performed blockwise. To see what this means, carve X into $n/2 \times n/2$ blocks, and also Y:

```
$X = \begin{bmatrix} A & B \ C & D \end{bmatrix}, \quad Y = \begin{bmatrix} E & F \ G & H \end{bmatrix}$
```

Then their product can be expressed in terms of these blocks and is exactly as if the blocks were single elements (Example 2.11).

```
$XY = \begin{bmatrix} A & B \ C & D \end{bmatrix} \begin{bmatrix} E & F \ G & H \end{bmatrix} = \begin{bmatrix} AE+BG & AF+BH \ CE+DG & CF+DH \end{bmatrix}$
```

We have a divide-and-conquer strategy: to recursively compute eight $n/2$ products $AE, BG, AF, BH, CE, DG, CF, DH$, and then do a $O(n^2)$-time additions. The total running time is described by the recurrence relation

```
$T(n) = 8T(n/2) + O(n^2)$
```

This comes out to an unimpressive $O(n^2)$, the same as for the default algorithm. But if the efficiency can be further improved, and as with integer multiplication, the key is some clever algebra. It turns out $XY$ can be decomposed from seven $n/2 \times n/2$ subproblems, by a decomposition strategy that intricate and that Strassen was able to discover it!

```
$XY = \begin{bmatrix} P_3+P_4-P_2+P_6 & P_1+P_3 \ P_3+P_4 & P_1+P_5-P_3 \end{bmatrix}$
```

where

```
$P_1 = A(F-H) \quad P_5 = (A+D)(E+H)$ \$P_2 = (A+B)H \quad P_6 = (B-D)(G+H)$ \$P_3 = (C+D)E \quad P_7 = (A-C)(E+F)$ \$P_4 = D(G-E)$
```

The new running time is

```
$T(n) = 7T(n/2) + O(n^2)$
```

which by the master theorem works out to $O(n^{\log_2 7}) \approx O(n^{2.81})$.

# 2.6 The fast Fourier transform

We have seen so far divide-and-conquer gives fast algorithms for multiplying integers and matrices; our next target is polynomials. The product of two degree-d polynomials is a polynomial of degree $2d$, for example:

```
$(1+2x+3x^2) \cdot (2+x+4x^2) = 2+5x+12x^2+11x^3+12x^4$.
```