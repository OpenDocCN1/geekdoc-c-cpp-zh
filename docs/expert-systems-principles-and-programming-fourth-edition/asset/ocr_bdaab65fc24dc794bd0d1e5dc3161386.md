It is convenient to represent a stochastic process in the form of a transition matrix. For the simple case of two states, S1 and S2, the transition matrix is:

| | S1 | S2 |
|---|---|---|
| S1 | P11 | P12 |
| S2 | P21 | P22 |

where Pmn is the probability of a transition from state m to state n.

As an example, assume that 10% of all people who now use Brand X drives will buy another Brand X drive when needed. Also, 60% of the people who don't use Brand X now will buy Brand X when they need a new drive (the only good thing about Brand X is their advertising). Over a long period of time, how many people will use Brand X?

The transition matrix, T, is:

| | X | X' |
|---|---|---|
| X | 0.1 | 0.9 |
| X' | 0.6 | 0.4 |

where the sum of each row must add up to 1. A vector whose components are not negative and add up to 1 is called a probability vector. Each row of T is a probability vector. One way of interpreting the transition matrix is in terms of a state diagram as shown in Figure 4.13. Notice that there is a 0.1 probability of remaining in state X, a 0.4 probability of remaining in state X', a 0.9 probability of going from X to X', and a 0.6 probability of going from X' to X.

Suppose initially that 80% of the people use Brand X. Figure 4.14(a) shows a probability tree for a few state transitions, where the states are labeled by state number and drive owned. Notice how the tree is starting to grow. If there were 10 transitions, the tree would have 2^10 = 1024 branches. An alternate way of drawing the tree as a lattice is shown in Figure 4.14b. The advantage of the lattice representation is that it doesn't need as many links connecting the states.

Figure 4.13 State Diagram Interpretation of a Transition Matrix

![](bbox=[0.12, 0.79, 0.92, 0.93])