
Thus $R_a$ is $\Sigma^1_1(r_a)$. Let $r'_a \le_T r_a$ be a well-ordering of $\omega$ of order type $\alpha + 1$. Then $x \in R_a$ if and only if

- (vf) $(\forall n \in O^{r_a*})(f$ is not an embedding of $r_a^*$ into $O^{r_a*}) \wedge$
- (vn) $(\exists m \in O^{r_a*})(\exists g$ is an isomorphism of $(m \mid m <_{r_a} n)$ into an initial segment of $(i \mid i \prec_\omega m))$.

By Exercise 3.6.4, one may take $g$ in the above expression to be hyperarithmetic in $r_a \oplus [i \prec_\omega m]$ which is in turn hyperarithmetic in $r_a \oplus x$. Hence $R_a$ is also $\Pi^1_1(r_a)$ and thus $\Delta^1_1(r_a)$.

### Lemma 3.7.8.

For any $\alpha < \omega_1$, the relation $C_\alpha(x, y) \Leftrightarrow y \le_B x \wedge x \in R_a$ is $\Delta^1_1(r_a)$.

### Proof.

By Corollary 2.2.2 and Lemma 3.7.7, $C_a$ is $\Pi^1_1(r_a)$.

We prove that $C_a$ is $\Sigma^1_1(r_a)$. Now $y \le_B x$ if and only if there is an $n \in O^{r_a}$ such that $y \le_T H_n^a$, and by the previous lemma the latter holds if and only if there is an $n \in O^{r_a*}$ and an $f : [m \mid m <_{\omega^*} n] \to \omega$ such that for all $i <_{\omega^*} j$, $(f(i), f(j)) \in r_a$. Then $y \le_B x$ is $\Sigma^1_1(r_a)$. Thus $C_a$ is $\Sigma^1_1(r_a)$.

### Lemma 3.7.9.

- (i) Every $\Pi^1_1$-set of reals is the union of $\aleph_1$-many Borel sets.
- (ii) Every $\Sigma^1_1$-set of reals is the union of $\aleph_1$-many Borel sets.

### Proof.

(i) Suppose that $A \in \omega^\omega$ is $\Pi^1_1$. By Corollary 3.7.4, there is an arithmetical predicate $A(x, z)$ such that $x \in A \Leftrightarrow (\exists z \le_B x)\Sigma(x, z)$. For any $\alpha < \omega_1$, let $A_\alpha = A \cap R_\alpha$. Then $A_\alpha$ is $\Pi^1_1(r_\alpha)$. By Lemma 3.7.8, $A_\alpha$ is also $\Sigma^1_1(r_\alpha)$. Thus $A_\alpha$ is $\Delta^1_1(r_\alpha)$ and hence Borel.

(ii) Suppose that $A \subseteq 2^\omega$ is $\Sigma^1_1$. Then there is a $\Pi^0_2$ set $B \subseteq \omega^\omega \times 2^\omega$ such that $x \in A$ if and only if $(\exists \beta)B(f, x)$. For $\alpha < \omega_1$, let $A_\alpha = A \cap R_\alpha$. By Lemma 3.7.7, $A_\alpha$ is $\Sigma^1_1(r_\alpha)$.

By the Gandy Basis Theorem 2.5.3, $x \in A$ if and only if $(\exists f <_B O^{r_\alpha}) B(f, x)$. Since $\omega_1^{f*_1} > \omega_1^r$, we have $x \notin r_\alpha$. Relativizing the proof of Corollary 2.4.10 to $r_\alpha$ gives $O^{r_\alpha} \le_B x \oplus r_\alpha$. We conclude that $A_\alpha$ is $\Pi^1_1(r_\alpha)$ and hence $\Delta^1_1(r_\alpha)$.

### Corollary 3.7.10 (Lusin [86]).

Every $\Pi^1_1$-set of reals is measurable.

### Proof.

Following the notations of Lemma 3.7.9, for each $n \in \omega$ and $\alpha < \omega_1$, let $D_{n, \alpha} = \{x \mid n \in O^{r_\alpha*} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$.

Then $D_{n, \alpha}$ is $\Sigma^1_1(r_\alpha)$. By the proof of Lemma 3.7.8 and Exercise 3.6.4,

$D_{n, \alpha} = \{x \mid n \in O^{r_\alpha} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$

and is $\Pi^1_1(r_\alpha)$. Thus $D_{n, \alpha}$ is Borel. Note that $D_{n, \alpha} \cap D_{n, \beta} = \emptyset$ for $\alpha \neq \beta$. Hence for any $n$, there exists an $\alpha_n < \omega_1$ such that $\mu(D_{\beta, n}) = 0$ for $\beta \geq \alpha_n$. Let $\alpha_\omega < \omega_1$ be an upper bound of these $\alpha_n$'s.

Now suppose that $A$ is $\Pi^1_1$. Then for any $\alpha > \alpha_\omega$, $x \in A_\alpha$ implies that there exists an $n$ such that $x \in D_{n, \alpha_\omega}$. In other words, $\bigcup_{\alpha > \alpha_\omega} A_\alpha \subseteq \bigcup_n D_{n, \alpha_\omega}$. By the choice of $\alpha_\omega$, \(\mu(\bigcup_{n<\omega} A_n) = 0\). But \(\bigcup_{n<\omega} A_n\) is a Borel set which is measurable. We conclude that \(A = \bigcup_{\alpha<\omega} A_\alpha\) is measurable.

We will compute the value of \(\alpha_\omega\) in Chapter 14.

### Theorem 3.7.11 (Sierpinski [135]). Every \(\Sigma^1_2\)-set of reals is a union of \(\omega_1\)-many Borel sets.

### Proof.

Suppose that \(A \subseteq 2^\omega\) is \(\Sigma^1_2\). Then there is a \(\Pi^1_1\)-set \(B \subseteq \omega^\omega\) such that \(x \in A\) if and only if \((\exists f \in \omega^\omega) B(f, x)\). By (i) of Lemma 3.7.9, there is an \(\omega_1\)-sequence of Borel sets \(\{B_\alpha\}_{\alpha<\omega_1}\) such that \(\bigcup_{\alpha<\omega_1} B_\alpha = B\). Then \(C_\alpha = \{x \mid (\exists f \in \omega^\omega) B_\alpha(f, x)\}\) is \(\Sigma^1_1\) for each \(\alpha < \omega_1\). Clearly \(A = \bigcup_{\alpha<\omega_1} C_\alpha\). By relativizing (ii) of Lemma 3.7.9, each \(C_\alpha\) is a union of \(\omega_1\)-many Borel sets. Thus \(A\) is a union of \(\omega_1\)-many Borel sets.

### Corollary 3.7.12. Every \(\Sigma^1_2\)-set of reals of cardinality greater than \(\aleph_1\) has a perfect subset.

### Proof.

By Theorem 3.7.11, every \(\Sigma^1_2\)-set \(A\) of reals is the union of \(\aleph_1\)-many Borel sets. If \(A\) has cardinality greater than \(\aleph_1\), then one of these Borel sets is uncountable and so has a perfect subset.

## 3.7.4 Exercises

### Exercise 3.7.1. The following is another proof of Theorem 2.4.7.

- (i) Show that \(\emptyset\) is \(\Sigma_1\)-definable over \(L_{\omega_1^{CK}}\);
- (ii) show that for any reals \(x\) and \(y\), \(x \le_T y\) if and only if \(x \in L_{\omega_1^y}[y]\) and hence \(\emptyset \le_B y\) if and only if \(\omega_1^x < \omega_1^y\).

### Exercise 3.7.2. Prove that there exists a sequence of reals \(\{x_n\}_{n<\omega}\) such that for each \(n\), \(x_n \ge_T x_{n+1}^T\).

### Exercise 3.7.3. Prove that if \(\{x_n\}_{n<\omega}\) is a sequence as above, then for each \(n\), \(x_n\) is not hyperarithmetical.

### Exercise 3.7.4. Use the first version of the Spector–Gandy Theorem (3.7.1) to prove Theorem 3.7.11.

### Exercise 3.7.5. Prove that if \(x\) is a real so that every nonempty \(\Pi^0_1\) set \(A \subseteq \omega^\omega\) has a member hyperarithmetical in \(x\), then \(x \ge_T \emptyset\).

### Exercise 3.7.6. Prove that the set \(\{(x, y) \mid x_0^y > \omega_1^x\}\) is \(\Pi^1_1\) but not \(\Sigma^1_1\).

### Exercise 3.7.7. Assume \(\mathsf{MA} + 2^{\aleph_0} > \aleph_1\) (cf. Definition 6.1.5). Prove that every \(\Sigma^1_2\)-set is measurable.

## 4 The theory of \(\Pi^1_1\)-sets

\(\Pi^1_1\)-sets of reals are endowed with rich structural properties, including those that are best understood from the perspective of the constructible universe \(L\). In this chapter a deeper analysis of such sets is presented to elucidate this point.

### 4.1 A \(\Pi^1_1\)-basis theorem

### 4.1.1 Tree presentations for \(\Pi^1_1\)-sets

Recall that given a \(\Pi^1_1\)-set \(A \subseteq 2^\omega\), there is a recursive predicate \(P \subseteq 2^{<\omega} \times \omega^\omega\) such that \(x \in A\) if and only if \((\forall f)(\exists n) \neg P(x \mid n \mid f \mid n)\). In other words, \(x \in A\) if and only if the \(x\)-recursive tree \(T_x = \{\sigma \mid (\forall \tau)(\tau \subseteq \sigma \rightarrow P(x \mid |\tau|, \tau))\}\) is wellfounded under the Kleene-Brouwer ordering. Then there is a function \(p_x : T_x \rightarrow \omega_1^\omega\) with \(p_x \in L_{\omega_1^x}[x]\) such that \(p_x\) is order preserving underlying the Kleene-Brouwer ordering.

Now let \(T \subseteq 2^{<\omega} \times \omega_1^{<\omega}\) be a set so that \((\sigma, p) \in T\) if and only if \(p\) is an order-preserving finite function from \(\{\tau \mid \tau \subseteq [\sigma]^{|\sigma|}\} \wedge (\forall \tau')( \tau' \subseteq \tau \rightarrow P(\sigma \mid [\tau'], \tau'))\) to \(\omega_1\). Define \((\sigma', p') \geqslant (\sigma, p)\) if and only if \(\sigma' \supseteq \sigma\) and \(p'\) extends \(p\). Then \(T\) is a tree under \(>\). Thus \(x \in A\) if and only if there is an \(f : T_x \rightarrow \omega_1\) such that \((x, f)\) is an infinite path in \(T\), and this holds if and only if there is an \(f : T_x \rightarrow \omega_1\) with \(f \in L_{\omega_1^x}[x]\) such that \((x, f)\) is an infinite path in \(T\).

The advantage with a tree presentation is that the companion path of \(x\) exists in \(L_{\omega_1^x}[x]\).

- Given \((\sigma, p), (\sigma', p') \in 2^{<\omega} \times \omega_1^{<\omega}\), we say that \((\sigma', p') \prec_l (\sigma, p)\) if
  - either \((\sigma', p') \prec (\sigma, p)\), or
  - there is an \(i\) such that \(\sigma'(i) < \sigma(i)\) and for all \(j < i\), \(\sigma'(j) = \sigma(j)\), or
  - there is a \(v \in \omega^{<\omega}\) such that \(p'(v) < p(v)\) and for all \(v' \prec_{KB} v\), \(v \in \text{Dom}(p) \Rightarrow p'(v') = p(v')\).

An infinite path \((x, f)\) in \(T\) is the *leftmost path* if there is no infinite path in \(\{(\sigma, p) \mid (\sigma, p) \prec_l (x \mid [n], f \mid \text{Dom}(p))\}\).

### Lemma 4.1.1. Suppose that \((x, f)\) is the leftmost path of \(T\). Then \(f \in L_{\omega_1^x}[x]\).

### Proof.

Suppose that \((x, f)\) is the leftmost path of \(T\). Then \(f\) is the unique order-preserving function from the \(x\)-recursive tree \(T_x = \{\sigma \mid P(x \mid |\sigma|, o)\}\) onto an initial segment of \(\omega_1^x\). Since \(L_{\omega_1^x}[x]\) is admissible, by the \(\Sigma\)-induction Theorem (3.18), we have \(f \in L_{\omega_1^x}[x]\).
