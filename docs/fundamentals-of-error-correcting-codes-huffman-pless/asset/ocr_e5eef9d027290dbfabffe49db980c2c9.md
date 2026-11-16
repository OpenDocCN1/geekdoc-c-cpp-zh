Exercise 596 Prove that if x and y are in \(\mathbb{F}_3^n\), then

```
d(x, y) \equiv wt(x) + wt(y) - x \cdot y \pmod 3.
```

Hint: By rescaling, which does not change distance or inner product modulo 3, you may assume all nonzero components of x equal 1.

This discussion and the accompanying exercises have proved the following theorem.

**Theorem 10.4.1** Both length 11 and length 12, possibly nonlinear, ternary codes each containing 0 with \(M \ge 3^6\) codewords and minimum distance 5 and 6, respectively, are unique up to equivalence. They are the [11, 6, 5] and [12, 6, 6] ternary Golay codes.

# ## 10.4.2 Properties of ternary Golay codes

In Example 6.6.11, we gave generating idempotents for the odd-like ternary quadratic residue codes of length 11. One such code has generating idempotent

```
$e_{11}(x) = -(x^2 + x^6 + x^7 + x^8 + x^{10})$
```

and generator polynomial

```
$g_{11}(x) = -1 + x^2 - x^3 + x^4 + x^5$.
```

This code has minimum distance \(d_0 \ge 4\) by Theorem 6.6.22. By Theorem 6.6.14, the extended code is a [12, 6] self-dual code with minimum distance a multiple of 3. Therefore \(d_0 \ge 5\), and by Theorem 10.4.1 this is one representation of the [11, 6, 5] ternary Golay code \(\mathcal{G}_{11}\). Extending this odd-like quadratic residue code gives one representation of the [12, 6, 6] extended ternary Golay code \(\mathcal{G}_{12}\).

**Exercise 597** Verify that \(g_{11}(x)\) is the generator polynomial for the cyclic code with generating idempotent \(e_{11}(x)\).

**Exercise 598** Create the generator matrix for the extended quadratic residue code extending the cyclic code with generator polynomial \(g_{11}(x)\), adding the parity check coordinate on the row. Reduce this generator matrix and show that columns can indeed be permuted and scaled to obtain the generator matrix in Exercise 592(i).

As in Section 10.1.2, the following permutations are automorphisms of \(\mathcal{G}_{12}\), viewed as the extended quadratic residue code obtained by extending the cyclic code with generating idempotent \(e_{11}(x)\), where the coordinates are labeled \(0, 1, \dots, 10, \infty\):

```
$s_{12} = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10), \text{ and } \mu_3 = (1, 3, 9, 5, 4)(2, 6, 7, 10, 8).$
```

The element from the Gleason-Prange Theorem is

```
$v_{12} = \text{diag}(1, -1, -1, 1, 1, -1, -1, -1, 1, -1, -1) \times (0, \infty)(1, 10)(2, 5)(3, 7)(4, 8)(6, 9).$
```