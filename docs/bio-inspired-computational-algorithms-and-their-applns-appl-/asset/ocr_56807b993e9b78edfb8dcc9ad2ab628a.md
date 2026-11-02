![](bbox=[0.1, 0.08, 0.95, 0.53])

Fig. 3. Initial Population of Individuals GA (generation "0")

# 3.2 Production operators

The production operators are applied to each new generation. One or two individuals can be taken to produce new individuals for next generation by applying the transformations imposed by the operator. Both mutation operators and crossover will be implemented indistinctly. Both operators depend on a mutation probability and / or cross that is assigned to GA [7].

*A mutation operator is applied on nodes (documents), selecting an individual from the population using the tournament method, and then randomly select a pair of terminal nodes of that individual to mutate its terminal nodes, generating a new individual transposing the nodes that have been chosen (see figure 4).*

![](bbox=[0.2, 0.95, 0.9, 1.0])

Fig. 4. Basic mutation operator applied to terminal