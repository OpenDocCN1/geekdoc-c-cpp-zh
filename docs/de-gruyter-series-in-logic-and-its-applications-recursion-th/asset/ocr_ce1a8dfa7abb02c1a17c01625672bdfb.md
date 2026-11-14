# 2.4 Hyperarithmetic reducibility

# 2.4.1 \( A_n^1 \)-reducibility

Definition 2.4.1. \( x \le_{A_1^1} y \) if \( x \) is \( \Delta_1^1(y) \). In particular, \( x \le_h y \) if \( x \le_{A_1^1} y \).

Proposition 2.4.2 (Shoenfield). If \( x \le_{A_1^1} y \) and \( y \le_{A_1^1} z \), then \( x \le_{A_1^1} z \).

Proof. If \( x \le_{A_1^1} y \), then there there is a \( A_1^1 \)-predicate \( R \) such that \( n \in x \Leftrightarrow R(n, y) \).
If \( y \le_{A_1^1} z \), then there is a \( A_1^1 \)-predicate \( S \) such that \( n \in y \Leftrightarrow S(n, z) \).
Then
\( n \in x \Leftrightarrow (\exists r)(R(n, r) \land (\forall m)(m \in r \leftrightarrow S(m, z))) \)
\( \leftrightarrow (\forall r)(\forall m)((m \in r \leftrightarrow S(m, z)) \rightarrow R(n, r)) \).
Thus \( x \le_{A_1^1} z \).

Reals \( x, y \) are said to have the same \( A_n^1 \)-degree if \( x \le_{A_1^1} y \) and \( y \le_{A_1^1} x \). If \( n = 1 \), then we also say that they have the same hyperdegree. By Theorem 2.2.6, \( x \le_h y \) if and only if there is an \( n \in O^y \) and an \( e \) such that \( x = \Phi_e^{y_n} \). The hyperjump of \( x \) is defined to be the set \( O^x \).

The \( h \)-reduction relation \( x \le_h y \) suggests another reason for introducing the \( \dot{H}^x \)-sets. One of the problems with \( h \)-reducibility is that, unlike the case of Turing reducibility where one examines a fixed recursive list of possible reduction algorithms (independently of the sets \( x \) and \( y \) being considered), there is no uniform procedure to search for an algorithm that \( h \)-reduces \( x \) to \( y \). The reduction depends on what can be Turing computed by the \( H^x \)-sets and this involves ordinal notations for \( y \). Different reals \( y \) have different ordinal notations. In certain cases the notations may be markedly different since \( \{ \omega_1^y \mid y \in 2^\omega \} \) is unbounded in \( \omega_1 \). The use of \( \dot{H}^x \)-sets circumvents this difficulty. If \( \omega_1^y = \omega_1^{y, \text{CK}} \), then the sets Turing computable by the \( \dot{H}^x \)-sets are precisely the \( A_1^1(y) \).sets. Hence while it is not true in general, for reals \( y \) with \( \omega_1^y = \omega_1^{y, \text{CK}} \), one does have a uniform reduction.

# 2.4.2 The partial order of hyperdegrees

The Turing jump operator is order preserving on the Turing degrees. This remains true for the hyperjump operator which preserves order on the hyperdegrees.

Proposition 2.4.3. \( x \le_h y \iff O^x \le_m O^y \).

Proof. First of all \( O^x \) is \( \Pi_1^1(x) \). If \( x \le_h y \), then as in the proof of Proposition 2.4.2 \( O^x \) is \( \Pi_1^1(y) \). By Theorem 1.5.1, \( O^x \le_m O^y \).
If \( O^x \le_m O^y \), then \( x \le_m O^y \) and \( \omega \setminus x \le_m O^y \). Since \( \omega \setminus x \) is \( \Pi_1^1(x) \), \( \omega \setminus x \le_m O^x \). Then \( \omega \setminus x \) is \( \Pi_1^1(y) \) and this implies that \( x \le_h y \).