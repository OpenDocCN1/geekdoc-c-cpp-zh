# 14.3.3 Hyperdegrees of random reals

By Corollary 14.2.6, we know that the hyperdegrees of the set of $\Delta_1^1$-random reals include the cone of hyperdegrees with base 0. This raises the natural question of whether the hyperdegrees of $\Delta_1^1$-random reals are closed upwards.

Proposition 14.3.5. If $x$ is $\Delta_1^1$-random and $\omega_1^x = \omega_1^{CK}$, then there is a $y \ge_h x$ such that no $z \equiv_h y$ is $\Delta_1^1$-random.

Proof. Suppose that $x$ is $\Delta_1^1$-random and $\omega_1^x = \omega_1^{CK}$. Let

$F(x) = \{ y \mid y \ge_T x \land (\forall f \le_T y)(\forall g \le_h x)(g < f) \}.$

Then $F(x)$ is $\Sigma_1^x(x)$. Since $\emptyset^x \in F(x)$, $F(x)$ is not empty. By Gandy's Basis Theorem and relativized to $x$, there is a $y \in F(x)$ with $\omega_1^y = \omega_1^x = \omega_1^{CK}$. By Corollary 14.3.2 and Proposition 14.3.4, no $z \equiv_h y$ is $\Delta_1^1$-random.

On the other hand, the hyperdegrees of $\Pi_1^1$-random reals are closed downwards.

Lemma 14.3.6. If $x$ is $\Pi_1^1$-random and $y \le_h x$, then there is a recursive ordinal $\gamma$ such that $y \le_T x \oplus \emptyset^{(\gamma)}$.

Proof. Since $x$ is $\Pi_1^1$-random, we have $\omega_1^x = \omega_1^{CK}$. Let $y \le_h x$. Then there is a formula $\varphi(\dot{n}, \dot{x})$ with rank at most $\beta_0 < \omega_1^{CK}$ such that

$n \in y \Leftrightarrow \mathfrak{A}(\omega_1^{CK}, x) \vDash \varphi(\dot{n}, \dot{x})$.

By Lemma 13.1.11, there is a recursive ordinal $\beta > \beta_0$ such that

$A_{\beta_0} = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta_0 \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

is recursive in $\emptyset^{(\beta)}$. By Lemma 13.1.10, there is a recursive ordinal $\beta_1 \ge \beta$ such that for any number $i$ and formula $\psi$ with rank $\beta$, there is a formula $\psi'$ with rank at most $\beta_1$ such that $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ is a $\Pi_1^0(\emptyset^{(\beta)})$-subset of $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ with difference in measure less than $2^{-i}$. Note that the search procedure for $\beta_1$ from $\beta_0$ is effective in $L_{\omega_1^x}$. In this way one obtains a $\Delta_1$-sequence of ordinals $\beta_0 < \beta_1 < \cdots$ in $L_{\omega_1^x}$. Let $\gamma = \bigcup_{i < \omega} \beta_i$. Then for any $\beta < \gamma$,

(i) $A_\beta = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

is recursive in $\emptyset^{(\beta)}$, and

(ii) for any number $i$ and formula $\psi$ with rank $\beta$, there is a formula $\psi'$ with rank less than $y$ so that $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ is a $\Pi_1^0(\emptyset^{(\beta)})$-subset of $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ for some $\beta' < \gamma$ with difference in measure less than $2^{-i}$.

Note that for any ranked formula $\psi$, if $x \in P_\psi = \{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$, then $P_\psi$ has positive measure.