![](bbox=[0.22, 0.1, 0.85, 0.42])

FIG. 4.7 Cycles and distances: (A) code example with a loop (based on code from the UTDSP benchmark repository [133], (B) intermediate three-address representation, and (C) DDG example.

respectively, while all other operations require 1 clock cycle to execute. The loops in this DDG show the loop-carried dependencies with a distance of 1.

In the presence of sequences of loops (each one consisting of a nested loop or a single loop) as in the example in Fig. 4.8A, it might be important to identify if there are data dependences between them. This information can be represented in a graph known as Loop Dependence Graph (LDG) as the one presented in Fig. 4.8B. The edges of the LDG represent information regarding the dependences. The LDG of Fig. 4.8B illustrates as edge labels the array variables responsible for the true dependences between the loop nests (represented as nodes).

In the example presented in Fig. 4.8, all loops in sequence impose data dependences between every two loops. For instance, the two loops in sequence have a data dependence as the first nested loop writes the hist array and the second loop reads elements of the hist array. The indirect indexing in the first nested loops prevents the compiler from determining that elements written at this point are used in the subsequent loop. The LDG can be seen as a special case of the Task Graph (see Section 4.4), where nodes are always loops and edges represent the data dependences between loops.