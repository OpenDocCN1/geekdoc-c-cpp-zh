+   (a) Give the Sphere Packing, Johnson, and Elias Bounds for $A_2(9, 3)$ and $A_2(10, 4)$.
+   (b) Apply the Linear Programming Bound (ii) with $n=10, q=2$, and $d=4$.
+   (c) Prove that $B_k + 5B_{10} \le 5$.
+   (d) Combine the inequalities from the Linear Programming Bound (ii) with the inequality in (c) to obtain an upper bound for $A_2(10, 4)$. Is it an improvement over the bound found in (b)?
+   (e) What is the best bound on $A_2(9, 3) = A_2(10, 4)$ from parts (a), (b), and (d)? How does it compare to the value in Table 2.1?
+   (f) Assuming the value of $A_2(9, 4)$ in Table 2.1 is correct, what bound do you get on $A_2(9, 3) = A_2(10, 4)$ from Theorem 2.1.6?

# Exercise 119 Do the following to obtain bounds on $A_2(13, 5) = A_2(14, 6)$. (It may be helpful to use a computer algebra program that can perform linear programming.)

+   (a) Give the Sphere Packing, Johnson, and Elias Bounds for $A_2(13, 5)$ and $A_2(14, 6)$.
+   (b) Apply the Linear Programming Bound (ii) with $n=14, q=2$, and $d=6$ to obtain an upper bound for $A_2(14, 6)$.
+   (c) What is the best bound on $A_2(13, 5) = A_2(14, 6)$ from parts (a) and (b)? How does it compare to the value in Table 2.1?
+   (d) Assuming the value of $A_2(13, 6)$ in Table 2.1 is correct, what bound do you get on $A_2(13, 5) = A_2(14, 6)$ from Theorem 2.1.6?

# 2.7 The Griesmer Upper Bound

The final upper bound we discuss is a generalization of the Singleton Bound known as the Griesmer Bound. We place it last because, unlike our other upper bounds, this one applies only to linear codes.

To prove this bound we first discuss the generally useful idea of a residual code due to H. J. Helgert and R. D. Stinaff [120]. Let $\mathcal{C}$ be an $[n, k]$ code and let $\mathbf{c}$ be a codeword of weight $w$. Let the set of coordinates on which $\mathbf{c}$ is nonzero be $\mathcal{T}$. Then the *residual code* of $\mathcal{C}$ with respect to $\mathbf{c}$, denoted $\text{Res}(\mathcal{C}, \mathbf{c})$, is the code of length $n-w$ punctured on all coordinates of $\mathcal{T}$. The next result gives a lower bound for the minimum distance of residual codes [131].

# Theorem 2.7.1 Let $\mathcal{C}$ be an $[n, k, d]$ code over $\mathbb{F}_q$ and let $\mathbf{c}$ be a codeword of weight $w < (q/(q-1))d$. Then $\text{Res}(\mathcal{C}, \mathbf{c})$ is an $[n-w, k-1, d']$ code, where $d' \ge d - w + \lceil w/q \rceil$.

Proof: By replacing $\mathcal{C}$ by a monomially equivalent code, we may assume that $\mathbf{c} = 11 \cdots 100 \cdots 0$. Since puncturing $\mathbf{c}$ on its nonzero coordinates gives the zero vector, $\text{Res}(\mathcal{C}, \mathbf{c})$ has dimension less than $k$. Assume that the dimension is strictly less than $k-1$. Then there exists a nonzero codeword $\mathbf{x} = x_1 \cdots x_n \in \mathcal{C}$ which is not a multiple of $\mathbf{c}$ with $x_{w+1} \cdots x_n = \mathbf{0}$. There exists $\alpha \in \mathbb{F}_q$ such that at least $w/q$ coordinates of $x_1 \cdots x_w$ equal $\alpha$. Therefore
$$d \le \text{wt}(\mathbf{x} - \alpha \mathbf{c}) \le w - \frac{w}{q} = \frac{w(q-1)}{q},$$
contradicting our assumption on $w$. Hence $\text{Res}(\mathcal{C}, \mathbf{c})$ has dimension $k-1$.