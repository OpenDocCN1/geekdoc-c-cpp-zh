The main point of the effective interpolation method is that by establishing a good upper bound for a proof system $P$ in the form of the effective interpolation we prove lower bounds on the size of the proofs in $P$. That is,

**Theorem 2.17.** *Assume that $U$ and $V$ are two disjoint $\mathcal{N}^P$-sets such that $U_l$ and $V_l$ are inseparable by a set of circuit complexity $\leqslant (n)$, all $n \geqslant 1$. Assume that $P$ admits effective interpolation. Then the implications $A_n \to \neg B_n$ require proofs in $P$ of size $\geqslant s(n)^r$ for some $r > 0$.*

The system resolution admits feasible interpolation, as was proven in (41). In fact,

**Theorem 2.18** (Krajíček (41)). *Assume that the set of clauses*

$\{A_1, \ldots, A_m, B_1, \ldots, B_l\}$

+   where
+   1. $A_i \in \{p_1, \neg p_1, \ldots, p_n, \neg p_n, q_1, \neg q_1, \ldots, q_s, \neg q_s\}$, all $i \leq m$
+   2. $B_j \in \{p_1, \neg p_1, \ldots, p_n, \neg p_n, r_1, \neg r_1, \ldots, r_t, \neg r_t\}$, all $j \leq l$
+   
+   has a resolution refutation with $k$ clauses.
+   Then the implication

$\displaystyle \bigwedge_{i\leq m}(\bigvee A_i) \to \neg\bigwedge_{i\leq l}(\bigvee B_j)$

*has an interpolant $I$ whose circuit-size is $kn^{O(1)}$.*

The key idea of the proof of the previous theorem is that the structure of a resolution refutation allows one easily to decide which clauses cause the unsatisfiability under a specific assignment. Furthermore, it should be noticed that the interpolant can be computed by a polynomial time algorithm having an access to the resolution refutation. Theorem 2.18 is important because it is a theorem used later on in the next section.

# 2.4 “Mathematical” proof systems

The set of propositional tautologies $TAUT$ is a $co\mathcal{N}^P$-complete set. In general a proof system is a relation $R(x,y)$ computable in polynomial time such that

$x \in TAUT$ if and only if $\exists y(R(x,y))$.

A proof of $x$ is a $y$ such that $R(x,y)$ holds. Thus one can take an $co\mathcal{N}^P$-complete set and a suitable relation $R$ over it and investigate the complexity of such proofs. In this section we recall a few proof systems (only one in some detail) “mathematically” based on $co\mathcal{N}^P$-complete sets.

A nice example of a well-known “mathematical”$^{16}$ proof system is the proof system Cutting Plane CP. The Cutting Plane proof system $(CP)$ is a refutation system based on showing the non-existence of solutions for a family of linear equalities. A line in a proof in this system CP is an expression of the form

$\displaystyle \sum a_i \cdot x_i \geq B$

where $a_1, \ldots, a_n$, $B$ are integers. Then for a given clause $C$, and the variables $x_i$, $i \in P$, occur positively in $C$, and variables $x_i$, $i \in N$, occur negatively in $C$, then $C$ is represented by the linear inequality

$\displaystyle \sum_{i\in P} x_i - \sum_{i\in N} x_i \geq 1-|N|.$

$^{16}$ This expression is taken from Pudlák (51).