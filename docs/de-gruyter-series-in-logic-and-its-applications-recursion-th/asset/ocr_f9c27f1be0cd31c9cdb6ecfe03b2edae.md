We say that a function $f : 2^\omega \to 2^\omega$ presents an automorphism $\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le)$ if for every Turing degree $\mathbf{x}$ and real $x \in \mathbf{x}$, $f(x) \in \pi(\mathbf{x})$. The next two results are needed for Theorem 9.4.2 and are stated without proof.

# **Theorem 9.4.3.** Every automorphism $\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le)$ is presented by an arithmetical function $f : 2^\omega \to 2^\omega$.

If $R$ is a degree invariant relation over $(2^\omega)^{n+1}$ for some $n$, then it induces a relation $\bar{R}$ on degrees such that $(x_0, \dots, x_n) \in \bar{R} \Leftrightarrow (\exists x_0) \dots (\exists x_n)(x_0 \in x_0 \land \dots \land x_n \in x_n \land (x_0, \dots, x_n) \in R)$. We identify $\bar{R}$ with $R$ for simplicity.

# **Theorem 9.4.4.** For any relation $R$ over $\mathscr{P}$ which is induced by a degree invariant analytical relation over $2^\omega$, if $R$ is invariant under any automorphism of $\mathscr{P}$, then $R$ is definable in $(\mathscr{P}, \le)$. 

We now prove Theorem 9.4.2.

# **Lemma 9.4.5.** If $V = L$, then $(\mathscr{P}, \le)$ is $\omega$-homogeneous.

Proof. By Proposition 4.4.2, $<_1$ is a $\Delta^1_2$ well-ordering of $2^\omega$. The lexicographic ordering of $n + 1$-tuples induced by $<_1$ implies that for each $n$ there is a $\Delta^1_2$ well-ordering $<_{n+1}$ of $(2^\omega)^{n+1}$. 

For $m < \omega$ and $k \le n$, let $R_{m,k} \subseteq (2^\omega)^{n+1}$ be such that
\[
(x_0, \dots, x_n) \in R_{m,k} \Leftrightarrow k \le n \land \\
(\exists y_0) \dots (\exists y_n)((y_0, \dots, y_n) \text{ is the } <_{n+1}\text{-least so that} \\
(\exists \pi)(\forall i \le n)(\pi : (\mathscr{P}, \le) \to (\mathscr{P}, \le) \text{ is an automorphism } \land \pi(y_i) = x_i \land m \in y_k)).
\]

It is straightforward to verify that $R_{m,k}$ is degree invariant and hence induces a relation on $\mathscr{P}$ under invariant any automorphism. By Theorem 9.4.3, $R_{m,k}$ is also analytical. Hence by Theorem 9.4.4, $R_{m,k}$ is definable in $(\mathscr{P}, \le)$. 

Suppose that $(\mathscr{P}, \le, a_0, \dots, a_n) \equiv (\mathscr{P}, \le, b_0, \dots, b_n)$. Then $R_{m,k}(a_0, \dots, a_n) \Leftrightarrow R_{m,k}(b_0, \dots, b_n)$ for every $m$ and $k \le n$. For such a $k$, define $y_k$ so that $m \in y_k$ if and only if $R_{m,k}(a_0, \dots, a_n)$. By the definition of $R_{m,k}$, there are automorphisms $\pi_0$ and $\pi_1$ such that for every $k \le n$, $\pi_0(y_k) = x_k$ and $\pi_1(y_k) = b_k$. Then $\pi_1 \circ \pi_0^{-1}$ is an automorphism between $(\mathscr{P}, \le)$ and $(\mathscr{P}, \le)$, and $\pi_1 \pi_0^{-1}(a_k) = b_k$, implying that $(\mathscr{P}, \le)$ is $\omega$-homogeneous.

We complete the proof of Theorem 9.4.2 with the following lemma.

# **Lemma 9.4.6.** If $V = L[g]$ where $g$ is a Cohen generic real, then $(\mathscr{P}, \le)$ is not $\omega$-homogeneous.

Proof. Let $g = g_0 \oplus g_1$. We leave it to the reader to verify that $(g_0, g_1)$ is a pair of generic reals over a product Cohen forcing $\mathbb{C} \times \mathbb{C}$. Then by Theorem 9.4.3, there is no automorphism of $(\mathscr{P}, \le)$ sending $g_0$ to $g_1$.