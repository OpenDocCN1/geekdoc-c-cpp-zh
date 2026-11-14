
## 10 Rigidity and biinterpretability of hyperdegrees

Let $(\mathscr{P}_h, \le)$ denote the structure of hyperdegrees under the partial ordering $\le$ for hyperarithmetic reducibility. As for the Turing degrees $(\mathscr{P}, \le_T)$, the hyperdegrees form an upper semilattice under the join operator $\cup$, where if the hyperdegrees of $x$ and $y$ are respectively $\mathbf{a}$ and $\mathbf{b}$, then $x \oplus y$ has hyperdegree $\mathbf{a} \cup \mathbf{b}$. Note that $\cup$ may be defined in terms of $\le$. A map of $\mathscr{P}$ or $\mathscr{P}_h$ into itself is an *automorphism* if it is a bijection and preserves $\le$. A major open problem in recursion theory asks whether the identity map is the only automorphism for the Turing degrees, i.e. whether the Turing degrees are *rigid*. Slaman and Woodin ([141] and [144]) used a sophisticated metamathematical argument to prove a number of remarkable results about $(\mathscr{P}, \le_T)$, including the theorem that there are at most countably many nontrivial automorphisms for the structure (indeed the degrees $\ge \mathbf{0}'$ are invariant under any automorphism), and that the hyperdegrees are rigid. In this chapter, we present a more “elementary” proof of the latter due to Shore [133]. The biinterpretability of $(\mathscr{P}_h, \le)$ with second-order arithmetic follows as an application of rigidity (see § 10.3).

### 10.1 Embedding lattices into hyperdegrees

Recall that a partially ordered set $(\mathscr{C}, \le)$ is a *lattice* if any two members $c, c' \in \mathscr{C}$ have a least upper bound and a greatest lower bound denoted $c \cup c'$ and $c \cap c'$ respectively. A lattice is recursively presented if its elements (via some effective coding) are enumerated recursively. A partial ordering under $\le$ is a partial lattice if the relations $\le, \nleq$ and operators $\cup, \cap$ are partial recursive. The next theorem goes back to Jónsson [61] (see also Lerman [81] and Shore [132]).

**Theorem 10.1.1.** *Suppose* $\mathscr{C} = \{c_i\}_{i < \omega}$ *is an enumeration of a recursively presentable partial lattice with least element* $c_0$*. There is a uniformly recursive array* $\langle f_n \in \omega^\omega \mid n < \omega \rangle$ *of functions such that for all* $i, j, k, m$ *and* $n$ *,*

- (i) $f_n(0) = 0$;
- (ii) $c_i \le c_j \Rightarrow [\exists d, e (f_d(i) = f_e(i) \land f_d(i) \neq f_e(i))]$;
- (iii) $c_i \cup c_j = c_k \Rightarrow [\exists d, e (f_d(i) = f_m(i) \land f_d(j) = f_m(j) \Rightarrow f_n(k) = f_m(k)];$
- (iv) $c_i \cup c_j = c_k \Rightarrow f_m(i) = f_m(i) \land f_n(j) \Rightarrow f_m(i) = f_m(k)];$
- (v) $c_i \cap c_j = c_k \land f_n(k) = f_m(k) \Rightarrow (\exists d_1, d_2, d_3)[f_n(i) = f_{d_1}(i) \land f_n(i) = f_{d_1}(i) \land f_{d_2}(i) = f_{d_3}(i) \land f_{d_3}(i) = f_{d_3}(i)];$

Proof. Define

$f^*_{2j+1}(i) = \begin{cases} 0 & i = 0, \\ 2^{j+1} & i > 0. \end{cases}$

and

$$f^*_{2j}(i) = \begin{cases} 0 & i = 0, \\ 2^{j+1} & c_i \le c_j, \\ 2^j & c_i \nleq c_j. \end{cases}$$

We use $\{f_i^*\}_{i \in \omega}$ as the basis to generate the array $\{f_n\}_{n \in \omega}$. It is straightforward to verify that (i)--(v) hold for each $f_i^*$. For any two functions $f, \hat{f}$ that have been generated and satisfy the hypothesis of (v), we define the functions $\hat{f}_{d_1}, \hat{f}_{d_2}, \hat{f}_{d_3}$ as follows: If $c_i \le c_j$, then set $\hat{f}_{d_1} = \hat{f}_{d_2} = \hat{f}_{d_3} = \hat{f}$ and (v) holds. If $c_i \nleq c_j$, let $a_1, a_2, a_3, a_4$ be numbers not in the range of $f$ and $\hat{f}$. Define

$$\hat{f}_{d_1}(s) = \begin{cases} f(s) & c_s \le c_i, \\ a_1 & c_s \nleq c_i. \end{cases}$$ $$\hat{f}_{d_2}(s) = \begin{cases} f(s) & c_s \le c_j, \\ a_2 & c_s \le c_i \land c_s \notin c_j, \\ a_3 & \text{Otherwise.} \end{cases}$$ $$\hat{f}_{d_3}(s) = \begin{cases} \hat{f}(s) & c_s \le c_j, \\ a_2 & c_s \le c_i \land c_s \notin c_j, \\ a_4 & \text{Otherwise.} \end{cases}$$

We leave it to the reader to verify that (v) is satisfied for $f, \hat{f}$, and that (i)--(iv) remain valid with the addition of the three new functions. The collection of functions generated through this process is a recursive array $\{f_n\}_{n \in \omega}$ stipulated by the theorem.

An adaptation of Cohen forcing (§ 5.2) allows one to embed a recursively presented lattice into the hyperdegrees.

**Theorem 10.1.2.** Let $\mathcal{C} = \{c_i\}_{i < \omega}$ be a recursive partial lattice with 0 and let $\{f_n\}_{n < \omega}$ be a recursive representation of $\mathcal{C}$ as given in Theorem 10.1.1. Let $\mathfrak{A}(\omega_1^{\text{CK}})$ be the structure defined in § 5.1 for the ramified analytical hierarchy. If $g$ is Cohen generic over $\mathfrak{A}(\omega_1^{\text{CK}})$, then there is a sequence of sets $\{h_i\}_{i < \omega}$ such that $h_i \le_T g$ and the map taking $c_i$ to the hyperdegree of $h_i$ is an embedding of $\mathcal{C}$ in $\mathscr{D}_h$ preserving $\le, \vee, \cup$ and $\cap$.

**Proof.** The notion of Cohen forcing we consider here is defined over the Baire space $\omega^\omega$ rather than over the Cantor space $2^\omega$ as was defined in § 5.2. A condition is a finite collection of a consistent set of relations of the form $\sigma(m) = n$. The generic set $g$ is then a function that is an element of $\omega^\omega$ such that $\omega_1^{\text{CK}} = \omega_1^{\text{CK}, g}$. Recall also by Corollary 5.2.6 (ii) that if $g$ is Cohen generic and $h \le_T g$, then $h \le_T g \oplus \emptyset'$ for some recursive ordinal $\gamma$.

For each $i$, let $h_i(n) = f_{g(n)}(i)$. First of all, $h_0(n) = f_{g(n)}(0) = 0$ for all $n$ according to Theorem 10.1.1 (i), so that $0 \in \mathcal{C}$ is mapped to a recursive set. Suppose $c_i \le c_j$. For each $n$, search for the least $m$ such that $f_m(n) = h_i(n) = f_{g(n)}(j)$. Note that such $m$ must exist since $g(n)$ is a candidate. Then $f_m(i) = f_{g(n)}(i) = h_i(n)$. Since $\{f_n\}_{n < \omega}$ is uniformly recursive, we have in fact $h_i \le_T h_j$, showing that the map preserves order.

Now suppose \(c_i \cup c_j = c_k\). To compute \(h_k(n)\) which is \(f_{g(n)}(k)\), recursively find an \(m\) such that \(f_m(i) = h_i(n) = f_{g(n)}(i)\) and \(f_m(j) = h_j(n) = f_{g(n)}(j)\). By Theorem 10.1.1 (iv), one has \(f_m(k) = f_{g(n)}(k) = h_k(n)\). Hence the embedding preserves join when it is defined.

We use the genericity of \(g\) to argue that \(\vee\) and \(\cap\) are preserved under the embedding. Assume \(c_i \nleq c_j\). By Theorem 10.1.1 (iii), there exist \(m, n\) such that \(f_m(i) = f_n(j)\) and \(f_m(i) \neq f_n(i)\). If \(h_i \leq h_j\), then there is a \(k \in \omega\), a number \(e\) and a condition \(p\) such that
\(p \Vdash h_i = \Phi_{e_i}^{h_j}\).

Let \(q\) be a condition extending \(p\) containing \(d\) not in the domain of \(p\) such that \(q \Vdash g(\bar{d}) = \bar{n}\), and \(q\) decides the value of \(\Phi_{e_i}^{h_j}(\bar{d})\). Let \(q'\) be similar to \(q\) except that it replaces \(m\) for \(n\). Since generic extensions of \(q\) and \(q'\) which differ in value only at \(d\) have the same interpretation for \(h_j\), both conditions force the same value for \(\Phi_{e_i}^{h_j}(\bar{d})\). Then
\(q \Vdash \Phi_{e_i}^{h_j}(\bar{d}) = f_n(i) \text{ and } q' \Vdash \Phi_{e_i}^{h_j}(\bar{d}) = f_m(i)\).

which contradict our choice of \(m\) and \(n\). Hence \(c_i \nleq c_j\) implies \(h_i \nleq h_j\).

The final case to consider is when \(c_i \cap c_j = c_k\). By the preservation of order under embedding, we have \(h_i \cap h_j \leq h_k\). Assume that \(f \nleq h_i\) and \(f \nleq h_j\) with the aim of showing \(f \nleq h_k\). Let \(p\) be a condition extended by \(g\) such that
\(p \Vdash f = \Phi_{e_0}^{h_j} = \Phi_{e_1}^{h_j}\).

for some \(m, n \in \omega\) and \(e_0, e_1\). For a given \(u\), use \(h_k\) to find a condition \(q\) extending \(p\) such that \(q\) forces a (necessarily common) value for \(\Phi_{e_0}^{h_j}(i)\) and \(\Phi_{e_1}^{h_j}(i)\) so that \(h_k(d) = f_{g(d)}(k)\) for every \(d\) in the domain of \(q\) (note that \(f_{g(d)}(k) = f_{g(d)}(k)\) for every \(d\) in the domain of \(q\)). We claim that this is an algorithm for computing \(f\) hyperarithmetically in \(h_k\).

Since forcing relation for a ranked formula is hyperarithmetic, and since the search for a condition to satisfy the second half of the above statement is recursive, \(q\) may be computed hyperarithmetically in \(h_k\). We show that the value \(\Phi_{e_i}^{h_j}(i)\) is the correct value for \(f(u)\). Assume for the sake of contradiction that \(v \neq w\) are numbers such that
\(\Phi_{e_0}^{h_j}(u) = \Phi_{e_1}^{h_j}(u) = w \text{ and } q \Vdash \Phi_{e_0}^{h_j}(v) = \Phi_{e_1}^{h_j}(v) = v\).

By the genericity of \(g\), there is a condition \(r\) stronger than \(p\) and extended by \(g\) such that
\(r \Vdash \Phi_{e_0}^{h_j}(u) = \Phi_{e_1}^{h_j}(u) = \bar{w}\).

By extending the domains if necessary, we may assume that \(q\) and \(r\) have the same domain. Then \(f_{g(d)}(k) = h_d(k) = f_{g(d)}(k)\) for every \(d\) in the domain. By Theorem 10.1.1 (v), for each such \(d\) there exist numbers \(d_1, d_2\) and \(\bar{d}_3\) satisfying the conclusion in (v) for \(f_{g(d)}\) and \(f_{f(d)}\). For \(l = 1, 2, 3\), let \(q_l\) be a condition such that \(q_l(d) = \bar{d}_l\) and let \(g_l(d) = g(d)\) if \(d\) is not in the domain of \(q_l\), and equal to \(q_l(d)\) otherwise. Then \(g_1\)
