# Exercise 545 Prove the following:

+   (a) A code has a double circulant construction if and only if it is equivalent to a code with a reverse circulant construction.

+   (b) A code has a bordered double circulant construction if and only if it is equivalent to a code with a bordered reverse circulant construction.

A subfamily of formally self-dual codes is the class of isodual codes. A code is isodual if it is equivalent to its dual. Clearly, any isodual code is formally self-dual; however, a formally self-dual code need not be isodual as in [84]. Exercise 546 shows how to construct isodual codes and hence formally self-dual codes.

# Exercise 546 Prove the following:

+   (a) A code of even length n with generator matrix [I_{n/2} A], where A = A^T is isodual.

+   (b) A code with a double circulant or reverse circulant construction is isodual. Hint: See Exercises 544 and 545.

+   (c) A code with a bordered double circulant or bordered reverse circulant construction is isodual provided the bordered matrix (9.11) used in the construction satisfies either \beta = \gamma = 0 or both \beta and \gamma are nonzero.

# 9.9 Formally self-dual codes

In this section we examine general properties of formally self-dual codes and describe the current state of their classification. Recall that a code is formally self-dual if the code and its dual have the same weight enumerator. When considering codes over fields F_2, F_3, and F_4, the only formally self-dual codes that are not already self-dual and whose weight enumerators are combinations of Gleason polynomials, are the even formally self-dual binary codes. Therefore in this section we will only consider even formally self-dual binary codes; relatively little work has been done on formally self-dual codes over nonbinary fields.

We begin by summarizing results about self-dual binary codes that either apply or do not apply to formally self-dual binary codes.

+   - While self-dual codes contain only even weight codewords, formally self-dual codes may contain odd weight codewords as well. See Exercise 547.
+   - A formally self-dual binary code C is even if and only if 1 in C; see Exercise 548.
+   - If C is an even formally self-dual binary code of length n with weight distribution A_i(C), then A_i(C) = A_{n-i}(C); again see Exercise 548.
+   - Gleason's Theorem then applies to even formally self-dual binary codes. If C is such a code of length n, then

```
W_C(x, y) = \sum_{i=0}^{\lfloor l/2 \rfloor} a_i g_1(x, y)^{l-4i} g_2(x, y)^i.
where g_1(x, y) = y^2 + x^2 and g_2(x, y) = y^8 + 14x^4y^4 + x^8.
```