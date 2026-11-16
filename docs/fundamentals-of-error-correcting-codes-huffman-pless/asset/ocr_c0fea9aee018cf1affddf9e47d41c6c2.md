| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| c1 = c2 | a | a | -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 |
| c3 = c4 = c5 | -1 | -1 | 1 | 1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 |
| c6 = c7 = c8 | -1 | -1 | -1 | -1 | 1 | 1 | 1 | 1 | -1 | -1 | -1 |
| c9 = c10 = c11 | -1 | -1 | -1 | -1 | -1 | -1 | -1 | -1 | 1 | 1 | 1 |

Figure 10.2 Configuration for c1, ..., c11, where a = 0 or a = 1.

Now let x have type (-1)^12 with 1s in coordinates 1 and 3. Since d(x, c1) ≤ 3, x ∉ C. Suppose that c covers x. Again c has weight 9 or 11. If wt(c) = 9, then it has type (-1)^10^2 with 0s in coordinates 1 and 3. Then d(c, c1) ≤ 3, which is a contradiction. So wt(c) = 11. If c has type (-1)^10^, b ≤ 4 since c covers x. If b = 1 or b = 4, then d(c, 1) is 10 or 7, a contradiction. If b = 2, then d(c, c1) ≤ 4, a contradiction. So b = 3 and c must have 1s in both coordinates 1 and 3. Again d(c, c1) ≤ 4, a contradiction. Therefore -1 ∈ C.
So C has codewords 0, 1, and -1. Furthermore, if c ∈ C with wt(c) = 11, -c ∈ C as follows. Choose a diagonal matrix D so that cD = 1. Then CD has minimum distance 5 and codewords 0 and 1 = cD. By the preceding argument, -1 ∈ CD implying that -cD ∈ CD. So -c ∈ C.

In summary, we know the following. C is a perfect (11, 3^5) code with minimum distance 5 containing 0 and 1. Furthermore, the negative of every weight 11 codeword of C is also in C. We next show that the same is true of all weight 9 codewords. Exercise 594 gives the possible types of codewords in C.

# Exercise 594 Show that codewords of the given weight have only the listed types:

+   (a) weight 5: 1^10^0^, (-1)^1^0^, (-1)^2^1^0^, (-1)^3^2^0^,
+   (b) weight 6: (-1)^3^1^0^, (-1)^4^0^, 1^6^0^,
+   (c) weight 8: (-1)^4^1^0^, (-1)^5^1^0^, (-1)^6^1^0^, (-1)^7^1^0^, (-1)^8^1^0^,
+   (d) weight 9: (-1)^1^0^, (-1)^2^1^0^, (-1)^3^1^0^,
+   (e) weight 11: (-1)^11^, 1^11^, (-1)^5^1^6^, (-1)^6^1^5^.

Hint: Consider each possible type for a given weight and compute its distance to each of 1 and -1. Use (10.5). ◆

To show the negative of a weight 9 codeword c is also a codeword, rescaling all 11 coordinates by -1 if necessary, we may assume c has type (-1)^3^1^0^ by Exercise 594. By permuting coordinates

```
c = (1, 1, 1, 1, 1, 1, -1, -1, -1, 0, 0).
```

Assume -e ∉ C. Consider the weight 11 vector

```
x1 = (-1, -1, -1, -1, -1, -1, 1, 1, 1, 1, 1).
```

If x1 ∈ C, then -x1 ∈ C and d(-x1, c) = 2, contradicting (10.5). Suppose c1 covers x1. Then wt(c1) is 9 or 11. By reordering coordinates and using Exercise 594, the only possibilities for c1 are