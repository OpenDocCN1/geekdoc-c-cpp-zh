is accepted. This involves nondeterminism because the automaton has to “guess” when to jump to state q2; it has no way of knowing whether it has actually reached the end of the string.

Although this pushdown automaton is not deterministic, we can modify it easily to get a deterministic pushdown automaton that accepts a closely related language. We just have to add a special end-of-string symbol to the language. We use the symbol $ for this purpose. The following deterministic automaton accepts the language {w$ | w ∈ {a, b}* n_a(w) = n_b(w)} :

![](bbox=[0.1, 0.27, 0.9, 0.55])

In this modified automaton, it is only possible for the machine to reach the accepting state q2 by reading the end-of-string symbol at a time when the number of a’s that have been consumed is equal to the number of b’s. Taking our cue from this example, we define what it means for a language to be deterministic context-free as follows:

Definition 4.5. Let L be a language over an alphabet Σ, and let $ be a symbol that is not in Σ. We say that L is a deterministic context-free language if there is a deterministic pushdown automaton that accepts the language L$ (which is equal to {w$ | w ∈ L}).

There are context-free languages that are not deterministic context-free. This means that for pushdown automata, nondeterminism adds real power. This contrasts with the case of finite automata, where deterministic finite automata and nondeterministic finite automata are equivalent in power in the sense that they accept the same class of languages.

A deterministic context-free language can be parsed efficiently. LL(1) parsing and LR(1) parsing can both be defined in terms of deterministic pushdown automata, although we have not pursued that approach here.