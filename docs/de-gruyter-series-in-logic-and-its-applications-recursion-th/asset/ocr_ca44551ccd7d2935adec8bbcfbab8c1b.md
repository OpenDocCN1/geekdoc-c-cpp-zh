# **Lemma 6.3.4.**

(i) For each \(i \in I\), \(D_{0,i} = \{p \in \mathbf{P} \mid x_i \subseteq \text{Dom}(p)\}\) is dense. (ii) For each \(i \in X\) and \(i \in \omega\), \(D_{1,i} = \{p \in \mathbf{P} \mid |\{n \in x_i \mid p(n) = 1\}| > i\}\) is dense.

**Proof.** (i) is obvious. To see (ii), given any condition \(p\), we have \(|\text{Dom}(p) \cap x_i| < \infty\). Then simply extend \(p\) to a condition \(q\) such that \(|\{n \in x_i \mid q(n) = 1\}| > i\).

# **Theorem 6.3.5.**

If \(G\) is a generic set meeting all \(D_{0,i}\)’s and \(D_{1,i}\)’s for all \(i \in I\), then the generic set \(g = \bigcup_{p \in G} p\) is a real such that for any \(i \in I, x \in X\) and only if \(g \cap x_i\) is infinite.

**Proof.** Let \(G\) be a generic meeting all \(D_{0,i}\)’s and \(D_{1,i}\)’s for all \(i \in I\). If \(i \in X\), then by (ii) of Lemma 6.3.4, \(x_i \cap g\) is infinite. If \(i \notin X\), then by (i) of Lemma 6.3.4, \(x_i \subseteq \text{Dom}(p)\) for some \(p \in G\). But \(|\{n \mid p(n) = 1\}| < \infty\), and so \(x_i \cap g\) is finite.

Hence almost disjoint forcing produces a real \(g\) which codes a large set \(X\) via an almost disjoint set \(A\).

# 6.3.2 Martin–Solovay's characterization

# **Lemma 6.3.6.**

Assume \(\text{MA}_{\aleph_1}\) and suppose that \((\omega_1)^{1[x]} = \omega_1\) for some \(x \in 2^\omega\). If \(B \subseteq 2^\omega\) has cardinality \(\aleph_1\), then \(B\) is \(\Pi^1_1\).

**Proof.** We assume that \(x(0) = 1\) for any \(x \in B\).

Since \((\omega_1)^{1[x]} = \omega_1\), let \(C = \{z \mid z(0) = 0 \wedge z \in L_{\omega_1^{1[x]}}[z \oplus x]\}\). Then \(C\) is a \(\Pi^1_1\)-set of cardinality \(\aleph_1\).

Let \(f : \omega \to 2^\omega\) be a recursive bijection. Define

\(T = \{t \in 2^{<\omega} \mid (\exists \tau \in 2^{<\omega})(\forall n < |t|)(t(n) = 1 \mapsto f(n) \prec \tau)\}.\)

Note that \(|T|\) is an almost disjoint set tree. Moreover \(T\) is a recursive perfect tree and there is a recursive homomorphism \(h : 2^\omega \to [T]\). Also note that any \(x \in [T]\) is recursive in each of its infinite subsets. Let \(C_0 = \{y \mid (\exists x \in C)(h(x) = y)\}\) and \(B_0 = \{y \mid (\exists x \in B)(h(x) = y)\}\). Suppose \(p_0, p_1, \dots\) is a recursive enumeration of the prime numbers. Let

+   \(B_0 = \{x_a\}_{a < \aleph_1},\)
+   \(C_0 = \{y_a\}_{a < \aleph_1},\)
+   \(B_1 = \{x_{a,n} \mid (\forall i \in \omega)(x_{a,n}(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } x_a))\}\)

and

\(C_1 = \{y_{a,n} \mid (\forall i \in \omega)(y_{a,n}(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } y_a))\}.\)

Set \(B = B_0 \cup C_0\). Then \(A\) is almost disjoint, and \(x \in C_1\) if and only if

+   (i) there is a \(z \le_T x\) and an \(n \in \omega\) such that \(z \in C_0\), and
+   (ii) \((\forall i \in \omega)(x(i) = 1 \leftrightarrow (\exists j)(i \text{ is the } p_n^j\text{-th element of } z))\).