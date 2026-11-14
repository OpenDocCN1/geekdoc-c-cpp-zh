guarantees the existence of a uniformization function for P. However, our interest is in strong uniformization, i.e. a function that uniformizes “initial segments of reals” that does roughly the following: if X codes a set of reals in \(\epsilon\) such that any two elements \(w <_L z\) in x satisfy P(w, z), then there is a “least” \(y \in \epsilon\) such that \(x \le y\) and P(x, y) holds. This strong uniformization property enables one to implement an inductive construction which is made precise by the \(\Pi^1_1\)-inductive principle \(\exists\) defined as follows:

# \(\Pi^1_1\)-inductive principle 3. If P(x, y) is \(\Pi^1_1\) and cofinally progressive, then there is a \(\Pi^1_1\)-set \(A \subseteq \epsilon\) such that:

+   (i) \(|\le_L| A\), the height of \(\le_L\) restricted to A, is \(\omega_1\);
+   (ii) \((\forall y)(y \in A \to (\exists x)(x \in L_{\omega_1^y} \wedge x \text{ codes the set } \{z \mid z \in A \wedge z <_L y\} \wedge P(x, y)))\).

# Theorem 8.2.3 (Chong and Yu [17]). V = L implies \(\exists\).

Proof. Suppose V = L, and P is \(\Pi^1_1\) and cofinally progressive. Recall that for each constructibly countable \(\beta\), there is an \(\alpha > \beta\) such that \((L_{\alpha+1} \setminus L_\alpha) \cap 2^\omega \neq \emptyset\). Given ordinals \(\beta < \alpha\) and \(X \subseteq \alpha \omega\), denote by \(X[\beta]\) the real \(n \mapsto (\beta, n) \in X)\). We may regard X as a sequence of reals of length \(\alpha\).

Since P is \(\Pi^1_1\), by the Spector–Gandy Theorem (3.71) there is a \(\Sigma_0\)-formula \(\psi(x, y, s)\) such that

\(P(x, y) \Leftrightarrow (L_{\omega^{xy}}[x, y], \in) \models (\exists s)\psi(x, y, s).\)

Assume V = L. We define a partial function F which we will show to be total on \(\omega_1 \times \bigcup_{\alpha < \omega_1} 2^{\alpha \omega}\). For \(\alpha < \omega_1\), \(z \in 2^\omega\) and \(X \subseteq \alpha \omega\), let \(\omega_1^{X,z}\) be the least ordinal \(\gamma\) such that \(L_\gamma[X, z]\) is admissible. We define \(F(\alpha, X)\) to be the real z such that \(L_{\omega_1^{X,z}}[X, z]\) satisfies the following properties:

+   (1) there is a \(\beta \ge \alpha\) such that \(z \in L_{\beta+1} \setminus L_\beta\);
+   (2) there is an \(x \in L_{\omega_1^{X,z}}\) which codes X;
+   (3) there is a limit ordinal \(\gamma\) and an element \(s \in L_\gamma\) such that \(L_\gamma[X, z] \models \psi(x, z, s)\);
+   (4) if \((t, y) \prec_L (s, z, y)\), then \((L_\mu[X, y], \in) \models \psi(x, y, t)\) implies \(\omega_1^{(X,y)} < \beta\);
+   (5) if \((t, y) \prec_L (s, z, y)\) and \((L_\mu[X, y], \in) \models \psi(x, y, t)\), then either no real \(t \in L_{\omega_1^{X,y}}\) codes X or \(y \in L_{\omega_1^{(t,y)}}\).

Since \(L_{\omega_1^{X,z}}[X, z] = L_{\omega_1^{X,z}} \prec_L\) is uniformly \(\Delta_1\) in \(L_{\omega_1^{X,z}}[X, z]\). Moreover, (4) implies that (5) is \(\Sigma_1\) in \(L_{\omega_1^{X,z}}[X, z]\). We show that \(F(\alpha, X)\) is defined for \(\alpha < \omega_1\) if X is countable.

Fix (a, X). Since V = L, there is a countable \(\gamma' > \alpha\) with a real \(x \in L_{\gamma'}\) coding X. Since P is cofinally progressive, by Lemma 8.2.2 there is a \(\beta > \gamma'\) such that \((L_{\beta+1} \setminus L_\beta) \cap 2^\omega \neq \emptyset\), and a real \(z \in L_{\beta+1} \setminus L_\beta\) such that \(x \in z \prec \omega_1^{X,z} \models \psi(x, z, s)\) for some limit ordinal \(\gamma < \omega_1^z\) and \(s \in L_\gamma\). Note that \(L_{\omega_1^z} = L_{\omega_1^{X,z}}[X, z]\) and \(\gamma' = L_\gamma[X, z]\) for all sufficiently large \(\gamma' < \omega_1^z\). Hence (1)–(3) are satisfied. Clearly we can assume that \((s, z, y)\) is the \(<_L\)-least satisfying these properties. Thus (4) and (5) are satisfied as well. By the absoluteness of \(<_L\), one concludes that F is a well-defined function on each \((\alpha, X)\), where \(\alpha < \omega_1\) and X is countable.