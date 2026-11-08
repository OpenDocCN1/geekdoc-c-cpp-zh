A CNF formula is represented by the family of linear inequalities corresponding to its clauses. Thus for example the formula $(x_1 \lor \bar{x}_2 \lor x_3) \land (\bar{x}_1 \lor x_3 \lor \bar{x}_4 \lor \bar{x}_5)$ is represented by the inequalities $x_1-x_2+x_3 \ge 0$ and $-x_1+x_3+x_4-x_5 \ge -1$. The axioms of the proof system are $x_i \ge 0$, $-x_i \ge -1$. The rules of inference are:

+   (a) $\dfrac{\sum a_i \cdot x_i \ge A \;\land\; \sum b_i \cdot x_i \ge B}{\sum (a_i+b_i)\cdot x_i \ge A+B}$

+   (b) $\dfrac{\sum a_i \cdot x_i \ge A}{\sum (c\cdot a_i)\cdot x_i \ge c\cdot A}$

where $c \ge 1$ is an arbitrary integer;

+   (c) $\dfrac{\sum (c\cdot a_i)\cdot x_i \ge A}{\sum a_i\cdot x_i \ge \left\lceil \frac{A}{c} \right\rceil}$

where $c>1$ is an arbitrary integer.

A derivation $D$ of the inequality $I$ from inequalities $I_1,\ldots,I_m$ is a sequence $D_1,\ldots,D_n$ such that $I=D_n$ and for all $i<n$ either $D_i$ is an axiom, or one of $I_i,\ldots,I_m$ or inferred from $D_j,D_k$ for $j,k<i$ by means of a rule of inference. A CP refutation of $I_1,\ldots,I_m$ is a derivation of $0\ge 1$ from $I_1,\ldots,I_m$.

We have seen above the soundness and the completeness of Resolution for CNF formulas, see Theorem 2.15. Soundness in the sense that given any formula $\phi$ which has a resolution refutation $\pi$, $\phi$ is not satisfiable and completeness in the sense that given any unsatisfiable formula $\phi$, there is a resolution refutation $\pi$ of $\phi$. Theorem 2.19 can be proved exploiting the completeness of $R$, since CP easily simulates resolution as observed in (23).

**Theorem 2.19.** *The proof system CP is sound and complete with respect to CNF formulas.*

For the soundness part we can argue as follows. Let $\phi$ be a CNF formula with a CP refutation $\gamma$. Suppose $\phi$ is satisfied by the assignment $\alpha$. Instantiate each inequality in $\gamma$ of $\phi$ by assigning the boolean variables their value under $\alpha$. By induction on the length of $\gamma$ we can prove that each instantiated inequality in the resulting $\gamma$ holds. This is contradiction, because we cannot have the inequality $0\ge 1$ as the last element of the refutation. Goerdt (30) proved that Frege systems polynomially simulate the CP proof system.

Other examples of mathematical proof systems are for instance the Nullstellensatz system introduced in (4), the Polynomial Calculus (15) and the Gaussian Calculus first defined in (5). At the end of this chapter a new mathematical proof system using cellular automata will be proposed.

# 3. Applications of propositional logic to cellular automata

Cellular automata can be described as large collections of simple objects locally interacting with each other. A $d$-dimensional cellular automaton consists of an infinite $d$-dimensional array of identical cells. Each cell is always in one state from a finite state set. The cells change their states synchronously in discrete time steps according to a local rule. The rule gives the