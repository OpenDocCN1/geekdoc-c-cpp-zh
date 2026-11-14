Hence the set of \(\Delta^1_1\)-Kurtz random reals is \(\Sigma^1_1\). Now \(\mu(E) = 1\), and since no hyperarithmetic real is \(\Delta^1_1\)-Kurtz random, by Theorem 13.11.3 one concludes that \(E\) is not \(\Delta^1_1\).

# Theorem 14.1.3 (Kjos-Hanssen, Nies, Stephan and Yu [68]). \(\Pi^1_1\)-Kurtz randomness \(\subset \Sigma^1_1\)-Kurtz randomness \(= \Delta^1_1\)-Kurtz randomness.

Proof. It is obvious that \(\Pi^1_1\)-Kurtz randomness \(\subseteq \Sigma^1_1\)-Kurtz randomness \(\subseteq \Delta^1_1\)-Kurtz randomness. We show that the first inclusion is proper. Let

```
\(R(\langle e, n \rangle, z) \Leftrightarrow n \in \emptyset \wedge \Phi_e^\emptyset \in \Sigma^1_1 \wedge \exists z \in \Phi_e^\emptyset \wedge\)
\((\mu(A_\sigma) > 1 - 2^{-(e,n)}).\)
```

By Proposition 13.16.1, \(R\) is \(\Pi^1_1\) and by Theorem 4.2.1, there is a \(\Pi^1_1\)-function \(f: \omega \to 2^{<\omega}\) uniformizing \(R\). Let

```
\(C = \{y \mid (\forall m)(f(m) \downarrow \to y \in A_{f(m)})\}.\)
```

Then \(C\) is a closed \(\Sigma^1_1\)-set and \(\mu(C) \ge 2^{-1}\). Note that if \(z_1 \in \Sigma^1_1 \cap \text{HYP}\) and \(\mu(A_{z_1}) > p\) for some \(p\), then there is a finite \(z \le z_1\) in \(\Sigma^1_1 \cap \text{HYP}\) such that \(\mu(A_z) > p\). By Proposition 14.1.2, every real in \(C\) is \(\Delta^1_1\)-Kurtz random. Since \(C\) is closed and \(\Sigma^1_1\), it can be presented by a \(\Sigma^1_1\)-tree. By Theorem 11.1.2, there is an \(x \in C\) such that \(x \equiv_h \emptyset\). Let \(e\) and \(n \in \emptyset^\circ\) be such that \(x = \Phi_e^{H_n^\emptyset}\). Then

```
\(z \in \{x\} \Leftrightarrow (\exists y \le_P x)(y \in \{0\} \Leftrightarrow x = \Phi_e^{H_n^\emptyset}).\)
```

In other words, \(x\) is a \(\Pi^1_1\)-singleton which is therefore not \(\Pi^1_1\)-Kurtz random.

We now show that every \(\Delta^1_1\)-Kurtz random real is \(\Sigma^1_1\)-Kurtz random. Let \(A\) be a \(\Pi^1_1\)-open set of measure 1. Define \(X = \{ \sigma \in 2^{<\omega} (\forall y)(\forall \sigma \to y \in A) \}\). Then \(x\) is a \(\Pi^1_1\)-real coding \(A\) (i.e. \(y \in A\) if and only if there is a \(\sigma \in x\) such that \(y \in A_\sigma\)). Hence there is a recursive function \(f : 2^{<\omega} \to \omega\) such that \(\sigma \in x\) if and only if \(f(\sigma) \in \emptyset\). Define a \(\Pi^1_1\)-relation \(R \subseteq \omega \times \omega\) such that \((k, n) \in R\) if and only if \(n \in \emptyset\) and \(\mu(\bigcup \{ \sigma \mid \exists m \in \emptyset_n)(f(\sigma) = m) \}) > 1 - \frac{1}{k}\). Clearly \(R\) is a \(\Pi^1_1\)-relation which can be uniformized by a \(\Pi^1_1\)-function \(f\). Since \(\mu(A) = 1\), \(f\) is a total function. Thus the range of \(f\) is bounded by a notation \(n \in \emptyset\). Define \(B = \{ y \mid (\exists \sigma)(y > \sigma \land f(\sigma) \in \emptyset_n) \}\). Then \(B \subseteq A\) is a \(\Delta^1_1\)-open set with measure 1. It follows that every \(\Pi^1_1\)-open co-null set has a \(\Delta^1_1\)-open co-null subset. Hence \(\Sigma^1_1\)-Kurtz randomness \(= \Delta^1_1\)-Kurtz randomness.

The following result clarifies the connection between \(\Delta^1_1\) and \(\Pi^1_1\)-Kurtz randomness.

# Proposition 14.1.4. If \(\omega_1^x = \omega_1^{CK}\), then \(x\) is \(\Pi^1_1\)-Kurtz random if and only if \(x\) is \(\Delta^1_1\)-Kurtz random.

Proof. Suppose that \(\omega_1^x = \omega_1^{CK}\) and \(x\) is \(\Delta^1_1\)-Kurtz random. If \(A\) is a \(\Pi^1_1\)-closed nullset such that \(x \in A\), then by the Spector-Gandy Theorem 3.7.3, there is an arithmetic formula \(\varphi(z, y)\) such that the formula \((\exists z \in \text{HYP})\varphi(z, y)\) defines \(A\). Since \(\omega_1^x = \omega_1^{CK}\), there is a recursive ordinal \(\beta\) such that

```
\(x \in B = \{ y \mid \exists \beta(\omega_1^{CK}, y) = (\exists \beta 2^\beta)(\varphi(x^\beta, y) \subseteq A \}.\)
```