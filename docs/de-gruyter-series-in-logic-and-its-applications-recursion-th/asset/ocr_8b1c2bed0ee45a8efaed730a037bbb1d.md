Although the proof of Proposition 6.6.3 looks straightforward, it reveals the remarkable fact that the global structure of the Turing degrees may be sensitive to set-theoretic assumptions.

# Definition 6.6.4.

+   - \( A \in \omega^\omega \) is cofinal if for every \( x \) there is a \( y \in A \) such that \( y \ge_T x \).
+   - A tree \( T \in \omega^{<\omega} \) is pointed if \( T \) is perfect and for any \( x \in [T] \), \( x \ge_T T \).
+   - A pointed tree \( T \) is uniformly pointed if there exists an \( e \) such that for any \( x \in [T] \), \( T = \Phi^e_x \).

# Proposition 6.6.5 (Martin [91]).

ZF + DC + AD implies that every cofinal set of reals has a uniformly pointed subtree.

# Proof.

Suppose that \( A \subseteq \omega^\omega \) is cofinal. Let \( B \subseteq \omega^\omega \) be such that \( z = x \oplus y \in B \) if and only if either

+   - \( x \notin_T y \); or
+   - \( x \le_T y \) and \( y \notin A \).

By AD, \( G_B \) is determined. Suppose that \( \Pi \) has a winning strategy \( \dot{\sigma} \). Let \( y \in A \) so that \( y \ge_T \dot{\tau} \). Then \( \dot{\sigma} * y = y \oplus x \) for some \( x \le_T y \). Hence \( \dot{\sigma} * y \notin B \).

Thus \( \Pi \) has a winning strategy \( \dot{\tau} \). Let \( T_0 \subseteq 2^{<\omega} \) be a uniformly pointed tree such that \( T_0 \models \dot{\tau} \) (see Exercise 6.6.1). Let \( T_1 \) be defined such that \( (n_0, \dots, n_i) \in T_1 \) if and only if there exists a finite string \( (m_0, \dots, m_i) \in T_0 \) such that \( (m_0, n_0, \dots, m_i, n_i) \) is a play by \( \Pi \) at step \( i \) following \( \dot{\tau} \). Clearly \( T_1 \le_T \dot{\tau} \). Since \( \dot{\tau} \) is \( \Pi \)’s winning strategy, for any \( y \in [T_1] \), there is an \( x \in [T_0] \) such that \( y = x \oplus \dot{\tau} \) and \( \dot{\tau} * x \le_T y \). Moreover \( T_1 \) is a perfect tree: Every \( \tau = (m_0, \dots, n_i) \in T_1 \) that is the image of a \( \sigma = (m_0, \dots, m_i) \in T_0 \) (i.e. a play by \( \Pi \) of \( (m_0, n_0, \dots, m_i, n_i) \) at step \( i \) following \( \dot{\tau} \)) has a pair of (immediate) incompatible extensions \( \tau_1 \) and \( \tau_2 \) in \( T_1 \) so that there exist \( x_1, x_2 >_T x \) with \( x_1 * \dot{\tau} >_T \tau_1 \) and \( x_2 * \dot{\tau} >_T \tau_2 \), since otherwise there is a unique \( y \) such that for any \( x >_T \sigma \) in \( [T_0] \), \( x \le_T \tau * \dot{\tau} = y \) and this would imply that there are uncountably many reals recursive in \( y \), which is a contradiction. We conclude that \( T_1 \) is a pointed subtree of \( A \).

We follow the idea in [58] to construct a subtree \( T_2 \) of \( T_1 \) so that \( T_2 \) is uniformly pointed. Define a sequence of trees \( T_1 = T_1^{-1} \supseteq T_1^0 \supseteq T_1^1 \dots \) which are recursive in \( T_1 \) as follows:

# Stage e:

Case (I). There is an \( n \) such that \( \Phi_e^e(n) \downarrow T_1(n) \) for some \( \sigma \in T_e^{<e-1} \). Let \( T_e^e = \{ \tau \mid \tau \in T_1^{e-1} \wedge (\tau \ge_T \sigma \lor \tau \subseteq \sigma) \} \) and proceed to the next stage.

Case (2) Otherwise.

Subcase (i) \( (\forall n)(\forall \sigma \in T_e^{<e-1})(\exists \tau > \sigma)(\sigma(\tau \in T_e^{<e-1} \wedge \Phi_e^\tau(n)[|\tau|]) \). Then it is not difficult to define a \( T_1 \)-recursive perfect tree \( T_e^e \subseteq T_1^{e-1} \) such that for every \( x \in [T_e^e] \), we have \( \Phi_e^x = T_1 \). In this case, terminate the construction since \( T_1^e \le_T T_1 \) and \( T_1^e \) is a uniformly pointed tree.