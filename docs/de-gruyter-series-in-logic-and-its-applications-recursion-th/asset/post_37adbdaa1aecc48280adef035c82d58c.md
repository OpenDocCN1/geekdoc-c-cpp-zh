
Proof. Let \(\hat{U} \subseteq \omega \times 2^{<\omega}\) be a universal \(\Pi^1_1\)-set, i.e. \(\hat{U}\) is \(\Pi^1_1\) and every \(\Pi^1_1\)-set \(\hat{V} \subseteq 2^{<\omega}\) is \(\hat{U}_n = \{ \sigma \mid (n, \sigma) \in \hat{U} \}\) for some \(n\). Then there is a recursive function \(f : \omega \times 2^{<\omega} \to \omega\) such that \((n, \sigma) \in \hat{U} \Leftrightarrow (n, \sigma) \in \emptyset\).

\(\hat{V} = \{ (n, \sigma) \mid (n, \sigma) \in \hat{U} \wedge \sum_{(3k \in O_{(n, \sigma)}) \cap (f(n, r) = k)} 2^{-|\Gamma|} < 2^{-n} \}.\)

In other words, \((n, \sigma)\) is enumerated into \(\hat{V}\) if the measure of \(\hat{U}_n\) up to stage \(f(n, \sigma)\) is less than \(2^{-n}\).

\(U = \{ (n, \sigma) \mid (\exists m)(m \ge n + 1 \wedge (m, \sigma) \in \hat{V}) \}.\)

Then \(U\) is \(\Pi^1_1\) as well. Setting \(U_n = \{ \sigma \mid (n, \sigma) \in U \}\), we have

\(\mu(U_n) < \sum_{m \ge n+1} 2^{-m} = 2^{-n}.\)

Hence \(\{ U_n \}_{n < \omega}\) is a \(\Pi^1_1\)-ML test. By the universality of \(\hat{U}\), \(\{ U_n \}_{n < \omega}\) is a universal \(\Pi^1_1\)-ML test. \(\square\)

### **Corollary 14.2.6** (Hjorth and Nies [51])

- (i) There is a \(\Sigma^1_1\)-closed set of positive measure of \(\Pi^1_1\)-ML random reals.
- (ii) For every \(z \ge_T \emptyset\), there is a \(\Pi^1_1\)-ML random \(x \equiv_T z\).

Proof. (i) follows immediately from Proposition 14.2.5, while (ii) is a consequence of (i) and Theorem 11.1.2. \(\square\)

The following result says that every \(\Sigma^1_1\)-closed set of positive measure essentially contains all the \(\Pi^1_1\)-ML random reals.

### **Proposition 14.2.7.** Suppose that \(T \subseteq 2^{<\omega}\) is a \(\Sigma^1_1\)-tree with \(\mu([T]) > 0\). Then for any \(\Pi^1_1\)-ML random \(x\), there is a \(z \in [T]\) such that \(z =^* x\), i.e. \((\exists m)(\forall n \ge m)(x(n) = z(n))\).

Proof. Let \(T \subseteq 2^{<\omega}\) be as given. For any \(n \ge 0\), let

\(U^n = \{ \sigma_0^* \sigma_1 \dots \sigma_n^* \mid (\forall i \le n)(\sigma_i \notin T) \}.\)

Then \(\{ U^n \}_{n < \omega}\) is a \(\Pi^1_1\)-ML test. Moreover, \(\mu(U^n) = \mu(2^{<\omega} \setminus [T]) = 1 - \mu([T])\). For any \(n\), \(\mu(U^{n+1}) = \mu(U^n) \cdot (1 - \mu([T])) = (1 - \mu([T]))^{n+2}\). Let \(V_n = \bigcup_{m \ge n} U^m\). Then \(\mu(V_n) \le \sum_{m \ge n} (1 - \mu([T]))^{n+1}\) and hence \(\{ V_n \}_{n < \omega}\) can be viewed as a \(\Pi^1_1\)-ML test. It follows that there is a least \(n\) such that \(x \notin V_n\). If \(n = 0\), then \(x \in [T]\). Otherwise there is a \(\sigma_0^* \sigma_1 \dots \sigma_{n-1} < x\) so that \(x = \sigma_0^* \sigma_1 \dots \sigma_{n-1} z\) for some \(z \in [T]\). Hence \(x =^* z\). \(\square\)

## 14.2.3 Separating \(\Pi^1_1\)-Martin-Löf randomness from \(\Delta^1_1\)-randomness

Define a notion of forcing \(\mathbf{D} = \langle \mathbf{D}, \le \rangle\) as follows:

- (i) \(P \in \mathbf{D}\) if and only if \(P \subseteq 2^\omega\) is \(\Delta^1_1\)-closed and of positive measure;
- (ii) for any \(P, Q \in \mathbf{D}\), \(P \le Q\) if and only if \(P \subseteq Q\).

Suppose \(U \subseteq \omega \times 2^{<\omega}\) is \(\Delta^1_1\) and \(U_n = \{ \sigma \mid (n, \sigma) \in U \}\). Assume \(\lim_{n \to \infty} \mu(U_n) = 0\) and let

\(\mathscr{D}_U = \{ P \mid P \in \mathbf{D} \wedge P \cap (\bigcap_{n < \omega} U_n) = \emptyset \}.\)

### Lemma 14.2.8. \(\mathscr{D}_U\) is dense.

Proof. Let \(P \in \mathbf{D}\). There is an \(n\) such that \(\mu(U_n) < \mu(P)/2\). Now the complement \(P_0 = 2^\omega \setminus U_n\) has measure greater than or equal to \(1 - \mu(P)/2\). Then \(P_0 \cap P\) is a \(\Delta^1_1\)-closed set and has measure greater than or equal to \(\mu(P)/2\). Thus \(P_0 \cap P \in \mathbf{D}\).

For any \(\Pi^1_1\)-set \(G\), let \(\mathscr{D}_G = \{ P \mid P \in \mathbf{D} \wedge P \cap G = \emptyset \}\).

### Lemma 14.2.9. If \(G\) is a \(\Pi^1_1\)-set consisting only of \(\Delta^1_1\)-random reals, then \(\mathscr{D}_G\) is dense in \(\mathbf{D}\).

Proof. Let \(P \in \mathbf{D}\). Then there is a hyperarithmetic \(x\) such that \(P\) is \(P_0^x(x)\). Without loss of generality, we may assume that for any \(\sigma\), if \([\sigma] \cap P \neq \emptyset\), then \(\mu([\sigma] \cap P) > 0\) (since we may assume that \(P\) contains only 1-\(x\)-random reals). By Theorem 13.11.13, there is a hyperarithmetic \(z\) in \(P\). Hence \(z \notin G\). Since \(G\) is closed, there is an \(n\) such that \([z \nmid n] \cap G = \emptyset\). Let \(Q = [z \nmid n] \cap P\). Then \(Q \in \mathscr{D}_G\).

### Theorem 14.2.10 (Chong, Nies and Yu [12]). \(\Pi^1_1\)-ML randomness \(< \Delta^1_1\)-randomness.

Proof. By Proposition 14.2.2, \(\Pi^1_1\)-ML randomness \(\subseteq \Delta^1_1\)-randomness. By Proposition 14.2.5, let \(\{U_n\}_{n < \omega}\) be a universal \(\Pi^1_1\)-ML test. For \(n < \omega\), let

\(\mathscr{D}_{U_n} = \{ P \mid P \in \mathbf{D} \wedge P \subseteq U_n \}.\)

By Lemma 14.2.9, \(\mathscr{D}_{U_n}\) is dense. By Lemma 14.2.8, there is a \(\Delta^1_1\)-random \(x\) such that for any \(n\), there is a \(P \in \mathscr{D}_{U_n}\) with \(x \in P\). Hence \(x \in \bigcap_{n < \omega} U_n\), i.e. \(x\) is not \(\Pi^1_1\)-ML random.

We remark that \(\mathbf{D}\) is an analog of random forcing \(\mathbf{R}\) discussed in §6.2.2. However, \(\mathbf{R}\) is c.c.c. and so preserves all cardinals while \(\mathbf{D}\) is not c.c.c. in \(L_{\omega_1^{CK}}\). By the proof of Theorem 14.2.10 and Corollary 14.3.2 below, any \(\mathbf{D}\)-generic \(x\) collapses \(\omega_1^{CK}\) and hence does not preserve admissible ordinals.

## 14.2.4 Strong \(\Pi^1_1\)-Martin-Löf randomness

A sequence of open sets \(\{U_n\}_{n<\omega}\) is a *generalized Martin-Löf test* (ML test) if \(\lim_{n\to\infty} \mu(U_n) = 0\). Given a class \(\Gamma\) of sets of reals (e.g. \(\Pi^1_1\)), \(\{U_n\}_{n<\omega}\) is a generalized \(\Gamma\)-ML test if \((\sigma, n) \mid \sigma \in 2^{<\omega} \wedge \sigma \in U_n\} \in \Gamma\).

### Definition 14.2.11. Given a class \(\Gamma\) of sets of reals, \(x\) is strongly \(\Gamma\)-ML random if \(x \notin \bigcap_{n<\omega} U_n\) for any generalized \(\Gamma\)-ML test \(\{U_n\}_{n<\omega}\).

Obviously every strongly \(\Pi^1_1\)-ML random real is \(\Pi^1_1\)-ML random.

### Lemma 14.2.12. If \(x\) is the leftmost path of a \(\Sigma^1_1\)-closed set of reals, then \(x\) is not strongly \(\Pi^1_1\)-ML random.

Proof. Let \(P\) be a \(\Sigma^1_1\)-closed set. Then there is a \(\Sigma^1_1\)-tree \(T \subseteq 2^{<\omega}\) such that \(P = [T]\). By the Gandy–Spector Theorem (3.71), there is a \(\Sigma_0\)-formula \(\varphi(\sigma, \beta)\) such that \(\sigma \in T \Leftrightarrow (L_{\omega_1^{CK}}, \in) \models (\forall \beta) \varphi(\sigma, \beta)\).

For \(\beta < \omega_1^{CK}\), let \(T[\beta] = \{\sigma \mid (L_{\omega_1^{CK}}, \in) \models (\forall \gamma \le \beta) \varphi(\sigma, \gamma)\}\).

For \(n < \omega\) and \(\beta < \omega_1^{CK}\), let \(U_{n,\beta} = \{\sigma \mid (\exists z)(z \text{ is the leftmost path in } T[\beta] \cap [\sigma] \wedge \sigma \sqsubset z \nmid n+1)\}\).

Define \(U_{n,<\beta} = \bigcup_{\gamma < \beta} U_{n,\gamma}\)

and \(U_n = \bigcup_{\beta < \omega_1^{CK}} U_{n,\beta}\).

The following facts are straightforward to verify: For \(n < \omega\) and \(\beta < \omega_1^{CK}\),

- (1) \(U_{n+1,\beta} \subseteq U_{n,\beta}\);
- (2) \(\mu(U_{n,\beta}) < 2^{-n}\);
- (3) \(x \in \bigcap_{n<\omega} U_n\);
- (4) for any \(z\), if \(z \in U_{n,<\beta} \setminus U_{n,\beta}\), then \(z \notin U_{n,\gamma}\) for any \(\gamma \ge \beta\).

Now suppose that \(\mu(\bigcap_{n<\omega} U_n) > 0\). Then there is a \(\sigma_0\) such that \(\mu(\bigcap_{n<\omega} U_n \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\).

Let \(n_0 = |\sigma_0| + 2\). Then there is a \(\beta_0 < \omega_1^{CK}\) such that \(\mu(U_{n_0,<\beta_0} \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\).
