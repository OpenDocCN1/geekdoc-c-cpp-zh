Lemma 7.1.5. There exists a perfect tree \( T_1 \subseteq T_0 \) such that \( T_1 \le_T T_0 \) and \( F \) is either injective or a constant on \( [T_1] \).

Proof. If there exists \( \sigma \in T_0 \) such that \( \Phi^\sigma_{e_0} = \Phi^\sigma_{e_0} \) for all \( x, y \in [T_0] \cap [\sigma] \), then let \( T_1 = T_0 \cap \{ \tau \in 2^{<\omega} \mid \tau \supset \sigma \} \). Obviously \( F \) is a constant on \( [T_1] \). Otherwise, \( T_0 \)-recursively finds a perfect subtree \( T_1 \subseteq T_0 \) such that \( F \) is injective on \( [T_1] \). \(\square\)

By Lemma 7.1.5, we may assume that \( F \) is injective on \( T_0 \). Let

```
\( S_0 = \{ \tau \in 2^{<\omega} \mid (\exists \sigma \in T_0)(\forall n \le |\tau|)(\tau(n) = \Phi^\sigma_{e_0}(n)) \} \).
```

Then \( S_0 \) is a \( T_0 \)-recursive perfect tree so that \( \Phi_{e_0} \) is a homeomorphism from \( [T_0] \) to \( [S_0] \).

Since \( T_0 \) is perfect, let \( p : 2^{<\omega} \to T_0 \) be an order-preserving, \( T_0 \)-recursive bijection. Then \( p \) may be viewed as a homeomorphism from \( 2^\omega \) to \( [T_0] \). Let \( \pi : 2^{<\omega} \to 2^{<\omega} \) be a recursive function such that for any \( \sigma \) and \( i < 2 \), \( p(\sigma^\frown i) = p(\sigma)^\frown i \) if \( \sigma^\frown i \neq \emptyset \) and \( o(i) = 1 \) for some \( j < |\sigma| \); else \( \pi(\sigma^\frown i) = \sigma^\frown (1-i) \). Then \( \pi \) can be viewed as a homeomorphism from \( 2^\omega \) to \( 2^\omega \) by letting \( \pi(\alpha) = (\bigcup_n \pi(\alpha \upharpoonright n)) \). Let

```
\( p_0 = p \circ p \circ p^{-1} \).
```

Then \( p_0 \) is a homeomorphism from \( T_0 \) to \( T_0 \). We leave it to the reader to verify the following lemma.

Lemma 7.1.6. For any \( \sigma \), \( \{\pi^{(n)}(\alpha)\}_{n \in 2^{<\omega}} \) is a permutation of \( 2^{|\sigma|} \).

Let \( p_1 = F \circ p_0 \circ F^{-1} \) be a homeomorphism from \( [S_0] \) to \( [S_0] \) and fix an \( x_0 \in [T_0] \). Since \( T_0 \) is uniformly pointed, there is a pair \( (i_0, j_0) \) such that for any \( n \), \( p_1^{(n)}(x_0) \equiv p_1^{(n+1)}(x_0) \) via \( (i_0, j_0) \). Then \( F(p_0^{(n)}(x_0)) \equiv F(p_0^{(n+1)}(x_0)) \) via \( (i_1, j_1) = \ell((i_0, j_0)) \). Note that for any \( n \), \( F(p_0^{(n)}(x_0)) = p_1^{(n)}(F(x_0)) \). So the real \( \Phi_{e_0 < p}(p_1^{(n)}(F(x_0)) \) is recursive in \( p_1^{(n)}(x_0) = F(x_0) \).

Given a perfect tree \( T \) and a number \( n \), we say that a finite tree \( S \subseteq T \) codes a \( 2^n \) copy of \( T \) if

+   - \( S \) is isomorphic to \( 2^n \);
+   - for any \( \tau \in T \setminus S \), there exists an end node \( \sigma \in S \) such that \( \tau \supset \sigma \).

Lemma 7.1.7. \( S_0 \) is recursive in \( F(X_0) \).

Proof. Note that we may view \( F : [T_0] \to [S_0] \) as a homeomorphism. Hence for any \( \sigma \), there is an \( m \) such that \( p^{-1}(F^{-1}((F(x_0) \upharpoonright m))) \) is of length \( 2^{|\sigma|} \). By Lemma 7.1.6, \( \{\pi^{(n)}(p^{-1}(F^{-1}((F(x_0) \upharpoonright m))))\}_{n \in 2^{<\omega}} \) is a permutation of \( 2^{|\sigma|} \). Since both \( F \) and \( p \) are homeomorphisms, the finite tree

```
\( S_0^{[\sigma]} = \{ \tau \mid (\exists n < 2^{|\sigma|})(\tau \le p_1^{(n)}(F(x_0) \upharpoonright m)) \} \).
```

codes a \( 2^{|\sigma|} \) copy of \( S_0 \).

Thus \( \sigma \in S_0 \) if and only if \( \sigma \in S_0^{[\sigma]} \). Obviously \( S_0^{[\sigma]} \) can be effectively computed from \( \{p_1^{(n)}(F(x_0))\}_{n \in 2^{<\omega}} \). Hence \( S_0 \le_T F(x_0) \). \(\square\)