# 9.7.5  An Algorithm for Region-Based Analysis

The following algorithm solves a forward data-flow-analysis problem on a reducible flow graph, according to some framework that satisfies the assumptions of Section 9.7.4. Recall that $f_{R,\mathrm{IN}[R']}$ and $f_{R,\mathrm{OUT}[B]}$ refer to transfer functions that transform data-flow values at the entry to region $R$ into the correct value at the entry of subregion $R'$ and the exit of the exit block $B$, respectively.

**Algorithm 9.53:** Region-based analysis.

**INPUT:** A data-flow framework with the properties outlined in Section 9.7.4 and a reducible flow graph $G$.

**OUTPUT:** Data-flow values $\mathrm{IN}[B]$ for each block $B$ of $G$.

**METHOD:**

+   1. Use Algorithm 9.52 to construct the bottom-up sequence of regions of $G$, say $R_1, R_2, \ldots, R_n$, where $R_n$ is the topmost region.
+   
+   2. Perform the bottom-up analysis to compute the transfer functions summarizing the effect of executing a region. For each region $R_1, R_2, \ldots, R_n$, in the bottom-up order, do the following:
+      - (a) If $R$ is a leaf region corresponding to block $B$, let $f_{R,\mathrm{IN}[B]} = I$, and $f_{R,\mathrm{OUT}[B]} = f_B$, the transfer function associated with block $B$.
+      - (b) If $R$ is a body region, perform the computation of Fig. 9.50(a).
+      - (c) If $R$ is a loop region, perform the computation of Fig. 9.50(b).
+   
+   3. Perform the top-down pass to find the data-flow values at the beginning of each region.
+      - (a) $\mathrm{IN}[R_n] = \mathrm{IN}[\mathrm{ENTRY}]$.
+      - (b) For each region $R$ in $\{R_1, \ldots, R_{n-1}\}$, in the top-down order, compute $\mathrm{IN}[R] = f_{R',\mathrm{IN}[R]}(\mathrm{IN}[R'])$, where $R'$ is the immediate enclosing region of $R$.

Let us first look at the details of how the bottom-up analysis works. In line (1) of Fig. 9.50(a) we visit the subregions of a body region, in some topological order. Line (2) computes the transfer function representing all the possible paths from the header of $R$ to the header of $S$; then in lines (3) and (4) we compute the transfer functions representing all the paths from the header of $R$ to the exits of $R$ — that is, to the exits of all blocks that have successors outside $S$. Notice that all the predecessor blocks $B'$ in $R$ must be in regions that precede $S$ in the topological order constructed at line (1). Thus, $f_{R,\mathrm{OUT}[B']}$ will have been computed already, in line (4) of a previous iteration through the outer loop.