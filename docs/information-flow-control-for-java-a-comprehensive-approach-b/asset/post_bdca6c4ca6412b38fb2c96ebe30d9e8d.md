
## 5.2. FOUNDATIONS OF PATH CONDITIONS

$PC(x, y)$ is a necessary condition for flow from $x$ to $y$, and $E(z)$ is a necessary condition for the execution of $z$. A control path is a path that consists of control dependence edges only. $E(x)$ is computed along all control paths from the $Start$ node of function $x$ based on the conditions $c(u \to \mu)$ associated with dependence edge $u \to \mu$. For control dependences, $c(u \to \mu)$ is typically a condition from a *while-* or *if-statement*. Program variables in a path condition are (implicitly) existentially quantified, which are necessary conditions for potential information flow.

Because the path between the criterion nodes are based on the chops, we will be interested in the set of paths $P_1, P_2, \dots \in CH(x, y)$ and a slightly relaxed relation for path conditions is:

```
$PC(x, y) = \bigwedge_{z \in PC(x,y)} E(z)$
```

In [[SRK06]] Selting et al. explain why this formula is correct and precise, and why it clearly simplifies computation. They also show that cycles in $CH(x, y)$ can be safely ignored for computation of $PC(x, y)$, such that the formula is always finite. For the example in Figure 5.1, the following equation and path conditions are computed:

```
$c(2 \to 3) \equiv c(2 \to 4) \equiv (n > 0), \quad c(4 \to 5) \equiv (x > 0)$,
$c(4 \to 7) \equiv (x \le 0)$,
$E(1) = \text{true}, \quad E(3) \equiv (n > 0) \wedge E(5) \equiv (n > 0) \wedge (x > 0)$,
$PC(1, 5) \equiv E(1) \wedge E(5) \equiv (n > 0) \wedge (x > 0)$
```

In the presence of data structures like arrays or pointers, additional constraints will be generated. For data dependences, $\Phi(\nu \to \mu)$ is a condition constraining information flow through data types. As an example we consider arrays (a full presentation can be found in [[SRK06]]) A data dependence $u \to \mu$ between array element $a[E_1] = \dots$ and a usage $a[E_2]$ generates $\Phi(\nu \to \mu) = E_1 \wedge E_2$; all other dependences will generate $\Phi(\nu \to \mu) = \text{true}$. The equation to compute a path condition becomes:

```
$PC(x, y) = \bigwedge_{z \in PC(x,y)} (\bigwedge_{z \in P} E(z) \wedge \bigwedge_{u \in P} \Phi(u \to v)) \quad (5.2)$
```

For classification the following program fragments and their path conditions:

- 1 a[i+3] = x;
- 2 if (i>10)
- 3 y = a[2*j-42];

```
$PC(1, 3) \equiv (i > 10) \wedge (i + 3 = 2j - 42)$
```

which, apart from the execution condition, contains a term that requires the two index expressions to be equal,

## CHAPTER 5. PATH CONDITIONS

```
1 x = a;
2 while (x < 7) {
3 x = y + x;
4 if (x == 8)
5 p(x);
6 }
1 x1 = a;
2 while (x2=Φ(x1,x3),x2<7) {
3 x3 = y + x2;
4 if (x3 == 8)
5 p(x3);
6 }
```

Figure 5.2: Multiple variable assignments

```
1 a[i+3] = x;
2 if ((i>10)&&(j<5))
3 y = a[2*j];
```

> PC(1,3) ≡ (i > 10) ∧ (j < 5) ∧ (i + 3 = 2j - 42) ≡ false

which is not satisfiable, as the index expression and the execution conditions contradict.
These examples indicate that path conditions give precise conditions for information flow, and sometimes determine that such flow is impossible even though there is a path in the graph. Note that in practice path conditions tend to be large and a constraint solver is used to simplify them.

### Multiple Variable Assignments

Computing paths based on the original program text may render the condition unsatisfiable even if the influence is possible. As an example, consider the code in Figure 5.2 (left) and the (primitive) path condition

> PC(1,5) ≡ (x < 7) ∧ (x = 8)

between a in line 1 and x in line 5. The condition is unsatisfiable, although there is definitely a way how line 1 can influence line 5. The problem is that the program contains multiple assignments to the variable x that path condition cannot distinguish. For static path conditions this is solved by using a variant of SSA-form [CFR91] of the program. How, different variables are distinguished and eventually brought together using the ϕ operator, replacing multiple assignments with single assignments. Figure 5.2 (right) shows the SSA form of the original program (left).

The SSA form makes our path condition solvable by distinguishing different variables of the x:

> PC(1,5) ≡ (x < 7) ∧ (x = 8)

Transforming a program into SSA, however, modifies the code representation and is not desirable for dependence graphs in code ValSoft which is close to the source code structure. In order to maintain the code structure, an assignment form similar to the SSA form is used: Index numbers represent the

128

## 5.2. FOUNDATIONS OF PATH CONDITIONS

node numbers in the dependence graph, allowing a precise distinction between different variable occurrences. Path conditions as

```
($e\puf[idx] = "" + $)
```

are thus written as

```
($e\puf_{99}[idx_{98}]=97$ + ""_{101}$)
```

The $\phi$ operator does not occur in the code structure, but is only used for computing path conditions.

### Weak and Strong Path Conditions

For a given chop between two statements $x, y$, one can usually define more than one path condition. Still, every instance is a necessary condition for information flow along the chop. To argue about quality, a partial order $\le$ is defined for the pair $(x, y)$

```
$PC(x,y) \le PC(x,y) \quad PC(x,y) \Rightarrow PC'(x,y)$
```

In such a case $PC(x,y)$ is called stronger than $PC'(x,y)$. Stronger conditions are generally easier to solve by the constraint solver and thus more favorable.

Note that the underlying chop affects the strength of the path condition: if two chops exist where one is more precise than the other $CH(x,y) \subset CH'(x,y)$, then every path $P \in CH(x,y)$ in the smaller chop is also a path in the larger chop. Thus, the smaller chop generates a stronger path condition, since the division in the path runs over several:

![](img/27c6595637bae6b27613772d7079f8a2_138_0.png)

This fact forms the theoretic basis for Section 5.4.2, as the dynamic chop is smaller than the static chop.

Adding another conjunctive term $R$ to the path condition is a different way to strengthen it. In Section 5.4.3 logical formula will be generated from dynamic trace once joined with the original path condition, yielding a stronger (or equal) path condition:

```
$PC(x,y) \wedge R \ge PC(x,y)$
```

### 5.2.2 Interprocedural Path Conditions

In analogy to interprocedural slicing and chopping, interprocedural path conditions need to be realizable [Ki05] paths. Intuitively, this means that a path in the system dependence graph (SDG) [HRB90]-i.e. several PDGs connected by interprocedural edges calling the graph that enters a procedure through a certain invocation site must not leave at a different invocation site. As an illustration, consider Figure 5.3. Here are only

> In fact, path conditions only a preorder. Modulo equivalence one obtains a partial order [SRK06, Ram94].

## CHAPTER 5. PATH CONDITIONS

![](img/27c6595637bae6b27613772d7079f8a2_139_0.png)

two realizable paths at call site $\Lambda$ (left), namely from parameter $a$ to $d$ and from $b$ to $c$. These transitive dependencies, stemming from dependencies in method $f$, are represented in the SDG as summary edges (dashed in Figure 5.3). The path from $a$ to $h$ is invalid, as parameters from one invocation cannot influence another invocation.

In the following, we focus on path conditions where start and end node are in the same method (same-level), and concentrate on object-oriented constructs. The general case, where start and end node of the path condition lie in different methods, can be constructed by concatenating several-level conditions. However, this is not specific to Java and has been addressed in previous work [SRK06].

Path conditions favor common subpaths with virtual decomposition [SRK06]; common subpaths between formal parameters connected by a summary edge have found candidates for decomposition. Virtual decomposition ignores call and parameter-passing edges but includes summary edges instead. A $\Phi$ condition (which is conjunctively added to the execution condition) represents the condition for information flow along a summary edge [SRK06]. This condition is induced by the path between the corresponding formal parameters combined with conditions that represent parameter binding. In Figure 5.3 the condition between $a$ and $d$ would be:

```
$\Phi(a) \equiv u = a \wedge PC(u, y) \wedge d = y$
```

$PC(u, y)$ can be reused at other call sites with a different parameter binding.

Details of path generation are not presented here, but the reader should be aware that making path conditions work for C and realistic programs requires years of theoretical and practical work [Sne96, RS02, Rob05, SRK06]. The major steps include that programs must be transformed into assignment form (see above); and while PDG cycles can be ignored, due to the high number of cycle-free PDG paths in realistic programs, interval

130
