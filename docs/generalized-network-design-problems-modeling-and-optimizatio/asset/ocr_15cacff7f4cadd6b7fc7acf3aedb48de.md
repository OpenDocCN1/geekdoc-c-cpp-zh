a candidate solution for the simulated annealing in the neighborhood of the current solution. The next figure shows a current solution and a modified solution.

![](bbox=[0.18, 0.15, 0.82, 0.3])

Figure 2.5. A current solution and a modified solution of the GMSTP.

In the previous figure, we considered a graph G whose nodes are partitioned into 6 clusters and a current solution T. Randomly selecting a subtree U of T (for example by discarding the edges connecting nodes from clusters V4 with V5 and V2 with V5) we apply the local greedy algorithm, in order to obtain the best modified solution in the neighborhood of T, given the subtree U.

# Implementation details and computational results

Our computational experiments were performed on a Dual Intel Pentium III Processor – 1000 MHz computer with 512 MB RAM. The procedures for the combined Simulated Annealing and local greedy scheme were written in Java.

After some preliminary tests, we have chosen the following cooling schedule: we start with a temperature T0 = 100, the cooling rate r = 0.95 will be used to reduce the temperature in each step, and in each stage L = 30 moves are evaluated.

We considered an undirected graph G = (V, E) having n nodes, partitioned into m clusters, such that each cluster contains the same number of nodes. Edges are defined between all the nodes from different clusters and the costs of the edges were randomly generated in the interval [1,100]. For each type of instance (n, m) we randomly generated five different problems, i.e. with different costs of the edges. The instances that we used are similar to those considered by Myung [128] and Feremans [37].

In the next table, we compare the computational results obtained for solving the GMSTP, using the combined simulated annealing, with a local greedy algorithm, with the computational results given by Feremans [37] and Pop [142, 150].

The first two columns in the table list the size of the problem as the number of clusters (m) and the number of nodes (n). The next two columns describe the simulated annealing procedure and contain the upper bounds, obtained as a percentage of the optimal value of the GMSTP (UB/OPT), and the computation times (CPU) in seconds for solving the GMSTP. The last columns contain the lower bounds as a percentage of the optimal value of the GMSTP problem (UB/OPT), the computation times (CPU) in seconds for solving the GMSTP with the rooting procedure (see [142, 150]), the