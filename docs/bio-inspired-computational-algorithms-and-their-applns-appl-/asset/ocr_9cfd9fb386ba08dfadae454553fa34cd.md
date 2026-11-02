# The Network Operator Method for Search
of the Most Suitable Mathematical Equation

Askhat Diveev¹ and Elena Sofronova²
¹Institution of Russian Academy of Sciences Dorodnicyn Computing Centre of RAS,
²Peoples' Friendship University of Russia
Russia

# 1. Introduction

For many applied and research problems it is necessary to find solution in the form of mathematical equation. These problems are the selection of function at approximation of experimental data, identification of control object model, control synthesis in the form of state space coordinates function, the inverse problem of kinetics and mathematical physics, etc. The main method to receive mathematical equations for solution of these problems consists in analytical transformations of initial statement formulas of the problem. A few problems have the exact analytical solution, therefore mathematicians use various assumptions, decomposition, and special characteristics of solutions. Usually mathematicians set the form of mathematical equation, and the optimal parameters are found using numerical methods and PC. Such methods as the least-square method have been applied to the problems of approximation for many years (Kahaner D. et al., 1989).

Recently the neural networks have been used to solve complex problems when the mathematical equation cannot be found analytically. The structure of any neural network is also given within the values of parameters or weight coefficients. In problems of function approximation and the neural network training the form of mathematical equation is set by the researcher, and the computer searches for optimum values of parameters in these equations (Callan, 1999; Demuth et al., 2008).

In 1992 a new method of genetic programming was developed. It allows to solve the problem of search of the most suitable mathematical equation. In genetic programming mathematical equations are represented in the form of symbol strings. Each symbol string corresponds to a computation graph in the form of a tree. The nodes of this graph contain operations, and the leaves contain variables or parameters ( Koza, 1992, 1994; Koza, Bennett et al., 1999 & Koza, Keane et al., 2003).

Genetic programming solves the problems by applying genetic algorithm. To perform the crossover it is necessary to find symbol substrings that correspond to branches of trees. The analysis of symbol strings increases the operating time of the algorithm. If the same parameter or variable is included in the required mathematical equation several times, then to solve the problem effectively the genetic programming needs to crossover the trees so that the leaves contain no less than the required number of parameters or variables.