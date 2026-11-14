
By the Claim and Lemma 5.3.3, one may define a condition \( S \le T \) such that

\( (\forall \sigma, \sigma' \in S)(\exists m)(\exists j < 2)(\sigma \upharpoonright j' \to S \cap \sigma \upharpoonright j \neq \varphi(m, j) \land S \cap \sigma \upharpoonright j' \neq \varphi(m, 1 - j)). \)

Furthermore, there is a hyperarithmetic function \( f \) mapping \( (\sigma, \sigma') \) to an appropriate \( (m, j, 1 - j) \).

\( D_\varphi = \{S \mid S \Vdash \neg(\forall n)(\exists l < 2)\varphi(n, i) \text{ or } S \text{ satisfies } (*)\}.\)

Then \( D_\varphi \) is a dense set arithmetic in \( \mathcal{O} \). By the assumption on \( x \), there is an \( S \in D_\varphi \) such that \( x \in [S] \) and \( S \) satisfies (*). The function \( f \) defined on \( S \) effectively separates the reals in \( [S] \), and hence \( x \) is recursive in \( y \# f \). Since \( f \) is hyperarithmetic, we conclude that \( x \le_h y \).

## 5.3.3 A \(\Sigma^1_1\)-set of minimal hyperdegrees

Let \( \varphi \) be ranked and

\( \hat{D}_\varphi = \{S \mid S \Vdash \neg(\forall n)(\exists l < 2)\varphi(n, i) \text{ or } (\forall n)(\exists l < 2)S \Vdash \varphi(n, i) \text{ or } S \text{ satisfies } (*) \text{ defined in the proof of Theorem 5.3.8}.\}\)

Define \( x \) to be weakly Sacks generic if for any ranked \( \varphi(n, i) \), there is a condition \( S \in \hat{D}_\varphi \) such that \( x \in [S] \). Note that the set \(\{S \mid \forall n,i \, S \in \hat{D}_\varphi \}\) is \(\Pi^1_1\). By the proof of Theorem 5.3.8, \(\hat{D}_\varphi\) is dense for every ranked \( \varphi(n, i) \). Moreover, by going through the proof of Theorem 5.3.8, we have the following lemma.

### Lemma 5.3.9. Let \( x \) be weakly Sacks generic and \( n \in \mathcal{O} \). If \( 0 <_n y \le_T H_n^x \), then \( x \le_h y \).

Let \(\{\varphi_\beta\}_{\beta < \omega_1^{ck}}\) be a \(\Sigma^1_1(L_{\omega_1^{ck}}(x))\)-enumeration of all ranked sentences. By the Fusion Lemma (5.3.3) and Theorem 5.3.8, we may define by induction a \(\Sigma^1_1(L_{\omega_1^{ck}})\)-enumeration of sets of conditions \(\{\mathscr{I}_\beta\}_{\beta < \omega_1^{ck}}\) such that for any \(\gamma < \beta < \omega_1^{ck}\),

- (i) \( (\forall S \in \mathscr{I}_\gamma)(S_0 \in \mathscr{I}_\beta \to S_0 \le S \cap [t_S(0)] \wedge S_1 \le S \cap [t_S(1)]) \), where \( t_S \) is the natural homeomorphic map from \( 2^{<\omega} \) to \( S \);
- (ii) \( (\forall S \in \mathscr{I}_\beta)(\exists n)(\exists \sigma \in S)(\forall \tau \in S)([S] \subseteq \bigcup_{\sigma \in S}[S_\tau]) \), and
- (iii) \( (\forall S \in \mathscr{I}_\beta)(\forall \alpha \in 2^{n+1})(S \cap [t_S(\alpha)] \in \hat{D}_{\varphi_\beta}) \).

Let \(\mathscr{I}_0 = \{2^{<\omega}\}\). At stage \(\beta + 1\), for any \( S \in \mathscr{I}_\beta \), by the density of \(\hat{D}_{\varphi_\beta}\), let \( S_0, S_1 \in \hat{D}_{\varphi_\beta} \) be the \( <_l \)-least pair of conditions such that \( S_0 \le S \cap [t_S(0)] \) and \( S_1 \le S \cap [t_S(1)] \). Let \( S_0, S_1 \in \mathscr{I}_{\beta+1} \).

At limit stage \(\lambda\), let \(\{\beta_i\}_{i < \omega}\) be the \( <_l \)-least increasing \(\omega\)-sequence of ordinals with limit \(\lambda\). For \(\beta < \lambda\), let \(\beta_i\) be the least \( i \) such that \(\beta \le \beta_i\). By the inductive hypothesis, it is not difficult to see that there is a \( <_l \)-least fusion sequence \(\{S_\alpha\}_{\alpha \in 2^{<\omega}}\) such that

- - \( S_0 = S \);
- - \( (\forall n)(\forall \alpha \in 2^{n+1})(S_\alpha \in \mathscr{I}_{\beta_{|\alpha|}}). \)

Let \( T = \bigcap_{n<\omega} \bigcup_{n<\omega} S_n \). Put \( T \cap [\tau_T(0)] \) and \( T \cap [\tau_T(1)] \) into \( \mathscr{S}_A \). We leave it to the reader to verify that \( \{\mathscr{S}_\beta\}_{\beta < \alpha^{CK}_1} \) satisfies (i)-(iii). The following is an immediate consequence of (iii).

### **Lemma 5.3.10.** If for any \( \beta < \omega_1^{CK} \) there is a condition \( S_p \in \mathscr{S}_\beta \) such that \( x \in [S_p] \), then \( x \) is weakly Sacks generic.

Now let

\( A = \{(n, x) \mid (\exists S)(x \in [S] \land S \in \mathscr{S}_{\langle n \rangle} \land n \in \omega\} \).

Since every \( S \in \mathscr{S}_\beta \) is hyperarithmetic, by Corollary 2.2.12, \( A \) is \( \Pi^1_1 \). Moreover, for any \( n \), \( A_n = \{x \mid (n, x) \in A\} \) is \( \Delta^1_1 \).

### **Lemma 5.3.11.** \( \bigcap_{n \in \mathcal{O}_1} A_n \) is an uncountable \( \Sigma^1_1 \)-set.

**Proof.** Obviously \( \bigcap_{n \in \mathcal{O}_1} A_n \) is \( \Sigma^1_1 \). By the definition of \( \{\mathscr{S}_\beta\}_{\beta < \alpha^{CK}_1} \), for any \( n \in \mathcal{O}_1 \), \( \bigcap_{m < n} A_m \neq \emptyset \). Hence for any \( A'_1 \supseteq \mathcal{O}_1 \cap \bigcap_{n \in \mathcal{O}_1} A_n \neq \emptyset \). By the Kreisel Compactness Theorem (4.2.4), \( \bigcap_{n \in \mathcal{O}_1} A_n \) is nonempty. Since no member of this set is hyperarithmetic, by Lemma 2.5.4 it is uncountable.

### **Theorem 5.3.12** (Simpson [138]). There is an uncountable \( \Sigma^1_1 \)-set of minimal hyperdegrees.

**Proof.** Let \( M = \{x \mid x \notin HYP \land x \in \bigcap_{n \in \mathcal{O}_1} A_n \land \omega^x_1 = \omega_1^{CK}\} \). Then \( M \) is \( \Sigma^1_1 \) and by Lemma 5.3.11 and the Gandy Basis Theorem (2.5.3), \( M \) is nonempty. By Lemma 2.5.4, \( M \) is uncountable. By Lemma 5.3.9, every \( x \in M \) is of minimal hyperdegree.

By relativizing the proof of Theorem 5.3.12 (see [138]), one can show that there is a \( \Sigma^1_1 \)-set \( M \subseteq 2^\omega \times 2^\omega \) such that for any \( x \), there is a \( y \) with \( (x, y) \in M \), and for any \( (x, y) \in M \), \( y \)'s hyperdegree is a minimal cover of the hyperdegree of \( x \).

## 5.3.4 Exercises

### **Exercise 5.3.1** (Sacks [123]). Prove that \( x \) is Sacks generic if and only if for every sentence \( \varphi \), there is an \( S \in D_\varphi \) such that \( x \in [S] \).

### **Exercise 5.3.2** (Simpson [138]). Prove that there are two reals \( x, y \) of minimal hyperdegree such that \( x \oplus y \geq_T 0 \).

### **Exercise 5.3.3.** Prove that no weakly Sacks generic real is hyperarithmetic.

### **Exercise 5.3.4.** Let \( X \) be a \( \Pi^1_1 \)-set of ranked sentences. Assume that if \( A \subseteq X \) is \( \Delta^1_1 \), then there is an \( x \) such that \( \mathfrak{A}(\omega_1^{CK}, x) \) is a model of \( A \). Show that there is an \( x \) such that \( \mathfrak{A}(\omega_1^{CK}, x) \) is a model of \( X \).

### **Exercise 5.3.5** (Simpson [138]). If there is an \( x \) such that \( 2^\omega = L(x) \cap 2^\omega \), then for any \( z \), there is a \( y \geq_T z \) whose hyperdegree is not a minimal cover of any hyperdegree.

## 5.4 Characterizing countable admissible ordinals

By relativizing the proof of Corollary 3.6.7, one can show that $\omega_1^x$ is a countable admissible ordinal for any $x$. The converse was proved by Sacks [122]: every countable admissible ordinal $\alpha > \omega$ is $\omega_1^x$ for some $x$. His proof produces in addition an $x$ such that no $y <_h x$ satisfies $\omega_1^y = \alpha$. We prove a weaker result, that $\alpha = \omega_1^x$ for some $x$, using a notion of forcing introduced by Steel [158]. Let $\alpha$ be a countable admissible ordinal greater than $\omega$ for the rest of the section.

### 5.4.1 Generalized ramified analytical hierarchy

Let \(\mathfrak{L}(\alpha, x)\) be a language consisting of the following:

- number variables: $i, j, k, m, n, \dots$
- numerals: $0, \bar{1}, \bar{2}, \dots$
- constants: $x, y, \dots$
- ranked set variables: $x^\gamma, y^\gamma, \dots$ where $\gamma < \alpha$
- unranked set variables: $x, y, \dots$
- operations and relation: $+, \cdot, (\text{times}), / (\text{successor})$ and $\in$.

Formulas are defined by induction. The set of number-theoretic terms is the set of terms closed under $+, \cdot$ over numerals and number variables. Atomic formulas are formulas of the form $t = s$ and $t \in x$, where $t$ and $s$ are number-theoretic terms. The other formulas are generated in the usual way. A formula is *ranked* if all of its set variables are ranked. A ranked formula $\varphi$ has rank at most $\gamma$ if

- - for any $\beta$, if $x^\beta$ is a free variable occurring in $\varphi$, then $\beta \le \gamma\);
- - for any $\beta$, if $x^\beta$ is a bound variable occurring in $\varphi$, then $\beta < \gamma\).

By $\Sigma$-induction on $L_\alpha$, we have

- - the set of formulas is $\Sigma_1$ in $L_\alpha\);
- - the set \(\{(\gamma, \varphi) \mid \varphi \text{ is a ranked formula of rank at most } \gamma\}\) is \(\Delta_1\) in \(L_\alpha\).

Given $x$, one now defines the structure \(\mathfrak{A}(\alpha, x) = \bigcup_{\beta < \alpha} \mathfrak{A}(\beta, x)\), where $x$ interprets the symbol \(\dot{x}\) as a countable union of collations of reals. During the construction, a ranked variable $x^\gamma$ is to be interpreted as a real in \(\bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x)\). The satisfaction relation \(\bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \models \varphi\), for a ranked formula \(\varphi\) with rank at most \(\gamma\), is well defined. \(\mathfrak{A}(\alpha, x)\) is constructed by induction on ordinals less than \(\alpha\):

- - $\gamma = 0$: $\mathfrak{A}(\gamma, x) = t(\gamma) \cup \omega$.
- - $\gamma > 0$: Suppose $\mathfrak{A}(\beta, x)$ is defined for all $\beta < \gamma$. For a ranked formula $\varphi(n)$ with rank at most $\gamma$ and $n$ as the only free variable, let

```
$i \in z_\varphi \Leftrightarrow \bigcup_{\beta < \gamma} \mathfrak{A}(\beta, x) \models \varphi(i).$
```
