For each $n$, let $\varphi_n(v)$ be a formula defining $n$ so that

$$(\exists v_0) \cdots (\exists v_n)(\forall v)(\varphi v_0 \land v_1 = v_0 \cup \{v_0\} \land v_2 = v_1 \cup \{v_1\} \land \dots \land v_n = v_{n-1} \cup \{v_{n-1}\} \land V = v_n).$$

Then

$$n \in x \Leftrightarrow (L_{\omega_1}, \in) \models (\exists v)(\varphi_n(v) \land \varphi_x(v, i_1, \dots, i_m)).$$

By Definition 6.4.6 (i) and (ii),

$$n \in x \Leftrightarrow (L_{\aleph_\omega}, \in) \models (\exists v)(\varphi_n(v) \land \varphi_x(v, N_1, \dots, N_m)).$$

Clearly the set $\{(\exists v)(\varphi_n(v) \land \varphi_x(v, u_1, \dots, u_m)) \mid n < \omega\}$ is recursive and

$$n \in x \Leftrightarrow \ulcorner (\exists v)(\varphi_n(v) \land \varphi_x(v, u_1, \dots, u_m)) \urcorner \in 0^\sharp.$$

Thus $x \le_T 0^\sharp$.

Proposition 6.4.7 implies that $0^\sharp$ has extremely high computational power. Recursion-theoretically, one may view $0^\sharp$ as the "jump" of $\emptyset$ under the #-operator.

While $0^\sharp$ collapses cardinals in $L$, its absence presents quite a different picture provided by Jensen's remarkable Covering Lemma.

Theorem 6.4.8 (Jensen [21]). If $0^\sharp$ does not exist then every uncountable set of ordinals is contained in a constructible set of the same cardinality.

# 6.5 Axiom of determinacy

In this book our focus is mostly on low level definable sets of reals such as those that are $\Pi^1_1$ or $\Sigma^1_2$. To go "higher up", one resorts to the use of games and strategies which lie at the heart of the Axiom of Determinacy. It turns out that this axiom is at its core a large cardinal axiom.

# 6.5.1 Games and strategies

Let $A \subseteq \omega^\omega$. An infinite game $G_A$ with perfect information has two players labeled I and II. The game is played by choosing a natural number alternately between the two players and ends in $\omega$-many steps. Each game generates a real $x = (n_0, m_0, \dots, n_i, m_i, \dots) \in \omega^\omega$ where $n_i$ and $m_i$ are the numbers played by I and II respectively at step i. If $x \in A$, then I wins the game. Otherwise, II wins.

# Definition 6.5.1.

Given a set $A \subseteq \omega^\omega$, I has a winning strategy $\vec{\sigma} : \omega^{<\omega} \to \omega$ for the game $G_A$ if for every $g \in \omega^\omega$, the real $\vec{\sigma} * g = (n_0, g(0), \dots, n_i, g(n_i), \dots) \in A$ where $n_0 = \vec{\sigma}(0)$ and $n_i = \vec{\sigma}(\langle n_0, g(0), \dots, n_{i-1}, g(i-1) \rangle)$ for $i > 0$. The string