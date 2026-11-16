
- ((q_0, \varepsilon, \varepsilon), (q_1, S));
- ((q_1, \sigma, \sigma), (q_1, \varepsilon)), for \(\sigma \in \Sigma\); and
- ((q_1, \varepsilon, A), (q_1, x)), for each production \(A \longrightarrow x\) in G.

The transition $((q_0, \varepsilon, \varepsilon), (q_1, S))$ lets $M$ move from the start state $q_0$ to the accepting state $q_1$ while reading no input and pushing $S$ onto the stack. This is the only possible first move by $M$.

A transition of the form $((q_1, \sigma, \sigma), (q_1, \varepsilon))$, for $\sigma \in \Sigma$ allows $M$ to read $\sigma$ from its input string, provided that there is a $\sigma$ on the top of the stack. Note that if $\sigma$ is at the top of the stack, then this transition is _only_ transition that applies. Effectively, any terminal symbol that appears at the top of the stack must be matched by the same symbol in the input string, and the transition rule allows $M$ to consume the symbol from the input string and remove it from the stack at the same time.

A transition of the third form, $((q_1, \varepsilon, A), (q_1, x))$ can be applied if and only if the non-terminal symbol $A$ is at the top of the stack. $M$ consumes no input when this rule is applied, but $A$ is replaced on the top of the stack by the string on the right-hand side of the production rule $A \longrightarrow x$. Since the grammar $G$ can contain several production rules that have $A$ as their left-hand side, there can be several transition rules in $M$ that apply when $A$ is on the top of the stack. This is the only source of nondeterminism in $M$; note that it is also the source of nondeterminism in $G$.

The proof that $L(M) = L(G)$ follows from the fact that a computation of $M$ that accepts a string $w \in \Sigma^*$ corresponds in a natural way to a left derivation of $w$ from $G$'s start symbol, $S$. Instead of giving a proof of this fact, we look at an example. Consider the following context-free grammar:

```
S \longrightarrow AB
A \longrightarrow aAb
A \longrightarrow \varepsilon
B \longrightarrow bB
B \longrightarrow b
```

This grammar generates the language $\{a^n b^m | m > n\}$. The pushdown automaton constructed from this grammar by the procedure given above has the following set of transition rules:

- ((q_0, \epsilon, \epsilon), (q_1, S))
- ((q_1, a, a), (q_1, \epsilon))
- ((q_1, b, b), (q_1, \epsilon))
- ((q_1, \epsilon, S), (q_1, AB))
- ((q_1, \epsilon, A), (q_1, aAb))
- ((q_1, \epsilon, A), (q_1, \epsilon))
- ((q_1, \epsilon, B), (q_1, bB))
- ((q_1, \epsilon, B), (q_1, b))

Suppose that the automaton is run on the input $aabbbb$. We can trace the sequence of transitions that are applied in a computation that accepts this input, and we can compare computation to a left derivation of the string:

| Transition | Input Consumed | Stack | Derivation |
| :--- | :--- | :--- | :--- |
| ((q_0, \epsilon, \epsilon), (q_1, S)) | | S | S \(\Rightarrow\) AB |
| ((q_1, \epsilon, S), (q_1, AB)) | | AB | \(\Rightarrow\) aAbB |
| ((q_1, \epsilon, A), (q_1, aAb)) | | aAbB | \(\Rightarrow\) aaAbbB |
| ((q_1, a, a), (q_1, \epsilon)) | a | AbB | \(\Rightarrow\) |
| ((q_1, \epsilon, A), (q_1, aAb)) | a | aAbbB | \(\Rightarrow\) aaAbbB |
| ((q_1, a, a), (q_1, \epsilon)) | aa | AbbB | \(\Rightarrow\) |
| ((q_1, \epsilon, A), (q_1, \epsilon)) | aa | bbB | \(\Rightarrow\) |
| ((q_1, b, b), (q_1, \epsilon)) | aab | bB | \(\Rightarrow\) |
| ((q_1, b, b), (q_1, \epsilon)) | aabb | B | \(\Rightarrow\) |
| ((q_1, \epsilon, B), (q_1, bB)) | aabb | bB | \(\Rightarrow\) aabbbB |
| ((q_1, b, b), (q_1, \epsilon)) | aabbb | B | \(\Rightarrow\) |
| ((q_1, \epsilon, B), (q_1, b)) | aabbb | b | \(\Rightarrow\) aabbbb |
| ((q_1, b, b), (q_1, \epsilon)) | aabbbb | | \(\Rightarrow\) |

Note that at all times during this computation, the concatenation of the input that has been consumed so far with the contents of the stack is equal to one of the strings in the left derivation. Application of a rule of the form ((q_1, \sigma, \epsilon), (q_1, \epsilon)) has the effect of removing one terminal symbol of the "Stack" column to the "Input Consumed" column. a rule of the form \(((q_1, \epsilon, A), (q_1, x))\) has the effect of applying the next step in the left derivation to the non-terminal symbol on the top of the stack. (In the "Stack" column, the pushdown automaton's stack is shown with its top on the left.) In the end, the entire input string has been consumed and the stack is empty, which means that the string has been accepted by the pushdown automaton. It should be easy to see that for any context free grammar G, the same correspondence will always hold between left derivations and computations performed by the pushdown automaton constructed from G.

The computation of a pushdown automaton can involve nondeterminism. That is, that at some point in the computation, there might be more than one transition rule that apply. When this is not the case—that is, when there is no circumstance in which two different transition rules apply—then we say that the pushdown automaton is **deterministic**. Note that a deterministic pushdown automaton can have transition rules of the form \(((q_i, \epsilon, x), (q_j, y))\) (or even \(((q_i, \epsilon, \epsilon), (q_j, y))\)) if that is the only transition from state \(q_i\). Note also that it is possible for a deterministic pushdown automaton to get "stuck": that is, it is possible that no rules apply in some circumstances even though the input has not been completely consumed or the stack is not empty. If a deterministic pushdown automaton gets stuck while reading a string x, then x is not accepted by the automaton.

The automaton given at the beginning of this section, which accepts the language \(\{a^n b^n | n \in \mathbb{N}\}\), is not deterministic. However, it is easy to construct a deterministic pushdown automaton for this language:

![](img/e1667d904eba93816cbfc3a4b0128062_211_0.png)

However, consider the language \(\{ww^R | w \in \{a, b\}\}\). Here is a pushdown automaton that accepts this language:

![](img/e1667d904eba93816cbfc3a4b0128062_211_1.png)

In state q0, this machine copies the first part of its input string onto the stack. In state q1, it tries to match the remainder of the input against the contents of the stack. In order for this to work, it must “guess” where the middle of the string occurs by following the transition from state \(q_0\) to state \(q_1\). In this case, it is by no means clear that it is possible to construct a deterministic pushdown automaton that accepts the same language.

At this point, it might be tempting to define a deterministic context-free language as one for which there exists a deterministic pushdown automaton which accepts that language. However, there is a technical problem with this definition: we need to make it possible for the pushdown automaton to detect the end of the input string. Consider the language \(\{w \mid w \in \{a, b\}^* \land n_a(w) = n_b(w)\}\), which consists of strings over the alphabet \(\{a, b\}\) in which the number of \(a\)’s is equal to the number of \(b\)’s. This language is accepted by the following pushdown automaton:

![](img/e1667d904eba93816cbfc3a4b0128062_212_0.png)

In this automaton, a \(c\) is first pushed onto the stack, and it remains on the bottom of the stack until the computation ends. During the process of reading an input string, if the machine is in state \(q_3\), then the number of \(a\)’s that have been read is greater than or equal to the number of \(b\)’s that have been read, and the stack contains (copies) of the excess \(a\)’s that have been read. Similarly, if the machine is in state \(q_4\), then the number of \(b\)’s that have been read is greater than or equal to the number of \(a\)’s that have been read, and the stack contains (copies) of the excess \(b\)’s that have been read. As the computation proceeds, if the stack contains nothing but \(c\), then the number of \(a\)’s that have been consumed by the machine is equal to the number of \(b\)’s that have been consumed; in such cases, the machine can pop the \(c\) from the stack—leaving the stack empty—and jump to state \(q_2\). If the entire string has been read at that time, then the string
