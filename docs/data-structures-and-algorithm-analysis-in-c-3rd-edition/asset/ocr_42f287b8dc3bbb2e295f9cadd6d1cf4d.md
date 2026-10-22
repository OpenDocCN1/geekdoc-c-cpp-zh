comparisons is the same for both methods, the total number of comparisons required by move-to-front is less than twice the number of comparisons required by the optimal static ordering.

# 14.4 Further Reading

A good introduction to solving recurrence relations appears in *Applied Combinatorics* by Fred S. Roberts [Rob84]. For a more advanced treatment, see *Concrete Mathematics* by Graham, Knuth, and Patashnik [GKP94].

Cormen, Leiserson, and Rivest provide a good discussion on various methods for performing amortized analysis in *Introduction to Algorithms* [CLRS09]. For an amortized analysis that the splay tree requires $m \log n$ time to perform a series of $m$ operations on $n$ nodes when $m > n$, see “Self-Adjusting Binary Search Trees” by Sleator and Tarjan [ST85]. The proof for Theorem 14.2 comes from “Amortized Analysis of Self-Organizing Sequential Search Heuristics” by Bentley and McGeoch [BM85].

# 14.5 Exercises

14.1 Use the technique of guessing a polynomial and deriving the coefficients to solve the summation

$$\sum_{i=1}^{n} i^2.$$

14.2 Use the technique of guessing a polynomial and deriving the coefficients to solve the summation

$$\sum_{i=1}^{n} i^3.$$

14.3 Find, and prove correct, a closed-form solution for

$$\sum_{i=a}^{b} i^2.$$

14.4 Use subtract-and-guess or divide-and-guess to find the closed form solution for the following summation. You must first find a pattern from which to deduce a potential closed form solution, and then prove that the proposed solution is correct.

$$\sum_{i=1}^{n} i/2^i$$