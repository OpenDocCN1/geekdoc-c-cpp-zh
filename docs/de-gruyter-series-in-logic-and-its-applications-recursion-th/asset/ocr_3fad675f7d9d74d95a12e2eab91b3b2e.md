Hence there is a \(\Pi_2^1\)-closed set P which contains only \(\Sigma_2^1\)-ML random reals. It follows that the leftmost path in P is \(\Delta_2^1\)-equivalent to a \(\Sigma_2^1\)-real and so belongs to L.

By Proposition 4.4.6, every \(x \in P \cap L\) satisfies \(\delta_2^{1+} > \delta_2^{1\uparrow}\). This applies in particular to the leftmost path x in P. Hence if one stays within L, the situation that one normally sees in standard randomness theory no longer applies. Note that by applying a method similar to that in the proof of Theorem 14.2.10, one may separate \(\Sigma_2^1\)-ML randomness from \(\Delta_2^1\)-randomness.

**Proposition 14.4.2.** If \(V = L\), then every nonzero \(\Delta_2^1\)-degree contains a \(\Sigma_2^1\)-ML random real.

**Proof.** First observe that the set P above can be presented by a \(\Pi_2^1\)-tree T. By Proposition 4.4.6, T is \(\Delta_2^1\) in every \(x \in [T]\) and T has the least nontrivial \(\Delta_2^1\)-degree. Hence the proposition follows.

# 14.4.3 \(\Sigma_2^1\)-randomness

**Definition 14.4.3.** We say that x is L-random if for any Martin-Löf test \(\{U_n\}_{n<\omega}\) in L, \(x \notin \bigcap_{n<\omega} U_n\).

L-randomness was essentially introduced by Solovay [150]. The following fact is immediate.

**Proposition 14.4.4.** The followings are equivalent:

+   (i) x is L-random;
+   (ii) x does not belong to any Borel nullset coded in L;
+   (iii) x is \(\mathbb{R} = (\mathbf{T}, \le)\)-generic over L, where R is the notion of random forcing as defined in § 6.2.2.

**Proof.** Obviously (iii) => (ii) => (i). By Proposition 6.2.6, R is c.c.c. Then it follows that for any dense subset \(\mathscr{D}_i \bigcup_{p \in \mathscr{D}} p\) is a Borel co-nullset with a Borel code in L. Hence (ii) => (iii).

**Theorem 14.4.5** (Solovay [150]). If the set of L-random reals has measure 1, then every \(\Sigma_2^1\)-set is measurable.

**Proof.** Suppose that A is a \(\Sigma_2^1\)-set of reals defined by a formula \(\varphi(x)\) in the language of set theory so that
\(x \in A \Leftrightarrow (L[x], \in) \models \varphi(x)\).

Let \(\mathscr{D}\) be a maximal antichain in L so that for any \(p \in \mathscr{D}\), \(p \Vdash \dot{\varphi}(\dot{G})\). Then \(\mathscr{D}\) is countable. Let \(R = \bigcup_{p \in \mathscr{D}} p\). Then R is a Borel set with a Borel code in L. If x is L-random, then x is an R-generic real over L. Hence if x is L-random in R, then \((L[x], \in) \models \varphi(x)\) and so x belongs to A. Note that \(\mathscr{D}' = \{r \mid (\exists p \in \mathscr{D})(r \le p) \lor (\forall q)(q \in \mathscr{D} \land q \le p \rightarrow q \not\parallel r)\}\) is a dense set. Thus if \(x \in A\), then \(x \in R\) so that for any L-random real x, \(x \in A\) if and