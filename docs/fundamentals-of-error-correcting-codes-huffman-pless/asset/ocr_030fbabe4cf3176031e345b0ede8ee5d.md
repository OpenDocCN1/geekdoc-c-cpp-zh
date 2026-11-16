$Z_4^n$ is not a vector space. Note that if a vector v has components that are all 0s or 2s, then 2v = 0 implying that such a vector cannot be in a basis of a free submodule of $Z_4^n$ since $2 \neq 0$. In describing codes over $Z_4$, we denote the elements of $Z_4$ in either of the natural forms {0, 1, 2, 3} or {0, 1, 2, -1}, whichever is most convenient.

# Example 12.1.1 Let C be the $Z_4$-linear code of length 4 with the 16 codewords:

```
0000, 1113, 2222, 3333, 0202, 1313, 2020, 3133,
0022, 1131, 2200, 3313, 0220, 1331, 2002, 3111.
```

This is indeed an additive subgroup of $Z_4^4$ as Exercise 679 shows. If this were a free $Z_4$-module, it would have a basis of two vectors b1 and b2 such that every codeword would be a unique $Z_4$-linear combination of b1 and b2. As described above, both b1 and b2 have at least one component equal to 1 or 3. However, if b1 and b2 are among the eight codewords with one component 1 or 3, then 2b1 = 2222 = 2b2. Hence {b1, b2} cannot be a basis of C implying C is not free. However, we can still produce a perfectly good generator matrix whose rows function for all intents and purposes as a "basis" for the code.

# Exercise 679 Let C be the cover over $Z_4$ of Example 12.1.1.

+   (a) show that every codeword of C can be written uniquely in the form xc1 + yc2 + zc3, where c1 = 1113, c2 = 0202, c3 = 0022, x in Z4, and y and z are in {0, 1}.

+   (b) Use part (a) to show that C is a $Z_4$-linear code.

# Example 12.1.2 Let C be the code over $Z_4$ of Example 12.1.1. By Exercise 679(a), we can consider

```
G = [ 1 1 1 3
      0 2 0 2
      0 0 2 2 ]
```

as a generator matrix for C in the following sense: every codeword of C is (xyz)G for some x in Z4, and y and z in Z2.

As Exercise 679 illustrates, every $Z_4$-linear code C contains a set of k1 + k2 codewords c1, ..., ck1, ck1+1, ..., ck1+k2 such that every codeword in C is uniquely expressible in the form

```
\sum_{i=1}^{k_1} a_i c_i + \sum_{i=k_1+1}^{k_1+k_2} a_i c_i,
```

where ai in Z4 for 1 <= i <= k1 and ai in Z2 for k1 + 1 <= i <= k1 + k2. Furthermore, each ci has at least one component equal to 1 or 3 for 1 <= i <= k1 and each ci has all components equal to 0 and 2 for k1 + 1 <= i <= k1 + k2. If k2 = 0, the code C is a free Z4-module. The matrix whose rows are ci for 1 <= i <= k1 + k2 is called a generator matrix for C. The code C has 4^{k1} 2^{k2} codewords and is said to be of type 4^{t} 2^{s}. The code of Example 12.1.1 has type 4^1 2^2.

As with codes over fields, we can describe equivalence of Z4-linear codes. Let C1 and C2 be two Z4-linear codes of length n. Then C1 and C2 are permutation equivalent provided there is an n x n permutation matrix P such that C2 = C1 P. We can also scale components