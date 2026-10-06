# 182 ■ Limits of Computation

In each case below, show how a polynomial solution to the decision problem will yield a polynomial solution to the search problem.

+   a. Decision problem: Given n and k, does n have a factor greater than k?

Search problem: Given n, find its prime factorization.

+   b. Decision problem: Given a graph G with vertices v and w and a number k, does G have a path from v to w of length at least k?

Search problem: Given G with vertices v and w, what is the length of the longest path from v to w

+   c. Decision problem: Given G = (V, E) and integer k, is G k-colorable?

Search problem: Given G = (V, E), find the smallest k such that G is k-colorable.

+   10. Let Y be any nontrivial problem in P, the class of problems with polynomial solutions. Show that Y is P-complete. (A problem is nontrivial if it has yes and no instances.)

+   11. Get rich (quick)? See http://www.claymath.org/millennium/P_vs_NP!. (Compare with Exercise 9 in Chapter 7.)

+   12. Prove:

Theorem: If L₁ ≤ L₂ and L₂ is not in P, then so is L₁.

Theorem: If L₁ ≤ L₂ and L₁ is not in P, then L₂ is not in P.

Theorem: If L₁ ≤ L₂, then L₁ ≤ L₂.

Theorem: If L₁ ≤ L₂ and L₂ ≤ L₃, then L₁ ≤ L₃.

+   13. Prove: If two functions f and g are in P, then so are: (a) f(n)g(n), f(n)+g(n), and (c) f(g(n)).

+   14. Give yes and no instances of CNF-SAT (different from the examples in the text) using:

+   a. The single Boolean variable x₁

+   b. At least two Boolean variables (x₁, x₂, ...)

Write out the encodings over Σ = {x, 0, 1, ...9, ∨, ∧, ¬, (, )} of instance of CNF-SAT from: