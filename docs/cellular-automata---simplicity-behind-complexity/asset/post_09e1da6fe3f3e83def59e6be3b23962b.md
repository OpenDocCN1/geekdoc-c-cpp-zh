
¬p₁, …, pₙ, ¬pₙ appear in C. We prove by induction on n that for any such C there is a resolution refutation of C.

**Basis Case:** If n = 1 there is nothing to prove: the set C must contain {p₁} and {¬p₁} and then by the resolution rule we have {}.

**Induction Step:** Assume that n > 1. Partition C in four disjoint sets:

C₀₀ ∪ C₀₁ ∪ C₁₀ ∪ C₁₁

of those clauses which contain no pₙ and no ¬pₙ, no pₙ but do contain ¬pₙ, do contain pₙ but not ¬pₙ and contain both pₙ and ¬pₙ, respectively. Produce a new set of clauses C′ by:

1. Delete all clauses from C₁₁.
2. Replace C₀₁ ∪ C₁₀ by the set of clauses that are obtained by the application of the resolution rule to all pairs of clauses C₁ ∪ {¬pₙ} from C₀₁ and C₂ ∪ {pₙ} from C₁₀.

The new set of clauses do not contain either pₙ or ¬pₙ. It is easy to see that the new set of clauses C′ is also satisfiable. Any assignment α′: {p₁, …, pₙ₋₁} → {0, 1} satisfies all clauses C₁ such that C₁ ∪ {¬pₙ} ∈ C₀₁, or all clauses C₂ such that C₂ ∪ {pₙ} ∈ C₁₀. Hence α′ can be extended to a truth assignment α satisfying C′, which is a contradiction because by our hypothesis C is unsatisfiable.

A resolution refutation π = D₁, …, Dₖ can be represented as a directed acyclic graph (dag-like) in which the clauses are the vertices, and if two clauses C ∪ {p} and D ∪ {¬p} are resolved by the resolution rule, then there exists a directed edge going from the two clauses to the clause produced by the resolvent C ∪ D. A resolution refutation π = D₁, …, Dₖ is tree-like if and only if each Dᵢ is used at most once as a hypothesis of an inference in the proof. The underlying graph of π is a tree. The proof system allowing exactly tree-like proofs is called tree-like resolution and denoted by R*.

In propositional proof complexity, perhaps the most important relation between dag-like refutations and refutations in R* is that the former can produce exponentially shorter refutations than the latter. A simple remark on this is that in tree-like proof anything which is needed more than once in the refutation must be derived again each time from the initial clauses. A superpolynomial separation between R* and R was given in (64), and later by others in (16) and (32). Later on, in (10) has been presented a family of clauses for which R* suffers an exponential blow-up with respect to R. For an improvement of the exponential separation the reader can see (6).

## 2.3 Interpolation and effective interpolation

A basic result in mathematical logic is the Craig interpolation theorem (24). The theorem says that whenever an implication A → B is valid then there exists a formula I, called an interpolant, which contains only those symbols of the language occurring in A and B and such that the two implications A → I and I → B are both valid formulas. Craig’s interpolation theorem is a fundamental result in propositional logic and in predicate logic as well.

Finding an interpolant for the implication is a problem of some relevance with respect to computational complexity theory. Mundici in (45) pointed out the following. Let $U$ and $V$ be two disjoint $\mathsf{NP}$-sets, subsets of $\{0,1\}^*$. By the proof of the $\mathsf{NP}$-completeness of satisfiability (19) there are sequences of propositional formulas $A_n(p_1,\ldots,p_n,q_1,\ldots,q_{s_n})$ and $B_n(p_1,\ldots,p_n,r_1,\ldots,r_{t_n})$ such that the size of $A_n$ and $B_n$ is $n^{O(1)}$ and such that

$$U_n := U \cap \{0,1\}^n = \{(\delta_1,\ldots,\delta_n) \in \{0,1\}^n \mid \exists \alpha_1,\ldots,\alpha_{s_n}\ A_n(\bar{\delta},\bar{\alpha})\text{ holds}\}.$$

and

$$V_n := V \cap \{0,1\}^n = \{(\delta_1,\ldots,\delta_n) \in \{0,1\}^n \mid \exists \beta_1,\ldots,\beta_{t_n}\ B_n(\bar{\delta},\bar{\beta})\text{ holds}\}.$$

Assuming that the sets $U$ and $V$ are disjoint sets is equivalent to the statement that the implications $A_n \to \neg B_n$ are all tautologies. Craig's interpolation theorem guarantees there is a formula $I_n(p)$ constructed only using atoms $p$ such that

$$A_n \to I_n$$

and

$$I_n \to \neg B_n$$

are both tautologies. Thus the set

$$W := \bigcup_n\{\delta \in \{0,1\}^n \mid I_n(\bar{\delta})\text{ holds}\}$$

defined by the interpolant $I_n$ separates $U$ from $V$: $U \subseteq W$ and $W \cap V = \varnothing$. Hence an estimate of the complexity of propositional interpolation formulas in terms of the complexity of an implication yields an estimate to the computational complexity of a set separating $U$ from $V$. In particular, a lower bound to a complexity of interpolating formulas gives a lower bound on the complexity of sets separating disjoint $\mathsf{NP}$-sets. Of course, we cannot really expect to have a lower bound on the size of a formula or a circuit defining a suitable $W$ from the length of the implication $A_n \to \neg B_n$. This is because, as remarked by Mundici (45), it would imply that $\mathsf{NP} \cap \mathsf{coNP} \subseteq \mathsf{P/poly}$. In fact, for $U \in \mathsf{NP}$, $V \in \mathsf{coNP}$ we can take $V$ to be the complement of $U$ and hence it must hold that $W = U$. In (39), Krajíček formulated the idea of effective interpolations as follows:

> *For a given propositional proof system, try to estimate the circuit-size of an interpolant of an implication in terms of the size of the shortest proof of the implication.*

In other words, for a given propositional proof system establish an upper bound on the computational complexity of an interpolant of $A$ and $B$ in terms of the size of a proof of the validity of $A_n \to \neg B_n$. Then any pair $A$ and $B$ which is hard to interpolate yields a formula which must have large proofs of validity. This fact can be exploited in proving lower bounds, and indeed several new lower bounds came out from its application, see (41), (52). Besides lower bounds, effective interpolation revealed to be an excellent idea in other areas in proving results of independence in bounded arithmetic (53) and in establishing links between proof complexity and modern cryptography.

**Definition 2.16.** A propositional proof system $P$ admits effective interpolation if and only if there is a polynomial $p(x)$ such that any implication $A \to B$ with a proof in $P$ of size $m$ has an interpolant of a circuit size $\leq p(m)$.

15 A general overview of these applications has been given in (38) and (51).

The main point of the effective interpolation method is that by establishing a good upper bound for a proof system $P$ in the form of the effective interpolation we prove lower bounds on the size of the proofs in $P$. That is,

**Theorem 2.17.** *Assume that $U$ and $V$ are two disjoint $\mathsf{NP}$-sets such that $U_l$ and $V_l$ are inseparable by a set of circuit complexity $\leqslant (n)$, all $n \geqslant 1$. Assume that $P$ admits effective interpolation. Then the implications $A_n \to \neg B_n$ require proofs in $P$ of size $\geqslant s(n)^r$ for some $r > 0$.*

The system resolution admits feasible interpolation, as was proven in (41). In fact,

**Theorem 2.18** (Krajíček (41)). *Assume that the set of clauses*

$\{A_1, \ldots, A_m, B_1, \ldots, B_l\}$

*where*

1. $A_i \in \{p_1, \neg p_1, \ldots, p_n, \neg p_n, q_1, \neg q_1, \ldots, q_s, \neg q_s\}$, all $i \leq m$
2. $B_j \in \{p_1, \neg p_1, \ldots, p_n, \neg p_n, r_1, \neg r_1, \ldots, r_t, \neg r_t\}$, all $j \leq l$

*has a resolution refutation with $k$ clauses. Then the implication*

$\displaystyle \bigwedge_{i\leq m}(\bigvee A_i) \to \neg\bigwedge_{i\leq l}(\bigvee B_j)$

*has an interpolant $I$ whose circuit-size is $kn^{O(1)}$.*

The key idea of the proof of the previous theorem is that the structure of a resolution refutation allows one easily to decide which clauses cause the unsatisfiability under a specific assignment. Furthermore, it should be noticed that the interpolant can be computed by a polynomial time algorithm having an access to the resolution refutation. Theorem 2.18 is important because it is a theorem used later on in the next section.

## 2.4 “Mathematical” proof systems

The set of propositional tautologies $TAUT$ is a $\mathsf{coNP}$-complete set. In general a proof system is a relation $R(x,y)$ computable in polynomial time such that

$x \in TAUT$ if and only if $\exists y(R(x,y))$.

A proof of $x$ is a $y$ such that $R(x,y)$ holds. Thus one can take an $\mathsf{coNP}$-complete set and a suitable relation $R$ over it and investigate the complexity of such proofs. In this section we recall a few proof systems (only one in some detail) “mathematically” based on $\mathsf{coNP}$-complete sets.

A nice example of a well-known “mathematical”$^{16}$ proof system is the proof system Cutting Plane CP. The Cutting Plane proof system $(CP)$ is a refutation system based on showing the non-existence of solutions for a family of linear equalities. A line in a proof in this system CP is an expression of the form

$\displaystyle \sum a_i \cdot x_i \geq B$

where $a_1, \ldots, a_n$, $B$ are integers. Then for a given clause $C$, and the variables $x_i$, $i \in P$, occur positively in $C$, and variables $x_i$, $i \in N$, occur negatively in $C$, then $C$ is represented by the linear inequality

$\displaystyle \sum_{i\in P} x_i - \sum_{i\in N} x_i \geq 1-|N|.$

$^{16}$ This expression is taken from Pudlák (51).
