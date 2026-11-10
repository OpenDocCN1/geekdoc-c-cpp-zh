# 11.7.1 Evolutionary Algorithms Parameters

The term evolutionary computation or evolutionary algorithms include the domains of genetic algorithms (GA), evolution strategies, evolutionary programming, and genetic programming. Evolutionary algorithms have a number of parameters, procedures or operators that must be specified in order to define a particular EA. The most important parameters of EA are

+   - Representation
+   - Fitness function
+   - Population
+   - Parent selection mechanism
+   - Variation operators, recombination and mutation
+   - Reproduction operator

The initialization procedure and a termination condition must be defined along with the above parameters.

# 11.7.2 Solution Representation

The method of representing solutions/individuals in evolutionary computation methods is known as representation. This can encode appearance, behavior, and physical qualities of individuals. An expressive and evolvable design of a representation is a hard problem in evolutionary computation. The conflict in genetic representations in one of the major criteria drawing a line between known classes of evolutionary computation.

Evolutionary algorithm more commonly uses linear binary representations among which the most typical representation is an array of bits. Arrays of other types of data and structures can also be used in a similar manner. The primary attribute that makes these genetic representations favorable is that their sections are well co-ordinated due to their fixed size. Due to this well co-ordinated arrangement simple crossover operation is easily facilitated. Evolutionary algorithms are capable of operating on variable length representations also, but crossover implementation is more complex in this case.

Human-based genetic algorithm (HBGA) provides a mode to avoid solving hard representation problems by outsourcing all genetic operators to outside agents (in this case, humans). In this case, the algorithm need not be aware of a particular genetic representation used for any solution. Some of the common genetic representations are