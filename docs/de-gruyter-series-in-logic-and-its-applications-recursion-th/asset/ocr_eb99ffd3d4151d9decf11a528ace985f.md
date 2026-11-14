Corollary 11.2.11 (Harrington). There is an uncountable $\Pi^1_2$-set $A$ such that for any recursive ordinal $\beta$ and $x \in A$, $x^{(\beta)} \not\ge_T 0^{(\beta+1)}$.

Proof. Suppose not. Let $B = \omega \times \omega^{<\omega}$ be arithmetical such that $[\{B_e\}]_{e < \omega}$, where $B_e = \{ \alpha \in \omega^{<\omega} \mid (e, \alpha) \in B \}$, is a recursive list of all $\Pi^1_1$-subsets of $\omega^{<\omega}$. Let $O \subseteq \Theta$ be as defined in Theorem 2.6.5.

Recall that the system satisfying (1)–(6) was obtained by fixing an ordinal notation $n$ with $|n| \ge \omega$. Let $e_0$ be such that $3 \cdot 5^{e_0} = \omega$. Define a $\Pi^1_1$-relation $R \subseteq \omega \times \omega$ such that

$R(e, n) \Leftrightarrow 3 \cdot 5^{e_0} \le_\Theta n \wedge n \in \Theta \wedge$

there is no system satisfying (1)–(6) for $n$ and $B_e = T_0^0$.

Then by Theorem 4.2.1 and the assumption, there is a total $\Pi^1_1$, hence $\Delta^1_1$, uniformizing function $f : \omega \to O$ for $R$. Let $I = \{ e \mid [B_e] > \aleph_0 \}$. By Theorem 11.10, $I$ is $\Sigma^1_1$. By Corollary 11.5.2, there is an $n \in O$ such that for all $m \in I(f(e) \in e \mid I)$, we have $m <_\Theta n$ and that contradicts the proof above.

Hence there is an $e \in I$ such that $B_e = T_0^0$ and a system satisfying (1)–(6) exists for each $n \in O$ where $|n| \ge \omega$. By the proof above, $H_n^1 \not\ge_T H_{2n}$.

# 11.2.2 Exercises

Exercise 11.2.1. Prove that in Theorem 11.2.1, the set $A$ may be chosen to be a subset of $2^\omega$.

Exercise 11.2.2 (Harrington). There is a $\Pi^1_1$-path through $\Theta$ such that the only hyperarithmetic reals recursive in it are recursive.

Exercise 11.2.3 (Harrington). Prove that for any recursive ordinal $\beta < \omega_1^{CK}$, there are two $\Pi^1_1$-singletons $x$ and $y$ in $2^\omega$ such that $x^{(\beta)} \not\ge_T y$ and $y^{(\beta)} \not\ge_T x$.

Exercise 11.2.4 (Harrington). Prove that there is a transitive model $N$ of KP such that $N \models \text{“Not every } \Delta^1_1\text{-real is hyperarithmetic”}$.

# 11.3 Perfect sets in L

# 11.3.1 A question of Prikry

In [98], Prikry posed the following question.

Question 11.3.1. Suppose that there is a nonconstructible real. Does every perfect set contain a nonconstructible real?

Friedman [29] also raised a question related to Question 11.3.1: