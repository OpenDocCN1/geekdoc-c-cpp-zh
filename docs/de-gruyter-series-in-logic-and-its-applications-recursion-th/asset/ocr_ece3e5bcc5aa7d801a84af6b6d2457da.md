Note that $\mathbb{P}(\kappa)$ only preserves the successor cardinal $\kappa^+$. The next notion of forcing allows one to preserve limit cardinals which are regular.

# Definition 6.2.8. Let $\kappa \ge \omega$ be a cardinal. Define Lévy forcing for $\kappa$, $\mathbb{L}(\kappa) = (\mathbb{L}_\kappa, \le)$, as follows:

+   - $p \in \mathbb{L}_\kappa$ if and only if $p$ is a finite function mapping a subset of $\kappa \times \omega$ into $\kappa$ such that for any $\alpha < \kappa$ and $n < \omega$, if $p(\alpha, n)$ is defined, then $p(\alpha, n) < \alpha$.

+   - For any $p, q \in \mathbb{L}_\kappa$, $q \le p$ if and only if $q \supseteq p$.

$\mathbb{L}(\kappa)$ may be considered as product forcing with finite support of length $\kappa$, where at each $\alpha < \kappa$ the forcing action collapses $\alpha$ onto $\omega$.

# Proposition 6.2.9. Let $\kappa \ge \omega$ be a regular cardinal and let $G$ be $\mathbb{L}(\kappa)$-generic. Then $\kappa = (\omega_1)^{M[G]}$.

Proof. It is clear that for any $\alpha < \kappa$, $G(\alpha) = \bigcup_{n \le p \in G} p(\alpha, n)$ maps $\omega$ onto $\alpha$. Hence $M[G] \models \kappa \le \omega_1$. We prove that $\mathbb{L}(\kappa)$ satisfies c.c.c.

Suppose that $A \subseteq \mathbb{L}_\kappa$ is an antichain of cardinality $\kappa$. Without loss of generality, we may assume that there is an $n^*$ such that $|\text{Dom}(p)| = n^*$ for every $p \in A$. We claim that there is an $\alpha < \kappa$ such that $A_\alpha = \{p \in A \mid (\exists n)(\alpha, n) \in \text{Dom}(p)\}$ has cardinality $\kappa$. Otherwise, there exist $p, q \in A$ with disjoint domains such that $p$ and $q$ are compatible, which is a contradiction. Hence let $\alpha_0$ be the least $\alpha$ such that $A_\alpha$ has cardinality $\kappa$. Let $B_{\alpha_0} = \{p \in A_{\alpha_0} \mid (\forall \beta < \alpha_0)(\forall n)(\beta, n) \in \text{Dom}(p)\}$. By the assumption on $\alpha_0$, $|B_{\alpha_0}| = \kappa$.

Since $|B_{\alpha_0}| = \kappa$ and $|\alpha_0| < \kappa$, we may assume that for any $p, q \in B_{\alpha_0}$, $\{(\alpha_0, n) \mid (\alpha_0, n) \in \text{Dom}(p)\} = \{(\alpha_0, n) \mid (\alpha_0, n) \in \text{Dom}(q)\}$. Furthermore since $p(\alpha, n) < \alpha$ in general, we may even assume that for any $p, q \in B_{\alpha_0}$, $(\alpha_0, n) \in \text{Dom}(p)$ implies $p(\alpha_0, n) = q(\alpha_0, n)$. 

Then by the same argument as that for $\alpha_0$, there is an $\alpha_1 > \alpha_0$ which is the least ordinal $> \alpha_0$ such that $B_{\alpha_0} \ge A_{\alpha_1}$ and the latter has size $\kappa$. Let $B_{\alpha_1} = A_{\alpha_1} \cap \{p \mid (\forall \beta)(\forall n)(\alpha_0 < \beta < \alpha_1 \rightarrow (\beta, n) \notin \text{Dom}(p))\}$. Then $|B_{\alpha_1}| = \kappa$.

Thus as before we may define a sequence of ordinals $\alpha_0 < \alpha_1 < \dots < \alpha_\kappa$ and a sequence of sets $B_{\alpha_0} \ge B_{\alpha_1} \ge \dots \ge B_{\alpha_\kappa}$ such that $|B_{\alpha_\kappa}| = \kappa$ and for all $p \in B_{\alpha_\kappa}$, $\text{Dom}(p) = \{\alpha_0, \dots, \alpha_\kappa\}$. Then $|B_{\alpha_\kappa}| \le |\alpha_\kappa|^\omega < \kappa$, a contradiction.

# 6.2.4 Sacks forcing

Forcing with perfect sets was introduced by Spector [154] in his construction of a set of minimal Turing degree. This method was generalized by Sacks and applied to the hyperarithmetic and set-theoretic setting to produce sets of minimal hyperdegree and minimal degree of constructibility [121] respectively.