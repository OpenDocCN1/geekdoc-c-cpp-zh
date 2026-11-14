(HF, \(\epsilon\), A) and A is \(\Delta_1\)-definable in (HF, \(\epsilon\), x). By Theorem 3.2.5, every \(\Sigma_1\)-definable real in (HF, \(\epsilon\), x) is r.e. in x. Hence every real \(\Sigma_2\)-definable in (HF, \(\epsilon\)) is \(\Sigma_1\)-definable in (HF, \(\epsilon\), A) and so r.e. in x. Thus the \(\Sigma_1\)-master codes are precisely the reals that are r.e. and complete (hence Turing equivalent to \(\emptyset'\)). In general, a real which is a \(\Sigma_n\)-master code in \(\langle J_1, \epsilon \rangle\) is \(\Sigma_n\)-complete and hence Turing equivalent to \(\emptyset^{(n)}\). We may therefore consider master codes to be Turing jumps in the set-theoretic sense. Second, suppose that \(\rho_2^\alpha = 1\). A \(\Sigma_1\)-master code for \(\langle J_\alpha, \epsilon \rangle\) is a set \(A \in HF\) such that every \(\Sigma_2(J_\alpha)\)-definable real is \(\Sigma_1\) in (HF, \(\epsilon\), A). Again by Proposition 3.2.6 and Theorem 3.2.5, every \(\Sigma_2(J_\alpha)\)-definable real is r.e. in some real x which is \(\Sigma_1(J_\alpha)\)-definable. In particular, every real \(x \in J_\alpha\) is recursive in x. Thus if \(\alpha\) is much larger than \(\rho_2^\alpha\), the real x must be remarkably strong in computational power. Historically, the notion of a master code for \(\rho = 1\) was first introduced by Boolos and Putnam [8] when they studied the Turing degrees of reals in the constructible universe. We now show that \(\Sigma_1\)-master codes exist for any admissible ordinal \(\alpha\).

# Theorem 3.4.10. Let \(\alpha > 0\). There is a \(\Sigma_1\)-master code for \(\langle J_\alpha, \epsilon \rangle\), i.e. a \(\Sigma_1(J_\alpha)\)-definable \(A \subseteq J_{\rho_\alpha^\alpha}\) such that for any \(B \in J_{\rho_\alpha^\alpha}\), if \(B\) is \(\Sigma_{m+1}(J_\alpha)\)-definable, then it is \(\Sigma_m\)-definable in \(\langle J_{\rho_\alpha^\alpha}, \epsilon, A \rangle\).

Proof. We only prove the case m = 1 for simplicity. Suppose that \(f\) is \(\Sigma_1(J_\alpha)\)-definable with parameter p mapping a subset of \(\rho_2^\alpha\) onto \(\alpha\). Fix a \(\Delta_1\)-enumeration \(\langle \varphi_i(x, p) \rangle_{i < \omega}\) of \(\Sigma_1\)-formulas with parameter p. Let
\[
A = \{\langle i, x \rangle \mid i < \omega \land x \in J_{\rho_\alpha^\alpha} \land \langle J_\alpha, \epsilon \rangle \models \varphi(x, p)\}.
\]

It is obvious that A is \(\Sigma_1\)-definable over \(\langle J_\alpha, \epsilon \rangle\). Now suppose that \(B \in J_{\rho_\alpha^\alpha}\) is \(\Sigma_2\)-definable over \(\langle J_\alpha, \epsilon \rangle\). Then there is a \(\Sigma_1(J_\alpha)\)-formula \(\varphi(u, v, w)\) such that
\[
x \in B \Leftrightarrow \langle J_\alpha, \epsilon \rangle \models (\exists y) \neg \varphi(x, u, v, s),
\]

where s is a parameter in \(J_\alpha\). Since f is onto, there is an \(s_0 \in J_{\rho_\alpha^\alpha}\) such that \(f(s_0) = s\). Then
\[
x \in B \Leftrightarrow (\exists y \in J_{\rho_\alpha^\alpha})(\langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, f(y), f(s_0))).
\]

Since f is \(\Sigma_1(J_\alpha)\)-definable with parameter p, there is an index i such that for x, y \(\in J_{\rho_\alpha^\alpha}\),
\[
\langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, y, s_0, p) \Leftrightarrow \langle J_\alpha, \epsilon \rangle \models \neg \varphi(x, f(y), f(s_0)).
\]

Thus
\[
x \in B \Leftrightarrow (\exists y \in J_{\rho_\alpha^\alpha})((i, x, y, s_0) \notin A \Leftrightarrow (\exists y)((i, x, y, s_0)) \notin A).
\]
Hence B is \(\Sigma_1\)-definable over \(\langle J_{\rho_\alpha^\alpha}, \epsilon, A \rangle\). \(\square\)

As an example, \(\theta'\) is a \(\Sigma_1(J_1)\)-master code since it satisfies the property described in Theorem 3.4.10. Jensen [55] proved the following general result: