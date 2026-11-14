# 14.2.4 Strong \(\Pi^1_1\)-Martin-Löf randomness

A sequence of open sets \(\{U_n\}_{n<\omega}\) is a *generalized Martin-Löf test* (ML test) if \(\lim_{n\to\infty} \mu(U_n) = 0\). Given a class \(\Gamma\) of sets of reals (e.g. \(\Pi^1_1\)), \(\{U_n\}_{n<\omega}\) is a generalized \(\Gamma\)-ML test if \((\sigma, n) \mid \sigma \in 2^{<\omega} \wedge \sigma \in U_n\} \in \Gamma\).

**Definition 14.2.11.** Given a class \(\Gamma\) of sets of reals, \(x\) is strongly \(\Gamma\)-ML random if \(x \notin \bigcap_{n<\omega} U_n\) for any generalized \(\Gamma\)-ML test \(\{U_n\}_{n<\omega}\).

Obviously every strongly \(\Pi^1_1\)-ML random real is \(\Pi^1_1\)-ML random.

**Lemma 14.2.12.** If \(x\) is the leftmost path of a \(\Sigma^1_1\)-closed set of reals, then \(x\) is not strongly \(\Pi^1_1\)-ML random.

Proof. Let \(P\) be a \(\Sigma^1_1\)-closed set. Then there is a \(\Sigma^1_1\)-tree \(T \subseteq 2^{<\omega}\) such that \(P = [T]\). By the Gandy–Spector Theorem (3.71), there is a \(\Sigma_0\)-formula \(\varphi(\sigma, \beta)\) such that \(\sigma \in T \Leftrightarrow (L_{\omega_1^{CK}}, \in) \models (\forall \beta) \varphi(\sigma, \beta)\).

For \(\beta < \omega_1^{CK}\), let \(T[\beta] = \{\sigma \mid (L_{\omega_1^{CK}}, \in) \models (\forall \gamma \le \beta) \varphi(\sigma, \gamma)\}\).

For \(n < \omega\) and \(\beta < \omega_1^{CK}\), let \(U_{n,\beta} = \{\sigma \mid (\exists z)(z \text{ is the leftmost path in } T[\beta] \cap [\sigma] \wedge \sigma \sqsubset z \nmid n+1)\}\).

Define \(U_{n,<\beta} = \bigcup_{\gamma < \beta} U_{n,\gamma}\)

and \(U_n = \bigcup_{\beta < \omega_1^{CK}} U_{n,\beta}\).

The following facts are straightforward to verify: For \(n < \omega\) and \(\beta < \omega_1^{CK}\),

+   (1) \(U_{n+1,\beta} \subseteq U_{n,\beta}\);
+   (2) \(\mu(U_{n,\beta}) < 2^{-n}\);
+   (3) \(x \in \bigcap_{n<\omega} U_n\);
+   (4) for any \(z\), if \(z \in U_{n,<\beta} \setminus U_{n,\beta}\), then \(z \notin U_{n,\gamma}\) for any \(\gamma \ge \beta\).

Now suppose that \(\mu(\bigcap_{n<\omega} U_n) > 0\). Then there is a \(\sigma_0\) such that \(\mu(\bigcap_{n<\omega} U_n \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\).

Let \(n_0 = |\sigma_0| + 2\). Then there is a \(\beta_0 < \omega_1^{CK}\) such that \(\mu(U_{n_0,<\beta_0} \cap [\sigma_0]) > \frac{3}{4} \cdot 2^{-|\sigma_0|}\).