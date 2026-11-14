First note that $|[T_\gamma] \setminus [T_{\gamma+1}]| \le \aleph_0$ for each $\gamma < \omega_1^{CK}$, and hence $[T_{\omega_1^{CK}}] 
eq \emptyset$. We claim that $T_{\omega_1^{CK}} = \cap_{\gamma < \omega_1^{CK}} T_\gamma \in T$ is a perfect tree. First note that given $\sigma \in T_{\omega_1^{CK}}$, there is a $	au > \sigma$ such that $	au \in T_{\omega_1^{CK}}$. Otherwise, let $g_0(n)$ be the least ordinal $\gamma < \omega_1^{CK}$ for which $\sigma^\frown n 
otin T_\gamma$. Then $g_0$ is a total function and $\Sigma_1$ in $L_{\omega_1^{CK}}$. By the admissibility of $\omega_1^{CK}$ (Corollary 3.6.7), there is an ordinal $eta < \omega_1^{CK}$ so that $g_0(n) < eta$ for all $n$. Then $\sigma 
otin T_{eta+1}$, a contradiction.

Now suppose that $\sigma \in T_{\omega_1^{CK}}$ is an isolated path, i.e. $[\sigma] \cap [T_{\omega_1^{CK}}]$ contains exactly one path. Let $h_0(n)$ be the least ordinal $\gamma < \omega_1^{CK}$ such that $[\{	au \in T \mid T_\gamma \wedge 	au \supset \sigma \mid [\sigma] = [\sigma] \mid n\}] = 1$. Then $h_0$ is a total function and $\Sigma_1$ in $L_{\omega_1^{CK}}$. By Corollary 3.6.7 again, there is an ordinal $eta < \omega_1^{CK}$ such that $h_0(n) < eta$ for all $n$. Then for any $	au_0, 	au_1 > \sigma$, if $	au_0, 	au_1 \in T_eta$, then $	au_0$ and $	au_1$ are compatible. So $\sigma 
otin T_{eta+1}$, a contradiction.

# 3.6.6 Exercises

+   Exercise 3.6.1. Complete the proof of Proposition 3.6.5.

+   Exercise 3.6.2. Relativize and prove the results in § 3.6.4.

+   Exercise 3.6.3. Prove that there is a recursive tree $T$ with uncountably many infinite paths (as in Proposition 3.6.10) such that for each $\gamma < \omega_1^{CK}$, $T_\gamma$ is not a perfect tree.

+   Exercise 3.6.4. Suppose that $R_0$ and $R_1$ code well-ordering relations of $\omega$ and the order type of $R_0$ is not greater than that of $R_1$. Show that there is an order-preserving function $f \le_H R_0 \oplus R_1$ which embeds $R_0$ onto an initial segment of $R_1$.

+   Exercise 3.6.5. Given a hyperarithmetic real $x$, show that there exist two recursive well-orderings $R_0 \cong R_1$ of $\omega$ such that there is no isomorphism between $R_0$ and $R_1$ recursive in $x$.

+   Exercise 3.6.6. Without using Kreisel's Basis Theorem, give a direct proof of Theorem 3.6.8.

# 3.7 The Spector–Gandy Theorem

# 3.7.1 First version

Theorem 3.7.1(Spector[156], Gandy[34]). $x \in 2^\omega$ is $\Pi^1_1$ if and only if there is a $\Sigma_1$-formula $\varphi(u)$ such that $n \in x \iff (L_{\omega_1^{CK}}, \in) \models \varphi(n)$.

Proof. Suppose that $x \in 2^\omega$ is $\Pi^1_1$. By Proposition 1.1.14, there is a recursive tree $T \subseteq \omega 	imes \omega^{<\omega}$ and a recursive function $f$ such that $n \in x$ if and only if $f(n) = [\sigma \mid (f(n), \sigma) \in T]$ is a wellfounded tree. Since $T$ is recursive, we have $T \in L_{\omega_1^{CK}}$. Given $n$, we say that $g : T_{f(n)} 	o \gamma$ is order preserving if $\sigma \succ 	au$ implies $g(\sigma) < g(	au)$. By Corollary 3.6.7,