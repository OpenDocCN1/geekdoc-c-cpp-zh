# # Performance Study of Cultural Algorithms
Based on Genetic Algorithm with
Single and Multi Population for the MKP

Deam James Azevedo da Silva¹, Otávio Noura Teixeira²  
and Roberto Célio Limão de Oliveira¹  
¹Universidade Federal do Pará (UFPA),  
²Centro Universitário do Estado do Pará (CESUPA)  
Brazil

# ## 1. Introduction

Evolutionary Computation (EC) is inspired from by evolution that explores the solution space by gene inheritance, mutation, and selection of the fittest candidate solutions. Since their inception in the 1960s, Evolutionary Computation has been used in various hard and complex optimization problems in search and optimization such as: combinatorial optimization, functions optimization with and without constraints, engineering problems and others (Adeyemo, 2011). This success is in part due to the unbiased nature of their operations, which can still perform well in situations with little or no domain knowledge (Reynolds, 1999). The basic EC framework consists of fairly simple steps like definition of encoding scheme, population generation method, objective function, selection strategy, crossover and mutation (Ahmed & Youas, 2011). In addition, the same procedures utilized by EC can be applied to diverse problems with relatively little reprogramming.

Cultural Algorithms (CAs), as well as Genetic Algorithm (GA), are evolutionary models that are frequently employed in optimization problems. Cultural Algorithms (CAs) are based on knowledge of an evolutionary system and were introduced by Reynolds as a means of simulating cultural evolution (Reynolds, 1994). CAs algorithms implements a dual mechanism of inheritance where are inherited characteristics of both the level of the population as well as the level of the area of belief space (culture). Algorithms that use social learning are higher than those using individual learning, because they present a better and faster convergence in the search for solutions (Reynolds, 1994). In CAs the characteristics and behaviors of individuals are represented in the Population Space. This representation can support any population-based computational model such as Genetic Algorithms, Evolutionary Programming, Genetic Programming, Differential Evolution, Immune Systems, among others (Jin & Reynolds, 1999).

Multidimensional Knapsack Problem (MKP) is a well-known nondeterministic-polynomial time-hard combinatorial optimization problem, with a wide range of applications, such as cargo loading, cutting stock problems, resource allocation in computer systems, and