
### 2.7.3 Exercises

- Exercise 2.7.1. Prove Lemma 2.4.8.

- Exercise 2.7.2. Prove that \( y \in \Sigma_\beta \) if and only if \( |T'| \le \beta + 1 \).

## 3 Admissibility and constructibility

This chapter introduces the basic notions of effective computability from the set-theoretic perspective. While somewhat abstract at first sight, they are natural when viewed from the standpoint of definability.

An admissible structure is essentially an inner model of computation. The constructive universe \( L \) is defined via a transfinite iteration of the Gödel operators. By considering an appropriate initial segment of \( L \) which forms an admissible structure, we will see how a \( \Pi^1_1 \)-set assumes the role of an r.e. set in higher recursion theory.

### 3.1 Kripke–Platek set theory

The Kripke–Platek (KP) theory of sets was developed by Kripke [75] and Platek [113]. KP is a weak version of the ZF axiom system and captures the basic features of effective computation in the setting of set theory. It offers a natural platform for the study in domains beyond \( \omega \).

### 3.1.1 KP

Definition 3.1.1. Let \( \mathscr{L} \) denote the language of ZF. The collection of \( \Delta_0 \)-formulas in \( \mathscr{L} \) is the smallest collection \( X \) consisting of the atomic formulas of \( \mathscr{L} \) and closed under the following operations:

- (i) If \( \varphi \in X \) then \( \neg \varphi \in X \).
- (ii) If \( \varphi, \psi \in X \), then \( \{ \varphi \land \psi, \varphi \lor \psi \} \subseteq X \).
- (iii) If \( \varphi \in X \), then \( \{ (\forall u \in v)\varphi, (\exists u \in v)\varphi \} \subseteq X \).

In (iii) above, both of the formulas \( (\forall u \in v)\varphi \) or \( (\exists u \in v)\varphi \) are called *bounded formulas*. A prefix of the form \( \exists u \in v \) or \( \forall u \in v \) is a *bounded quantifier*. \( \Delta_0 \)-formulas are analogs of *primitive recursive predicates* in recursion theory.

Definition 3.1.2. A \( \Delta_0 \)-formula is also known as a \( \Sigma_0 \)-formula as well as a \( \Pi_0 \)-formula. In general, a formula \( \varphi(u) \) is \( \Sigma_{n+1} \) if it is of the form \( (\exists v)\psi(u, v) \) where \( \psi \) is a \( \Pi_n \)-formula. A formula \( \varphi(u) \) is \( \Pi_{n+1} \) if it is of the form \( (\forall v)\psi(u, v) \) where \( \psi \) is a \( \Sigma_n \)-formula.

Definition 3.1.3. The class of \( \Sigma \)-formulas is the smallest class \( X \) consisting of the \( \Delta_0 \)-formulas and closed under conjunction, disjunction, bounded quantification, and if \( \varphi \in X \) then \( (\exists u)\varphi \in X \).

The class of \( \Pi \)-formulas is the smallest class \( X' \) consisting of the \( \Delta_0 \)-formulas, closed under conjunction, disjunction, bounded quantification, and if \( \varphi \in X' \) then \( (\forall u)\varphi \in X' \).

\(\Sigma\)-formulas are analogs of recursively enumerable predicates in classical recursion theory. Note that there is a difference between a \( \Sigma_1 \)-formula and a \( \Sigma \)-formula. A \( \Sigma_1 \)-formula is a \( \Sigma \)-formula but not necessarily conversely.

### Definition 3.1.4. The theory KP consists of the universal closure of the following formulas:

- Extensionality: \((\forall x)((\forall y)((y \in u \leftrightarrow x \in u) \rightarrow x = y))\).
- Foundation: \((\exists x)\varphi(x) \rightarrow (\exists x)(\varphi(x) \land (\forall y \in x)\neg\varphi(y))\), for all formulas \(\varphi\) in which \(y\) does not occur free.
- Pair: \((\forall x)(\forall y)(\exists z)(x \in z \land y \in z)\).
- Union: \((\forall x)(\exists y)(\forall u \in x)(\forall v \in u)(v \in y)\).
- \(\Delta_0\)-separation: \((\forall x)(\exists y)(\forall u)(u \in y \leftrightarrow u \in x \land \varphi(u))\), for all \(\Delta_0\)-formulas \(\varphi\) in which \(u\) does not occur free.
- \(\Delta_0\)-collection: \((\forall x)(\forall u \in x)(\exists v)\varphi(u, v) \rightarrow (\exists y)(\forall u \in x)(\exists v \in y)\varphi(u, v)\), for all \(\Delta_0\)-formulas \(\varphi\) in which \(y\) does not occur free.

Given a formula \(\varphi\), we write \(\varphi^{(w)}\) for the formula obtained upon replacing each unbounded quantifier in \(\varphi\) with a bounded quantifier restricted to \(w\). Specifically, replace \(\exists u\) with \(\exists u \in w\) and \(\forall u\) with \(\forall u \in w\). Clearly if \(\varphi\) is \(\Sigma\), then \(\exists w \varphi^{(w)}\) is \(\Sigma\). Under KP, each \(\Sigma\)-formula is equivalent to a \(\Sigma_1\)-formula, as given by the following theorem which is proved by induction on the complexity of formulas. We leave it as an exercise.

### Theorem 3.1.5 (The \(\Sigma\)-reflection principle). Let \(\varphi\) be a \(\Sigma\)-formula. Then

\(\text{KP} \vdash \varphi \rightarrow (\exists w) \varphi^{(w)}\).

Hence the theorem asserts under KP the existence of a \( \Delta_0 \)-definable set for a given \( \Sigma \)-formula. In fact, it says more:

### Theorem 3.1.6 (The \(\Sigma\)-collection principle). Let \(\varphi\) be a \( \Sigma \)-formula and let \( a \) be a set. Then

\(\text{KP} \vdash (\forall x \in a)(\exists y) \varphi(x, y) \rightarrow (\exists w)((\forall x \in a)(\exists y \in w) \varphi(x, y) \land (\forall y \in w)(\exists x \in a) \varphi(x, y))\).

Proof. Assume that \((\forall x \in a)(\exists y) \varphi(x, y)\). Then the formula \((\forall x \in a)(\exists y) \varphi(x, y)\) is \( \Sigma \). By Theorem 3.1.5, there is a set \( c \) such that \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\). Define \( b = \{y \mid (\exists x \in a) \varphi^{(c)}(x, y)\} \). By \( \Delta_0 \)-separation, such a \( b \) exists. It is straightforward to verify that \( \varphi^{(c)}(x, y) \) implies \( \varphi(x, y) \), since \( \varphi(x, y) \) is \( \Sigma \). Hence \((\forall y \in b)(\exists x \in a) \varphi(x, y)\). Since \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\), we have in fact \((\forall x \in a)(\exists y) \varphi^{(c)}(x, y)\). It follows that \((\forall x \in a)(\exists y \in b) \varphi^{(c)}(x, y)\).

### Theorem 3.1.7 (The \( \Delta \)-separation principle). Let \( a \) be a set. For any \( \Sigma \)-formula \( \varphi(x) \) and \( \Pi \)-formula \( \psi(x) \),

\(\text{KP} \vdash (\forall x \in a)(\varphi(x) \leftrightarrow \psi(x)) \rightarrow (\exists w)(\forall x)(x \in w \leftrightarrow x \in a \land \varphi(x))\).

Proof. Assume \((\forall x \in a)(\varphi(x) \leftrightarrow \psi(x))\). Then \((\forall x \in a)(\varphi(x) \lor \neg \psi(x))\). Note that the formula \( \varphi(x) \lor \neg \psi(x) \) is \( \Sigma \). By Theorem 3.1.5, there is a set \( c \) such that \((\forall x \in a)(\varphi(x) \lor \neg \psi(x)) \leftrightarrow (\forall x \in a)(\varphi^{(c)}(x) \lor \neg \psi^{(c)}(x))\). Define \( b = \{y \mid y \in a \land \varphi^{(c)}(y)\} \). By \( \Delta_0 \)-separation, such a \( b \) exists.

If \( y \in b \), then \( y \in a \land \varphi^{(c)}(y) \) and so \( y \in a \land \varphi(y) \) since \( \varphi(y) \) is \( \Sigma \). If \( y \in a \land \varphi(y) \), then \( y \in a \land \psi(y) \) and so \( y \in a \land \psi^{(c)}(y) \) since \( \psi \) is \( \Pi \).

### 3.1.2 Definition by \( \Sigma \)-recursion

As seen in Chapters 1 and 2, definition by recursion using effective transfinite induction is a powerful tool in second order arithmetic. We now study definition by recursion in the setting of admissible set theory. This may be viewed as a generalization of recursion over \( \omega^{CK} \).

Recall that a set \( x \) is transitive if \((\forall y)(\forall z)(y \in x \land z \in y \rightarrow z \in x)\). Note that the formula "\( x \) is transitive" is \( \Delta_0 \).

A function \( f \) is \( \Sigma \) if there is a \( \Sigma \)-formula \( \varphi \) such that \( f(x) = y \leftrightarrow KP \vdash \varphi(x, y) \). By Theorem 3.1.5, \( f \) is defined by a \( \Sigma_1 \)-formula. It is not difficult to see that if \( f \) is \( \Sigma \), then for any set \( u \), \( KP \vdash (\exists y)(v = f \upharpoonright u) \), where \( f \upharpoonright u = \{(x, y) \mid f(x) = y \land x \in u\} \).

### Theorem 3.1.8.

Let \( G \) be an \( n+2 \)-ary \( \Sigma \)-function. There is an \( n+1 \)-ary \( \Sigma \)-function \( F \) such that

```
KP \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, \langle z, F, x_1, \dots, x_n \rangle \mid z \in y).
```

Proof. Assume \( n = 0 \) for simplicity. Let \( P(f) \) be the sentence:

```
f \text{ is a function } \land \text{Dom}(f) \text{ is transitive } \land
(\forall y \in \text{Dom}(f))(y = G(y, \langle z, f(z) \rangle \mid z \in y)).
```

Note that \( P(f) \) is a \( \Sigma \)-formula. Define

```
Q(y, z) = (\exists f)(P(f) \land f(y) = z),
```

and

```
F(y) = z \Leftrightarrow Q(y, z).
```

It suffices to show that

```
KP \vdash F \text{ is a function } \land (\forall y)(\exists z)Q(y, z).
```

We show that KP \( \vdash (\forall y)(\exists z)Q(y, z) \). The other conjunct may be proved using a similar argument. Suppose KP does not prove \( (\forall y)(\exists z)Q(y, z) \). Then there is a model \( \mathcal{M} = \langle M, \in \rangle \) of KP such that \( \mathcal{M} \models (\exists y)(\forall z)\neg Q(y, z) \). By the Axiom of Foundation, choose \( y \) such that

```
\mathcal{M} \models (\forall z)\neg Q(y, z) \land (\forall y' \in y)(\exists z)Q(y', z).
```
