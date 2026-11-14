
Proof. If \(\omega_1^\alpha = \omega_1^{CK}\), then by Corollary 5.1.4, for any real \(z, z \in \mathfrak{A}(\omega_1^{CK}, x)\) if and only if \(z \le_h x\). Now suppose that \(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)((\exists z)\varphi(n, z) \leftrightarrow (\forall z)\psi(n, z))\). Then for each \(n\), let \(f(n)\) be the \(<_{\mathcal{O}^*}\)-least \(m \in \mathcal{O}^*\) such that \(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\exists z^{[m]})(\varphi(n, z^{[m]})) \lor \neg\psi(n, z^{[m]}))\). \(f\) is a total \(\Pi_1^1\), and hence \(\Delta_1^1\), function. It follows that there is an \(n_0 \in \omega\) such that \(f(n) < n_0\) for all \(n\). Let \(y\) be a real such that \(n \in y\) if and only if \(\mathfrak{A}(\omega_1^{CK}, x) \vDash \exists z^{[n_0]}(\varphi(n, z^{[n_0]}))\). Then \(y \in \mathfrak{A}(\omega_1^{CK}, x)\) and

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash n \in y \leftrightarrow (\exists z)\varphi(n, z)\).

Suppose that \(\mathfrak{A}(\omega_1^{CK}, x)\) satisfies the \(\Delta_1^1\)-comprehension axiom. For the sake of contradiction, assume that \(\omega_1^\alpha > \omega_1^{CK}\). Let \(n \in \mathcal{O}^*\) be such that \(n = 3 \cdot 5^e\) and \(|n|_k = \omega_1^{CK}\). Note that \(H_m^\alpha \in \mathfrak{A}(\omega_1^{CK}, x)\) for \(m <_{\mathcal{O}^*} n\). Let \(\varphi(n, z)\) be

\((\exists m)(\exists i)[\hat{H}(\hat{\varphi}_{e(m)}^x(m), z, x) \wedge n = \langle m, i \rangle \wedge i \in z]\).

If \(m <_{\mathcal{O}^*} n\), then \(\hat{H}_{\varphi^{[m]}}^x\) is the unique real \(z\) such that \(\hat{H}(\hat{\varphi}_{e(m)}^x(m), z, x)\). Thus

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)((\exists z)\varphi(n, z) \leftrightarrow (\forall z)((\exists i)(\langle m, i \rangle = n \wedge i \in z) \to \neg\varphi(n, z))\).

Then by \(\Delta_1^1\)-comprehension, there is a \(y \in \mathfrak{A}(\omega_1^{CK}, x)\) such that

\(\mathfrak{A}(\omega_1^{CK}, x) \vDash (\forall n)(n \in y \leftrightarrow (\exists z)\varphi(n, z))\).

Since \(\hat{H}_{\varphi^{[m]}}^x \in \mathfrak{A}(\omega_1^{CK}, x)\) for \(m <_{\mathcal{O}^*} n\), we have \(y = \hat{H}_n^x\), contradicting Proposition 5.1.3.

### Remark 5.1.16.
The results above may be generalized. For example, one may introduce the language \(\mathscr{L}(\omega_1^x, x, z)\), define the structure \(\mathfrak{A}(\omega_1^x, x, z)\), and show that all the results above hold. Then \(\{(x, \ulcorner p \urcorner, z) \mid p \in \Sigma_1^x \wedge \mathfrak{A}(\omega_1^x, x, z) \vDash p\} \Pi_1^1\). Moreover, \(\mathfrak{A}(\omega_1^x, z)\) satisfies \(\Delta_1^1\)-comprehension if and only if \(\mathfrak{A}(\omega_1^x, x, z)\) is precisely the collection of reals hyperarithmetic in \(x \oplus z\), and if and only if \(\omega_1^{x \oplus x} = \omega_1^x\).

## 5.1.4 Exercise

### Exercise 5.1.1.
Prove that \(\mathfrak{A}(\omega_1^{CK}, \emptyset)\) is the smallest \(\omega\)-model satisfying the \(\Delta_1^1\)-comprehension axiom.

## 5.2 Cohen forcing

Cohen's original notion of forcing was defined over a structure similar to the ramified analytical hierarchy, although subsequent developments in set theory have since followed a different approach. For hyperarithmetic theory, this hierarchy is the most natural setting in which to study forcing.

The collection \(\mathcal{P}\) of forcing conditions we consider here are relatively simple, such as finite binary strings or hyperarithmetically encoded perfect sets. A forcing relation \(\Vdash\) is a binary relation that is a subset of \(\mathcal{P} \times \{\varphi \mid \varphi \text{ is a formula in } \mathcal{L}(\omega_1^{CK}, x)\}\). The objective is to make \(\Vdash\) as simply defined as possible. For example, to be hyperarithmetic when the formula \(\varphi\) being forced is ranked, or \(\Pi^1_1\) when \(\varphi\) is \(\Sigma^1_1\). The generic set \(x\) will be a real that is obtained from a collection of pairwise compatible conditions through a union or intersection operation. The model \(\mathfrak{A}(\omega_1^{CK}, x)\) is then a generic extension of \(\mathfrak{A}(\omega_1^{CK}, \omega)\). We always make \(\mathfrak{A}(\omega_1^{CK}, x)\) satisfy \(\Delta^1_1\)-comprehension so that \(\omega_1^x = \omega_1^{CK}\). With this, one can construct generic \(x\)'s with a prescribed property.

### 5.2.1 Cohen forcing

A Cohen condition \(p\) is a finite string \(\sigma \in 2^{<\omega}\) which may be identified with the basic open set \([\sigma]\). Define a partial ordering \(\le\) such that \(p \le q\) if and only if \(p \supseteq q\).

Given formulas \(\varphi(x)\) and \(\psi(n)\), denote by \(\varphi(x \mid \psi)\) the formula obtained upon replacing every occurrence of \(n \in x\) in \(\varphi\) with \(\psi(n)\) and every occurrence of \(n \notin x\) in \(\varphi\) with \(\neg\psi(n)\).

For a sentence \(\varphi \in \mathcal{L}(\omega_1^{CK}, x)\), define \(p \Vdash \varphi\) by induction on the complexity of \(\varphi\):

- \(p \Vdash \check{n} \in x\) if and only if \(p(n) = 1\);
- \(p \Vdash t_1 = t_2\) if and only if \(\mathfrak{A}(\omega_1^{CK}, 0) \models t_1 = t_2\), where \(t_1, t_2\) are terms involving only numerals and arithmetic operations;
- \(p \Vdash t \in x\) if and only if \(\mathfrak{A}(\omega_1^{CK}, 0) \models t = \check{n}\) for some \(n\) and \(p \Vdash \check{n} \in x\), where \(t\) is a term involving only numerals and arithmetic operations;
- \(p \Vdash (\exists n)\psi(n)\) if and only if \(p \Vdash \psi(\check{n})\) for some \(n \in \omega\);
- \(p \Vdash (\exists \beta < \omega_2^{CK})\dot{\varphi}\) if and only if \(p \Vdash \varphi(\dot{\omega}\beta \mid \psi)\) for some ranked formula \(\psi(\check{n})\) with rank at most \(\beta\);
- \(p \Vdash (\exists \beta)\dot{\varphi}\) if and only if \(p \Vdash (\exists \beta < \omega_2^{CK})\varphi(\dot{\omega}\beta)\) for some \(\beta < \omega_1^{CK}\);
- \(p \Vdash \varphi \lor \psi\) if and only if \(p \Vdash \varphi\) and \(p \Vdash \psi\);
- \(p \Vdash \neg \varphi\) if and only if \(\forall q \le p (q \not\Vdash \varphi)\).

The following basic facts are easy to verify.

### Proposition 5.2.1.
For any formula \(\varphi\),
(i) \((\neg p) \Vdash \neg \varphi\);
(ii) \((\forall p)(\exists q \le p)(q \Vdash \varphi \lor q \Vdash \neg \varphi)\);
(iii) \((\forall p)(\forall q \le p)(p \Vdash \varphi \to q \Vdash \varphi)\).

### Theorem 5.2.2.
The set \(\{(p, \ulcorner \varphi \urcorner) \mid p \Vdash \varphi \land \varphi \text{ is } \Pi^1_1\}\) is \(\Pi^1_1\).

Proof. Note that the set of \(\Sigma^1_1\)-sentences is \(\Pi^1_1\), and if \((\exists x)\theta(x)\) is \(\Sigma^1_1\) where \(\theta(x)\) is arithmetical, then \(p \Vdash (\exists x)\theta(x)\) if and only if there exists an \(n \in \omega\) such that \(p \Vdash \theta(\check{n})\). By the \(\Sigma\)-Induction Theorem (3.1.8) and the definition of forcing, there is a \(\Sigma^1_1\) formula \(\psi(u, v)\) in the language of set theory such that for a \(\Sigma^1_1\)-sentence \(\varphi\), \((L_{\omega_1^{CK}}, \in) \models \psi(p, \ulcorner \varphi \urcorner)\) if and only if \(p \Vdash \varphi\). By the Spector–Gandy Theorem (3.7.1), the set \(\{(p, \ulcorner \varphi \urcorner) \mid p \Vdash \varphi \text{ or } p \Vdash \neg \varphi\}\) is \(\Pi^1_1\).

A set \(D \subseteq 2^{<\omega}\) is dense if for any \(p \in 2^{<\omega}\), there is a \(q \in D\) such that \(q \le p\). Given a sentence \(\varphi\), let \(D_p = \{p \mid p \Vdash \varphi \lor p \Vdash \neg \varphi\}\). The next lemma follows from (ii) of Proposition 5.2.1.

### Lemma 5.2.3.
Given a formula \(\varphi\), \(D_p\) is dense.

A real \(x\) is Cohen generic if for any sentence \(\varphi\) there is an \(n\) such that \(x \Vdash \check{n} \Vdash \varphi\) or \(x \Vdash \check{n} \Vdash \neg \varphi\). By Lemma 5.2.3 and induction on the set of Gödel numbers of formulas, it is an easy exercise to show that a Cohen generic real exists. The following theorem states that for a generic real, forcing equals truth.

### Theorem 5.2.4.
Suppose that \(x\) is Cohen generic. Then for any sentence \(\varphi\), \(\mathfrak{A}(\omega_1^{CK}, x) \models \varphi\) if and only if there is an \(n\) such that \(x \Vdash \check{n} \Vdash \varphi\).

Proof. Either direction of the theorem may be proved by induction on the complexity of formulas. We show the nontrivial case when \(\varphi\) is of the form \(\neg \psi\).

Suppose that there is an \(n\) such that \(x \Vdash \check{n} \Vdash \neg \psi\). We claim that \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\). Otherwise, by induction, there is an \(m\) such that \(x \Vdash \check{m} \Vdash \psi\). By Lemma 5.2.1, \(x \Vdash \check{(m+n)} \Vdash \psi \land \neg \psi\), contradicting Lemma 5.2.1. Hence \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\), i.e. \(\mathfrak{A}(\omega_1^{CK}, x) \models \varphi\).

Assume that \(\mathfrak{A}(\omega_1^{CK}, x) \models \neg \psi\). By induction, \(x \Vdash \check{n} \Vdash \psi\) for any \(n\). Since \(x\) is Cohen generic, there exists an \(m\) such that \(x \Vdash \check{m} \Vdash \psi\) or \(x \Vdash \check{m} \Vdash \neg \psi\). Hence \(x \Vdash \check{m} \Vdash \neg \psi\).

### Theorem 5.2.5.
If \(x\) is Cohen generic, then \(\mathfrak{A}(\omega_1^{CK}, x)\) satisfies \(\Delta^1_1\)-comprehension.

Proof. Suppose that \(x\) is Cohen generic and

\(\mathfrak{A}(\omega_1^{CK}, x) \models (\forall n)(\exists z)\varphi(n, z) \leftrightarrow (\forall z)(\psi(n, z)).\)

where both \(\varphi(n, z)\) and \(\psi(n, z)\) are arithmetical. Then

\(\mathfrak{A}(\omega_1^{CK}, x) \models (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z)).\)

By Theorem 5.2.4, there exists a \(p < x\) such that

\(p \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z)).\)

By the definition of forcing,

\((\forall q \le p)(q \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))).\)

Hence

\((\forall q \le p)(\forall n)(q \Vdash (\exists z)(\varphi(n, z) \lor \neg \psi(n, z))).\)

Therefore

\((\forall q \le p)(\forall n)(\exists r \le q)(r \Vdash (\exists z)(\varphi(n, z) \lor \neg \psi(n, z))).\)
