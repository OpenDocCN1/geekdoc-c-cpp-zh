
Then \( z_0 \in M \) and may be coded as a real.

Note that \( g \in [T]^2 \). Since \( x \in M[g] \), to compute \( g \restriction n \) for a given \( n \), search for a \( |\tau| \ge n \) and a \( \sigma \) such that for any \( k \le |\tau| \), there are unique \( n_{0k} \) and \( n_{1k} < \tau k \) such that \( (\sigma \upharpoonright k, \tau_k, n_{0k}, n_{1k}) \in j_0 \) if and only if \( x(n_{0k}) = j \). Then \( \tau \cap n = g \restriction n \). Hence \( g \le_T \sigma \times \tau_0 \).

To see that there is a real \( z_1 \in M \) such that \( g \Vdash z_1 \ge_T x \), assume that

for some \( \tau \in 2^\omega \). Let \( z_1 = ((\sigma \circ \tau) \cap T^2 [(T \circ \tau)] \models x \neq \dot{\tau} \} \). Then \( x \le z_1 \Vdash g \).

The method in the proof of Theorem 6.2.11 is typical of what is known as a fusion construction. This line of construction allows one to find, in \( M \), a fusion sequence \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \) for which there is a condition \( T^2 \) in \( M \) that is an intersection of \( \langle T_\alpha \rangle_{\alpha < 2^\omega} \), such that \( (\forall \alpha)(\forall i < 2)(T^2 \cap [T(\sigma(i))] \models x(\dot{n}_\alpha) = \dot{i}) \). This "splitting property" facilitates the decoding of \( G \) from \( x \) and the real \( z \).

### Corollary 6.2.12. If \( g \) is Sacks generic over \( M = (M, \in) \), then every countable set of ordinals in \( M[g] \) is a subset of a countable set in \( M \) and \( (2^{\aleph_0})^{M[g]} = (2^{\aleph_0})^M \).

Hence Sacks forcing preserves \( \aleph_1 \). It is known, however, that Sacks forcing may collapse cardinals (see [6]).

## 6.2.5 Destroying the Axiom of Choice

In general there is no direct way of destroying the Axiom of Choice (AC) by a forcing extension of a transitive model of ZFC. One introduces an intermediate model to achieve this.

### Definition 6.2.13.

- A set \( X \) is ordinal definable in \( M \), written \( X \in \text{OD}^M \), if there is a formula \( \varphi(x, v_0, \dots, v_n) \) together with ordinals \( a_0, \dots, a_n, \beta \) in \( M \) such that \( a \in X \Leftrightarrow V_\beta^M \models \varphi(a, a_0, \dots, a_n) \), where \( V_\beta^M \) is the collection of sets in \( M \) of rank less than \( \beta \).

- \( X \) is hereditarily ordinal definable in \( M \), written \( X \in \text{HOD}^M \), if \( \text{TC}(\{X\}) \subset \text{OD}^M \).

If \( M \) is a transitive model of ZFC, then \( (\text{HOD}^M)^\in \) is a transitive model of ZFC (see [53]).

The notion may be generalized to a wider class by defining \( \text{OD}(A)^M \) and \( \text{HOD}(A)^M \). If \( M \) is a transitive model of ZFC and \( A \in M \), then \( (\text{HOD}(A)^M, \in) \) is a transitive model of ZF (see [53]). We use \( \text{HOD}(A)^M \) to obtain a model that destroys AC.

### Definition 6.2.14. Let \( A \in M \).

- A set \( X \) is ordinal definable relative to \( A \) in \( M \), written \( X \in \text{OD}(A)^M \), if there exist ordinals \( a_0, \dots, a_n \), elements \( a_0, \dots, a_m \in A \) and a formula \( \varphi(x, a_0, \dots, a_n, a_0, \dots, a_m, A) \) in the expanded language defining \( X \) in the structure \( \langle M, A, a_0, \dots, a_m, \in \rangle \).

- A set \( X \) is in \( \text{HOD}(A)^M \) if \( \text{TC}(\{X\}) \subset \text{OD}(A)^M \).

### Theorem 6.2.15. Suppose that $\mathcal{M} \models V = L$. Let $\mathbb{P} = \Pi_{\alpha < \omega} C$ be a notion of product Cohen forcing with finite support and let $G$ be a $\mathbb{P}$-generic filter. If $A = \{g \in (\exists i)(\forall j)(g(j) = \bigcup_{p \in G} p(i)(j))$, then there is no well-ordering of the reals in $N = \text{HOD}(\text{TC}(\{A\}))^{\mathcal{M}[G]}$.

Proof. Suppose that there is a bijection $F : 2^\omega \to A$ in $N$ for some $\alpha \in \text{ON}$. We may identify $G$ with the $\omega$-sequence of generic reals $\langle (i, j) \mid g(j) \rangle = \bigcup_{p \in G} p(i)(j) \rangle$.

Let

$\hat{A} = \langle (\dot{G}_i, p) \mid i < \omega \land p \in \mathbf{P} \rangle,$

where $G_i = (\forall j)(\exists p)(p \in G \land G_i(j) = (p(i)(j)))$. Obviously $\text{val}(A, \dot{G}) = A$. Then there is a formula $\phi(x, v, \vec{a}, \vec{a}, A)$ defining $F(x) = v$ via $A$, ordinals $\vec{a}$ and $\vec{a} \in A^{<\omega}$. Let $\phi_1(x, v, \vec{a}, \vec{a}, A)$ be

$x$ is the unique real such that $\phi_0(x, v, \vec{a}, \vec{a}, A)$.

Then for any real $x \in M[G]$, there is a $v < \omega_1$ such that

$\mathcal{M}[G] \models \phi_1(x, v, \vec{a}, \vec{a}, A).$

Let $n$ be the least number such that $\vec{a} \in \mathcal{M}[G_{<n}]$ where $G_{<n} = \langle (i, j) \mid i < n \land (\forall j)(\exists p)(p \in G \land (p(i)(j)) = 1) \rangle$. Then $G_n \in N$, and hence

$\mathcal{M}[G] \models \phi_1(G_n, v, \vec{a}, \vec{a}, A)$

for some $v < a$.

Thus there is a condition $p \in G$ such that

$p \Vdash \phi_1(G_n, \vec{v}, \vec{a}, \vec{a}, \vec{A}).$

Let $m > n$ be the least number not in $\text{Dom}(p)$. Set $\pi : \omega \to \omega$ to be a permutation of $\omega$ that only swaps $m$ with $n$. Then $\pi$ induces an automorphism $\tilde{\pi}$ of $\mathbb{P}$: For every $p \in \mathbf{P}$,

$\text{Dom}(\tilde{\pi}(p)) = \{\pi(i) \mid i \in \text{Dom}(p)\}$

and

$(\tilde{\pi}(p))(\pi(i)) = p(i).$

Obviously $\tilde{\pi}(\dot{v}) = \dot{v}$, $\tilde{\pi}(\dot{\vec{a}}) = \dot{\vec{a}}$, $\tilde{\pi}(\dot{\vec{a}}) = \dot{\vec{a}}$, $\tilde{\pi}(\dot{A}) = A$. Moreover, $p$ is compatible with $\tilde{\pi}(p)$. Hence there is a $q \in \mathbf{P}$ such that $q \le p, \tilde{\pi}(p)$. Then

$q \Vdash \phi_1(G_m, \vec{v}, \vec{a}, \vec{a}, \vec{A})$

and

$q \Vdash \phi_1(G_m, \vec{v}, \vec{a}, \vec{a}, \vec{A}).$

This implies that $q \Vdash G_n = G_m$ which is a contradiction.

## 6.2.6 Exercises

### Exercise 6.2.1. Prove that if ZF is consistent, then so is ZF+ “There is an infinite set \( A \) of reals all of whose subsets are either finite or cofinite in \( A \).”

### Exercise 6.2.2. Prove that Sacks forcing does not satisfy c.c.c.

### Exercise 6.2.3. Prove that if \( g \) is a real Cohen generic over \( M \models \text{ZFC} \), then for any real \( x \in M[g] \setminus M \), there is a \( z \in M \) such that \( x \le_T g \oplus z \).

### Exercise 6.2.4. Prove that if \( g \) is a real Cohen generic over \( M \models \text{ZFC} \), then every analytical real in \( M[g] \) is a member of \( M \).

### Exercise 6.2.5 (Levy [84]). Prove that if \( g \) is a real Cohen generic over \( L \), then \( (\text{HOD})^{L[g]} = L \).

## 6.3 A cardinality characterization of \(\Pi^1_1\)-sets

In this section, we present an application of Martin’s Axiom to the characterization of \(\Pi^1_1\)-sets due to Martin and Solovay [90].

### 6.3.1 Almost disjoint forcing

### Definition 6.3.1. A set \( A \subseteq 2^\omega \) of reals is *almost disjoint* if for any \( x \in A \), \( |x| = \infty \) and for any \( x \neq y \in A \), \( x \cap y \) is finite.

The following notion of forcing was introduced by Silver.

### Definition 6.3.2. Given an index set \( I \), an almost disjoint set \( A = \{x_i\}_{i \in I} \) and \( X \subset I \), \(\mathbb{P} = (\mathbb{P}, \le)\) is an *almost disjoint forcing* corresponding to \( A \) and \( X \) if every \( p \in \mathbb{P} \) is a partial function from \( \omega \) to 2 such that

- \( (\forall i \in X)(|\text{Dom}(p) \cap x_i| < \infty) \); and
- \( |\{n \mid p(n) = 1\}| < \infty \).

We write \( p \le q \) if \( p \supseteq q \).

### Lemma 6.3.3. Given an almost disjoint set \( A = \{x_i\}_{i \in I} \) on an index set \( I \) and \( X \subset I \), the almost disjoint forcing corresponding to \( A \) and \( X \) is c.c.c.

**Proof.** Given two conditions \( p \) and \( q \), \( p \) is incompatible with \( q \) if and only if \(\{n \mid p(n) = 1\} \neq \{n \mid q(n) = 1\}\). Since there are only countably many finite subsets of \( \omega \), the lemma is immediate. \(\square\)
