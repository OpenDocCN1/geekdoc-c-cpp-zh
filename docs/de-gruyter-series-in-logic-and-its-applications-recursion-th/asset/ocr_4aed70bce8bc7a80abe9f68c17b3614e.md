# 8.3 \(\Pi^1_1\)-maximal chains and antichains of Turing degrees

We now apply the \(\Pi^1_1\)-inductive principle \(\mathfrak{I}\) to construct some special \(\Pi^1_1\)-sets of Turing degrees.

# 8.3.1 Chains in the Turing degrees

Given a partial ordering \((P, \le_P)\), \(p \in P\) is a minimal cover of \(A \subseteq P\) if \(q <_P p\) for all \(q \in A\) and if there is no \(r \in P\) such that \(r <_P p\) having the same property. A set \(A \subseteq P\) is a *chain* if for any \(x, y \in A\), either \(x \le_P y\) or \(y \le_P x\). A chain \(A\) is *maximal* if there is no chain \(B \supset A\). Define \(P(x, y)\) if and only if

\(y\) is a minimal cover of \(\{\chi(n) \mid n \in \omega\}\) under \(\le_T\).

Lemma 8.3.1. P(x, y) is a cofinally progressive relation.

Proof. We prove that for any countable set \(A = \{x_i\}_{i < \omega}\) and any real \(x\), there is a minimal cover \(z\) of \(A\) such that \(z'' \ge_T x\).

Fix an effective enumeration of partial recursive functions \(\{\Phi_e\}_{e < \omega}\).

Given a perfect tree \(T\), define the \(n\)-th level \(Lev_n(T)\) of \(T\) to be

\(\{\sigma \notin Lev_{n-1}(T) \mid (\exists \tau)(\tau \in T \land \sigma \preceq \tau \land \tau \text{ is an } n\text{-th splitting node on } T)\}.\)

Let \(\{p_n\}_{n < \omega}\) be a recursive one-one enumeration of prime numbers. Allowing ambiguity, we will also use \(p_\sigma\) to denote the prime number which codes the string \(\sigma\). Given a recursive oracle function \(\Phi\), we use \(\Phi^v = T\) to express the following:

+   (1) \(\Phi^v\) is total;
+   (2) \((\forall n)(\Phi^v(n) = \prod_{\sigma \in Lev_n(T)} p_\sigma)\).

Given a tree \(T\) and a string \(v \in T\), let \(T^v\) be the subtree of \(T\) consisting of all \(v' \in T\) extending \(v\). Define \(L_n(T)\) to be the leftmost \(n+1\)-th splitting node and \(R_n(T)\) to be the rightmost \(n+1\)-th splitting node on \(T\).

For each finite string \(\sigma^*\), real \(x\) and perfect tree \(T \subseteq 2^{<\omega}\) with \(\sigma^* \in T\), define \(T(\sigma^*, x, T)\) to be the perfect tree that is the intersection of a sequence of perfect trees \(T_n\) given as follows:

\(T_0 = T^{\sigma^*}\).

\(T_{n+1} = \{\tau \mid (\exists \sigma \in Lev_n(T_n))(\tau(\sigma \le \sigma) \cup S_{n+1} \subseteq T_n\)

where \(S_{n+1}\) is defined as:

Case 1. \(x(n) = 0\): \(\sigma \in S_{n+1}\) if and only if there exists \(\tau \in Lev_{n+1}(T_n)\) so that \(\sigma \succeq \tau\) and \(r = L_1(T_n^\tau)\) for some \(v\) which is an \(n\)-th splitting node of \(T_n\).

Case 2. \(x(n) = 1\): \(\sigma \in S_{n+1}\) if and only if there exists \(\tau \in Lev_{n+1}(T_n)\) so that \(\sigma \succeq \tau\) and \(r = R_1(T_n^\tau)\) for some \(v\) which is an \(n\)-th splitting node of \(T_n\).