Note that polynomial transformability is a transitive relation, i.e if \(\Pi_1\) is polynomially transformable to \(\Pi_2\) and \(\Pi_2\) is polynomially transformable to \(\Pi_1\), then \(\Pi_1\) is polynomially transformable to \(\Pi_3\). Therefore, if we want to prove that a decision problem \(\Pi\) is \(\mathcal{NP}\)-complete, we only have to show that

+   (i) \(\Pi\) is in \(\mathcal{NP}\).

+   (ii) A decision problem already known to be \(\mathcal{NP}\)-complete can be polynomially transformed to \(\Pi\).

We now want to focus on combinatorial optimization problems. We therefore extend the concept of polynomial transformability. Let \(\Pi_1\) and \(\Pi_2\) be two problems (not necessarily decision problems).

**Definition 1.3.** A **polynomial reduction** from \(\Pi_1\) to \(\Pi_2\) is an algorithm \(\mathcal{A}_1\) that solves \(\Pi_1\) by using an algorithm \(\mathcal{A}_2\) for \(\Pi_2\) as a subroutine such that, if \(\mathcal{A}_2\) were a polynomial time algorithm for \(\Pi_2\), then \(\mathcal{A}_1\) would be a polynomial time algorithm for \(\Pi_1\).

**Definition 1.4.** An optimization problem \(\Pi\) is called \(\mathcal{NP}\)-**hard** if there exists an \(\mathcal{NP}\)-**complete** decision problem that can be polynomially reduced to \(\Pi\).

Clearly, an optimization problem is \(\mathcal{NP}\)-**hard**, if the corresponding decision problem is \(\mathcal{NP}\)-**complete**.

# 1.3 Heuristic and relaxation methods

As we have seen, once it is established that a combinatorial problem is \(\mathcal{NP}\)-**hard**, it is unlikely that it can be solved by a polynomial algorithm. Different approaches have been suggested in the past, to solve this kind of problems. In principle, they can be classified as exact algorithms, approximation algorithms, relaxation methods, or heuristic approaches.

When trying to find good solutions to hard minimization problems in combinatorial optimization, two issues must be taken into consideration:

+   calculating an upper bound that is as close as possible to the optimum;

+   calculating a lower bound that is as close as possible to the optimum.

It is a fundamental goal of computer science to find algorithms which have both provably good running times and provably good or optimal quality of the solution.

A heuristic is an algorithm that abandons one aspect, e.g. it usually finds pretty good solutions, but there is no proof that the solutions may not become arbitrarily bad. On the other hand, the algorithm may run reasonably quickly, but there is no