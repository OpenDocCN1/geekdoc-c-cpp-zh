+   2. In the symbol table, set $x$ to "not live" and "no next use."
+   3. In the symbol table, set $y$ and $z$ to "live" and the next uses of $y$ and $z$ to $i$.

Here we have used $+$ as a symbol representing any operator. If the three-address statement $i$ is of the form $x = + y$ or $x = y$, the steps are the same as above, ignoring $z$. Note that the order of steps (2) and (3) may not be interchanged because $x$ may be $y$ or $z$. $\square$

# 8.4.3 Flow Graphs

Once an intermediate-code program is partitioned into basic blocks, we represent the flow of control between them by a flow graph. The nodes of the flow graph are the basic blocks. There is an edge from block $B$ to block $C$ if and only if it is possible for the first instruction in block $C$ to immediately follow the last instruction in block $B$. There are two ways that such an edge could be justified:

+   - There is a conditional or unconditional jump from the end of $B$ to the beginning of $C$.
+   - $C$ immediately follows $B$ in the original order of the three-address instructions, and $B$ does not end in an unconditional jump.

We say that $B$ is a *predecessor* of $C$, and $C$ is a *successor* of $B$.

Often we add two nodes, called the *entry* and *exit*, that do not correspond to executable intermediate instructions. There is an edge from the entry to the first executable node of the flow graph, that is, to the basic block that comes from the first instruction of the intermediate code. There is an edge to the exit from any basic block that contains an instruction that could be the last executed instruction of the program. If the final instruction of the program is not an unconditional jump, then the block containing the final instruction of the program is one predecessor of the exit, but so is any basic block that has a jump to code that is not part of the program.

**Example 8.8:** The set of basic blocks constructed in Example 8.6 yields the flow graph of Fig. 8.9. The entry points to basic block $B_1$, since $B_1$ contains the first instruction of the program. The only successor of $B_1$ is $B_2$, because $B_1$ does not end in an unconditional jump, and the leader of $B_2$ immediately follows the end of $B_1$.

Block $B_3$ has two successors. One is itself, because the leader of $B_3$, instruction 3, is the target of the conditional jump at the end of $B_3$, instruction 9. The other successor is $B_4$, because control can fall through the conditional jump at the end of $B_3$ and next enter the leader of $B_4$.

Only $B_6$ points to the exit of the flow graph, since the only way to get to code that follows the program from which we constructed the flow graph is to fall through the conditional jump that ends $B_6$. $\square$