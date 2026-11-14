We are now ready to prove Theorem 7.3.2. We establish the case where \(\beta\) is a successor ordinal and leave the limit case to the reader.

Let \(a \in \omega\) so that \([a = \beta\). Fix \(z > \tau_H\) for all \(b <_a\). We may assume that \(z\) is not r.e. in \(H_b\) for any \(b <_a\). Given \(b <_a\) and \(i, j < \omega\), consider the following statement:

\((\forall \sigma \in 2^{<\omega})(\exists n)[(n \notin z \cap \sigma^0 1^n \vdash \neg P_{\Phi(b,i)}(x,j)) \lor\)
\((n \notin z \land (\exists \tau \supseteq \sigma^0 1^n)(\tau \vdash P_{\Phi(b,j)}(x,i)))]\). \((\sharp_{b,(i,j)})\)

Since \(z\) is not r.e. in \(H_b\) for \(b <_o a\), by Lemma 7.3.4, \((\sharp_{b,n})\) is true for every \(b <_o a\) and \(n < \omega\). We construct \(g\) in stages as the union of the sequence \(\{g_s\}_{1 \le s < \omega} 2^{<\omega}\) with \(g_0 < g_1 < g_2 < \cdots\).

Let \(\langle \langle b_s, \langle i_s, j_s \rangle \rangle \rangle_{s < \omega}\) be an enumeration of \(\{b \mid b <_o a\} \times \omega^2\).

+   Stage 0: Let \(g_0 = \emptyset\).

+   Stage s + 1:

+   Substage 1. Define \(g(s, 1) = g_s \frown z^*(s) \frown H_a(s)\).

+   Substage 2. Define \(g(s, 2) = g(s, 1) \frown 0^{\langle b_s, \langle i_s, j_s \rangle \rangle} 1\).

+   Substage 3.

+   Case (1): \(2^{b_s} \# a\). Define \(g(s, 3) = g(s, 2) \frown 0^{e_s} 1\) where \(e_s\) is an index so that \(\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a}\).

+   \((b_s = 2^c\) for some \(c)\) or \(\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a} (b_s = 3 \cdot 5^e\) for some \(e)\).

+   Case (ii): \(2^{b_s} = a\). Let \(g(s, 3) = g(s, 2) \frown 0^{e_s} 1\) where \(e_s\) is an index such that \(\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a} (b_s = 2^c\) for some \(c)\) or \(\Phi_{e_s}^z = \Phi_{H_a(b_s)}^{H_a} (b_s = 3 \cdot 5^e\) for some \(e)\).

+   Substage 4. Find the least \(n\) such that either

\(n \notin z \land g(s, 3) \frown 0^n 1 \vdash \neg P_{\Phi(b,i_s)}(x, j_s)\)

or

\(n \notin z \land (\exists \tau \supseteq g(s, 3) \frown 0^n 1)(\tau \vdash P_{\Phi(b,j_s)}(x, j_s))\).

By \((\sharp_{b,(i_s,j_s)})\), such a number \(n\) exists. If it satisfies the first half of the disjunction, define \(g_{s+1} = g(s, 3) \frown 0^n 1\). Otherwise, select the lexicographically least \(\tau\) such that \(\tau \supseteq g(s, 3) \frown 0^n 1\) and \(\tau \vdash P_{\Phi(b,i_s)}(x, j_s))\). Define \(g_{s+1} = g(s, 3) \frown \tau\).

Let \(g = \bigcup_{s < \omega} g_s\).

It is clear that \(g\) is a-generic. By Lemma 7.3.6, \(\hat{H}_g^z \equiv_T g \oplus H_a\). By Lemma 7.3.4, the construction can be decoded by \(g\) in \(H_a\). So \(z \oplus g \le_T g \oplus H_a \equiv_T \hat{H}_g^z\).

To prove that \(z \oplus g \ge_T \hat{H}_g^z\), it is sufficient to decode the construction by \(z \oplus g\) and compute \(H_a\). To do this, we go through the same steps as in the proof of Theorem 7.3.1. Suppose we know \(g_s\). Then \(z(s+1) = g(|g_s|+1)\) and \(H_a(s) = g(|g_s|_2)\). Then one obtains \((b_s, i_s, j_s)\) by calculating \(g(s, 2)\). By calculating \(g(s, 3)\), we find an \(e_s\) such that \(\Phi_{e_s}^z\) computes the set \(\{(\sigma, i_s, j_s) \mid \sigma \vdash P_{\Phi(b,i_s)}(x, j_s)\}\). To compute \(g_{s+1}\), search for the unique number \(n\) such that \((g \mid |g(s, 3)|) \frown 0^n 1 \prec g\). By the construction, either

+   (1) \(n \notin z\) or

+   (2) \(n \notin z\) and there is a \(\tau \supseteq g(s, 3) \frown 0^n 1 (\tau \vdash P_{\Phi(b,i_s)}(x, j_s))\).