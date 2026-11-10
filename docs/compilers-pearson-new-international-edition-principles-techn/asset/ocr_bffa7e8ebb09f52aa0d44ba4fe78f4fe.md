![](bbox=[0.235, 0.177, 0.765, 0.522])

Figure 8.18: Code sequence using global register assignment

# ### 8.8.3 Register Assignment for Outer Loops

Having assigned registers and generated code for inner loops, we may apply the same idea to progressively larger enclosing loops. If an outer loop $L_1$ contains an inner loop $L_2$, the names allocated registers in $L_2$ need not be allocated registers in $L_1-L_2$. However, if we choose to allocate $x$ a register in $L_2$ but not $L_1$, we must load $x$ on entry to $L_2$ and store $x$ on exit from $L_2$. We leave as an exercise the derivation of a criterion for selecting names to be allocated registers in an outer loop $L$, given that choices have already been made for all loops nested within $L$.

# ### 8.8.4 Register Allocation by Graph Coloring

When a register is needed for a computation but all available registers are in use, the contents of one of the used registers must be stored (*spilled*) into a memory location in order to free up a register. Graph coloring is a simple, systematic technique for allocating registers and managing register spills.

In the method, two passes are used. In the first, target-machine instructions are selected as though there are an infinite number of symbolic registers; in effect, names used in the intermediate code become names of registers and