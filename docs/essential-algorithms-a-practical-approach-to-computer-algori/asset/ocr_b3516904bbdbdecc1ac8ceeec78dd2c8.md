# Chapter 17  Complexity Theory 425

+   - $T_{ijk}$ is true if tape cell i contains symbol j at step k of the computation.
- $H_{ijk}$ is true if the machine's read/write head is on tape cell i at step k of the computation.
- $Q_{ijk}$ is true if the machine is in state q at step k of the computation.

The expression must also include some terms to represent how a Turing machine works. For example, suppose the tape can hold only 0s and 1s. Then the statement ($T_{001}$ AND NOT $T_{011}$) OR NOT ($T_{001}$ AND $T_{011}$)) means that cell i at step k of the computation contains a 0 or a 1 but not both.

Other parts of the expression that the read/write head is in a single position at each step of the computation, the machine starts in state 0, that the read/write head starts at cell 0, and so on.

The full boolean expression is equivalent to the original Turing machine for the problem in NP. In other words, if you set the variables $T_{ijk}$ to represent a series of inputs, the truth of the boolean expression tells you the original Turing machine would accept those inputs.

This reduces the original problem to the problem of determining whether the boolean expression can be satisfied so that SAT is NP-complete.

Once you have found one problem that is NP-complete, such as SAT, you can prove that other problems are NP-complete by reducing them to the first problem.
If A and B can be reduced to problem B in polynomial time, you can write $A \le B$.

The following sections provide examples that reduce one to another.

# 3SAT

3SAT problem is to determine whether a boolean expression in three-term conjunctive normal form can be satisfied. Three-term conjunctive normal form (3CNF) means that the boolean expression consists of a series of clauses combined with AND and NOT, and each clause contains three variables with OR and NOT. For example, the following statements are all in 3CNF:

+   - (A OR OR NOT C) AND (C OR NOT A OR B)
- (A OR C OR C) AND (A OR B OR B)
- (NOT A OR B OR NOT C)

Clearly 3SAT is in NP, as is the case with SAT, you can guess the assignment of true to false and then check whether the statement is true.

With some work, you can convert any boolean expression SAT in polynomial time into an equivalent expression in 3CNF. That means SAT is polynomial-time reducible to SAT. Because SAT is NP-complete, 3SAT must also be NP-complete.