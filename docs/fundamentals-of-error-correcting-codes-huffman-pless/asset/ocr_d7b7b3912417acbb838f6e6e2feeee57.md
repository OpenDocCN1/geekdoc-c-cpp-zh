# Exercise 18 Prove Theorem 1.4.11.

Binary codes for which all codewords have weight divisible by four are called **doubly-even**. By Theorem 1.4.8, doubly-even codes are self-orthogonal. A self-orthogonal code must be even by Theorem 1.4.5(iv), one which is not doubly-even is called **singly-even**.

# Exercise 19 Find the minimum weights and weight distributions of the codes $\mathcal{H}_3$ in Example 1.2.3, $\mathcal{H}_3^\perp$ in Example 1.3.2, the tetracode in Example 1.3.3, and the hexacode in Example 1.3.4. Which of the binary codes listed are self-orthogonal? Which are doubly-even? Which are singly-even?

There is a generalization of the concepts of even and odd weight binary vectors to vectors over arbitrary fields, which is useful in the study of many types of codes. A vector $\mathbf{x} = x_1 x_2 \cdots x_n$ in $\mathbb{F}_q^n$ is **even-like** provided that

$$ \sum_{i=1}^n x_i = 0 $$

and is **odd-like** otherwise. A binary vector is even-like if and only if it has even weight; so the concept of even-like vectors is indeed a generalization of even weight binary vectors. The even-like vectors in a code form a subcode of a code over $\mathbb{F}_q$ as did the even weight vectors in a binary code. Except in the binary case, even-like vectors need not have even weight. The vectors $(1, 1, 1)$ in $\mathbb{F}_3^3$ and $(1, \omega, \bar{\omega})$ in $\mathbb{F}_4^3$ are examples. We say that a code is **even-like** if it has only even-like codewords; a code is odd-like if it is not even-like.

# Theorem 1.4.12 Let $C$ be an $[n, k]$ code over $\mathbb{F}_q$. Let $C_e$ be the set of even-like codewords in $C$. Then either:
(i) $C = C_e$, or
(ii) $C_e$, is an $[n, k - 1]$ subcode of $C$.

# Exercise 20 Prove Theorem 1.4.12.

There is an elementary relationship between the weight of a codeword and a parity check matrix for a linear code. This is presented in the following theorem whose proof is left as an exercise.

# Theorem 1.4.13 Let $C$ be a linear code with parity check matrix $H$. If $\mathbf{c} \in C$, the columns of $H$ corresponding to the nonzero coordinates of $\mathbf{c}$ are linearly dependent. Conversely, if a linear dependence relation with nonzero coefficients exists among $w$ columns of $H$, then there is a codeword in $C$ of weight $w$ whose nonzero coordinates correspond to these columns.

One way to find the minimum weight $d$ of a linear code is to examine all the nonzero codewords. The following corollary shows how to use the parity check matrix to find $d$.