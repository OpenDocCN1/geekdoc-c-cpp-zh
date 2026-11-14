
Define a notion of forcing $\mathbf{P} = (\mathbf{P}, \le)$ such that each \(p \in \mathbf{P}\) is a triple \((p_1, p_2, p_3)\) such that \(p_1, p_2 \in 2^{<\omega}\) have the same length (called the length of \(p\)), \(p_3 \in \omega\) and for \(p, q \in \mathbf{P}\), \(p \le q\) if and only if

- (i) \(q_j \ge p_j\) for \(j = 1, 2\);
- (ii) \(q_3 \ge p_3\);
- (iii) for all \(k \le p_3\), for all \(m \in a_k\), if \((k, m)\) is in the domain of \(q_1 \setminus p_1\) (hence in the domain of \(q_2 \setminus p_2\)), then \(q_1((k, m)) = q_2((k, m))\).

Expand the language of Cohen forcing in second order arithmetic (see § 5.2) relativized to \(a\) by introducing ranked variables \(x^\alpha\) for \(\beta < \alpha^+\), terms \(a_i\) for each \(i < \omega\), \(a\) for \(a\) and \(g_1, g_2\) for the generic reals \(g_1\) and \(g_2\) to be obtained from \(\mathbf{P}\). For a formula \(\phi\) in the expanded language, define \(\mathbf{p} \Vdash \phi\) as in Section 5.2. We leave it to the reader to verify that \(a_i^{\omega_g} = \omega_i^a\) for any generic \(g\).

Let \(g\) be \(\mathbf{P}\)-generic with \(\mathbf{g}\) the hyperdegree of \(g_j\) for \(j = 1, 2\) where \(g_1 = \bigcup \{p_1 \mid (\exists p_2)(\exists p_3)((p_1, p_2, p_3) \in g)\}\) and \(g_2 = \bigcup \{p_2 \mid (\exists p_1)(\exists p_3)((p_1, p_2, p_3) \in g)\}\). The plan is to show that \(A\) is the set of minimal solutions of

\(\{x \in a \mid (\exists z)((z \subseteq x \cup g_1) \land (z \subseteq x \cup g_2) \land (z \notin x))\}.\)

**Lemma 10.3.2.** Let \(g_1\) and \(g_2\) be as above. For each \(k\), there is a real \(c_k\) so that \(c_k \le_h a_k \oplus g_j\) for each \(j\) and \(c_k \not\le_h a_k\).

**Proof.** Let \(p \in g\) be a condition such that \(|p_1| > k\). Let \(c_k = \{m \mid m \in a_k \land |p_1| < (k, m) \in g_1\}\). Clearly \(c_k \le_T a_k \oplus g_1\). Also by (iii), we have \(c_k = \{m \mid m \in a_k \land |p_1| < (k, m) \in g_2\}\) so that \(c_k \le_T a_k \oplus g_2\) as well. Note that \(c_k \not\le_h a_k\): A simple diagonalization method shows that \(c_k\) is not equal to \(x\) for any \(x \le_h a\). So \(c_k \not\le_h a\) and so \(c_k \not\le_h a_k\).

**Lemma 10.3.3.** For any reals \(x, z \le_h a\), if \(z \le_h x \oplus g_j\) for \(j = 1, 2\) and \(z \not\le_h x\), then \(x \ge_h a_k\) for some \(k\).

**Proof.** Fix ranked formulas \(\varphi_x, \varphi_z\) so that \(m \in x \Leftrightarrow \mathfrak{A}(\omega_1^a, a) \models \varphi_x(m)\) and \(m \in z \Leftrightarrow \mathfrak{A}(\omega_1^a, a) \models \varphi_z(m)\). Also for \(j = 1\) and \(2\), let \(\varphi_{x \oplus g_j}\) be such that \(m \in z \Leftrightarrow \mathfrak{A}(\omega_1^a, a, g_j) \models \varphi_{x \oplus g_j}(m) \Leftrightarrow \mathfrak{A}(\omega_1^a, a, g) \models \varphi_{x \oplus g_j}(m)\). Note that \(\varphi_{x \oplus g_j}\) is expressed in terms of \(\varphi_x\) and \(g_j\). Hence there is a condition \(p \in g\) such that

\(p \Vdash (\forall m)(\varphi_x(m) \leftrightarrow \varphi_{x \oplus g_1}(m)) \land (\varphi_z(m) \leftrightarrow \varphi_{x \oplus g_2}(m)).\)

**Claim.** There exist infinitely many \(m\)’s and conditions \(q^m, r^m > p\) of common length at least \(m\) such that \(q^m \Vdash \varphi_{x \oplus g_1}(m)\) and \(r^m \Vdash \neg \varphi_{x \oplus g_1}(m)\).

**Proof of Claim.** Otherwise, for all sufficiently large \(m\), for all \(q, r > p\) with length at least \(m\), \(q\) and \(r\) do not force different values for \(\varphi_{x \oplus g_1}(m)\). Since \(x \le_h a\), the sentence \(\varphi_{x \oplus g_1}(m)\) has (the same) rank less than \(\omega_1^a\) for each \(m\) and so the relation \(\text{‘}q \Vdash \varphi_{x \oplus g_1}(m)\text{’}\) is hyperarithmetic in \(x\). But then this implies that \(z \le_h x\) which contradicts the hypothesis.

Thus let \(q^m, r^m\) be chosen as in the Claim. Note that \(m \mapsto (q^m, r^m)\) is hyperarithmetic in \(x\).

We start with (the least) \(i < |Q|\) such that \(q_1^m\) and \(r_1^m\) disagree at \(i\) (if any). Define a condition \(s(0) = (s_1(0), s_2(0), s_3(0))\) by first changing the value of \(q_1^m\) at the point \(i\) to agree with that of \(r_1^m\), \(s_2(0) \mid [q_1^m]^2 = q_2^m\) and \(s_3(0) = q_3^m\), and then extending it to decide the value of \(\varphi_{x \oplus g_i}(m)\). Then extend the domains of \(q_1^m, q_2^m\) and \(r_1^m, r_2^m\) to that of \(s_1(0)\) so that the new points in these domains agree with \(s_1(0)\) in their values. Call the resulting conditions \(q^m(0)\) and \(r^m(0)\). Either \(s_1(0)\) and \(q_1^m(0)\) disagree at exactly one point, \(s_2(0) = q_2^m(0)\), and \(s(0)\) and \(q^m(0)\) force incompatible values for \(\varphi_{x \oplus g_i}(m)\), or \(s(0)\) and \(r^m(0)\) force incompatible values and have fewer points of disagreement between them than that between \(q^m\) and \(r^m\). For \(q_1^m\) and \(r_1^m\), we carry out the same construction. By induction, one defines successively \(s(0), s(1), \dots\) and concludes that there is a \(j\) so that \(s(j)\) and \(s(j+1)\) with exactly one point of disagreement in the first two components forcing incompatible values for \(\varphi_{x \oplus g_i}(m)\).

Thus we may assume that \(q^m\) and \(r^m\) differ exactly at one point \((k, l)\) so that \(q_1^m((k, l)) \neq r_1^m((k, l))\). If either \(k > p_3\) or \(l \notin a_k\), then let \(s = (s_1^m, r_2^m, q_3 + r_3)\). Then \(s \le p\). This implies that we can extend \(p\) to a generic \(g\) having the same values for \(g_1\) and \(g_2\) as those for \(q^m\) and \(r^m\) respectively at their common points. This, however, contradicts the assumption on \(p\).

It follows that there exist infinitely many pairs of conditions extending \(p\) which differ at exactly one \((k, l)\) with \(k \le p_3\) and \(l \in a_k\), forcing different values as described above. In particular there is a \(k \le p_3\) for infinitely many such \(l\)'s to satisfy this requirement. Now as noted earlier the forcing relation for sentences of fixed rank considered here is hyperarithmetic in the parameter \(x\), and so one can hyperarithmetically in \(x\) enumerate an infinite set of \(l\)'s contained in \(a_k\). Since \(a_k\) is recursive in each of its infinite subsets, this set computes \(a_k\).

Thus \(x \ge_h a_k\), proving the lemma.

One may now convert an arbitrary countable relation on the degrees into an antichain so that the original relation is definable from the antichain using parameters.

## Proof of Theorem 10.3.1.

Let \(R\) be an \(n\)-ary relation on the hyperdegrees. Let \(\{\mathbf{a}_j \mid j < \omega\}\) be a list of all the hyperdegrees \(\le \mathbf{a}\), with \(a_j \in \mathbf{a}_j\) and \(a \in \mathbf{a}\). Let \(\{g_{i,j} \mid 1 \le i \le n \text{ and } j < \omega\}\) be reals which are mutually Cohen generic over \(a\). This can be obtained following §5.2 with the expanded language described earlier, taking \(g_{i,j}\) to be the appropriate columns of a single generic \(g\). By Exercise 10.3.1, the following sets are antichains of hyperdegrees:

\(S_i = \{g_{i,j} \mid j < \omega\}\);
\(T_i = \{\mathbf{a}_j \mid j < \omega\}\);
\(U = \{\mathbf{g}_{1,j}, \dots, \mathbf{g}_{n,j} \mid R(\mathbf{a}_j, \dots, \mathbf{a}_j)\}\).

Then $S_i, T_i$ and $U$ are definable in $(\mathscr{P}_n, \le)$. For any $\mathbf{x}_1, \dots, \mathbf{x}_n \le \mathbf{a}$, $R(\mathbf{x}_1, \dots, \mathbf{x}_n)$ holds if and only if for each $i \in [1, n]$, there is a $\mathbf{y}_i \in S_i$ and $\mathbf{z}_i \in T_i$ such that $\mathbf{y}_1 \cup \cdots \cup \mathbf{y}_n \in U$ and $\mathbf{x}_i \cup \mathbf{y}_i = \mathbf{z}_i$. Hence $R$ restricted to the hyperdegrees below $\mathbf{a}$ is definable, completing the proof of Theorem 10.3.1.

## 10.3.2 Coding an expanded standard model of PA

Consider the standard model \(\langle \omega, x, <, +, \cdot, 0, 1 \rangle\) of Peano arithmetic expanded by a unary predicate \(x\). We may represent it as a relation on degrees. Let \(\langle \mathbf{d}_n \rangle_{n < \omega}\) be a countable sequence of hyperdegrees. We interpret \(\mathbf{d}_n\) as the number \(n\) and define arithmetical relations and functions on finite subsets of \(\langle \mathbf{d}_n \rangle_{n < \omega}\) in the obvious way. From these one may define a countable relation \(R^*\) on \(\langle \mathbf{d}_n \rangle_{n < \omega}\) turning it into (a copy of) the standard model of arithmetic with a unary predicate representing the real \(x\). By Theorem 10.3.1, there is a finite sequence of degrees \(\bar{\mathbf{p}}\) and a formula \(\varphi\) in the language of partial ordering which together define \(R^*\). Fix the formula \(\varphi\) throughout this section. Note that not every \(\bar{\mathbf{p}}\) together with \(\varphi\) necessarily code a standard model of arithmetic.

**Definition 10.3.4.** Given a finite sequence \(\bar{\mathbf{p}}\) of hyperdegrees and a real \(x\), we say that \(\bar{\mathbf{p}}\) codes a standard model with \(x\) (as a second order element) if \(\bar{\mathbf{p}}\) and \(\varphi\) together define a relation \(R^* = (R_\omega, R_<, R_+, R_\cdot, R_0, R_1)\) which represents the standard model of arithmetic \(\mathcal{M} = \langle \omega, x, <, +, \cdot, 0, 1 \rangle\).

If one removes the unary predicate \(x\), then \(\bar{\mathbf{p}}\) codes a standard model if \(\bar{\mathbf{p}}\) and \(\varphi\) define a relation \(R = (R_\omega, R_<, R_+, R_\cdot, R_0, R_1)\) which represents \(\mathcal{M} = \langle \omega, <, +, \cdot, 0, 1 \rangle\). Then the relation "\(\bar{\mathbf{p}}\) and \(\varphi\) code a standard model" is definable in \((\mathscr{P}_n, \le)\). To see this, we make the following observations:

- (i) The model \(\mathcal{M}\) represented by \(R\) satisfies the system of Robinson arithmetic \(Q\). Since \(Q\) is a finite collection of axioms, it can be expressed in one sentence;
- (ii) \(\mathcal{M}\) is wellfounded. In other words, there is no infinite descending \(R_<\)-sequence. By Theorem 10.3.1, there is a formula \(\psi(\bar{U}, \mathbf{v})\) so that \(\mathcal{M}\) is wellfounded if and only if for any finite sequence \(\bar{\mathbf{q}}\), the set \(\{ \mathbf{d} \mid (\mathscr{P}_n, \le) \vDash \psi(\bar{\mathbf{q}}, \mathbf{d}) \}\) is not an infinite descending \(R_<\)-sequence.

Thus the statement that \(\bar{\mathbf{p}}\) and \(\varphi\) code a standard model is definable.

## 10.3.3 Biinterpretability

For a general definition of biinterpretability, see Hodges [52]. We focus our attention on biinterpretability in the context of hyperdegrees.

Fix a relation \(R^*\) so that

\(R^*(\bar{\mathbf{p}}, \mathbf{x})\) if and only if \(\bar{\mathbf{p}}\) codes a real \(x\) and \(x \in \mathbf{x}\).
