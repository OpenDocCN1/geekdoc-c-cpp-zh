# Chapter 17  Complexity Theory 423

+   ■ EXPTIME (EXP)—Problems that can be solved in exponential time by a deterministic computer. These problems can be solved by some algorithm with run time O(2f(N)) for some polynomial function f(N).

The following list summarizes the most important nondeterministic classes:

+   ■ NTIME(f(N))—Problems that can be solved in f(N) time by a deterministic computer. These problems can be solved by some algorithm with run O(f(N)) for some function f(N). For example, NTIME(N²) includes problems in which an algorithm can guess the answer and verify that it is correct in O(N²) time.

+   ■ NP—Problems that can be solved in polynomial time by a nondeterministic computer. For these problems, an algorithm guesses the correct solution and verifies it in polynomial time O(N^P) for some power P.

+   ■ NEXPT (or NEXP)—Problems that can be solved in exponential time by a nondeterministic computer. For these problems, an algorithm guesses the correct solution and verifies that it works in exponential time O(2^f(N)) for some polynomial function f(N).

Similarly, you can define classes of problems that can be solved with different amounts of space. These have the rather predictable names SPACE(f(N)), PSPACE (polynomial space), EXPSPACE (exponential space), NPSPACE (nondeterministic polynomial space), and NEXPSPACE (nondeterministic exponential space).

Some relationships among these classes are known. For example, P ⊆ NP means “is a subset of,” this statement “P is a subset of NP” To see this true, suppose a problem is in P. Then there is a nondeterministic algorithm that can find a solution to the problem in polynomial time. In that case, you can use the same algorithm to solve the problem with a nondeterministic computer—in other words, if the algorithm works it must be correct—trivially proves the solution is correct, so the nondeterministic works too.

Some of the other relationships are less obvious. For example, PSPACE = NSPACE, and EXPSPACE = NEXSPACE.

The most profound question in complexity theory is, does P equal NP? Many problems, such as sorting, are known to be in P. Many other problems, as the knapsack and traveling salesman problems described in Chapter 12, are known to be in NP. The big question is, are the problems in NP also in P?

Lots of people have spent a huge amount of time trying to determine whether these two sets are the same. No one has discovered a polynomial time algorithm to solve the knapsack or traveling salesman problem, but that does not prove that no such algorithm is possible.