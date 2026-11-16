# Exercise 524 Prove Theorem 9.5.1 as a corollary of Theorem 9.5.4.

Now we would like to count the number of Type II codes, which is more complicated than counting the number of self-dual codes. We will state the results here and will leave most proofs to Section 9.12. We have the following theorem counting the number of Type II codes.

# Theorem 9.5.5 Let n = 0 (mod 8).

+   (i) Then there are
+   $$
+   \prod_{i=0}^{\frac{n}{2}-2} (2^i + 1)
+   $$
+   Type II codes of length n.

+   (ii) Let C be an [n, k] doubly-even code containing 1. Then C is contained in
+   $$
+   \prod_{i=0}^{\frac{n}{2}-k-1} (2^i + 1)
+   $$
+   Type II codes of length n.

Example 9.5.6 Applying Theorem 9.5.5 to n = 8, we see that there are 2(2 + 1)(2^2 + 1) = 30 Type II [8, 4, 4] codes. By Exercise 56, all these codes are equivalent.

Exercise 525 The matrix

| 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

is the generator matrix of an [8, 3, 4] doubly-even binary code C. How many Type II codes are there that contain C?

# Exercise 526 Prove that if n = 0 (mod 8), then every [n, (n/2) - 1] doubly-even code containing 1 is contained in one Type I code and two Type II codes.

When n is a multiple of eight, the number of [n, k] doubly-even binary codes with k <= n/2 has been counted; for example, see Exercise 567 for the number of such codes containing 1.

We can also count the number of maximal doubly-even binary codes of length n in the case when 8 | n.

# Theorem 9.5.7 The number of [n, (n/2) - 1] doubly-even binary codes is:

+   (i)
+   $$
+   \prod_{i=1}^{\frac{n}{2}-1} (2^i + 1)
+   $$
+   if n = 4 (mod 8), and

+   (ii)
+   $$
+   \prod_{i=1}^{\frac{n}{2}-1} (2^i + 1)
+   $$
+   if n = 2 (mod 4).

The proof of Theorem 9.5.7(i) is left to Section 9.12, but the proof of (ii) is quite easy once we observe that the count in (ii) agrees with the count in Theorem 9.5.1. As the proof is instructive, we give it here. Let C be a self-dual code of length n where n = 2 (mod 4). Then, C is singly-even as C contains 1. There is a unique [n, (n/2) - 1]