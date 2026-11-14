Proof. Suppose that \(f(\psi) = \gamma\). For any condition \(p\), \(p \Vdash \neg \phi\) if and only if \((\forall q \le p)(q \not\Vdash \phi)\). Fix a condition \(q \le p\) and define \(q'\) so that \(t_{q'} = t_q\) and Case (1) \(t \in \epsilon_p\) or \(h_q(\sigma) > \omega_Y\). Let \(h_{q'}(\sigma) = h_q(\sigma)\); Case (2) otherwise. Let \(h_{q'}(\sigma) = \omega_Y + t_{q,\sigma}\) where \(t_{q,\sigma} = \{\tau \ge \sigma \mid \tau \in t_q\}\). Hence \(\text{Ret}(\omega_Y, q, q')\) holds. By Lemma 5.4.6, \(q \Vdash \phi \Leftrightarrow q' \Vdash \phi\). Thus

\((\forall q \le p)(\text{Range}(h_q) \subseteq \cup_{\sigma \in t_q} h_p(\sigma) + \omega \cdot (\gamma + 1)) \to q \Vdash \phi\).

The theorem now follows from this by applying the \(\Sigma\)-Induction Theorem (3.1.8).

Let \(\{D_i\}_{i<\omega}\) be an enumeration of all dense sets of conditions definable over \((L_\alpha, \in)\). Then there is a sequence \(\{p_i\}_{i<\omega}\) such that \(p_0 \ge p_1 \ge \cdots\) and \(p_i \in D_i\) for each \(i\). Let \(T = \bigcup_{i<\omega} p_i\), and \(h = \bigcup_{i<\omega} h_{p_i}\). The following lemma is immediate.

# **Lemma 5.4.8.** For any \(\gamma < \alpha\), - The set \(D_0^\gamma = \{p \mid (\exists \sigma)(\alpha \in t_p \land h_p(\sigma) = \gamma)\}\) is dense. - The set \(D_1^\gamma = \{p \mid (\forall \sigma)(\alpha \in t_p \land h_p(\sigma) > \gamma \to (\exists r > \sigma)(\tau \in t_p \land h_p(\tau) = \gamma))\}\) is dense.

# **Lemma 5.4.9.** \(\omega_1^T \ge \alpha\).

Proof. By Lemma 5.4.8, for any \(\gamma < \alpha\), there is a \(\sigma \in T\) such that \(h(\sigma) = \gamma\). By induction on \(\gamma\), it is straightforward to verify that the subtree \(T_\sigma = \{\tau \in T \mid \tau \ge \sigma\}\) is well ordered under the Kleene-Brouwer ordering with order type at least \(\gamma\). Hence \(\omega_1^T \ge \alpha\).

The following forcing lemma is proved by a routine argument and is left to the reader.

# **Lemma 5.4.10.** For any sentence \(\phi\), \(\mathfrak{A}(\alpha, T) \models \phi\) if and only if there is a \(p\) with \(t_p \subseteq T\) such that \(p \Vdash \phi\).

# **Lemma 5.4.11.** \(\mathfrak{A}(\alpha, T)\) satisfies the \(\Delta_1^1\)-comprehension axiom.

Proof. Let \(\phi\) and \(\psi\) be arithmetical such that

\(\mathfrak{A}(\alpha, T) \models (\forall n)((\exists z)\phi(n, z) \to (\forall z)\psi(n, z))\).

Then

\(\mathfrak{A}(\alpha, T) \models (\forall n)(\exists z)(\phi(n, z) \lor \neg \psi(n, z))\).

As in the proof of Theorem 5.2.5, there is a \(p\) with \(t_p \subseteq T\) such that

\((\forall q \le p)(\forall n)((\exists r \le q)(r \Vdash (\exists z)\phi(n, z) \lor \neg \psi(n, z)))\).

Hence

\((\forall q \le p)(\forall n)((\exists r \le q)(\exists r')(r \Vdash (\exists z)\phi(n, z') \lor \neg \psi(n, z')))\).

By Lemma 5.4.6 and Lemma 5.4.5, we have an increasing sequence \(\gamma_0 < \gamma_1 < \cdots\) in \(L_\alpha\) such that