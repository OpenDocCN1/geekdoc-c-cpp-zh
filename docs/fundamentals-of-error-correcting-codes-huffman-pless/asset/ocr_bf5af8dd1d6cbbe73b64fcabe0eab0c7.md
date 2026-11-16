be the Hamming weight enumerator of C. Let

$$Lee_C(x, y) = \sum_{c \in C} x^{wt_H(c)} y^{2n - wt_L(c)}$$

be the Lee weight enumerator of C; note the presence of 2n in the exponent of y, which is needed because there may be codewords of Lee weight as high as 2n. The analogs of (M_3) from Section 7.2 are [59, 116, 173, 174]:

$$Ham_{C^\perp}(x, y) = \frac{1}{|C|} Ham_C(y - x, y + 3x), \text{ and }$$

$$Lee_{C^\perp}(x, y) = \frac{1}{|C|} Lee_C(y - x, y + x).$$

**Exercise 692** Give the Hamming and Lee weight enumerators for the self-dual code C of Example 12.1.1. Then verify (12.5) and (12.6) for this code.

There are two other weight enumerators of interest with Z_4-linear codes. With n_t(v) defined as before, let

$$cwec(a, b, c, d) = \sum_{v \in \mathbb{Z}_4^n} a^{n(v)} b^{f_0(v)} c^{e_2(v)} d^{f_1(v)}$$

denote the complete weight enumerator of C, and let

$$swec(a, b, c) = \sum_{v \in C} a^{n(v)} b^{f_0(v) + n_2(v)} c^{f_1(v)}$$

denote the symmetrized weight enumerator of C. Notice that equivalent codes have the same symmetrized weight enumerators (making this one the more useful) while equivalent codes may not have the same complete weight enumerators. The corresponding MacWilliams equations are:

$$cwec_{C^\perp}(a, b, c, d) = \frac{1}{|C|} cwec(a + b + c + d, a + ib - c - id, a - b + c - d, a - ib - c + id), \text{ and }$$

$$swec_{C^\perp}(a, b, c) = \frac{1}{|C|} swec(a + 2b + c, a - c, a - 2b + c),$$

where $i = \sqrt{-1}$.

**Exercise 693** Give the complete and symmetrized weight enumerators for the self-dual code C of Example 12.1.1. Then verify (12.8) and (12.9) for this code.

**Exercise 694** Do the following:
(a) Show that swec(a, b, c) = cwec(a, b, c, b).
(b) Verify (12.9) assuming that (12.8) is valid.
(c) Show that Ham_C(x, y) = swec(x, y, x).
(d) Verify (12.5) assuming that (12.9) is valid.