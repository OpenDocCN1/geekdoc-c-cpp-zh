

Exercise 14.3.4. Prove that there is a \(\Sigma^1_1\)-set \(A\) and a \(\Pi^1_1\)-ML random \(x \in A\) such that \(\lim_{n \to \infty} \frac{\mu(A[n|x])}{2^{-n}} = 0\).

Exercise 14.3.5. Prove that every \(x \notin\) HYP hyperarithmetically reducible to a \(\Pi^1_1\)-random real is \(\Pi^1_1\)-random relative to a continuous measure.

Exercise 14.3.6 (Kjos-Hanssen and Yu). Let \(\Phi\) be a universal partial \(\Pi^1_1\)-function from \(\omega\) to 2, and assume that \(x(n) \neq \Phi(n, e)\) for each \(e\). Show that \(x\) hyperarithmetically computes some member of a given nonempty \(\Sigma^1_1\)-closed subset of \(2^\omega\).

Exercise 14.3.7 (Greenberg, Montalbán and Slaman [39]; Kulikumin and Nies). Suppose that \(\mathbb{M}\) is a structure such that the set \(A = \{x \mid (\exists N \le_T x)(N \equiv \mathbb{M})\}\) has measure 1. Prove that every \(\Pi^1_1\)-random real is in \(A\).

Exercise 14.3.8 (Kripke [120]). If \(A\) is a nullset of hyperdegrees such that \(\mathbf{0} \notin A\), then the set \(U_K(A) = \{x \mid (\exists y \in A)(x \ge_T y)\}\) is also null.

## 14.4 \(\Delta^1_2\) and \(\Sigma^1_2\)-randomness

### 14.4.1 \(\Delta^1_2\)-randomness

Since there is a \(\Delta^1_1\)-real which is \(\Pi^1_1\)-random, \(\Delta^1_2\)-randomness is strictly stronger than \(\Pi^1_1\)-randomness. By Corollary 13.1.7 and Proposition 13.1.12, we have the following conclusion.

**Proposition 14.4.1.** Assume that \(\omega_1^L < \omega_1\). Then \(\Delta^1_2\)-randomness = \(\Delta^1_2\)-ML randomness = \(\Pi^1_2\)-randomness.

### 14.4.2 \(\Sigma^1_2\)-ML randomness

Let \(\{\varphi_n(\sigma)\}_{n < \omega}\) be a recursive enumeration of \(\Sigma^1_1\)-formulas. There is a \(\Sigma_1\)-formula \(\psi(n, \sigma)\) (in set theory) such that

\(\varphi_n(\sigma) \leftrightarrow (\exists X)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega_1^X}, \in \rangle \models \psi(n, \sigma)).\)

Let \((n, \sigma) \in U\) if and only if

\((\exists x)(x \text{ is a } \Pi^1_1\text{-singleton} \land \langle L_{\omega_1^x}, \in \rangle \models \psi(n, \sigma)) \land \mu(\{z \mid (\exists m)(\langle L_{\omega_1^z}, \in \rangle \models \psi(n, z \mid m))\}) < 2^{-n}.\)

One may view \((n, \sigma) \in U\) as an enumeration of strings \(\sigma\) in \(U\) up to any stage coded by a \(\Pi^1_1\)-singleton where the measure is less than \(2^{-n}\). We leave it to the reader to verify that \(U\) is \(\Sigma^1_2\). Then the set \(\{U_n\}_{n < \omega}\), where \(U_n = \{\sigma \mid (n, \sigma) \in U\}\), is a universal \(\Sigma^1_2\)-ML test.

Hence there is a \(\Pi^1_2\)-closed set P which contains only \(\Sigma^1_2\)-ML random reals. It follows that the leftmost path in P is \(\Delta^1_2\)-equivalent to a \(\Sigma^1_2\)-real and so belongs to L.

By Proposition 4.4.6, every \(x \in P \cap L\) satisfies \(\delta_2^{1+} > \delta_2^{1\uparrow}\). This applies in particular to the leftmost path x in P. Hence if one stays within L, the situation that one normally sees in standard randomness theory no longer applies. Note that by applying a method similar to that in the proof of Theorem 14.2.10, one may separate \(\Sigma^1_2\)-ML randomness from \(\Delta^1_2\)-randomness.

**Proposition 14.4.2.** If \(V = L\), then every nonzero \(\Delta^1_2\)-degree contains a \(\Sigma^1_2\)-ML random real.

**Proof.** First observe that the set P above can be presented by a \(\Pi^1_2\)-tree T. By Proposition 4.4.6, T is \(\Delta^1_2\) in every \(x \in [T]\) and T has the least nontrivial \(\Delta^1_2\)-degree. Hence the proposition follows.

### 14.4.3 \(\Sigma^1_2\)-randomness

**Definition 14.4.3.** We say that x is L-random if for any Martin-Löf test \(\{U_n\}_{n<\omega}\) in L, \(x \notin \bigcap_{n<\omega} U_n\).

L-randomness was essentially introduced by Solovay [150]. The following fact is immediate.

**Proposition 14.4.4.** The following are equivalent:

- (i) x is L-random;
- (ii) x does not belong to any Borel nullset coded in L;
- (iii) x is \(\mathbb{R} = (\mathbf{T}, \le)\)-generic over L, where R is the notion of random forcing as defined in § 6.2.2.

**Proof.** Obviously (iii) => (ii) => (i). By Proposition 6.2.6, R is c.c.c. Then it follows that for any dense subset \(\mathscr{D}\), \(\bigcup_{p \in \mathscr{D}} p\) is a Borel co-nullset with a Borel code in L. Hence (ii) => (iii).

**Theorem 14.4.5** (Solovay [150]). If the set of L-random reals has measure 1, then every \(\Sigma^1_2\)-set is measurable.

**Proof.** Suppose that A is a \(\Sigma^1_2\)-set of reals defined by a formula \(\varphi(x)\) in the language of set theory so that
\(x \in A \Leftrightarrow (L[x], \in) \models \varphi(x)\).

Let \(\mathscr{D}\) be a maximal antichain in L so that for any \(p \in \mathscr{D}\), \(p \Vdash \dot{\varphi}(\dot{G})\). Then \(\mathscr{D}\) is countable. Let \(R = \bigcup_{p \in \mathscr{D}} p\). Then R is a Borel set with a Borel code in L. If x is L-random, then x is an R-generic real over L. Hence if x is L-random in R, then \((L[x], \in) \models \varphi(x)\) and so x belongs to A. Note that \(\mathscr{D}' = \{r \mid (\exists p \in \mathscr{D})(r \le p) \lor (\forall q)(q \in \mathscr{D} \land q \le p \rightarrow q \not\parallel r)\}\) is a dense set. Thus if \(x \in A\), then \(x \in R\) so that for any L-random real x, \(x \in A\) if and only if \( x \in R \). Since the set of \( L \)-random reals has measure 1, \( A \) is equal to \( R \) modulo a nullset. It follows that \( A \) is measurable.

**Theorem 14.4.6** (Stern [161]). For any real \( x \), \( x \) is \( \Delta^1_2 \)-random and \( \delta_2^{1,x} = \delta_2^1 \) if and only if \( x \) is \( L \)-random.

**Proof.** Let \( x \) be \( \Delta^1_2 \)-random such that \( \delta_2^{1,x} = \delta_2^1 \). If \( x \) is not \( L \)-random, then let

\( A = \{r \mid r \text{ codes a well-ordering } \wedge x \text{ is not } L_{|r|}\text{-random}\} \)

be a nonempty \( \Delta^1_2(x) \)-set. Then there is an \( r \le_{\Delta_1^1} x \) so that \( x \in L_{\delta_1} \), a contradiction.

Conversely, let \( x \) be \( L \)-random. Then \( x \) is \( \Delta^1_2 \)-random. Suppose that \( \delta_2^{1,x} > \delta_2^1 \). Then there are \( \Sigma^1_2 \)-formulas \( \varphi(x, m, n) \) and \( \psi(x, m, n) \) defining an \( r \in L \) coding a well-ordering greater than \( \delta_2^1 \). By Corollary 4.2.29, \( r \in L_{\delta_2^1}[x] \). By (iii) in Proposition 14.4.4, there is a condition \( p \in \mathbf{T} \cap L \) such that

\( p \Vdash (\forall m)(\forall n)((m, n) \in \dot{r} \leftrightarrow \varphi(x, m, n)) \wedge ((m, n) \in \dot{r} \leftrightarrow \psi(x, m, n)). \)

Then for any \( L \)-random real \( z \in p \), \( r \le_{\Delta_1^1} z \). Applying Levy collapse \( \mathbb{L}(\aleph_2)^L \) over \( V \), in \( V[G] \) the set of \( L \)-random reals is of measure 1. It follows that in \( V[G] \), the set

\( A_r = \{z \mid r \le_{\Delta_1^1} z\} \)

has positive measure. By Theorem 14.4.5 and Proposition 13.19, \( r \) is \( \Delta^1_2 \) in \( V[G] \) and so in \( V \), a contradiction.

Note that the set of \( L \)-random reals is \( \Pi^1_2 \). Thus if the measure of non-\( L \)-random reals is 0, then every \( \Sigma^1_2 \)-random real is \( L \)-random.

**Theorem 14.4.7** (Stern [161]). Assume that the set of \( L \)-random reals has measure 1. Then the set of non-\( L \)-random reals is the largest null \( \Sigma^1_2 \)-set and so \( \Sigma^1_2 \)-randomness is equivalent to \( L \)-randomness.

**Proof.** For a contradiction, suppose that \( A \) is a null \( \Sigma^1_2 \)-set containing an \( L \)-random real \( x \). Then there is a formula \( \varphi \) defining \( A \) such that \( L[x] \models \varphi(x) \). By Proposition 14.4.4, there is a condition \( p \in \mathbf{T} \cap L \) such that \( p \Vdash \varphi(\dot{x}) \). Hence for any random real \( y \in p \), we have \( (L[y], \in) \models \varphi(y) \). Thus \( \varphi(y) \) holds for any \( y \in p \). Since the set of \( L \)-random reals has measure 1, it follows that \( \mu(A) > 0 \), a contradiction.

Hence if \( (\omega_1)^L < \omega_1 \), then \( \Sigma^1_2 \)-randomness is strictly stronger than \( \Sigma^1_2 \)-ML randomness. Indeed, the conclusion is provable in ZFC.

**Proposition 14.4.8.** There is a \( \Sigma^1_2 \)-ML random real which is not \( \Sigma^1_2 \)-random.

**Proof.** Let \( T \subseteq 2^{<\omega} \) be a \( \Pi^1_2 \)-tree containing only \( \Sigma^1_2 \)-ML random reals. Then by a method similar to that used in the proof of Lemma 14.2.12, replacing \( \omega_1^{CK} \) with \( \delta_2^1 \), one is able to show that the leftmost path of \( T \) is covered by a \( \Sigma^1_2 \)-nullset. We leave it to the reader to fill in the details.

