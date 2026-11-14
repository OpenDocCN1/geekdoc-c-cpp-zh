Proof. Note that the set $\{\ulcorner \varphi \urcorner \mid \text{rank}(\varphi) \text{ is at most } \beta\}$ is r.e. and hence $\Delta_1^1$. By Theorem 5.1.1, both the sets $\{(x, \ulcorner \varphi \urcorner) \mid \text{rank}(\varphi) \text{ is at most } \beta \land \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi\}$ and $\{(x, \ulcorner \varphi \urcorner) \mid \text{rank}(\varphi) \text{ is at most } \beta \land \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \neg \varphi\}$ are $\Pi_1^1$ and hence $\Delta_1^1$.

# 5.1.2 Characterizing $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$

**Proposition 5.1.3.** For any real $z, z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ if and only if there is an $m \in \mathbb{O}$ such that $z \le_T H_m^x$.

Proof. Suppose that $z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x})$. Then there is a ranked formula $\varphi(n)$ such that \( n \in z \Leftrightarrow \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi(n) \).

By Corollary 5.1.2, the set \( C = \{\langle x, n \rangle \mid \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \models \varphi(n)\} \) is $\Delta_1^1$. By the $\Pi_1^1$-Uniformization Theorem (4.2.1), there is a total $\Pi_1^1$ and hence $\Delta_1^1$ function \( f : 2^\omega \to \omega \) such that \( f(x) = m \) if and only if \( m \in O^x \) and \( (\exists \beta)(\forall n)(n, x \in C \leftrightarrow \mathfrak{A}_m^{f(x)}(n) = 1) \). By relativized $\Sigma_1^1$-boundedness (Corollary 1.5.2), there is an ordinal \( \beta < \omega_1^{CK} \) such that \( f(x)|_x \le \beta \) for all \( x \). Thus if \( z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \), then there is an \( m \in \mathbb{O} \) such that \( z \le_T H_m^x \).

For the other direction, suppose there is an \( m \in \mathbb{O} \) such that \( z \le_T H_m^x \). It suffices to prove that \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \). We show this by induction on \( |m| \).

Suppose that \( m = 2^n \). Then \( H_m \in \mathfrak{A}(m|1+x) \). So \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \).

Suppose that \( m = 3 \cdot 5^n \) and \( H_n^x \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \) for all \( n < m \). Then \( i \in H_m^x \) if and only if

\(\mathfrak{A}(m|1+x) \equiv (\exists m'(\exists \beta)[\exists \beta](\hat{H}(f_C(\mathbf{l}), z^{m'|\mathbf{l}}, \mathbf{x}) \wedge \mathbf{l} = \langle j, l \rangle \wedge j \ge z^{m'}])\).

Thus \( H_m^x \in \mathfrak{A}(m|1+2, \mathbf{x}) \).

Theorem 2.3.3 and Proposition 5.1.3 immediately give the following

**Corollary 5.1.4.** Suppose that \( \omega_1^x = \omega_1^{CK} \). Then for any \( z, z \in \mathfrak{A}(\omega_1^{CK}, \mathbf{x}) \) if and only if \( z \le_h x \). In particular, \( z \) is hyperarithmetic if and only if \( z \in \mathfrak{A}(\omega_1^{CK}, \emptyset) \).

# 5.1.3 $\Delta_1^1$-comprehension

The $\Delta_1^1$-comprehension scheme states:

\( (\forall n)((\exists z)\varphi(n, z) \to (\forall z)\psi(n, z)) \to (\exists y)(\forall n)(n \in y \leftrightarrow (\exists z)\varphi(n, z)) \).

where both \(\varphi(n, z)\) and \(\psi(n, z)\) are arithmetical. In forcing constructions, satisfying $\Delta_1^1$-comprehension in $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ is used to guarantee \(\omega_1^x = \omega_1^{CK}\), as shown by the following theorem.

**Theorem 5.1.5.** \(\omega_1^x = \omega_1^{CK}\) if and only if $\mathfrak{A}(\omega_1^{CK}, \mathbf{x})$ satisfies the $\Delta_1^1$-comprehension axiom.