# Exercise 387 Find the weight enumerator of the [15, 11, 3] binary Hamming code.

To conclude this section, we use (7.7) to produce an interesting result about ternary codes, due to Kennedy [164].

# Theorem 7.5 Let C be an [n, k] ternary code with k >= 3 and weight distribution A0, A1, ..., An. For 0 <= i <= 2, let

```
N_i = \sum_{j \equiv i (\text{mod } 3)} A_j.
```

Then N0 = N1 = N2 = 0 (mod 3).

Proof: Because k >= 3, the first three equations of (7.7) with q = 3 yield

```
N_0 + N_1 + N_2 \equiv \sum_{i=0}^n A_i \equiv 0 (\text{mod } 3),
N_1 - N_2 \equiv \sum_{i=0}^n i A_i \equiv 0 (\text{mod } 3),
N_1 + N_2 \equiv \sum_{i=0}^n i^2 A_i \equiv 0 (\text{mod } 3).
```

since i = 0, 1, or -1 and i^2 = 0 or 1 modulo 3. The only solution modulo 3 is N0 = N1 = N2 = 0 (mod 3).

# Exercise 388 Show that the following weight distributions for ternary codes cannot occur:

+   (a) A0 = 1, A5 = 112, A6 = 152, A8 = 330, A9 = 110, A11 = 24.

+   (b) A0 = 1, A3 = 22, A4 = 42, A5 = 67, A6 = 55, A7 = 32, A8 = 24.

# 7.4 MDS codes

In this section, we show that the weight distribution of an [n, k] MDS code over Fq is determined by the parameters n, k, and q. One proof of this uses the MacWilliams equations; see [275]. We present a proof here that uses the inclusion-exclusion principle.

# Theorem 7.4.1 Let C be an [n, k, d] MDS code over Fq. The weight distribution of C is given by A0 = 1, Ai = 0 for 1 <= i < d, and

```
A_i = \binom{n}{i} \sum_{j=0}^{i-d} (-1)^j \binom{i}{j} (q^{i-j+1-d} - 1)
```

for d <= i <= n, where d = n - k + 1.

Proof: Clearly, A0 = 1 and Ai = 0 for 1 <= i < d. Let CT be the code of length n - |T| obtained from C by shortening on T. By repeated application of Exercise 317, CT is an [n - |T|, k - |T|] MDS code if |T| < k and CT is the zero code if |T| >= k. Let C(T) be the