# Sec. 17.2 Hard Problems

exponential-time program with cost 1.001^n is practical. The reality that we know of almost no problems where the best polynomial-time algorithm has high degree (nearly all have degree four or less), while almost no exponential-time algorithms (whose cost is $O(c^n)$) have their constant $c$ close to zero. There is no much gray area between polynomial and exponential algorithms in practice.

For the rest of this chapter, we define a **hard algorithm** to be one that runs in exponential time, that for some constant $c > 1$. A definition for a hard problem will be presented in the next section.

# 17.2.1 The Theory of $\mathcal{NP}$-Completeness

Imagine a magical computer that works by guessing the correct solution from all of the possible solutions to a problem. Another way to look at this is imagine a super parallel computer that could test all solutions simultaneously. Certainly this magical (or highly parallel) computer can do anything a normal computer can do. Consider some problem more quickly than a normal computer can, given a guess for a solution, the checking to see if it is correct can be done in polynomial time. Even if the number of possible solutions is exponential (equivalently, all possible solutions are checked simultaneously in polynomial time), and thus the problem can be solved in polynomial time by our hypothetical magical computer. Another view of this concept is: if you cannot get the answer to a problem in polynomial time by guessing the right answer and then checking it, then you cannot do it in polynomial time in any other way.

The idea of “guessing” the right answer to a problem — or checking all possible solutions in parallel to determine which is correct — is called non-determinism. An algorithm that works in this manner is called a **non-deterministic algorithm**, and any problem with an algorithm that runs on a non-deterministic machine in polynomial time is given a special name: It is said to be a problem in $\mathcal{NP}$. Thus, problems in $\mathcal{NP}$ are those problems that can be solved in polynomial time on a non-deterministic machine.

Not all problems requiring exponential time on a regular computer are in $\mathcal{NP}$. For example, Towers of Hanoi is not in $\mathcal{NP}$, because it must print out $O(2^n)$ for $n$ disks. A non-deterministic machine cannot “guess” and print the correct answer in less time.

On the other hand, consider the TRAVELING SALESMAN problem.

| TRAVELING SALESMAN (1) |
| **Input**: A complete, directed graph G with positive distances assigned to each edge in the graph.
| **Output**: The shortest cycle that includes every vertex. |