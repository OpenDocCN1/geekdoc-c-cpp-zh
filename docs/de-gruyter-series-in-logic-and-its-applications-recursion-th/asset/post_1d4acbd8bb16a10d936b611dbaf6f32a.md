
By induction hypothesis, there is a formula \(\phi'\) corresponding to \(\vee_{i \le j} \psi(\eta_i)\) (i.e. \(\ulcorner \phi' \urcorner = f(\ulcorner \vee_{i \le j} \psi(\eta_i) \urcorner, m+1)\)) so that

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \vee_{i \le j} \psi(\phi_i)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) < 2^{-m-1}.\)

Then \(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = (\exists \beta)\rho(\beta^x)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) < 2^{-m}\). Let \(f'((\exists \beta)\phi(\varphi(\beta^x)), m) = \ulcorner \phi' \urcorner\).

For \((\forall x \beta)\phi(\varphi(\beta^x))\), we have \(\mathfrak{A}(\omega_1^{\text{CK}}, x) = (\forall x \beta^j)\phi(\varphi(\beta^x))\) if and only if for all \(j < \omega\), \(\mathfrak{A}(\omega_1^{\text{CK}}, x) = \wedge_{i \le j} \psi(\eta_i)\). By induction hypothesis, there is a hyperarithmetic function taking each \(j\) to a formula \(\phi'_j\) corresponding to \(\wedge_{i \le j} \psi(\phi_i)\) (i.e. \(\ulcorner \phi'_j \urcorner = f(\ulcorner \wedge_{i \le j} \psi(\phi_i) \urcorner, m+j+2)\)) so that

\(\mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \wedge_{i \le j} \psi(\phi_i)\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j\}) < 2^{-m-j-2}.\)

Now \(\{x \mid (\forall j)\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j\}\) is hyperarithmetic. Hence there is a ranked formula \(\phi'\) such that for any \(x\),

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi' \Leftrightarrow (\forall j)\mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'_j.\)

Note that the set \(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}\) is closed. Moreover,

\(\mu(\{x \mid (\forall x \beta^j)\phi(\varphi(\beta^x))\}) - \mu(\{x \mid \mathfrak{A}(\omega_1^{\text{CK}}, x) = \phi'\}) \le \sum_{i < \omega} 2^{-m-i-2} < 2^{-m}.\)

Thus define \(f'((\forall x \beta)\phi(\varphi(\beta^x)), m) = \ulcorner \phi' \urcorner\). For the other cases, the definition of \(f\) is straightforward. \(\square\)

### Corollary 13.11.1.

If \(A\) is \(\Pi_1^1\) and \(\mu(A) = r\) where \(r\) is hyperarithmetic, then there is a \(\Delta_1^1\)-set \(B \subseteq A\) such that \(\mu(B) = \mu(A)\).

### Proposition 13.11.2 (Kechris [63]).

Assume that \(\omega_1^L < \omega_1\). Suppose that \(A \subseteq 2^\omega\) is a \(\Sigma_1^1\)-set with positive measure. Then for any \(n\), there is a \(\Delta_1^1\) perfect set \(B_n \subseteq A\) such that \(\mu(A) < \mu(B_n) + 2^{-n}\). Furthermore, if \(\mu(A)\) is \(\Delta_1^1\), then \(\{(n, x) \mid x \in B_n \land n < \omega\}\) is \(\Delta_1^1\).

### Proof.

Since \(A\) is \(\Sigma_2^1\), there is a \(\Pi_1^1\) relation \(R\) such that

\(x \in A \Leftrightarrow (\exists y \in L_{\omega_1^L}[x])R(x, y).\)

Let \(p\) be a rational between \(\mu(A)\) and \(\mu(A) - 2^{-n}\). By an argument similar to that for Corollary 13.11.7, \(\mu(A) > p\) if and only if there is an \(r \in L\) coding a well-ordering of \(\omega\) such that \(\mu(\{x \mid (\exists y \in L_r[x])R(x, y)\}) > p\). Let \(C = \{r \mid r \text{ codes a well-ordering of } \omega \land \mu(\{x \mid (\exists y \in L_r[x])R(x, y)\}) > p\}\). Then \(C\) is a nonempty \(\Pi_1^1\)-set. Hence there is an \(r_n \in C\) which is \(\Delta_2^1\). Let

\(B_n = \{x \mid (\exists y \in L_{r_n}[x])R(x, y)\}.\)

Then \(B_n \subseteq A\) is \(\Delta_1^1\) and \(\mu(B_n) > p > \mu(A) - 2^{-n}\). The other part of the proposition follows from the above. \(\square\)

The following is a measure-theoretic basis theorem:

### Theorem 13.1.13 (Sacks [120]).

If $A \subseteq 2^\omega$ is a $\Pi^1_1$-set with positive measure, then $A$ contains a hyperarithmetic real.

Proof. Suppose that $A \subseteq 2^\omega$ is a $\Pi^1_1$-set with positive measure. By Corollary 3.7.4, there is an arithmetical formula $\varphi(x, \omega)$ such that

$$
x \in A \Leftrightarrow (\exists z \le_h x) \varphi(x, z).
$$

Let $B = \{x \mid \aleph(x^K_1, x) = (\exists z)\varphi(x, z)\}$. Then $B \subseteq A$. By Theorem 13.1.4, $\mu(B) = \mu(A) > 0$. By Lemma 13.1.10, there is a closed nonempty set $C \subseteq B$ which is defined by a ranked formula $\psi(x)$. Let

$$
T = \{t \in 2^{<\omega} \mid \mu(\{x \mid \forall t(x^K_1, x) = \psi(x) \wedge x \supset t\}) > 0\}.
$$

Then, by Lemma 13.1.11, $[T] \subseteq C$ is a hyperarithmetic tree. The leftmost infinite path in $T$ is hyperarithmetic.

## 13.1.4 Exercises

- Exercise 13.1.11. Let $A \subseteq \omega \times 2^\omega$ be $\Pi^1_1$, and let $A_n = \{x \mid (n, x) \in A\}$. Show that the set $\{(n, p) \mid p(A_n) \ge p \wedge p \text{ is rational}\}$ is $\Pi^1_1$.

- Exercise 13.1.12. Prove that if $A \subseteq 2^\omega$ is $\Pi^1_1$, then $\mu(A) \le_T \emptyset$.

- Exercise 13.1.13. Prove that for any real $x$, the set $\{y \mid (\forall z)(\le_h x \wedge x \wedge z \le_h y \rightarrow z \in \text{HYP})\}$ has measure 1.

- Exercise 13.1.14. Prove Corollary 13.1.11.

- Exercise 13.1.15. Prove that for any recursive ordinal $\beta$, there is a hyperarithmetic set $A$ with measure 1 such that no real in $A$ is recursive in $0^{(\beta)}$.

- Exercise 13.1.16 (Jockusch). If $A \subseteq 2^\omega$ is a $\Pi^1_1$-set containing no hyperarithmetic real, then the set $\{x \mid (\exists y)(y \in A \wedge y \le_h x)\}$ is null.

- Exercise 13.1.17. Assume $V = L$. Prove that for any $x$, $\{y \mid x \le_{\Delta^1_1} y\}$ has measure 1.

## 13.2 Coding sets above Kleene's O

### 13.2.1 A join basis theorem for $\Sigma^1_1$-sets

The question whether there is an uncountable $\Sigma^1_1$-set $A$ such that $x \not\le_h y \not\le_h O$ for any $x, y \in A$ was raised in Friedman [29] and Simpson[138]. A negative answer was given by Harrington (unpublished). The following is a stronger version which is used to study higher randomness theory.

### Theorem 13.2.1 (Chong and Yu [14]).

Let \(A_0\) and \(A_1\) be uncountable \(\Sigma^1_1\)-sets. For any \(z \ge_h \emptyset\), there exist \(x_0 \in A_0\) and \(x_1 \in A_1\) such that \(x_0 \oplus x_1 \equiv_h z\).

### Proof.

Fix a real \(z \ge_h \emptyset\) and two uncountable \(\Sigma^1_1\)-sets \(A_0\) and \(A_1\). Then there are two recursive trees \(T_0, T_1 \subseteq 2^{<\omega} \times \omega^{<\omega}\) such that for \(i \le 1\), \(A_i = \{x \mid [\exists f](n \in [n, f] \in T_i)\}\). We may assume that neither \(A_0\) nor \(A_1\) contains a hyperarithmetic real. Also assume that if \((\sigma, \tau) \in T_i, i \le 1\), then \(|\sigma| = |\text{Dom}(\tau)|\). Let \(T_2 \subseteq \omega^{<\omega}\) be recursive so that \([T_2]\) is uncountable and does not contain a hyperarithmetic infinite path. Let \(f_0\) be the leftmost path in \(T_2\). Then \(f_0 \oplus_h \emptyset\).

For \(s=1\), let \([T_1] = (x_i, f_i) \mid \forall n [n \notin n \in T_i])\). Our plan is to define \(x_i \in A_i\) such that \(z \equiv_h x_0 \oplus x_1\). To this end, a procedure of coding \(z\) and \(f_0\) into \(x_0\) and decoding them from \(x_0 \oplus x_1\) will be introduced. Construction of \(x_i\) will be carried out in \(\omega^x[x]\) on the recursive tree \(T_i\), hence hyperarithmetically in \(z\) (since \(z \ge_h \emptyset\)). Since \(A_i\) is \(\Sigma^1_1\), \(x_{i-1}\) will also code in the function \(f_i\) which is the leftmost path in the second component of \([T_i]\) serving as a witness to \(x_i\) being in \(A_i\), (i.e. \((x_i, f_i) \in [T_i]\) and for any \(i\), if \((x_i, f_i) \in [T_i]\) and \(f_i \neq f_j\), then the least \(n\) where \(f_i(n) \neq f(n)\) satisfies \(f_i(n) < f(n)\)). Since \(A_i\) has no hyperarithmetic member, for any \((\sigma, \tau) \in T_i\), if \(\sigma \prec \tau\) and \(\tau \prec f\) for some \((x, f) \in [T_i]\), then there exist incompatible extensions \(\sigma'\) and \(\sigma''\) of \(\sigma\), and (possibly compatible) extensions \(\tau', \tau''\) of \(\tau\), so that \((\sigma', \tau')\) and \((\sigma'', \tau'')\) both have extensions in \([T_i]\). This "splitting property" of \([T_i]\) allows the coding of \(z, f_i\) and \(f_0\) in \(x_0\) and the coding of \(f_0\) in \(x_1\). More specifically, the branch to be selected by \(x_0\) at a splitting node when \(z(s)\) is to be coded (at stage \(s+1\) of the construction) will follow the value of \(z(s)\), so that a "left turn" is taken if \(z(s) = 0\) and a right turn is taken if \(z(s) = 1\). The coding at stage \(s+1\) of \(\tau_{1,s}\), which denotes the initial segment of \(f_1\) defined at the end of stage \(s\), is accomplished by taking \(\tau_{1,s}(t)\)-many consecutive left turns at splitting nodes, for each \(t \in \text{Dom}(\tau_{1,s})\). The coding of \(f_0(s)\) at stage \(s+1\) of the construction is carried out by taking left turns at \(f_0(s)\)-many consecutive splitting nodes.

For the purpose of decoding, one has to delineate different types of action taken during the coding phase. Since \(\tau_{1,s}\) is a finite function, the end of coding the value \(\tau_{1,s}(t)\) and the beginning of coding the value \(\tau_{1,s}(t+1)\), for \(t < |\text{Dom}(\tau_{1,s})|\), is separated by a right turn at the splitting node between the two codings (of course since the construction is executed stage by stage, one may assume that at the beginning of stage \(s+1\), the coding of \(\tau_{1,s-1}\) is already completed. This means that at stage \(s+1\), one only needs to code the values \(\tau_{1,s}(t)\) for \(t \in \text{Dom}(\tau_{1,s}) \setminus \text{Dom}(\tau_{1,s-1})\)). A "right turn" is chosen at the next splitting node to signify the end of coding \(\tau_{1,s}\), and the beginning of the coding of \(f_0(s)\). Finally, a right turn is taken at the next splitting stage after coding \(f_0(s)\) to mark the end of the coding action for \(x_0\) at stage \(s+1\). This initial segment of \(x_0\) coded at stage \(s+1\) is denoted \(\sigma_{0,s+1}\). Then \(\sigma_{0,s+1} \prec f_0\) is a finite string in \(\omega^{<\omega}\) such that \(|\text{Dom}(\tau_{0,s+1})| = |\sigma_{0,s+1}|\). \(\tau_{0,s+1}\) extends \(\tau_{0,s}\), and is the leftmost such string. The coding of the initial segment \(\tau_{0,s+1}\) of \(f_0\) in \(x_1\) at stage \(s+1\), denoted \(\sigma_{1,s+1}\), proceeds
