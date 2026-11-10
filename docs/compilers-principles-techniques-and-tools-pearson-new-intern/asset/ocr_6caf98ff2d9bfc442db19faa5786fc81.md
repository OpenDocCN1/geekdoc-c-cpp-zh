# ### 9.1. THE PRINCIPAL SOURCES OF OPTIMIZATION

![](bbox=[0.257, 0.18, 0.724, 0.575])

Figure 9.8: Strength reduction applied to $4 * j$ in block $B_3$

When processing loops, it is useful to work “inside-out”; that is, we shall start with the inner loops and proceed to progressively larger, surrounding loops. Thus, we shall see how this optimization applies to our quicksort example by beginning with one of the innermost loops: $B_3$ by itself. Note that the values of $j$ and $t4$ remain in lock step; every time the value of $j$ decreases by 1, the value of $t4$ decreases by 4, because $4 * j$ is assigned to $t4$. These variables, $j$ and $t4$, thus form a good example of a pair of induction variables.

When there are two or more induction variables in a loop, it may be possible to get rid of all but one. For the inner loop of $B_3$ in Fig. 9.5, we cannot get rid of either $j$ or $t4$ completely; $t4$ is used in $B_5$ and $j$ is used in $B_4$. However, we can illustrate reduction in strength and a part of the process of induction-variable elimination. Eventually, $j$ will be eliminated when the outer loop consisting of blocks $B_2$, $B_3$, $B_4$ and $B_5$ is considered.