matrix is the parity check matrix for a linear code with minimum weight at least d. We show that the construction can indeed be completed. Let j be an integer with 1 <= j <= n - 1 and assume that vectors h1, ..., hj have been found. Since j <= n - 1, the number of different linear combinations of d - 2 or fewer of h1, ..., hj is:

```
\sum_{i=0}^{d-2} \binom{j}{i} (q-1)^i \le \sum_{i=0}^{d-2} \binom{n-1}{i} (q-1)^i
```

Hence if (2.42) holds, then there is some vector h_{j+1} which is not a linear combination of d - 2 (or fewer) of h1, ..., hj. Thus the fact that h1, h2, ..., hn can be chosen follows by induction on j.

The matrix H in Lemma 2.9.1 is the parity check matrix of a code of length n over F_q that has dimension at least k and minimum distance at least d. Since the minimum distance of a subcode of a code is at least the minimum distance of the code, we have the following corollary.

# Corollary 2.9.2 Let n, k, and d be integers with 2 <= d <= n and 1 <= k <= n. Then there exists an [n, k] linear code over F_q with minimum distance at least d, provided

```
1 + \sum_{i=0}^{d-2} \binom{n-1}{i} (q-1)^i \le q^{n-k}.
```

# Theorem 2.9.3 (Varshamov Bound [337])

```
B_q(n, d) \ge q^{n - \lceil \log_q(\sum_{i=0}^{d-1} \binom{n-1}{i} (q-1)^i) \rceil}.
```

Proof: Let L be the left-hand side of (2.43). By Corollary 2.9.2, there exists an [n, k] code over F_q with minimum weight at least d provided log_q(L) <= n - k, or equivalently k <= n - log_q(L). The largest integer k satisfying this inequality is n - floor(log_q(L)). Thus B_q(n, d) >= q^{n - floor(log_q(L))}.

# 2.10 Asymptotic bounds

In this section we will study some of the bounds from previous sections as the code lengths go to infinity. The resulting bounds are called asymptotic bounds. Before beginning this exploration, we need to define two terms. For a (possibly) nonlinear code over F_q with M codewords, the information rate, or simply rate, of the code is defined to be n^{-1} log_q M. Notice that if the code were actually an [n, k] linear code, it would contain M = q^k codewords and n^{-1} log_q M = k/n; so for an [n, k, d] linear code, the ratio k/n is the rate of the code consistent with the definition of "rate" in Section 1.11.2. In the linear case the rate of a code is a measure of the number of information coordinates relative to the total number of coordinates. The higher the rate, the higher the proportion of coordinates in a