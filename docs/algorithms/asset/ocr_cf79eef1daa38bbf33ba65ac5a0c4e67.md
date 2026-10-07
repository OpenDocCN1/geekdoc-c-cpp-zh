# 222

# Exercises

constraints for each type of gate:

![](bbox=[0.075, 0.149, 0.673, 0.287])

These constraints force all the gates to take the right values—0 for false, and 1 for true. We don't need to maximize or minimize anything, and we can read the answer from the variable $x_0$ corresponding to the output gate.

This is a straightforward reduction to linear programming, from a problem that may seem very interesting at first. However, the CIRCUIT value problem is in a sense the most general problem solvable in polynomial time! After, any algorithm will eventually run on a computer, and the computer is ultimately a Boolean combination implemented on a chip. If the algorithm runs in polynomial time, it can be rendered as a Boolean circuit consisting of polynomially many copies of the computer's, one per unit of time, with the values of the gates in one layer used to compute the values for the next. The fact that CIRCUIT reduces to linear programming means that all problems can be solved in polynomial time do!

In our next topic, NP-completeness, we will see that many hard problems reduce, much the same way, to integer programming; linear programming's difficult.

Another parting thought: by what means can the circuit evaluation be solved? Let's think—a circuit is a dag. And what algorithmic technique is most appropriate for solving problems on dags? That's right: dynamic programming! Together with linear programming, the world's most general algorithmic techniques.

# Exercises

7.1. Consider the following linear program.

```
maximize $5x + 3y$
$5x - 2y \geq 0$
$x + y \leq 7$
$x \leq 5$
$x \geq 0$
$y \geq 0$
```

Plot the feasible region and identify the optimal solution.