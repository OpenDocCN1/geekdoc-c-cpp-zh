Exercise 14.3.4. Prove that there is a \(\Sigma^1_1\)-set \(A\) and a \(\Pi^1_1\)-ML random \(x \in A\) such that \(\lim_{n \to \infty} \frac{\mu(A[n|x])}{2^{-n}} = 0\).

Exercise 14.3.5. Prove that every \(x \notin\) HYP hyperarithmetically reducible to a \(\Pi^1_1\)-random real is \(\Pi^1_1\)-random relative to a continuous measure.

Exercise 14.3.6 (Kjos-Hanssen and Yu). Let \(\Phi\) be a universal partial \(\Pi^1_1\)-function from \(\omega\) to 2, and assume that \(x(n) \neq \Phi(n, e)\) for each \(e\). Show that \(x\) hyperarithmetically computes some member of a given nonempty \(\Sigma^1_1\)-closed subset of \(2^\omega\).

Exercise 14.3.7 (Greenberg, Montalbán and Slaman [39]; Kulikumin and Nies). Suppose that \(\mathbb{M}\) is a structure such that the set \(A = \{x \mid (\exists N \le_T x)(N \equiv \mathbb{M})\}\) has measure 1. Prove that every \(\Pi^1_1\)-random real is in \(A\).

Exercise 14.3.8 (Kripke [120]). If \(A\) is a nullset of hyperdegrees such that \(\mathbf{0} \notin A\), then the set \(U_K(A) = \{x \mid (\exists y \in A)(x \ge_T y)\}\) is also null.

# 14.4 \(\Delta^1_2\) and \(\Sigma^1_2\)-randomness

# 14.4.1 \(\Delta^1_2\)-randomness

Since there is a \(\Delta^1_1\)-real which is \(\Pi^1_1\)-random, \(\Delta^1_2\)-randomness is strictly stronger than \(\Pi^1_1\)-randomness. By Corollary 13.1.7 and Proposition 13.1.12, we have the following conclusion.

Proposition 14.4.1. Assume that \(\omega^L_1 < \omega_1\). Then \(\Delta^1_2\)-randomness = \(\Delta^1_2\)-ML randomness = \(\Pi^1_2\)-randomness.

# 14.4.2 \(\Sigma^1_2\)-ML randomness

Let \(\{\varphi_n(\sigma)\}_{n < \omega}\) be a recursive enumeration of \(\Sigma^1_1\)-formulas. There is a \(\Sigma_1\)-formula \(\psi(n, \sigma)\) (in set theory) such that

\(\varphi_n(\sigma) \leftrightarrow (\exists X)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega^X_1}, \in \rangle \models \psi(n, \sigma)).\)

Let \((n, \sigma) \in U\) if and only if

\((\exists x)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega^x_1}, \in \rangle \models \psi(n, \sigma)) \land \mu(\{z \mid (\exists m)(\langle L_{\omega^z_1}, \in \rangle \models \psi(n, z \mid m))\}) < 2^{-n}.\)

One may view \((n, \sigma) \in U\) as an enumeration of strings \(\sigma\) in \(U\) up to any stage coded by a \(\Pi^1_1\)-singleton where the measure is less than \(2^{-n}\). We leave it to the reader to verify that \(U\) is \(\Sigma^1_2\). Then the set \(\{U_n\}_{n < \omega}\), where \(U_n = \{\sigma \mid (n, \sigma) \in U\}\), is a universal \(\Sigma^1_2\)-ML test.