# # 13 More on hyperarithmetic theory

# ## 13.1 Hyperarithmetic measure theory

The application of measure theory in recursion theory was initiated by Spector [155], Sacks [117] and Leeuw, Moore, Shannon, and Shapiro [19]. Randomness theory on the natural numbers may be viewed as such an application, while higher randomness theory is the union of measure theory with hyperarithmetic theory. In this chapter we discuss these connections to set the stage for higher randomness in the next chapter.

# ### 13.1.1 The measure of $\Pi_1^1$-sets

Lemma 13.1.1 (Sacks [120]). The set

{{("$\varphi$, p) | p is rational $\land \varphi$ is ranked with x as its only free variable $\land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}}

is $\Pi_1^1$.

Proof. By the Spector–Gandy Theorem (3.7.1) it is sufficient to prove that the set

{{("$\varphi$, p) | p is rational $\land \varphi$ is ranked with x as its only free variable $\land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}}

is $\Sigma_1$ over $(L_{\omega_1^{CK}}, \in)$. We apply Theorem 3.1.8 by performing induction on the rank of $\varphi$.

If $\varphi$ is atomic, then

{{("$\varphi$, p) | p is rational $\land \varphi$'s only free variable is x $\land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}}

is recursive. By induction on the complexity of $\varphi$, it is not difficult to see that

{{("$\varphi$, p) | p is rational $\land \varphi$'s only free variable is x $\land \varphi$ is of rank $0 \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}}

is arithmetical and hence $\Sigma_1$ over $(L_{\omega_1^{CK}}, \in)$. Now suppose that the set

{{("$\varphi$, p) | p is rational $\land \varphi$'s only free variable is x $\land \varphi$ is of rank at most $\alpha \land \mu(\{x \mid \mathfrak{A}(\omega_1^{CK}, x) = \varphi\}) \ge p\}}

is $\Sigma_1$ over $(L_{\omega_1^{CK}}, \in)$. Now suppose that the set