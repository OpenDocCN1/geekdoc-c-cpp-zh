Similarly, the complete classification of self-dual codes of lengths 28 and 30 [53, 56, 264] shows that there are no such codes of minimum distance 8. At lengths 40, 42, and 44, the bound on the minimum distance of self-dual codes is 8, by Theorem 9.3.5. A number of the even formally self-dual codes counted in Table 9.12 have double circulant constructions. All those of lengths through 12 have a double circulant construction. It can be shown that the [14, 7, 4] self-dual code does not have a double circulant construction but exactly two of the nine even formally self-dual codes of length 14 that are not self-dual do have such constructions. It can also be shown that the length 18 code does also, as do two of the seven even formally self-dual codes of length 20. All the codes of length through 20, except possibly those of length 16, are isodual. For the minimum weights given in the table, length 22 is the smallest length for which a non-isodual even formally self-dual code is known to exist.

In Table 9.12, we see that there exist even formally self-dual codes with higher minimum weight than self-dual codes at lengths n = 10, 18, 20, 28, 30, 34, 2, and 44. Relatively little is known about even formally self-dual codes at lengths greater than 48.

**Research Problem 9.9.4** The bound in (9.13) on the minimum distance for even formally self-dual binary codes of length n = 40 ≤ 10, while the bound on self-dual codes of that length is d ≤ 8 by Theorem 9.3.5. No [40, 20, 10] even formally self-dual binary code, which necessarily must be non-self-dual, is known. Find one or show it does not exist.

By Theorem 9.3.5, if C is an [n, n/2, d] self-dual binary code with n ≡ 0 (mod 24), then d ≤ 4 [n/24] + 4, and when this bound is met, C is Type II. When n ≡ 0 (mod 24), there are no known even formally self-dual codes with d = 4 [n/24] + 4 that are not self-dual. Note that this value of d may not be the highest value possible; by [32] it is the highest for n = 24, 48, and 72.

**Research Problem 9.9.5** Find a [24m, 12m, 4m + 4] even formally self-dual binary code that is not self-dual or prove that none exists.

When codes are extremal Type II, the codewords support designs by Theorem 9.3.10. The following theorem, found in [165], illustrates the presence of designs in certain even formally self-dual codes.

**Theorem 9.9.6** Let C be an [n, n/2, d] even formally self-dual binary code with d = 2 [n/8] + 2 and n > 2. Let Sw be the set of vectors of weight w in C together with those of weight w in C⊥; a vector in C ∩ C⊥ is included twice in Sw. Then the vectors in Sw hold a 3-design in n = (mod 8) and a 1-design if n ≡ 6 (mod 8).

We note that this result holds only for the codes of lengths 6, 10, 14, 18, 22, and 30 from (9.13) and Table 9.12.

**Exercise 553** Let C be the [10, 5, 4] even formally self-dual C from Example 9.9.3.

+   (a) Show that C ∩ C⊥ = {0, 1}.
+   (b) By part (a) and Theorem 9.9.6, the codewords of weight 4 in C ∪ C⊥ hold a 3-(10, 4, λ) design. Find λ.
+   (c) Show that the weight 4 codewords of C do not support a 3-design.