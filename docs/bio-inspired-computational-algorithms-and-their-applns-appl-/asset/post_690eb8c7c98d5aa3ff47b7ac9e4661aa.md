
Ku, S. & Lee, B. (2001). A Set-Oriented Genetic Algorithm and the Knapsack Problem, In: Proceedings of the Congress on Evolutionary Computation, ISBN 0-7803-6657-3, pp. 650-654, Seoul, South Korea, May 27-30 2001.

Kumar, R. & Singh, P. K. (2010). Assessing Solution Quality of Biobjective 0-1 Knapsack Problem using Evolutionary and Heuristic Algorithms, In: Applied Soft Computing, Vol. 10, No. 3, June 2010, pp. 711 – 718, ISSN 1568-4946.

Martello, S. & Toth, P. (1990). Algorithms and Computer Implementations, John Wiley & Sons, ISBN 0471924202, New York.

Nowostawski, M. & Poli, R. (1999). Parallel Genetic Algorithm Taxonomy, In: Proceedings of the Third International Conference on Knowledge-Based Intelligent Information Engineering Systems, ISBN 0780355784, pp. 88-92, Adelaide, August 1999.

Reynolds, R. G., & Peng, B. (2004). Cultural Algorithms: Computational Modeling of How Cultures Learn to Solve Problems, In: Seventeenth European Meeting on Cybernetics and Systems Research, ISBN 3-85206-169-5, Vienna, Austria, April 13-16 2004.

Reynolds, R. G. & Chung, C. (1996). The Use of Cultural Algorithms to Evolve Multiagent Cooperation, In: Proc. Micro-Robot World Cup Soccer Tournament, pp. 53-56, Taejon, Korea, 1996.

Reynolds, R. G. (1994). An Introduction to Cultural Algorithms, In: Proceedings of the Third Annual Conference on Evolutionary Programming, ISBN 9810218109, pp. 131-139, San Diego, California, February 24-26 1994.

Reynolds, R. G. (1999). Chapter Twenty-Four: Cultural Algorithms: Theory and Applications, In: New Ideas in Optimization, Corne, D., Dorigo, M. & Glover, F., pp. 367-377, McGraw-Hill Ltd, ISBN 0-07-709506-5, UK, England.

Silva, D. J. A. & Oliveira, R. C. L. (2009). A Multi-population Cultural Algorithm Based on Genetic Algorithm for the MKP, In: Proc. of the 11th Annual Conference on Genetic and Evolutionary Computation, ISBN 978-1-60558-325-9, pp. 1815-1816, Montréal, Québec, Canada, July 8-12 2009.

Sivanandam, S.N. & Deepa, S. N. (2007). Introduction to Genetic Algorithms, (1st), Springer, ISBN 978-3-540-73189-4, New York.

Sivaraj, R. & Ravichandran, T. (2011). An Improved Clustering Based Genetic Algorithm for Solving Complex NP Problems, In: Journal of Computer Science, Vol. 7, No. 7, May 2011, pp. 1033-1037, ISSN 15493636.

Spillman, R. (1995). Solving Large Knapsack Problems with a Genetic Algorithm, In: IEEE International Conference on Systems, Man and Cybernetics, Vol. 1, ISBN 0-7803-2559-1, pp. 632-637, Vancouver, BC, Canada, October 22-25 1995.

Tavares, J., Pereira, F. B. & Costa, E. (2008). Multidimensional Knapsack Problem: A Fitness Landscape Analysis, In: IEEE Transactions on Systems, Man and Cybernetics, Part B: Cybernetics, Vol. 38, No. 3, June 2008, pp. 604-616, ISSN 1083-4419.

Tomassini, Marco (2005). Spatially Structured Evolutionary Algorithms: Artificial Evolution, Space and Time - Natural Computing Series (1st), Springer, New York, ISBN 3540241930, Secaucus, NJ, USA.

Zoheir, E. (2002). Solving the 0/1 Knapsack Problem Using an Adaptive Genetic Algorithm, In: Artificial Intelligence for Engineering Design, Analysis and Manufacturing, Vol. 16, No. 1, January 2002, pp. 23-30, ISSN 08900604.

## Using a Genetic Algorithm to Solve the Benders’ Master Problem for Capacitated Plant Location

Ming-Che Lai¹ and Han-suk Sohn²*
¹Yu Da University,
²New Mexico State University
¹Taiwan
²USA

## 1. Introduction

The capacitated plant location problem (CPL) consists of locating a set of potential plants with capacities, and assigning a set of customers to these plants. The objective is to minimize the total fixed and shipping costs while at the same time demand of all the customers can be satisfied without violating the capacity restrictions of the plants. The CPL is a well-known combinatorial optimization problem and a number of decision problems can be obtained as special cases of CPL. There are substantial numbers of heuristic solution algorithms proposed in the literature (See Rolland et al., 1996; Holmberg & Ling, 1997; Delmaire et al., 1999; Kratica et al., 2001; He et al., 2003; Uno et al., 2005). As well, exact solution methods have been studied by many authors. These include branch-and-bound procedures, typically with linear programming relaxation (Van Roy & Erlenkotter, 1982; Geoffrion & Graves, 1974) or Lagrangian relaxation (Cortinhal & Captivo, 2003). Van Roy (1986) used the Cross decomposition which is a hybrid of primal and dual decomposition algorithm, and Geoffrion & Graves (1974) considered Benders’ decomposition to solve CPL problem. Unlike many other mixed-integer linear programming applications, however, Benders decomposition algorithm was not successful in this problem domain because of the difficulty of solving the master system. In mixed-integer linear programming problems, where Benders’ algorithm is most often applied, the master problem selects values for the integer variables (the more difficult decisions) and the subproblem is a linear programming problem which selects values for the continuous variables (the easier decisions). If the constraints are explicit only in the subproblem, then the master problem is free of explicit constraints, making it more amenable to solution by genetic algorithm (GA). The fitness function of the GA is, in this case, evaluated quickly and simply by evaluating a set of linear functions. In this chapter, therefore, we discuss about a hybrid algorithm (Lai et al., 2010) and its implementation to overcome the difficulty of Benders’ decomposition. The hybrid algorithm is based on the solution framework of Benders’ decomposition algorithm, together with the use of GA to effectively reduce the computational difficulty. The rest of this section can be found in Goldberg (1989) and Davis (1991). The implementation of GA is a step-by-step procedure:

### 4.1 Initialization

Initialization is to generate an initial population. The population size and length of chromosome depends on the users' choice and other requirements of the specific problem. To start, we usually have a totally random population. Each random string (or chromosome) of the population, representing a possible solution for the problem, is then evaluated using an objective function. The selection of this objective function is important because it practically encompasses all the knowledge of the problem to be solved. The user is supposed to choose the proper combination of desirable attributes that could be best fit to his purposes. In CPL problem, the variable Y is a vector of binary integers. It is easily to be coded as a string of binary bit with the position #i corresponding to the plant #i. For example, Y = (0 1 1 0 1 0 0 0) means that plants #1, 4, 6 and 7 are not open and plants 2, 3 and 5 are open. In our GA, a population size of 50 was used and the fitness function is evaluated quickly and simply by evaluating a set of linear functions, i.e., σ_T(Y) ≡ Max_{1≤i≤T} { α^i Y + β^i }.

### 4.2 Selection

Selection (called reproduction by Goldberg) starts with the current population. Selection is applied to create an intermediate population or mating pool. All the chromosomes in the mating pool are waiting for other operations such as crossover and/or mutation to create the next population. In the canonical genetic algorithm, selection is made according to the fitness. The fitness could be determined by many ways. For example, the fitness could be assigned according to probability of a string in the current population (Goldberg, 1989), a string's rank in the population (Baker, 1985; Whitley, 1989), or simply by its performance of scores. In our GA, the latter case is used, i.e., a string with an average score is given one mating; a string scoring one standard deviation above the average is given two matings; and a string scoring one standard deviation below the average is given no mating (Michalewicz, 1998).

### 4.3 Crossover and mutation

We use a standard single-point crossover method. The duplicated strings in the mating pool are randomly paired off to produce two offspring per mating. The crossover location of the strings is generally chosen at random but not necessary always the case. For example, the distribution for selection the crossover point of the GenJam system, an interactive genetic algorithm jazz improviser, which was developed by Dannenberg for the Carnegie Mellon MIDI Toolkit, is biased toward the center of the chromosome to promote diversity in the population. If a crossover point is too near one end of the chromosome or the other, the resulting children are more likely to resemble their parents. This will lead the GenJam system to repeat itself when two nearly identical phrases happen to be played close to one another in the same solo and it does not seem desirable for GenJam to perform in that way. The role of mutation is to guarantee the diversity of the population. In most case, mutation alters one or more genes (positions in a chromosome) with a probability equal to the
