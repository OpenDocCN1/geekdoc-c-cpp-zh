# ## 2.1 Multidimensional Knapsack Problem

As mentioned earlier, the MKP is a well-known nondeterministic-polynomial time-hard combinatorial optimization problem, with a wide range of applications (Tavares et al., 2008). The classical 0-1 knapsack problem is one of the most studied optimization and involves the selection of a subset of available items having maximum profit so that the total weight of the chosen subset does not exceed the knapsack capacity. The problem can be described as follows: given two sets of n items and m knapsack constraints (or resources), for each item j, a profit p_j is assigned, and for each constraint i, a consumption value r_ij is designated. The goal is to determine a set of items that maximizes the total profit, not exceeding the given constraint capacities c_i. Formally, this is stated as follows (Tavares et al., 2008):

Maximize  
∑_{j=1}^{n} p_j x_j ,  (1)

Subject to  
∑_{j=1}^{n} r_{ij} x_j ≤ c_i ,  i = 1,...,m  (2)

x_j ∈ {0, 1},  j = 1,...,n  (3)

With  
p_j > 0 , r_{ij} ≥ 0 and c_i ≥ 0  (4)

The knapsack constraint is represented by each of the m constraints described in Eq. (2). The decision variable is the binary vector x = (x_1,...,x_n). Each item j is mapped to a bit and when x_j = 1, the corresponding item is considered to be part of the solution. The special case of m = 1 is generally known as the Knapsack Problem or the Unidimensional Knapsack Problem.

For single constraint the problem is not strongly NP-hard and effective approximation algorithms have been developed for obtaining near-optimal solutions. A review of the single knapsack problem and heuristic algorithms is given by Martello and Toth (Martello & Toth, 1990). Exact techniques and exhaustive search algorithms, such as branch-and-bound, are only of practical use in solving MKP instances of small size since they are, in general, too time-consuming (e.g., instances with 100 items or less, and depending on the constraints).

# ## 2.2 Evolutionary approach for the MKP

In a resolution of specific problems that implements an Evolutionary Algorithm, as for example, a simple Genetic Algorithm (GA), it is necessary the definition of five components (Agape et al., 1997). The first component is the genotype or a genetic representation of the potential problem (individual representation scheme). The second is a method for creating an initial population of solutions. The third is a function verifying the fitness of the solution (objective function or fitness function). The fourth are genetic operators and the fifth are some