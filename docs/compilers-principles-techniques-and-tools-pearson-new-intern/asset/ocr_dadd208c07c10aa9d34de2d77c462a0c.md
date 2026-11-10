transfer function for $P$, $f_P$, to be the composition of $f_{B_1}, f_{B_2} \cdots, f_{B_{n-1}}$. Note that $f_{B_n}$ is not part of the composition, reflecting the fact that this path is taken to reach the beginning of block $B_n$, not its end. The data-flow value created by executing this path is thus $f_P(v_{\text{ENTRY}})$, where $v_{\text{ENTRY}}$ is the result of the constant transfer function representing the initial node ENTRY. The ideal result for block $B$ is thus

$$\operatorname{IDEAL}[B] = \bigwedge_{P,\ \text{a possible path from ENTRY to } B} f_P(v_{\text{ENTRY}}).$$

We claim that, in terms of the lattice-theoretic partial order $\leq$ for the framework in question,

+   - Any answer that is greater than IDEAL is incorrect.
+   - Any value smaller than or equal to the ideal is conservative, i.e., safe.

Intuitively, the closer the value to the ideal the more precise it is.⁸ To see why solutions must be $\leq$ the ideal solution, note that any solution greater than IDEAL for any block could be obtained by ignoring some execution path that the program could take, and we cannot be sure that there is not some effect along that path to invalidate any program improvement we might make based on the greater solution. Conversely, any solution less than IDEAL can be viewed as including certain paths that either do not exist in the flow graph, or that exist but that the program can never follow. This lesser solution will allow only transformations that are correct for all possible executions of the program, but may forbid some transformations that IDEAL would permit.

# The Meet-Over-Paths Solution

However, as discussed in Section 9.1, finding all possible execution paths is undecidable. We must therefore approximate. In the data-flow abstraction, we assume that every path in the flow graph can be taken. Thus, we can define the meet-over-paths solution for $B$ to be

$$\operatorname{MOP}[B] = \bigwedge_{P,\ \text{a path from ENTRY to } B} f_P(v_{\text{ENTRY}}).$$

Note that, as for IDEAL, the solution MOP[$B$] gives values for IN[$B$] in forward-flow frameworks. If we were to consider backward-flow frameworks, then we would think of MOP[$B$] as a value for OUT[$B$].

The paths considered in the MOP solution are a superset of all the paths that are possibly executed. Thus, the MOP solution meets together not only the data-flow values of all the executable paths, but also additional values associated

⁸Note that in forward problems, the value IDEAL[$B$] is what we would like IN[$B$] to be. In backward problems, which we do not discuss here, we would define IDEAL[$B$] to be the ideal value of OUT[$B$].