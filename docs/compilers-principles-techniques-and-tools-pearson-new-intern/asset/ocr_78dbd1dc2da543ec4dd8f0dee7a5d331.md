# 11.3. **ITERATION SPACES**

![](bbox=[0.34, 0.177, 0.68, 0.396])

Figure 11.11: The iteration space of Example 11.6

# Iteration Spaces and Array-Accesses

In the code of Fig. 11.10, the iteration space is also the portion of the array $A$ that the code accesses. That sort of access, where the array indexes are also loop indexes in some order, is very common. However, we should not confuse the space of iterations, whose dimensions are loop indexes, with the data space. If we had used in Fig. 11.10 an array access like $Z[2*i,i+j]$ instead of $Z[j,i]$, the difference would have been apparent.

# 11.3.2 **Execution Order for Loop Nests**

A sequential execution of a loop nest proceeds through iterations in its iteration space in an ascending lexicographic order. A vector $i = [i_0,i_1,\ldots,i_n]$ is lexicographically less than another vector $i' = [i'_0,i'_1,\ldots,i'_{n'}]$, written $i \prec i'$, if and only if there exists an $m < \min(n,n')$ such that $[i_0,i_1,\ldots,i_m] = [i'_0,i'_1,\ldots,i'_m]$ and $i_{m+1} < i'_{m+1}$. Note that $m = 0$ is possible, and in fact common.

**Example 11.7:** With $i$ as the outer loop, the iterations in the loop nest in Example 11.6 are executed in the order shown in Fig. 11.12. □

# 11.3.3 **Matrix Formulation of Inequalities**

The iterations in a $d$-deep loop can be represented mathematically as

$$\{i \text{ in } \mathbb{Z}^d \mid Bi+b \geq 0\} \tag{11.1}$$