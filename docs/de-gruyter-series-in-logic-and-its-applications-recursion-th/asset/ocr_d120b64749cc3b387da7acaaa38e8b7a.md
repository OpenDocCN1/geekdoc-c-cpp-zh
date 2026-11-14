# 12.2.2 Characterizing randomness via complexity

The equivalence between Martin-Löf randomness and Kolmogorov complexity is given by the following:

Theorem 12.2.7 (Schnorr). A real x is Martin-Löf random if and only if

```
(∃c)(∀n)(K(x ↾ n) ≥ n - c).
```

Chaitin [9] gave a “concrete” example of a Martin-Löf random real:

```
\Omega = \sum_{U(\sigma)\downarrow} 2^{-|\sigma|},
```

and several randomness notions have been characterized in terms of Kolmogorov complexity. The next two theorems characterize Martin-Löf randomness and 2-randomness respectively in terms of plain Kolmogorov complexity.

Theorem 12.2.8 (Miller and Yu [103]). A real x is Martin-Löf random if and only if for every recursive function g with \sum_{n<\omega} 2^{-g(n)} < \infty,

```
(∃c)(∀n)(C(x ↾ n) ≥ n - g(n) - c).
```

Theorem 12.2.9 (Miller [101] and Nies, Stephan, Terwijn [112]). A real x is 2-random if and only if

```
(∃c)(∀n)(∃m ≥ n)(C(x ↾ m) ≥ m - c).
```

2-randomness may also be characterized via prefix-free Kolmogorov complexity as follows:

Theorem 12.2.10 (Ding, Downey, and Yu [173] and Miller [102]). A real x is 2-random if and only if

```
(∃c)(∀n)(∃m ≥ n)(K(x ↾ m) ≥ m + K(m) - c).
```

A connection between Martin-Löf randomness and the two notions of complexity is given by the following theorem:

Theorem 12.2.11 (Miller and Yu [103]). x ∨ y is Martin-Löf random if and only if

```
(∃c)(∀n)(K(x ↾ n) + C(y ↾ n) ≥ 2n - c).
```

There is a natural way of comparing two reals in terms of plain and prefix-free complexities:

Definition 12.2.12. Write x ≤_K y (resp. x ≤_C y) if and only if

```
(∃c)(∀n)(K(x ↾ n) ≤ K(y ↾ n) + c)
```

(resp. (∃c)(∀n)(C(x ↾ n) ≤ C(y ↾ n) + c)).