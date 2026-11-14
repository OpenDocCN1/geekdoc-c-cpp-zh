Further facts concerning KP may be found in [3].

# 3.1.6 Exercises

**Exercise 3.1.1.** _Prove Theorem_ 3.1.5_._

**Exercise 3.1.2.** _Complete the proof of Proposition_ 3.1.17_._

# 3.2 Admissible sets

The universe of sets $V$ is defined inductively on ordinals:

```
\( V_0 = \emptyset, \)
\( V_{\beta+1} = \mathscr{P}(V_\beta), \)
\( V_\lambda = \bigcup_{\alpha < \lambda} V_\alpha \text{ when } \lambda \text{ is a limit ordinal, and} \)
\( V = \bigcup_\alpha V_\alpha. \)
```

**Definition 3.2.1.** An _admissible structure_ (or an admissible set) is a model \(\mathfrak{M}\) of KP of the form \(\mathfrak{M} = \langle M, \in_M \rangle\) where \(M\) is a transitive set in \(V\) and \(\in_M\) is the restriction of \(\in\) to \(M\). We will often write \(\in_M\) simply as \(\in\) if the context is clear.

**Definition 3.2.2.** The _ordinal_ of a transitive structure \(\mathfrak{M}\), denoted \(o(\mathfrak{M})\), is the least ordinal not in \(M\). An ordinal \(\alpha\) is _admissible_ if \(\alpha = o(\mathfrak{M})\) for some admissible structure \(\mathfrak{M}\).

A relation \(S \subseteq M^n\) on \(\mathfrak{M}\) is \(\Sigma_n\) if there is a \(\Sigma_n\)-formula \(\varphi\) such that

```
\( S(a_1, a_2, \dots, a_n) \Leftrightarrow \mathfrak{M} \vDash \varphi(a_1, a_2, \dots, a_n). \)
```

We allow parameters in the above definition. Clearly both \(a\) and \(\{a\}\) are \(\Sigma_1\) for any \(a \in M\). Moreover, it follows from Theorem 3.1.5 that for \(\mathfrak{M}\) admissible, \(\Sigma_1\)-relations are closed under \(\vee, \wedge, \exists x \in a, \forall x \in a\) and \(\exists x\).

# 3.2.1 The smallest admissible set

**Definition 3.2.3.** A set \(a \in V\) is _hereditarily finite_, written \(a \in \text{HF}\), if \(\text{TC}(a)\) is finite.