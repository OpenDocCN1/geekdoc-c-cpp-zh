# Theorem 11.3.7 There is a constant $M$ such that for all $m \ge M$, $\rho_{\text{BCH}}(l, m) = 2t - 1$.

# 11.4 Covering radius of self-dual codes

In Chapters 9 and 10 we examined some well-known binary self-dual codes of moderate lengths. In this section we want to compute the covering radius of some of these codes.

We begin by considering extremal Type II binary codes. In Example 1.11.7, we presented the weight distribution of each coset of the unique [8, 4, 4] Type II binary code and conclude that it has covering radius 2. This same result comes from Theorem 11.1.7. In a series of examples and exercises in Section 7.5, we gave the complete coset weight distribution of each of the two [16, 8, 4] Type II binary codes and concluded that the covering radius is 4 for each code. Exercise 641 gives another proof without resorting to specific knowledge of the generator matrix of the code.

# Exercise 641 Let C be a [16, 8, 4] Type II binary code.

+   (a) Use the Delsarte Bound to show that $\rho(C) \le 4$.

+   (b) Use Theorems 11.1.1 and 11.1.7 to show that $3 \le \rho(C)$. 

+   (c) Suppose that C has covering radius 3. By Exercise 625, if C* is obtained from C by puncturing one coordinate, then $\rho(C^*) = 2$. Show that this violates the Sphere Covering Bound.

By Theorem 10.1.7 (or Example 8.3.2), we know that the unique [24, 12, 8] Type II binary code has covering radius 4. As this code is extended perfect, Theorem 11.1.7 also shows this. We now turn to the [32, 16, 8] Type II binary codes. In Section 9.7 we noted that there are exactly five such codes. Without knowing the specific structure of any of these except the number of weight 8 vectors, we can find their covering radii, a result found in [9].

# Theorem 11.4.1 Let C be a [32, 16, 8] Type II code. Then $\rho(C) = 6$.

Proof: We remark that the weight distribution of C is determined uniquely; see Theorem 9.3.1. It turns out that $A_6(C) = 620, C = C^\perp$ contains codewords of weights 8, 12, 16, 20, 24, 32, and 32. So by the Delsarte Bound $\rho(C) \le 6$. By Theorems 11.1.1 and 11.1.7, $5 \le \rho(C)$ as C is not extended perfect (Exercise 642). Suppose that $\rho(C) = 5$. This implies that every weight 6 vector in $\mathbb{F}_2^{32}$ is in a coset of even weight less than 6. The only coset of weight 0 is the code itself, which does not contain weight 6 codewords. Let x be a vector of weight 6. Then there must be a codeword c such that wt(x + c) = 2 or 4. The only possibility is that wt(c) = 8. Thus every weight 6 vector has support intersecting the support one of the 620 codewords of weight 8 in C in either five or six coordinates. The number of weight 6 vectors whose support intersects the support of a weight 8 vector in this manner is $\binom{8}{4}\binom{8}{2} + \binom{8}{5} = 1372$. Thus there are at most $620 \cdot 1372 = 850640$ weight 6 vectors in $\mathbb{F}_2^{32}$. But as there are $\binom{32}{6} = 906192$ weight 6 vectors in $\mathbb{F}_2^{32}$, we have a contradiction.

Exercise 642 Use the Sphere Packing Bound to show that a [32, 16, 8] even code is not extended perfect. Remark: We know this if we use the fact that the only perfect