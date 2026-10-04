# 4.5. ANALYZING INFORMATION FLOW

Later, we will provide an interpractical generalization of this definition
(Definition 4.2 in section 4.6), which additionally exploits the backward slices of all output ports instead of the
sufficient to consider the backward slices of all output PDG; this observation again reduces spurious flow and the risk for false alarms.
For the time being, we demand (4.7) and (4.8) for the whole PDG, which is still
a correct (if slightly less precise) definition.

For simplicity in presentation, we extend P and R to total functions P' and
R' such that all nodes have a provided and required security level:

```
$P'(x) = \begin{cases} P(x), & \text{if } x \in dom(P) \ \perp, & \text{otherwise} \end{cases} \quad (4.9)
```

```
$R'(x) = \begin{cases} R(x), & \text{if } x \in dom(R) \ \perp, & \text{otherwise} \end{cases} \quad (4.10)
```

Note that $\perp$ is the neutral element for $\sqcup$, and $	op$ is the neutral element for $\Pi$.
Now equation (4.7) simplifies to

```
$S(x) \geq P'(x) \sqcup_{y \in pred(x)} S(y) \quad (4.11)
```

and equation (4.8) simplifies to

```
$R'(x) \geq S(x) \quad (4.12)
```

# 4.5.2 Solving Flow equations

Equation (4.11) is satisfied in the most precise way, and hence the risk that
eequation (4.8) is violated is minimized, if the inequality for $S$ turns into equality:

```
$S(x) = P'(x) \sqcup_{y \in pred(x)} S(y) \quad (4.13)
```

Of course (4.13) also satisfies (4.11), and can be read as an algorithm which
computes $S(x)$ from $P(x)$ and $x$'s preds $S$ values. Thus equation (4.13)
defines a *forward propagation*: what happens if all the $P$ values are
propagated through the PDG (while ignoring $R$).

We now show that equation (4.13) corresponds to a well-known concept
in program analysis, a monotone dataflow framework [KU77]
presented in section 2.1, which allows efficient computation.nnFlows start with a lattice of attributes, which is in our case. L is for
every $x \in N$, a so-called function $f_x : L \rightarrow L$ must be defined, which
typically has the form $f_x(l) = g_x \sqcup in(k_x)$. In our case, $g_x = P'(x)$ and $k_x = \perp$,
so $f_x(l) = P'(x) \sqcup l$. Furthermore, for every $x \in N$, the framework defines
out(x) = f_x(in(x))$ and $in(x) = \sqcup_{y \in pred(x)} out(y)$. In our case, we

```
$out(x) = f_x(in(x)) = P'(x) \sqcup_{y \in pred(x)} S(y) = S(x)
```

> $^9$where $g_x

103