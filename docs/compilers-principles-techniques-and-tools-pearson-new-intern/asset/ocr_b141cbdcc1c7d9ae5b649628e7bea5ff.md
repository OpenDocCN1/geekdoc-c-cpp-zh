# 9.7. **REGION-BASED ANALYSIS**

+   3. $E$ is the set of all the control flow edges between nodes $n_1$ and $n_2$ in $N$, except (possibly) for some that enter $n_1$.

**Example 9.50:** Clearly a natural loop is a region, but a region does not necessarily have a back edge and need not contain any cycles. For example, in Fig. 9.47, nodes $B_1$, $B_2$, and $B_3$, together with the edge $B_1 \to B_2$, form a region; so do nodes $B_1$, $B_2$, and $B_3$ with edges $B_1 \to B_2$, $B_2 \to B_3$, and $B_1 \to B_3$.

However, the subgraph with nodes $B_2$ and $B_3$ with edge $B_2 \to B_3$ does not form a region, because control may enter the subgraph at both nodes $B_2$ and $B_3$. More precisely, neither $B_2$ nor $B_3$ dominates the other, so condition (1) for a region is violated. Even if we picked, say, $B_2$ to be the “header,” we would violate condition (2), since we can reach $B_3$ from $B_1$ without going through $B_2$, and $B_1$ is not in the “region.”

![](bbox=[0.439, 0.401, 0.555, 0.532])

Figure 9.47: Examples of regions

# 9.7.2  Region Hierarchies for Reducible Flow Graphs

In what follows, we shall assume the flow graph is reducible. If occasionally we must deal with nonreducible flow graphs, then we can use a technique called “node splitting” that will be discussed in Section 9.7.6.

To construct a hierarchy of regions, we identify the natural loops. Recall from Section 9.6.6 that in a reducible flow graph, any two natural loops are either disjoint or one is nested within the other. The process of “parsing” a reducible flow graph into its hierarchy of loops begins with every block as a region by itself. We call these regions *leaf regions*. Then, we order the natural loops from the inside out, i.e., starting with the innermost loops. To process a loop, we replace the entire loop by a node in two steps:

+   1. First, the *body* of the loop $L$ (all nodes and edges except the back edges to the header) is replaced by a node representing a region $R$. Edges to the header of $L$ now enter the node for $R$. An edge from any exit of loop $L$ is replaced by an edge from $R$ to the same destination. However, if the edge is a back edge, then it becomes a loop on $R$. We call $R$ a *body region*.