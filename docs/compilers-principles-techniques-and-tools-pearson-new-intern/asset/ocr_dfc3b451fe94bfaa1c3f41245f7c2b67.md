says

$$\operatorname{OUT}[B] = f_B(\operatorname{IN}[B]).$$

Since $\operatorname{IN}[B]^{k+1} \leq \operatorname{IN}[B]^k$, we have $\operatorname{OUT}[B]^{k+1} \leq \operatorname{OUT}[B]^k$ by monotonicity.

Note that every change observed for values of $\operatorname{IN}[B]$ and $\operatorname{OUT}[B]$ is necessary to satisfy the equation. The meet operators return the greatest lower bound of their inputs, and the transfer functions return the only solution that is consistent with the block itself and its given input. Thus, if the iterative algorithm terminates, the result must have values that are at least as great as the corresponding values in any other solution; that is, the result of Algorithm 9.25 is the MFP of the equations.

Finally, consider the third point, where the data-flow framework has finite height. Since the values of every $\operatorname{IN}[B]$ and $\operatorname{OUT}[B]$ decrease with each change, and the algorithm stops if at some round nothing changes, the algorithm is guaranteed to converge after a number of rounds no greater than the product of the height of the framework and the number of nodes of the flow graph.

# 9.3.4 Meaning of a Data-Flow Solution

We now know that the solution found using the iterative algorithm is the maximum fixedpoint, but what does the result represent from a program-semantics point of view? To understand the solution of a data-flow framework $(D, F, V, \wedge)$, let us first describe what an ideal solution to the framework would be. We show that the ideal cannot be obtained in general, but that Algorithm 9.25 approximates the ideal conservatively.

# The Ideal Solution

Without loss of generality, we shall assume for now that the data-flow framework of interest is a forward-flowing problem. Consider the entry point of a basic block $B$. The ideal solution begins by finding all the possible execution paths leading from the program entry to the beginning of $B$. A path is “possible” only if there is some computation of the program that follows exactly that path. The ideal solution would then compute the data-flow value at the end of each possible path and apply the meet operator to these values to find their greatest lower bound. Then no execution of the program can produce a smaller value for that program point. In addition, the bound is tight; there is no greater data-flow value that is a glb for the value computed along every possible path to $B$ in the flow graph.

We now try to define the ideal solution more formally. For each block $B$ in a flow graph, let $f_B$ be the transfer function for $B$. Consider any path

$$P = \operatorname{ENTRY} \to B_1 \to B_2 \to \cdots \to B_{k-1} \to B_k$$

from the initial node $\operatorname{ENTRY}$ to some block $B_k$. The program path may have cycles, so one basic block may appear several times on the path $P$. Define the