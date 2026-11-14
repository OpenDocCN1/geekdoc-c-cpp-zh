
and an order-preserving function \( f \) from \( x \) into \( \Phi^y_e \). In other words, WO\(_1\) is \( \Delta^1_1(T_0) \), a contradiction.

By Proposition 6.6.5 again, there is a pointed tree \( T_1 \subseteq T_0 \) and a countable ordinal \( \alpha_1 < \alpha_0 \) such that \( f(x) = \alpha_1 \) for any \( x \in [T_1] \).

If \( F : 2^\omega \to 2^\omega \) is degree invariant, then it is order preserving if for any \( x \le_T y \), \( F(x) \le_T F(y) \).

**Theorem 7.4.2** (Slaman and Steel [142]). Assume ZF + AD + DC. Suppose that \( F : 2^\omega \to 2^\omega \) is order preserving and increasing on a cone. Then either (i) there is an \( a < a_1 \) such that on a cone, \( F(x) =_T x^{(a)} \), or (ii) on a cone, \( F(x) >_T x^{(a)} \) for any \( a < a_1 \).

Proof. Assume that \( F \) is increasing on the cone \( C \). If (ii) is not true for \( F \), then by Lemma 7.4.1 and Proposition 6.6.5, there exists an ordinal \( a < \omega_1 \) such that \( x^{(a)} \le_T F(x) \) on a cone \( C_1 \subseteq C \). Let \( \alpha_0 \) be the least such ordinal. Then \( F(x) >_T x^{(\beta)} \) for any \( \beta < \alpha_0 \). We may assume that \( \alpha_1 > \alpha_0 \). Let \( x_0 \in C_1 \). By relativizing Theorem 7.3.2 to \( x_0 \), there is a \( y \ge_T x_0 \) such that \( F(x_0) \equiv_T y^{(\alpha_0)} \). Since \( F \) is order preserving and increasing, \( F(y) \ge_T F(x_0) \equiv_T y^{(\alpha_0)} \). Thus \( F(y) \equiv_T y^{(\alpha_0)} \). It follows that the set \( \{x \mid F(x) \equiv_T x^{(\alpha_0)}\} \) is cofinal. By Proposition 6.6.6 again, \( F(x) \equiv_T x^{(\alpha_0)} \) on a cone.

## 7.4 Exercises.

**Exercise 7.4.1.** Assume ZF + AD + DC. Suppose that \( F \) is order preserving and increasing on a cone. Then either (i) \( (\exists a < \omega_1)(F(x) \equiv_T x^{(a)}) \) on a cone, or (ii) \( F(x) \ge_T 0^\alpha \) on a cone.

## 7.5 Pressdown functions

A function \( F : 2^\omega \to 2^\omega \) is pressdown on a cone \( C \) if \( F(x) <_T x \) for \( x \in C \). By Theorem 7.1.3, every uniformly degree invariant function that is pressdown on a cone is a constant on a cone.

**Theorem 7.5.1** (Slaman and Steel [142]). Assume ZF + AD + DC. If \( F \) is a degree invariant pressdown function on a cone, then \( F \) is constant on a cone.

Proof of Theorem 7.5.1. Suppose that \( F \) is a degree invariant pressdown function on a cone \( C = \{x \mid x \ge_T z\} \) for some \( z \). By Proposition 6.6.5, there is an \( e_0 \) and a pointed tree T such that \( F(x) = \Phi^z_{e_0} \) for all \( x \in [T] \). By Lemma 7.1.5, we may assume that \( \Phi_{e_0} \) is a homeomorphism from [T] to a perfect set [S].

Without loss of generality, we may assume that for any splitting node \( \alpha \in T \), \( \Phi_{e_0}^{\alpha \upharpoonright 0} \) is compatible with \( \Phi_{e_0}^1 \). The plan is to find two reals \( x_0, x_1 \le_T T \) in [T] such that \( \Phi_{e_0}^{x_0} \oplus \Phi_{e_0}^{x_1} \ge_T T \). Since F is degree invariant and T is pointed, \( F(x_0 \oplus x_1) \equiv_T F(x_0) \equiv_T F(x_0) \oplus F(x_1) \ge_T T \equiv_T x_0 \oplus x_1 \). Then we have a contradiction to the assumption that \( F(x) <_T x \) on C. The following lemma says that for \( x \in [T] \), the growth rate of any function \( h \le_T x \) is controlled by F(x).

### Lemma 7.5.2. Suppose that \( x \in [T] \) and \( h \le_T x \). For each e, let \( l^e \) be a function recursive in \( \Phi_{e_0}^x \) so that

\( l^e(0) = 0 \)

and

\( l^e(n + 1) = \sum_{i \le n} \min \{ m \mid \Phi_{e(i)}^{x \upharpoonright m}(i) \downarrow \} \).

Then there is an e such that \( l^e \) is total and \( (\exists m)(\forall n \ge m)(h(l^e(n)) < l^e(n + 1)) \).

Proof. Without loss of generality, we may assume that h is increasing. Suppose that the lemma is false. We construct a real \( y \le_T x \) in [T] such that \( \Phi_e^y \ne \Phi_{e_0}^x \). By shrinking T if necessary, we may assume that \( x \le_T T \). Since T is pointed, we have \( y \equiv_T x \) but \( \Phi_{e_0}^x \not\ge_T \Phi_{e_0}^y \), a contradiction.

The construction of y is by full approximation recursive in x. We shall construct an x-recursive sequence \( \sigma_0 < \sigma_1 \cdots \) and let \( y = \bigcup_{s < \omega} \sigma_s \). At any stage s, we may declare a number e to be discarded.

Let \( \sigma_0 = 0 \).

At stage s + 1, let \( \tau > s \) be the immediate splitting node in T so that \( \Phi_{e_0}^{\tau \upharpoonright 0}(k_s) \downarrow \neq \Phi_{e_0}^{\tau \upharpoonright 1}(k_s) \downarrow \) for some \( k_s \). For \( i \in \{0,1\} \), let \( \tau_i > \tau \) be the next immediate splitting node in T so that \( \Phi_{e_0}^{\tau_i \upharpoonright 0}(k_s) \downarrow \neq \Phi_{e_0}^{\tau_i \upharpoonright 1}(k_s) \downarrow \) for some \( k_s^i > k_s \).

Search for the least e < s which has not been discarded and \( \Phi_e^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \).

If there exists such an e, then let \( \sigma_{s+1} = \tau^i \) where i is the least number such that \( \Phi_e^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \neq \Phi_{e_0}^{\tau_i}(k_s) \) and discard e. Otherwise, let \( \sigma_{s+1} = \sigma_s \).

Clearly \( y \le_T x \). Suppose that \( \Phi_e^y = \Phi_{e_0}^{x_0} \) for some e. By the assumption, for any m there exists \( n \ge m \) such that \( h(l^e(n)) \ge l^e(n + 1) \). Let \( s_0 \) be a stage large enough so that no \( e' \le e \) is discarded after \( s_0 \). Then there is a \( n > |s_0| + s_0 \) such that \( h(l^e(n)) \ge l^e(n + 1) \). Let \( s_1 \) be the largest stage \( \ge s_0 \) so that \( k_{s_1} \le l^e(n) \). Then at stage \( s_1 + 1 \), either \( k_0 \) or \( k_1 \) is greater than \( l^e(n) \). Hence \( \Phi_{e_0}(k_{s_1}) > l^e(n) \). Since \( k_{s+1} \le l^e(n + 1) \), we have \( \Phi_{e_0}^{h(h(|\tau_0| + |\tau_1|))}(k_s) \downarrow \). In other words, e is discarded at stage \( s_1 + 1 \).

Let \( t \) be a \( T \)-recursive increasing function such that for any \( k \) and \( \sigma \in 2^{t(k)} \cap T, |\Phi_{e_0}^\sigma| = k \). Let \( \pi : \omega^\omega \to T \) be a function defined by induction as follows:

- \( \pi(0) = \sigma \) where \( \sigma \) is the splitting node in \( T \) such that every \( \tau \in T \) is compatible with \( \sigma \);
- \( (\forall i)(\pi(i^\frown) = \pi(i)^\frown \tau) \), where \( \pi(i)^\frown \tau \) is a splitting node in \( T \) for which there is a finite sequence \( \sigma = \sigma_0 \succ \sigma_1 \succ \cdots \sigma_i \prec \tau \) such that for each \( j \le t(i) \), \( \sigma_j \) is the immediate splitting node extending \( \sigma_{j-1}^\frown 0 \) in \( T \) and \( \tau \) is the next immediate splitting node in \( T \) extending \( \sigma_i^\frown 1 \).

Hence \( \pi \) induces a \( T \)-recursive continuous injection from \( \omega^\omega \) to \([T]\) so that for each \( h \in \omega^\omega, \pi(h) \equiv_T h \oplus T \).

By Lemma 7.5.2, for each \( h \), there is a least \( e_h \) for which one chooses the least \( m_h \) such that \( (\forall n \ge m_h)(h(l^{e_h}(n)) < l^{e_h}(n+1)) \).

Note that the function \( h \mapsto (e_h, m_h) \) is \( \Delta_1^1(T) \). Then for each pair \( (e, m) \), the set \( H_{e,m} = \{h \mid (e_h, m_h) = (e, m)\} \) is a Borel set and therefore has the Baire property. Then there is a pair \( (e_1, m_1) \) such that \( H_{e_1, m_1} \) is not meager. In other words, there is a \( u \in \omega^{<\omega} \) such that for any \( \tau \supset u \), there is an \( h \in H_{e_1, m_1} \) with \( h \supset \tau \). Now for any \( \sigma \in \omega^{<\omega} \), we \( T \)-recursively define a finite function \( l_\sigma \) so that \( l_\sigma(0) = 0 \)

and \( l_\sigma(n+1) = \sum_{i \le l_\sigma(n)} \min\{m \mid |\Phi_{e_1}^{\sigma(i^\frown m)}[i](m)| \} \).

For \( h \in \omega^\omega \), let \( l_h(n) = k \) if there exists an \( m \) such that \( l_{h|n}(m) = k \). The proof of the following lemma is straightforward.

### Lemma 7.5.3.

- (i) \( (\forall \sigma)(\forall i)(k[\sigma] > k \land k \supset l_\sigma(i) \Rightarrow l_{k[\sigma]}(i) = k) \);
- (ii) \( (\forall \tau \supset u)(\forall n)(n \ge m_1 \land l_\tau(n) \ge [\tau] \Rightarrow n+1 \notin \text{Dom}(l_\tau)) \).

Proof. (i) If \( |\sigma| > k \) and \( k = l_\sigma(i) \), then \( |\tau[\sigma]| \ge t(|\sigma|) \ge t(|k|) \). Then \( |\Phi_{e_0}^{\pi(k)}| = k \). Thus \( l_{k[\sigma]}(i) = k \).

If (ii) is not true, then there exists a \( \tau \supset u \) and \( n \ge m_1 \) such that \( l_\tau(n) \ge [\tau] \) and \( l_\tau(n+1) \) is defined. Then \( l_\tau(l_\tau(n)) \) is undefined. By the assumption on \( u \), there is an \( h \supset \tau \) in \( H_{e_1, m_1} \), such that \( h(l_h(n)) > l_\tau(n+1) = l_h(n+1) \), a contradiction.

Let \( x \equiv_T T, m_2 \ge m_1 \) and \( h \supset u \) so that \( l_h(m_2) \) is defined. Let \( \tau_0 = \tau_1 = h \mid l_h(m_2) \). By Lemma 7.5.3, \( l_{\tau_0}(m_2) \) is defined and \( [\tau_0] = l_{\tau_0}(m_2) \) (so \( l_{\tau_0}(m_2+1) \) is undefined). We \( T \)-recursively construct two sequences \( \tau_0 = \tau_0^0 \prec \tau_1^0 \dots \) and \( \tau_1 = \tau_1^0 \prec \tau_1^1 \dots \) as follows.
