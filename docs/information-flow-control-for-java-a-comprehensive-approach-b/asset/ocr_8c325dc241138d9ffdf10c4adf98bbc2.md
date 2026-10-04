# 5.4. DYNAMIC PATH CONDITIONS IN DEPENDENCE GRAPHS

# 5.3.7 Path Conditions for Information Flow Control

When we discover an interference at a statement $s$ where the required security level $R(s)$ is not larger than the actual (computed) security level $S(s)$, we can investigate the source of this interference. We distinguish between *immediate* and *transitive* interference. The immediate interference exists between $s$ and its predecessors which lead to the computed security level $S(s)$. Usually, only a subset of the predecessors is responsible—it is the minimal subset $N \subseteq pred(s)$ that lead to $S(s)$: $S(s) = \bigcup_{y \in N} S(y)$.

Path conditions give the condition $PI$ of the immediate interference and we can compute it through

```
PI = \bigwedge_{y \in N} PC(y,s)
```

Often, we are more interested in the *transitive* interference, i.e. the interference between a statement $s$ with a required security level of $l$ and a statement $x$ with a provided security level $p$, where there is a path $x \to^* s$ which "transmits" $p$ to $s$. To investigate the transitive interference, we use the correspondence between slicing and noninterference. The first step is to compute the backwards slice $BS(s)$ that contains all statements that may influence $s$. From $BS(s)$ we extract all statements with a provided security level as the possible set of information sources:

```
T = {x \in BS(s) \mid\ x \in dom P}
```

```
PT = \bigwedge_{y \in T'} PC(y,s)
```

Note that there may exist multiple minimal subsets $N$ and $T'$ and we might want to examine all of them.

# 5.4 Dynamic Path Conditions in Dependence Graphs

The previous sections developed analyses that statically enforce a certain security policy. Ensuring that security breaches are impossible at compile time is favorable to registering a violation at runtime, where at least information is leaked, some illicit event has happened. Still, static checks can only validate the validity of the specified properties. For unforeseen incidents sensitive modules usually contain some sort of "flight recorder". It allows the posteriori reconstruction of problems leading to—possibly fatal—error.

This section presents a new approach leveraging data recorded during program execution—the *program trace*—for the posteriori detection and isolation of problem cases. The trace is used to improve precision in two ways, which may well be combined: First, a dynamic slicing algorithm identifies all statements that actually influenced the fatal statement during program execution.