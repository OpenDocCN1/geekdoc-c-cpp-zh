+   1. ((q_0, \varepsilon, \varepsilon), (q_1, S));

+   2. ((q_1, \sigma, \sigma), (q_1, \varepsilon)), for \sigma \in \Sigma; and

+   3. ((q_1, \varepsilon, A), (q_1, x)), for each production A \longrightarrow x in G.

The transition $((q_0, \varepsilon, \varepsilon), (q_1, S))$ lets $M$ move from the start state $q_0$ to the accepting state $q_1$ while reading no input and pushing $S$ onto the stack. This is the only possible first move by $M$.

A transition from the form $((q_1, \sigma, \sigma), (q_1, \varepsilon))$, for $\sigma \in \Sigma$ allows $M$ to read $\sigma$ from its input string, provided that there is a $\sigma$ on the top of the stack. Note that if $\sigma$ is at the top of the stack, then this transition is _only_ transition that applies. Effectively, any terminal symbol that appears at the top of the stack must be matched by the same symbol in the input string, and the transition rule allows $M$ to consume the symbol from the input string and remove it from the stack at the same time.

A transition of the third form, $((q_1, \varepsilon, A), (q_1, x))$ can be applied if and only if the non-terminal symbol $A$ is at the top of the stack. $M$ consumes no input when this rule is applied, but $A$ is replace on the top of the stack by the string on the right-hand side of the production rule $A \longrightarrow x$. Since the grammar $G$ can contain several production rules that have $A$ as their left-hand side, there can be several transition rules in $M$ that apply when $A$ is on the top of the stack. This is the only source of nondeterminism in $M$; note that is also the source of nondeterminism in $G$.

The proof that $L(M) = L(G)$ follows from the fact that a computation of $M$ that accepts a string $w \in \Sigma^*$ corresponds in a natural way to a left derivation of $w$ from $G$'s start symbol, $S$. Instead of giving a proof of this fact, we look at an example. Consider the following context-free grammar:

```
S \longrightarrow AB
A \longrightarrow aAb
A \longrightarrow \varepsilon
B \longrightarrow bB
B \longrightarrow b
```

This grammar generates the language $\{a^n b^m | m > n\}$. The pushdown automaton constructed from this grammar by the procedure given above