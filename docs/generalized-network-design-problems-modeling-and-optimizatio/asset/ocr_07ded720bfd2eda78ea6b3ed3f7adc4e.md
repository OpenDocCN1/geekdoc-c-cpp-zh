![](bbox=[0.26, 0.1, 0.73, 0.38])

Figure 5.7. An example of a feasible solution of the GVRP.

Several collections of generalized routes correspond to the given collection of global routes, the one represented in figure 1 consists in the following nodes: 3 ∈ V1, 6 ∈ V2, 7 ∈ V3, 10 ∈ V4, 16 ∈ V5 and 18 ∈ V6. The best w.r.t cost minimization collection of generalized routes can be determined using the approach described at the beginning of this section.

We can see that our described representation has variable length and allows empty routes by simply placing two route splitters together, without clients between them. Some routes in the chromosome may cause the vehicle to exceed its capacity. When this happens, in order to guarantee that the interpretation is always a valid candidate solution, we modify any route that exceeds the vehicle capacity by splitting it in several ones.

# The fitness value

The fitness function is defined over the genetic representation and measures the quality of the represented solution. In our case, the fitness value of a feasible solution, i.e. a collection of global routes, is given by the cost of the best corresponding collection of generalized routes (w.r.t. cost minimization), obtained by constructing the layered network and determined by solving a given number of shortest path problems.

# Initial population

The construction of the initial population is of great importance to the performance of GA, since it contains most of the material of which the final best solution is made. Experiments were carried out with a randomly generated initial population and with an initial population of structured solutions. In order to generate the population of