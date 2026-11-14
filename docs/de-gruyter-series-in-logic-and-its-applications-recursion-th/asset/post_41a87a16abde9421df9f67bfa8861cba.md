
Since Q(y, z) is \(\Sigma_1\), by Theorem 3.1.6, there is a \(v \in M\) such that

\(M \models (\forall y' \in y)(\exists f \in v)(\exists z'(f(y') = z \land P(f))).\)

Hence there is a \(w \in M\) such that \(w = \{f \mid f \in v \land P(f)\}\).

For any \(f_1, f_2 \in w\) and \(y' \in \text{Dom}(f_1) \cap \text{Dom}(f_2)\), we claim that \(f_1(y') = f_2(y')\). Suppose not. Then by the Axiom of Foundation again, there is a \(y'\) such that \(f_1(y') \neq f_2(y')\) but \(f_1(y'') = f_2(y'')\) for all \(y'' \in y'\). However,

\(f_1(y') = G(y', (\langle y'', f_1(y'') \rangle \mid y'' \in y')) = G(y', (\langle y'', f_2(y'') \rangle \mid y'' \in y')) = f_2(y')\),

a contradiction.

Now take \(f' = \bigcup_{f \in w} f\). By Theorem 3.1.7, \(f \in M\). Obviously, Dom(f) is transitive and so P(f). Define \(f' = f \cup \{\langle y, G(y, f \upharpoonright y) \rangle\}\). Then \(M \models f'(y) = G(y, f \upharpoonright y) \land P(f')\) and so \(M \models Q(y, G(y, f' \upharpoonright y))\). Hence \(M \models (\exists z)Q(y, z)\), a contradiction.

Thus KP ⊢ \((\forall y)(\exists z)Q(y, z)\).

### Remark 3.1.9.

Defining a function such as G in Theorem 3.1.8 quite often requires one to go through a series of straightforward, though tedious, steps of \(\Sigma_1\)-induction. Henceforth we will leave the details of these steps to the reader and refer to them simply as “applying Theorem 3.1.8 by \(\Sigma_1\)-induction”.

Theorem 3.1.8 is a central result in the theory of admissible sets. It plays the same role as that of effective transfinite induction in descriptive set theory. We illustrate this point with an application of the theorem. Define the transitive closure operator TC to be:

\(\text{TC}(\emptyset) = \emptyset\), and

\(\text{TC}(a) = a \cup \bigcup \{\text{TC}(x) \mid x \in a\}.\)

By induction on the relation \(\in\), one shows that for any set x, TC(x) is the smallest transitive set containing x. The question is whether this operator is well defined in KP.

Let G be a \(\Sigma\)-function such that \(G(\emptyset, y) = \emptyset\) and \(G(x, y) = x \cup \bigcup \{y_1 \mid \langle y_0, y_1 \rangle \in y\}\). Then by Theorem 3.1.8 there is a \(\Sigma\)-function F such that \(F(x) = G(x, (\langle y, F(y) \rangle \mid y \in x))\). It is not difficult to verify that for each x, F(x) = TC(x). We have the following corollary.

### Corollary 3.1.10.

KP ⊢ TC(x) is a \(\Sigma\)-function.

By Corollary 3.1.10, together with the proof of Theorem 3.1.8, we have the following theorem.

### Theorem 3.1.11.

Let G be an n + 2-ary \(\Sigma\)-function. There is an n + 1-ary \(\Sigma\)-function F such that

\(\text{KP} \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, (\langle z, F(z, x_1, \dots, x_n) \rangle \mid z \in \text{TC}(y))).\)

Let rk be a function such that

rk(∅) = 0, and

rk(x) = sup{rk(y) + 1 | y ∈ x}.

By Theorem 3.1.8, rk is a Σ-function from sets to ordinals. For any set x, rk(x) is called the rank of x. The rank function is a convenient tool to use when performing transfinite induction.

### 3.1.3 The collapsing lemma

A set x is transitive in z if y ⊆ z ⊆ x for all y ∈ x. A set x is transitive if z = x, i.e. y ⊆ x for all y ∈ x. Using Theorem 3.1.8, we define a Σ-operation C_x(y) as follows:

C_x(∅) = ∅;

C_x(a) = \{C_x(y) \mid y \in a \cap x\}.

It is easy to verify that C_b(b) is transitive for all b. Moreover if a ⊆ b and a is transitive, then C_b(x) = x for all x ∈ a. Define c_b = \{(x, C_b(x)) \mid x \in b\}. One may view c_b as a map from b onto the transitive set C_b(b). In general, c_b is not injective.

A set a is extensional if for all b_1, b_2 ∈ a, (∀x ∈ a)(x ∈ b_1 ↔ x ∈ b_2) → b_1 = b_2. In other words, a is extensional if each set in a is determined by its membership in a. Obviously any transitive set is extensional. The following theorem says that any extensional set is isomorphic to a transitive set.

### Theorem 3.1.12 (Mostowski [108]).

If a is extensional then c_a is a bijection between a and C_a(a). Furthermore, for all x, y ∈ a, x ∈ y ↔ C_a(x) ∈ C_a(y).

**Proof.** Obviously c_a is a surjective map from a to C_a(a) and x ∈ y implies c_a(x) ∈ c_a(y). We show that for all x, y ∈ a, c_a(x) ∈ c_a(y) implies x ∈ y. Then by the extensionality of a, c_a is injective.

Suppose there is a y_0 ∈ a such that for all y ∈ a with rk(y) < rk(y_0) and x ∈ a, x ∈ y ↔ c_a(x) ∈ c_a(y) but there is an x_0 ∈ a such that x_0 ∉ y_0 and c_a(x_0) ∈ c_a(y_0). Since c_a(x_0) ∈ c_a(y_0), there is z ∈ a∩y_0 such that c_a(x_0) = c_a(z) = c_a(y_0). Then rk(z) < rk(y_0). However, this implies x_0 = z ∈ y_0, a contradiction.

### 3.1.4 Definability

Denote by M the domain of a structure M.

### Definition 3.1.13.

Let F be a set of formulas in L.

- (i) Given a structure M and A ⊆ M, we say that A is F-definable in M if there is a formula φ(u, v_0, ..., v_n) ∈ F and a finite sequence a_0, ..., a_n in M such that x ∈ A if and only if M ⊨ φ(x, a_0, ..., a_n);
- (ii) if \(\mathfrak{M}\) is a collection of structures and \(A_M \subseteq M\) for \(\mathfrak{M} \in \mathfrak{M}\), then \(\{A_M\}_{\mathfrak{M} \in \mathfrak{M}}\) is \(\mathfrak{F}\)-uniformly definable in \(\mathfrak{M}\) if there is a formula \(\varphi(u)\) in \(\mathfrak{F}\) without parameters such that for any \(\mathfrak{M} \in \mathfrak{M}\), \(x \in A_{\mathfrak{M}}\) if and only if \(\mathfrak{M} \models \varphi(x)\).

Note that for a collection of structures to be uniformly definable, there should be no parameters in the formula defining it.

### 3.1.5 Absoluteness

### Definition 3.1.14.

Given a set of sentences \(\mathfrak{F}\) in \(\mathscr{L}\), we say that two \(\mathscr{L}\)-structures \(\mathfrak{M}\) and \(\mathfrak{N}\) are \(\mathfrak{F}\)-elementarily equivalent, written \(\mathfrak{M} \equiv_{\mathfrak{F}} \mathfrak{N}\), if for every \(\varphi \in \mathfrak{F}\), \(\mathfrak{M} \models \varphi \Leftrightarrow \mathfrak{N} \models \varphi\).

If \(\mathfrak{F}\) is the set of all sentences, then we say that \(\mathfrak{M}\) and \(\mathfrak{N}\) are *elementarily equivalent* and write \(\mathfrak{M} \equiv \mathfrak{N}\).

### Definition 3.1.15.

Given a set of sentences \(\mathfrak{F}\), we say that an embedding \(j\) from \(\mathfrak{M}\) into \(\mathfrak{N}\) is \(\mathfrak{F}\)-elementary and write \(\mathfrak{M} \prec_j^{\mathfrak{F}} \mathfrak{N}\) if for every \(\varphi(\bar{v}) \in \mathfrak{F}\) and finite sequence \(\bar{a} \in M^{<\omega}\), \(\mathfrak{M} \models \varphi(\bar{a}) \Leftrightarrow \mathfrak{N} \models \varphi(j(\bar{a}))\).

If \(\mathfrak{F}\) is the set of all formulas, then we write \(\mathfrak{M} \prec^j \mathfrak{N}\). If \(j\) is the inclusion map, then we write \(\mathfrak{M} < \mathfrak{N}\) and say that \(\mathfrak{M}\) is an *elementary substructure* of \(\mathfrak{N}\), and \(\mathfrak{N}\) is an *elementary extension* of \(\mathfrak{M}\).

### Definition 3.1.16.

Given a class \(\mathfrak{M}\) of structures and a formula \(\varphi(\bar{v})\), (i) \(\varphi\) is \(\mathfrak{M}\)-upward absolute if for every pair \(\mathfrak{M} \subseteq \mathfrak{N}\) in \(\mathfrak{M}\) and any finite sequence \(\bar{a} \in M^{<\omega}\), \(\mathfrak{M} \models \varphi(\bar{a})\) implies \(\mathfrak{N} \models \varphi(\bar{a})\); (ii) \(\varphi(\bar{v})\) is \(\mathfrak{M}\)-downward absolute if for every pair \(\mathfrak{M} \subseteq \mathfrak{N}\) in \(\mathfrak{M}\) and any finite sequence \(\bar{a} \in M^{<\omega}\), \(\mathfrak{N} \models \varphi(\bar{a})\) implies \(\mathfrak{M} \models \varphi(\bar{a})\); (iii) \(\varphi(\bar{v})\) is \(\mathfrak{M}\)-absolute if it is both \(\mathfrak{M}\)-upward and downward absolute.

### Proposition 3.1.17.

Let \(\mathfrak{M}\) be a class of transitive structures. (i) Every \(\Sigma_0\)-formula is \(\mathfrak{M}\)-absolute; (ii) every \(\Sigma_1\)-formula is \(\mathfrak{M}\)-upward absolute; (iii) every \(\Pi_1\)-formula is \(\mathfrak{M}\)-downward absolute. Hence every \(\Delta_1\)-formula is \(\mathfrak{M}\)-absolute.

**Proof.** We prove (i) by induction on the complexity of \(\Sigma_0\)-formulas and leave (ii) and (iii) to the reader. Suppose \(\mathfrak{M} \subseteq \mathfrak{N}\) and \(\varphi(a)\) has the form \((\exists u \in a)\psi(u, a)\) for some \(\Sigma_0\)-formula \(\psi(u, a)\) with \(a \in M\). If \(\mathfrak{M} \models \varphi(a)\), then there exists an \(a' \in M\) such that \(\mathfrak{M} \models \psi(a', a)\). Since \(\mathfrak{M} \subseteq \mathfrak{N}\), by induction \(\mathfrak{N} \models \psi(a', a)\). If \(\mathfrak{N} \models \varphi(a)\), then there exists an \(a' \in N\) such that \(\mathfrak{N} \models \psi(a', a)\). Since \(a' \in a\) and \(a \in M\), by transitivity we have \(a' \in M\). Then by induction, \(\mathfrak{M} \models \psi(a', a)\).
