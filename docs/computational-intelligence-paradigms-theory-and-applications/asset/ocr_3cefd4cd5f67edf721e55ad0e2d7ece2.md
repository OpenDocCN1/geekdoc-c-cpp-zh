# ## Strategy Variables

The real-valued s(i) variables or mean step sizes determine the mutability of the x(i). They represent the standard deviation (0, ... σi) of s(i)) gaussian distribution (GD) being added to each x(i) as an undirected mutation. If the expectancy value is 0, then the parents will produce offspring similar to themselves. In order to make a doubling and a halving of a step size equally probable, the s(i) mutate log-normally, distributed, i.e., exp(GD), from generation to generation. These step sizes hide the internal model the population has made of its environment, i.e., a self-adaptation of the step sizes has replaced the exogenous control of the (1+1) ES.

This concept works because selection sooner or later prefers those individuals having built a good model of the objective function, thus producing better offspring. Hence, learning takes place on two levels: (1) at the genotypic, i.e., the object and strategy variable level and (2) at the phenotypic level, i.e., the fitness level.

Depending on an individual's x(i), the resulting objective function value f(x), where x denotes the vector of objective variables, serves as the phenotype (fitness) in the selection step. In a plus strategy, the m best of all (m+l) individuals survive to become the parents of the next generation. Using the comma variant, selection takes place only among the l offspring. The next strategy is more naturalistic and hence more eminent, since no individual may survive evermore, which can be done by using the plus variant. The comma strategy performs better than conventional optimization algorithms. An everlasting adaptation of the step sizes can occur only if the highly fit individuals are forgotten. By this process long stagnation phases due to misadapted sizes can be avoided. These individuals have established an internal model that is no more appropriate for additional progress, and therefore it is better to be discarded.

The convergence of the evolutionary strategy can be obtained by choosing a suitable ratio of m/l. For a faster convergence the preferred ratio of m/l should be very small around (5,100). To find an optimal solution usually the preferred ratio is chosen around (15,100).

The following agents greatly influence self-adaptation within ESs:

# ## Randomness

Mutation cannot be designed as a pure random process since the child would be completely independent of its parents.