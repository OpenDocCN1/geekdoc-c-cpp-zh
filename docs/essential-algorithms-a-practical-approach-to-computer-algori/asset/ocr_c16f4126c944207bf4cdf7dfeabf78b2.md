# 424 Chapter 17 Complexity Theory

One way you can compare the difficulty of two algorithms is by reducing one to the other, as described in the next section.

# Reductions

To reduce one problem to another, you must come up with a way for the solution to one problem to give you the solution to the other. If you can do that within a certain amount of time, the maximum run time of the two algorithms is the same within the amount of time you spent on the reduction.

For example, you know that prime factoring is in NP and sorting is in P. Suppose you could find an algorithm that can reduce factoring into a sorting problem, and the reduction takes only polynomial time. In that case, you could solve problems in polynomial time by solving the corresponding problem. (Of course, no one knows how to reduce to sorting. If someone had discovered such a reduction, factoring wouldn't be as hard as it is.)

Polynomial time reductions are particularly important because they let you reduce many problems in NP to other problems in NP. In fact, there are some problems to which every problem in NP can be reduced. Those problems are called NP-complete.

The first NP-complete problem was the satisfiability problem (SAT). In this problem, you are given a boolean expression that includes variables that could be true or false, such as (A AND B) OR (B NOT C). The goal is to determine whether there is a way to assign the values true and false to the variables to make the statement true.

The Cook-Levin theorem (or Cook's theorem) proves that SAT is NP-complete. The details are rather technical (see http://en.wikipedia.org/wiki/Cook–Levin_theorem for details), but the basic ideas are not too confusing.

To show that SAT is NP-complete, you need to do two things: Show that any other problem in NP can be reduced to SAT.

SAT is in NP because you can guess the assignments for the variables and verify that those assignments make the statement true.

Proving that any other problem in NP can be reduced to SAT is the tricky part. Suppose a problem is in NP. In that case, you must be able to make a nondeterministic Turing machine with internal states that it solves the problem. The idea behind the proof is to build a boolean expression that factors the inputs are passed through the machine, correctly and that the machine stops in an accepting state.

The boolean expression contains three kinds of variables that are named $T_{ijk}$, $Q_{ik}$ for various values of i, j, k, and q. The following list explains each variable's meaning: