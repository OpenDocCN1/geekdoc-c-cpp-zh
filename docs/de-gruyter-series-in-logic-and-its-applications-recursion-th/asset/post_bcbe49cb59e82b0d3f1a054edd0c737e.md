
There is an obvious generalization of the above to allow parameters in \(\omega^\omega\), yielding the class of \(\Sigma^0_n\)-predicates relative to a real or a finite set of reals.

### Definition 1.1.4.

- (i) A predicate \(P^0(y, m)\) is \(\Sigma^1_1(\alpha)\) if there is a partial recursive predicate \(R(A, y, m)\) such that for all \(y\) and \(m\), \(P^0(y, m) \leftrightarrow R(\alpha, y, m)\).
- (ii) \(P^0(y, m)\) is \(\Pi^0_n(\alpha)\) if \(\neg P^0(y, m)\) is \(\Sigma^0_n(\alpha)\).
- (iii) \(P^0(y, m)\) is \(\Sigma^0_n(\alpha)\) if there is a \(\Pi^0_n(\alpha)\)-predicate \(R^0(y, m, k)\) such that \(P^0(y, m)\) if \((\exists k)R^0(y, m, k)\).
- (iv) \(P^0(y, m)\) is \(\Delta^0_n(\alpha)\) if it is \(\Sigma^0_{n+1}(\alpha)\) and \(\Pi^0_{n+1}(\alpha)\).

Given a collection of predicates \(\Gamma\), we say that a set \(a \subseteq \omega\) (resp. \(P^* \subseteq \omega^\omega\)) is a \(\Gamma\)-set, or a member of \(\Gamma\), if \(m \in a \leftrightarrow P(0, m)\) (resp. \(x \in P^* \leftrightarrow P(x, 0)\)) for some predicate \(P(x, m) \in \Gamma\). For each \(n < \omega\), let \(\Sigma^0_n\), \(\Pi^0_n\) and \(\Delta^0_n\) denote respectively the class of \(\Sigma^0_n\), \(\Pi^0_n\) and \(\Delta^0_n\)-predicates. The following lemma is well known. A proof may be found in [53].

### Lemma 1.1.5.

- (i) Let \(n < \omega\). There is a \(\Sigma^0_n\)-set \(U \subseteq \omega^\omega \times \omega^\omega\) such that for each \(P \in \Sigma^0_n\), \(P = \{x \mid (x, y) \in U\}\) for some \(y\).
- (ii) For each \(n\), \(\Sigma^0_n \subset \Delta^0_{n+1} \subset \Sigma^0_{n+1}\) and \(\Pi^0_n \subset \Delta^0_{n+1} \subset \Pi^0_{n+1}\).

In classical recursion theory, a set \(a \subseteq \omega\) is \(\Sigma^0_1\), if and only if \(a\) is \(\Sigma^0_1(\emptyset')\). However, it is not generally true for sets of reals. For example, the set \(\{\emptyset^{(\omega)}\}\) is \(\Sigma^0_3\) but is not \(\Sigma^0_1(x)\) (as a singleton) for any \(x \in \omega^\omega\) (see Exercise 1.1.5).

## 1.1.2 Analytical predicates

### Definition 1.1.6.

- (i) A predicate \(P(x, m)\) is \(\Sigma^1_1\) if it is \(\Sigma^1_1\);
- (ii) A predicate \(P(x, m)\) is \(\Pi^0_n\) if \(\neg P(x, m)\) is \(\Sigma^0_n\);
- (iii) A predicate \(P(x, m)\) is \(\Sigma^0_{n+1}\) if there is a \(\Pi^0_n\)-predicate \(R(x, y, m) \in \omega^\omega \times \omega^\omega \times \omega\) such that \(P(x, m)\) if and only if \((\exists y)R(x, y, m)\).
- (iv) A predicate \(P(x, m)\) is \(\Delta^0_1\) if it is both \(\Pi^0_1\) and \(\Sigma^0_1\).
- (v) A predicate \(P\) is *analytical* if \(P \in \Sigma^1_n\) for some \(n\).

As in Lemma 1.1.5, we have the following facts which are straightforward to verify.

### Lemma 1.1.7.

- (i) Let \(n < \omega\). There is a \(\Sigma^1_n\)-set \(U \subseteq \omega^\omega \times \omega^\omega\) such that for each \(P \in \Sigma^1_n\), \(P = \{x \mid (x, y) \in U\}\) for some \(y\).
- (ii) For each \(n\), \(\Sigma^1_n \subset \Delta^1_{n+1} \subset \Sigma^1_{n+1}\) and \(\Pi^1_n \subset \Delta^1_{n+1} \subset \Pi^1_{n+1}\).
- (iii) Every arithmetical set is \(\Delta^1_1\).

More basic facts about analytical sets may be found in Jech [53]. For \(\sigma \in \omega^{<\omega}\), let \([\sigma]\) denote the set of functions in \(\omega^\omega\) which extend \(\sigma\). We say that a function \(f : \omega^\omega \to \omega^\omega\) is in the class \(\Gamma\) if \((x, \sigma) \in \omega^\omega \times \omega^{<\omega} \mid x \in f^{-1}([\sigma]) \in \Gamma\). Note that every \(\Sigma_1^1\)-function is continuous.

The following proposition is immediate.

### Proposition 1.1.8.

- (i) If \(f : \omega \to \omega\) is total, then \(f \in \Sigma_2^0 \leftrightarrow f \in \Delta_2^0\).
- (ii) A function \(f : \omega^\omega \to \omega^\omega\) is \(\Sigma_1^1\) if and only if its graph \(G' = \{(x, y) \mid f(x) = y\}\) is \(\Sigma_1^1\); if \(f\) is \(\Pi_1^1\) then \(G' \in \Pi_1^1\); if \(f\) is \(\Delta_1^1\) then \(G' \in \Delta_1^1\).
- (iii) If \(f\) is total, then \(G'\) is \(\Delta_1^1\) if and only if \(f\) is \(\Delta_1^1\).
- (iv) If \(f : \omega^\omega \to \omega^\omega\) is total, then \(f \in \Sigma_1^1 \leftrightarrow f \in \Delta_1^1\).

Proof. (i) is obvious. For (ii), note that \((x, y) \in G'\) if and only if \((\forall n)(\forall \sigma \prec x \in f^{-1}([\sigma]))\). Hence if \(f\) is \(\Sigma_1^1\) (resp. \(\Pi_1^1\)) then \(G'\) is \(\Sigma_1^1\) (resp. \(\Pi_1^1\)). Moreover, if \(G'\) is \(\Sigma_1^1\), then \(x \in f^{-1}([\sigma])\) if and only if \((\exists y)(\forall \sigma \prec x, (y) \in G')\). So \(f\) is \(\Sigma_1^1\) if and only if its graph \(G' = \{(x, y) \mid f(x) = y\}\) is \(\Sigma_2^1\).
(iii). If \(f\) is total, then \(x \in f^{-1}([\sigma])\) if and only if \((\forall y)(\forall \tau \prec x \in f^{-1}([\tau]))\).
(iv). If \(f\) is total, then \(x \in f^{-1}([\sigma])\) if and only if \((\forall y)(\forall \sigma \prec x, y) \in G'\). So if \(G'\) is \(\Sigma_n^1\), then \(f\) is \(\Pi_n^1\). By (iii), \(f\) is \(\Delta_n^1\).

Given \(\sigma_i\) and \(\sigma'_i\) in \(\omega^{<\omega}\), where \(i \le n\), we say that \((\sigma'_0, \dots, \sigma'_n)\) is a substring of \((\sigma_0, \dots, \sigma_n)\) if \(\sigma'_i \subseteq \sigma_i\) for each \(i\). A tree \(T \subseteq \omega^{<\omega} \times \dots \times \omega^{<\omega}\) (\(n\)-fold product) is assumed to have the property that if \((\sigma_0, \dots, \sigma_n) \in T\) then all of its substrings are in \(T\). For our purpose, all trees grow downwards with root at the top. The following tree representation theorem provides a useful picture of \(\Sigma_1^1\)-sets of reals.

### Proposition 1.1.9.

A predicate \(P(x, m)\) is \(\Sigma_1^1\) if and only if there is a recursive sequence of recursive trees \(\{T_m\}_{m < \omega}\) such that \(T_m \subseteq \omega^{<\omega} \times \omega^{<\omega}\) and

\(P(x, m) \Leftrightarrow (\exists y)(\forall n)(\langle x \mid n, y \mid n \rangle \in T_m).\)

Proof. A predicate \(P(x, m)\) is \(\Sigma_1^1\) if and only if there is a partial recursive function \(\Phi(\sigma, \tau, m)\) which satisfies properties (i)—(iii) of Definition 1.1.1, so that \(P(x, m) \Leftrightarrow (\exists y)(\forall k)(\Phi(x \mid k, y \mid k, m) \downarrow \to \Phi(x \mid k, y \mid k, m) \neq 0)\). At stage \(\max\{|\sigma|, |\tau|\}\), put \((\sigma, \tau)\) in \(T_m\) if and only if \(\Phi(\sigma, \tau, m) \downarrow\) or \(\Phi(\sigma, \tau, m) \neq 0\). We leave it to the reader to verify that \(\{T_m\}_{m \in \omega}\) satisfies the requirement.

## 1.1.3 \(\Sigma_1^1\)-sets of reals

A set of reals is \(\Sigma_1^1\) if there is a \(\Sigma_1^1\)-predicate \(P\) (possibly with a number parameter \(m\)) such that \(P(x, m)\) holds if and only if \(x\) belongs to the set. A set of reals is \(\Pi_1^1\) if its complement is \(\Sigma_1^1\). Both \(\Sigma_1^1\) and \(\Pi_1^1\)-sets of reals play significant roles in higher recursion theory. In this section, we introduce some basic facts about these sets.

Recall that \( P \subseteq \omega^\omega \) is perfect if it is a closed set with no isolated point. The next theorem shows that every uncountable \( \Sigma^1_1 \)-set of reals has what may be described as the perfect set property.

### Theorem 1.1.10 (Suslin [162]).

If \( P \) is \( \Sigma^1_1 \) and uncountable, then it contains a perfect subset.

Proof. Suppose \( P(x) \) is \( \Sigma^1_1 \) (for simplicity assume that there is no number variable defining \( P \)). We give two proofs of Theorem 1.1.10. One is set-theoretic while the other is recursion-theoretic.

Set-theoretic proof. By Proposition 1.1.9, there is a recursive tree \( T \subseteq \omega^{<\omega} \times \omega^{<\omega} \) such that \( x \in P \) if and only if \( (\exists y)(\forall n)[x \mid y, n) \in T \). Let \( T' \) be a subtree of \( T \) such that

\( (\sigma, \tau) \in T' \iff \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0 \).

Define

\( Q = \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in T'\} \).

Since \( P \) is uncountable, \( Q \) is not empty. Obviously \( Q \subseteq P \). Note that if \( (\sigma, \tau) \in T' \) then there exist \( k \) and \( k' \) such that \( (\sigma \mid k, \tau \mid k') \in T' \). We show that \( Q \) contains a perfect set. By induction on \( n \), build a perfect tree \( S_0 \) and a tree \( S_1 \) with the following properties:

- (i) \( S_1 \subseteq T' \);
- (ii) let \( [S_0] \) denote the set of infinite paths in \( S_0 \). Then \( [S_0] \) is contained in \( \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in S_1\}\);
- (iii) \( (\forall(\sigma, \tau) \in S_1)(\{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0) \).

We begin with setting \( S_0 \) and \( S_1 \) to be empty at level 0. Suppose we are at level \( n+1 \). Let \( \sigma \in S_0 \) be defined at level \( n \) with \( |\sigma| = n \). By induction, there is a \( \tau \) such that \( (\sigma, \tau) \in S_1 \) was defined at level \( n \) and \( Q_{\sigma, \tau} = \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} \) is uncountable.

Claim. There exist incompatible extensions \( \sigma_0, \sigma_1 \) of \( \sigma \) such that \( Q_{\sigma_0, \tau} \) and \( Q_{\sigma_1, \tau} \) are both uncountable.

If the Claim is false, then there is a unique \( x > \sigma \) such that if \( \sigma' > \sigma \) is incompatible with \( x \), then \( Q_{\sigma', \tau} \) is countable. But this would imply that \( Q_{\sigma, \tau} = \{x\} \cup \bigcup_{\sigma' > \sigma, \sigma' \neq x} Q_{\sigma', \tau} \) is countable, which is a contradiction.

Fix \( (\sigma_0, \sigma_1) \) as in the Claim. Then there exist \( \tau_0, \tau_1 > \tau \) such that \( |\{x > \sigma_i \mid (\exists y > \tau_i)(\forall n)(\langle x \mid y, n \rangle \in T)\}| > \aleph_0 \) for \( i = 0, 1 \). Put \( \sigma_0 \) and \( \sigma_1 \) into \( S_0 \) and \( (\sigma_i, \tau_i) \), for \( i = 0, 1 \), into \( S_1 \). This procedure is carried out for every \( \sigma \in S_0 \). Clearly \( S_0 \) is a perfect tree and for each \( x \) there is a \( y \) such that \( (\forall n)(\langle x \mid y, n \rangle \in S_1 \). Since \( S_1 \subseteq T' \subseteq T \), \( [S_0] \subseteq Q \subseteq P \).
