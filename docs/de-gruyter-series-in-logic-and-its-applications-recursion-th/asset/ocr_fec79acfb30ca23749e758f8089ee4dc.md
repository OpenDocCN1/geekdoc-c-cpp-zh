Lemma 7.2.4. Assume ZF + AD + DC, the partial order $\le_M$ on increasing uniformly degree invariant functions is well-ordering.

In conclusion, we have the following theorem.

Theorem 7.2.5 (Steel [159], Slaman and Steel [142]). Assume ZF + AD + DC, Martin's conjecture (6.6.9) holds for uniformly degree invariant functions.

Remark 7.2.6. H. Friedman [30] proved that there is a hyperarithmetic predicate R and a sequence $\{x_n\}_{n<\omega}$ such that $x'_{n+1} \le_T x_n$ and $x_{n+1}$ is the unique y satisfying $R(y, x_n)$. 

# 7.2.1 Exercises

Exercise 7.2.1. Prove that there exists an arithmetical predicate P such that for any n > 0, there exists a sequence $\{x_i\}_{i \le n}$ satisfying: (i) for any i < n, $x'_{i+1} \le_T x_i$, (ii) $P(x_{i+1}, x_i)$ and (iii) if $P(x, y)$ then $y = x_{i+1}$. 

Exercise 7.2.2. Prove that there is an arithmetical predicate R and a $<_h$-descending sequence $\{x_n\}_{n<\omega}$ such that for any n, $x_{n+1}$ is the unique real y satisfying $R(y, x_n)$. 

# 7.3 The Posner–Robinson Theorem

# 7.3.1 The original Posner–Robinson Theorem

Theorem 7.3.1 (Posner and Robinson [114]). For any nonrecursive $x \le_T 0'$, there is a g such that $x \oplus g \equiv_T g' \equiv_T 0'$. 

Thus given a nonrecursive $\Delta^0_2$-real x, Theorem 7.3.1 says that there is a g relative to which x is its Turing jump.

Proof. To prove this, we use a method due to Jockusch and Shore [57]. Fix $x >_T 0$ to be $\Delta^0_2$. We may assume that x is not r.e.. For every e, consider the following statement:

```
\((\forall \alpha \in 2^\omega)(\exists n)(n \in x \wedge (\forall \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[r] \uparrow) \vee (n \notin x \wedge (\exists \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[r] \downarrow])\).
```

Since x is not r.e., $(\sharp_e)$ is true for every e. We construct g by induction.

Step 0: Define $g_0 = \emptyset$.

Step s + 1:

Substep 1. Define $g(s, 1) = g_s^c 0'(s)$. 

Substep 2. Find the least n such that either

```
\((n \in x \wedge \forall \tau \supseteq g(s, 1)^n0'1)(\Phi_s^\tau(s)[r] \uparrow)\)
```

or

```
\((n \notin x \wedge (\exists \tau \supseteq g(s, 1)^n0'1)(\Phi_s^\tau(s)[r] \downarrow])\).
```