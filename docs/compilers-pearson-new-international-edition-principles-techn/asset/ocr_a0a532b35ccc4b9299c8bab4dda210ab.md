pointer to the leader in the array of three-address instructions, together with a count of the number of instructions or a second pointer to the last instruction. However, since we may be changing the number of instructions in a basic block frequently, it is likely to be more efficient to create a linked list of instructions for each basic block.

# ### 8.4.5 Loops

Programming-language constructs like while-statements, do-while-statements, and for-statements naturally give rise to loops in programs. Since virtually every program spends most of its time in executing its loops, it is especially important for a compiler to generate good code for loops. Many code transformations depend upon the identification of “loops” in a flow graph. We say that a set of nodes $L$ in a flow graph is a loop if $L$ contains a node called the loop entry, such that:

+   1. $e$ is not ENTRY, the entry of the entire flow graph.
+   2. No node in $L$ besides $e$ has a predecessor outside $L$. That is, every path from ENTRY to any node in $L$ goes through $e$.
+   3. Every node in $L$ has a nonempty path, completely within $L$, to $e$.

**Example 8.9:** The flow graph of Fig. 8.9 has three loops:

+   1. $B_3$ by itself.
+   2. $B_6$ by itself.
+   3. {$B_2, B_3, B_4$}.

The first two are single nodes with an edge to the node itself. For instance, $B_3$ forms a loop with $B_3$ as its entry. Note that the last requirement for a loop is that there be a nonempty path from $B_3$ to itself. Thus, a single node like $B_2$, which does not have an edge $B_2 \to B_2$, is not a loop, since there is no nonempty path from $B_2$ to itself within {$B_2$}.

The third loop, $L = \{B_2, B_3, B_4\}$, has $B_2$ as its loop entry. Note that among these three nodes, only $B_2$ has a predecessor, $B_1$, that is not in $L$. Further, each of the three nodes has a nonempty path to $B_2$ staying within $L$. For instance, $B_2$ has the path $B_2 \to B_3 \to B_4 \to B_2$.

# ### 8.4.6 Exercises for Section 8.4

**Exercise 8.4.1:** Figure 8.10 is a simple matrix-multiplication program.

+   a) Translate the program into three-address statements of the type we have been using in this section. Assume the matrix entries are numbers that require 8 bytes, and that matrices are stored in row-major order.