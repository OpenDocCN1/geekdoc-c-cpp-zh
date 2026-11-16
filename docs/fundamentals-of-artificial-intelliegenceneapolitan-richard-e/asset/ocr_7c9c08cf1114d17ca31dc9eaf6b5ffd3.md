and therefore high edge preservation and possible early convergence to a low-quality solution. To increase exploration, the first half of the new tour can be taken from the union graph and the second half from the complete graph. In initial investigations, this version performed much better than the one that took as many edges as possible from the union graph. This is the version that was used in the evaluation discussed next.

NNA and NNX are very similar to Kruskal's algorithm for the Minimum Spanning Tree Problem (see, e.g., [Neapolitan and Naimipour, 2010]), and like that algorithm take \(\theta(n^2 \log n)\) and \(\theta(m \log m)\) time, where \(n\) is the number of vertices and \(m\) is the number of edges.

# 9.2.3.4 Evaluation

As is the case for many heuristic algorithms, genetic algorithms do not have provably correct properties. Therefore, we evaluate them by investigating their performance on a number of instances of the problem. Stral et al. [2010] did this as follows for NNX and GEX.

First, they obtained 10 instances of TSP from the TSPLIB, which represent distances between real cities and in which the distance is symmetric (the same in both directions). The largest instance had \(n\) (the number of cities) = 226. They investigated versions of NNX and GEX using no mutations, mutations M1 (discussed above), and mutations M2 (discussed above). Furthermore, they tried initializing the first population at random (R) and initializing using a hybrid technique (H) based on nearest neighbor and greedy edge heuristics. For each combination of mutation type and initialization type, they ran each of the algorithms 30 times on each of the 10 instances, making a total of 300 runs. The algorithm was coded in ANSIC and ran on a Pentium IV 1600 MHz machine with 256 MB RAM running RedHat Linux 8.0.

Table 9.5 shows the averages over all 300 runs. The headings in that table denote the following:

+   - Algorithm: The algorithm used.
+   - Mutation: The type of mutation used. “No M” denotes no mutations.
+   - Int. Pop.: Whether the population was initialized at random (R) or using hybrid initialization (H).
+   - Dev: Percent deviation of the final best solution from the optimal solution.
+   - #Gen: Number of generations until convergence.
+   - Time: Time in seconds until convergence.

We see from Table 9.5 that NNX performed much better than GEX, that mutation M2 performed the best of the mutations, and that hybrid initialization did not result in much better performance than random initialization. The researchers then investigated whether using NNX with various percentage usage