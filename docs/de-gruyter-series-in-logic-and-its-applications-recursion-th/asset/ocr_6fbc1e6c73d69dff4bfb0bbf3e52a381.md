Then \( z_0 \in M \) and may be coded as a real.

Note that \( g \in [T]^2 \). Since \( x \in M[g] \), to compute \( g \restriction n \) for a given \( n \), search for a \( |\tau| \ge n \) and a \( \sigma \) such that for any \( k \le |\tau| \), there are unique \( n_{0k} \) and \( n_{1k} < \tau k \) such that \( (\sigma \upharpoonright k, \tau_k, n_{0k}, n_{1k}) \in j_0 \) if and only if \( x(n_{0k}) = j \). Then \( \tau \cap n = g \restriction n \). Hence \( g \le_T \sigma \times \tau_0 \).

To see that there is a real \( z_1 \in M \) such that \( g \Vdash z_1 \ge_T x \), assume that

for some \( \tau \in 2^\omega \). Let \( z_1 = ((\sigma \circ \tau) \cap T^2 [(T \circ \tau)] \models x \neq \dot{\tau} \} \). Then \( x \le z_1 \Vdash g \).

The method in the proof of Theorem 6.2.11 is typical of what is known as a fusion construction. This line of construction allows one to find, in \( M \), a fusion sequence \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \) for which there is a condition \( T^2 \) in \( M \) that is an intersection of \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \), such that \( (\forall \alpha)(\forall i < 2)(T^2 \cap [T(\sigma(i))] \models x(\dot{n}_\alpha) = \dot{i}) \). This "splitting property" facilitates the decoding of \( G \) from \( x \) and the real \( z \).

# Corollary 6.2.12. If \( g \) is Sacks generic over \( M = (M, \in) \), then every countable set of ordinals in \( M[g] \) is a subset of a countable set in \( M \) and \( (2^{\aleph_0})^{M[g]} = (2^{\aleph_0})^M \).

Hence Sacks forcing preserves \( \aleph_1 \). It is known, however, that Sacks forcing may collapse cardinals (see [6]).

# 6.2.5 Destroying the Axiom of Choice

In general there is no direct way of destroying the Axiom of Choice (AC) by a forcing extension of a transitive model of ZFC. One introduces an intermediate model to achieve this.

# Definition 6.2.13.

+   - A set \( X \) is ordinal definable in \( M \), written \( X \in \text{OD}^M \), if there is a formula \( \varphi(x, v_0, \dots, v_n) \) together with ordinals \( a_0, \dots, a_n, \beta \) in \( M \) such that \( a \in X \Leftrightarrow V_\beta^M \models \varphi(a, a_0, \dots, a_n) \), where \( V_\beta^M \) is the collection of sets in \( M \) of rank less than \( \beta \).

+   - \( X \) is hereditarily ordinal definable in \( M \), written \( X \in \text{HOD}^M \), if \( \text{TC}(\{X\}) \subset \text{OD}^M \).

If \( M \) is a transitive model of ZFC, then \( (\text{HOD}^M)^\in \) is a transitive model of ZFC (see [53]).

The notion may be generalized to a wider class by defining \( \text{OD}(A)^M \) and \( \text{HOD}(A)^M \). If \( M \) is a transitive model of ZFC and \( A \in M \), then \( (\text{HOD}(A)^M, \in) \) is a transitive model of ZF (see [53]). We use \( \text{HOD}(A)^M \) to obtain a model that destroys AC.

# Definition 6.2.14. Let \( A \in M \).

+   - A set \( X \) is ordinal definable relative to \( A \) in \( M \), written \( X \in \text{OD}(A)^M \), if there exist ordinals \( a_0, \dots, a_n \), elements \( a_0, \dots, a_m \in A \) and a formula \( \varphi(x, a_0, \dots, a_n, a_0, \dots, a_m, A) \) in the expanded language defining \( X \) in the structure \( \langle M, A, a_0, \dots, a_m, \in \rangle \).

+   - A set \( X \) is in \( \text{HOD}(A)^M \) if \( \text{TC}(\{X\}) \subset \text{OD}(A)^M \).