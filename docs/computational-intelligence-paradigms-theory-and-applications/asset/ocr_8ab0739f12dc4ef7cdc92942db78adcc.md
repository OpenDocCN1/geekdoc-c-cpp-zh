example of biologically inspired computation. Other examples of biologically inspired computation include neural networks, which is computation based on analogy to animal nervous systems, artificial life, and artificial intelligence. During the evolutionary computation process a few populations of individuals undergo simulated evolution. While solving certain specific type of problems, these individuals generally comprise potential solutions to the problem. These solutions are presented by a kind of data structure. Selection mechanism is used by simulated evolution in order to find the best fit individuals which survive. The simulated evolution will include some variation-generating methods in which individuals can generate new individuals which are different from existing structures. Mutation and recombination (simulated mating) are two common variation-generating methods. Different evolutionary computation methods will differ in

+   - The data structure representation of individuals
+   - Variation producing mechanisms
+   - Parent selection methods
+   - Survival selection methods
+   - Population size

Following is a basic pseudo code for an evolutionary computation algorithm:

```
~~~
Generate an initial population in a random manner
While no stopping condition do
    Select parents based on fitness
    Produce offspring with some variants of their parents
    Select a few individuals to die based on fitness
End While
~~~
```

The fitness function of individuals is usually determined by the problem to be solved. Evolutionary computation is more commonly used in the field of optimization, when a function with several parameters is specified, and the aim is to find the parameter settings that give the largest or optimal value of the function. EC does not assure to find the optimal value of the function, EC merely attempts to find a parameter setting that gives a "large" or "near optimal" function value. Hence, ECs could be represented as "search algorithms" instead of "optimization algorithms". The function that is optimized does not need to be a