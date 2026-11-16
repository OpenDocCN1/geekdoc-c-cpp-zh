# Mutation

In our genetic algorithm, we use the following random mutation operator, called the inter-route mutation operator, which is a swap operator. It picks two random locations in the solution vector and swaps their values.

Let the parent solution be (6 8 1 | 0 2 7 | 0 5 4 3). The inter-route mutation operator picks two random clusters, for example V5 and V3 and swaps their values obtaining the new chromosome: (6 5 1 | 0 2 7 | 0 8 4 3).

# Selection

Selection is the stage a genetic algorithm in which individuals are chosen from a population for later breeding (crossover or mutation). The selection process is deterministic.

In our algorithm we investigated and used the properties of (μ, λ), selection, where μ parent produce λ (λ > μ) and only the offspring undergo selection. In other words, the lifetime of every individual is limited to only one generation. The limited life span allows us to forget the inappropriate internal parameter settings. This may lead to short periods of recession, but it avoids long stagnation phases due to unadapted strategy parameters.

# Genetic parameters

The genetic parameters are very important for the success of the algorithm, equally important as the other aspects, such as the representation of the individuals, the initial population and the genetic operators. The most important parameters are the population size μ, set to 10 times the number of clusters, the intermediate population size λ, chosen ten times the size of the population, λ = 10 · μ and the mutation probability, set at 5%. The number of epochs used in our algorithm was set to 2000.

# Local search improvement

We here present five routing plan improvements, used in our local search procedure. Two of them operate within the routes (the intra-route 2-opt and the 3-opt operators) and the rest operate between routes and are called relocate, exchange and cross operators. These last operators are extensions of the operators described by van Breedam [202] in the case of the classical VRP.

+   1. 2-opt. The two-opt procedure is used for improving single vehicle routes, and consists of eliminating two arcs and reconnecting the two resulting paths in a different way to obtain a new route. In Figure 5.8, the two-opt operator is shown and as we can see there are different ways to reconnect the paths that yield a different tour. Among all pairs of edges whose 2-opt exchange decreases the length, we choose the pair that gives the shortest tour. This procedure is then iterated until no such pair of edges found.