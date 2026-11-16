A probability vector S is a steady-state matrix for the transition matrix T if:

+   (1) S = S T

If T is a regular transition matrix, which has some power with only positive elements, then a unique steady-state S exists. The fact that the transition matrix elements are positive means that at some time, it is possible to be in any state no matter what the initial state had been. That is, every state is potentially accessible.

A Markov chain process is defined as having the following characteristics:

+   (1) The process has a finite number of possible states.
+   (2) The process can be in one and only one state at a time.
+   (3) The process moves or steps successively from one state to another over time.
+   (4) The probability of a move depends only on the immediately preceding state.

For example, given a finite set of states {A,B,C,D,E,F,G,H,I}, then if the next that the process goes to after H is I, the conditional probability is the following:

P(I | H) = P(I | H ∩ G ∩ F ∩ E ∩ D ∩ C ∩ B ∩ A)

Notice how the lattice diagram of Figure 4.14 (b) resembles a chain.

The disk drive case is a Markov chain process and the steady-state matrix can be found by applying equation (1). Assume some arbitrary vector S with components X and Y and apply equation (1) as follows:

[X Y] [0.1 0.9; 0.6 0.4] = [X Y]

Multiplying the left-hand side and setting its elements equal to the corresponding elements on the right-hand side gives:

0.1 X + 0.6 Y = X
0.9 X + 0.4 Y = Y

which is a dependent system of equations. Solving for X in terms of Y gives:

X = 0.6 / 0.9 Y = 2/3 Y

To completely solve for X and Y, we'll make use of the fact that the sum of the probabilities equals 1. That is,