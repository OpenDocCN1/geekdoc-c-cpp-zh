$$\begin{aligned}
\mathrm{OUT}[B_k] &= f_{B}(\mathrm{IN}[B_k]), && \text{for all } B_k \\
\mathrm{OUT}[B_1] &\ge \mathrm{IN}[B_2] \\
\mathrm{OUT}_i[B_2] &\ge \mathrm{IN}_{i,1}[B_3], && 1 \le i \le 10 \\
\mathrm{OUT}_{i,j-1}[B_3] &\ge \mathrm{IN}_{i,j}[B_3], && 1 \le i \le 100,\ 2 \le j \le 10 \\
\mathrm{OUT}_{i,10}[B_3] &\ge \mathrm{IN}_i[B_4], && 1 \le i \le 100 \\
\mathrm{OUT}_{i-1}[B_4] &\ge \mathrm{IN}_i[B_2], && 1 \le i \le 100
\end{aligned}$$

Figure 9.61: Constraints satisfied on each iteration of the nested loops

the symbolic maps shown in Fig. 9.58 satisfy the constraints imposed by the transfer functions, listed in Fig. 9.61.

The first constraint says that the output map of a basic block is obtained by applying the block’s transfer function to the input map. The rest of the constraints say that the output map of a basic block must be greater than or equal to the input map of a successor block in the execution.

Note that our iterative data-flow algorithm cannot produce the above solution because it lacks the concept of expressing data-flow values in terms of the number of iterations executed. Region-based analysis can be used to find such solutions, as we shall see in the next section.

# 9.8.3 Region-Based Symbolic Analysis

We can extend the region-based analysis described in Section 9.7 to find expressions of variables in the $i$th iteration of a loop. A region-based symbolic analysis has a bottom-up pass and a top-down pass, like other region-based algorithms. The bottom-up pass summarizes the effect of a region with a transfer function that sends a symbolic map at the entry to an output symbolic map at the exit. In the top-down pass, values of symbolic maps are propagated down to the inner regions.

The difference lies in how we handle loops. In Section 9.7, the effect of a loop is summarized with a closure operator. Given a loop with body $f$, its closure $f^*$ is defined as an infinite meet of all possible numbers of applications of $f$. However, to find induction variables, we need to determine if a value of a variable is an affine function of the number of iterations executed so far. The symbolic map must be parameterized by the number of the iteration being executed. Furthermore, whenever we know the total number of iterations executed in a loop, we can use that number to find the values of induction variables after the loop. For instance, in Example 9.58, we claimed that $a$ has the value of $i$ after executing the $i$th iteration. Since the loop has 100 iterations, the value of $a$ must be 100 at the end of the loop.

In what follows, we first define the primitive operators: meet and composition of transfer functions for symbolic analysis. Then show how we use them to perform region-based analysis of induction variables.