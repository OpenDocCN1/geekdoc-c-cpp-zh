\(\tau > \alpha)\) is wellfounded. Since \(L^K_{\omega_1^{CK}}\) is admissible, there is an \(h_\sigma : T_\sigma \to \omega^{CK}_1\) in \(L^K_{\omega_1^{CK}}\) such that for any \(r_1 >_T r_0\) in \(T_\sigma\), \(h_\sigma(r_1) < h_\sigma(r_0)\). Hence there is a \(\beta_\sigma \in \omega^{CK}_1\) such that \(h_\sigma \in L_{\beta_\sigma}\). Since \(\omega^{CK}_1 \backslash f_n \mid m \in L_{\alpha_\beta}\), by Theorem 3.3.2 and the \(\Sigma\)-Collection Theorem (3.1.6), there is a \(\beta^m < \omega^{CK}_1\) such that \(\beta_\sigma < \beta_m\) for all \(\sigma \in \omega^m \backslash f_n \mid m\}\). By Theorem 3.1.6 again, there is a \(\beta < \omega^{CK}_1\) which is an upper bound of all the \(\beta_m\)\('s\). Then \(\sigma < f_n\) if and only if

\(\langle L_\beta, \in \rangle \models (\forall \tau \in \omega^{|\alpha|} \langle \alpha \rangle)(\exists \beta)(\exists \gamma)(\forall r_1, r_2 \in T_\sigma)(h : T_\tau \to \gamma \wedge r_2 >_T r_1 \to h(r_2) < h(r_1)).\)

Thus \(f_n \in L_{\beta+1} \subset L^K_{\omega_1^{CK}}\).

Suppose that \(x \in L^K_{\omega_1^{CK}}\). Since \(L^K_{\omega_1^{CK}}\) is admissible, we have \(\omega^x_1 = \omega^{CK}_1\). Assume that \(x\) is not hyperarithmetic. Define

\(\mathscr{X} = \{E \mid \langle \omega, E \rangle \text{ nicely codes an } \omega\text{-model of KP}\}.\)

By Proposition 3.6.5, \(\mathscr{X}\) is a \(\Delta^1_1\)-set. By the Kreisel Basis Theorem (2.5.6), there is an \(E_0 \in \mathscr{X}\) with \(\omega^{E_0}_1 = \omega^{CK}_1\) and \(x \notin E_0\). Let \(\langle M, \in \rangle\) be the \(\omega\)-model coded by \(\langle \omega, E_0 \rangle\) and let \(M_1\) be the standard part of \(M\). Then every real \(z \in M_1\) is recursive in \(E_0\). Hence \(x \notin M_1\). By Proposition 3.5.5, \(L^K_{\omega^x_1} \subset M_1\). Thus \(x \notin L^K_{\omega^x_1}\).

This gives a model-theoretic characterization of the set of hyperarithmetic reals:

**Corollary 3.6.9.** A real \(x\) is hyperarithmetic if and only if it belongs to every \(\omega\)-model of KP.

**Proof.** By Theorem 3.6.8, \(x\) is hyperarithmetic if and only if \(x \in L^K_{\omega^x_1}\). By Theorem 3.5.5 and Corollary 3.6.7, \(x \in L^K_{\omega^x_1}\) if and only if \(x\) belongs to every \(\omega\)-model of KP.

# 3.6.5 The Cantor-Bendixson construction revisited

We now return to the recursion-theoretic proof of Theorem 1.1.10 and calculate the least ordinal \(\gamma\) for which \(T_{\gamma+1} = T_\gamma\).

**Proposition 3.6.10.** Suppose \(T \subset \omega^{<\omega}\) is a recursive tree with uncountably many infinite paths. Then there is a \(\Sigma_1(L_{\omega_1^{CK}})\)-function \(f : \omega^{CK}_1 \to L_{\omega_1^{CK}}\) such that for any \(\gamma_1 < \gamma_2 < \omega^{CK}_1\), \(f(\gamma_2) = T_{\gamma_2} \subseteq f(\gamma_1) = T_{\gamma_1} \subseteq T\) and \(\cap_{\gamma < \omega^{CK}_1} T_\gamma\) is a perfect subtree of \(T\).

**Proof.** Since \(T\) is recursive, we have \(T \in L_{\omega+1}\). By Theorem 3.1.8, there is a \(\Sigma_1(L_{\omega_1^{CK}})\)-function \(f : \omega^{CK}_1 \to L^K_{\omega_1^{CK}}\) such that

+   - \(f(0) = T\);
+   - for any \(\gamma < \omega^{CK}_1\), \(f(\gamma + 1) = T_{\gamma+1} = \{\sigma \in T_\gamma \mid (\exists r_0, \tau_1 > \sigma)(\tau_0, r_1 \in T_\gamma \wedge \tau_0 \perp_T \tau_1 | r_1)\} \subseteq f(\gamma)\);
+   - if \(\gamma\) is a limit ordinal, then \(f(\gamma) = T_\gamma = \cap_{\beta < \gamma} T_\beta\).