mutation rate. Typically, but not always, mutation will flip a single bit. In fact, GenJam's mutation operators, on the other hand, are more complex than flipping a bit. They adopt several standard melodic development techniques, such as transposition, retrograde, rotation, inversion, sorting, and retrograde-inversion. Because these operators are all musically meaningful, they operate at the event level rather than on individual bits (Biles, 2001).

# ### 4.4 Replacement

After the process of selection, crossover, and mutation, the current population is replaced by the new population. Those successful individuals of the each generation are more likely to survive in the next generation and those unsuccessful individuals are less likely to survive. In our GA, we use the incremental replacement method (See Beasley et al., 1993), i.e., only the new individuals whose fitness values are better than those of the current will be replaced. Thus, the individuals with the best fitness are always in the population.

# ### 4.5 Termination

In general, a genetic algorithm is terminated after a specified number of generations or when fitness values have converged. Our GA terminates when there has been no improvement in the best solution found for 100 iterations.

# ## 5. Hybrid Benders/Genetic algorithm

The basic idea of Benders' partitioning algorithm for mixed-integer linear problems is to decompose the original problem into a pure integer master problem and one or more subproblems in the continuous variables, and then to iterate between these two problems. If the objective function value of the optimal solution to the master problem is equal to that of the subproblem, then the algorithm terminates with the optimal solution of the original mixed-integer problem. Otherwise, we add constraints, termed Benders' cuts, one at a time to the master problem, and solve it repeatedly until the termination criteria are met. A major difficulty with this decomposition lies in the solution of the master problem, which is a “hard” problem, costly to compute.

For the addressed CPL problem, however, the constraints are explicit only in the subproblem and the master problem is free of explicit constraints. Thus, the master problem is more amenable to solution by GA.

Lai et al. (2010) introduced a hybrid Benders/Genetic algorithm which is a variation of Benders' algorithm that uses a genetic algorithm to obtain “good” subproblem solutions to the master problem. Lai and Sohn (2011) conducted a study applying the hybrid Benders/Genetic algorithm to the vehicle routing problem. Below is a detailed description of the hybrid algorithm and it is illustrated in Fig. 1 as well.

+   1. **Initialization.** We initialize the iteration counter k to zero, select initial trial values for the vector of binary variables Y which selects the plants to be opened.
+   2. **Primal Subsystem.** We evaluate the value of r(Y) by solving a transportation linear programming problem whose feasible region is independent of Y.