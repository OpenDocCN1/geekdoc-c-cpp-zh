# **The Algorithm**

+   1. Randomly generate an initial population
+   2. Compute and save the fitness for each individual in the current population
+   3. Define selection probabilities for each individual in so that it is proportional to the fitness
+   4. Generate the next population by probabilistically selecting individuals from current population to produce offspring via genetic operators
+   5. Repeat step 2 until satisfying solution is obtained

The paradigm of GAs described above is usually the one applied to solving most of the problems presented to GAs. Though it might not find the best solution more often than not, it would come up with a partially optimal solution.

# ### 1.5.2 Genetic Programming

In Genetic Programming programs are evolved to solve pre-described problems from both of these domains. The term evolution refers to an artificial process gleaned from the natural evolution of living organisms. This process has been abstracted and stripped off of most of its intricate details. It has been transferred to the world of algorithms where it can serve the purpose of approximating solutions to given or even changing problems (machine learning) or for inducing precise solutions in the form of grammatically correct (language) structures (automatic programming).

It has been realized that the representation of programs, or generally structures, has a strong influence on the behavior and efficiency of the resulting algorithm. As a consequence, many different approaches toward choosing representations have been adopted in Genetic Programming. The principles have been applied even to other problem domains such as design of electronic circuits or art and musical composition.

Genetic Programming is also part of the growing set of Evolutionary Algorithms which apply the search principles of natural evolution in a variety of different problem domains, notably parameter optimization. Evolutionary Algorithms, and Genetic Programming in particular, follow Darwin's principle of differential natural selection. This principle states that the following preconditions must be fulfilled for evolution to occur via (natural) selection