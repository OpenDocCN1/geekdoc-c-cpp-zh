Suppose space is fixed for one algorithm then only run time will be considered for obtaining the complexity of algorithm, these are

+   - Best case
+   - Worst case
+   - Average case

# Best Case

Generally, most of the algorithms behave sometimes in best case. In this case, algorithm searches the element for the first time by itself. For example: In linear search, if it finds the element for the first time by itself, then it behaves as the best case. Best case takes shortest time to execute, as it causes the algorithms to do the least amount of work.

# Worst Case

In worst case, we find the element at the end or when searching of elements fails. This could involve comparing the key to each list value for a total of N comparisons.
For example in linear search suppose the element for which algorithm is searching is the last element of array or it is not available in array then algorithm behaves as worst case.

# Average Case

Analyzing the average case behavior algorithm is a little bit complex than the best case and worst case. Here, we take the probability with a list of data. Average case of algorithm should be the average number of steps but since data can be at any place, so finding exact behavior of algorithm is difficult. As the volume of data increases, the average case of algorithm behaves like the worst case of algorithm.

# 1.5 Efficiency of an Algorithm

Efficiency of an algorithm can be determined by measuring the time, and amount of resources it uses for executing the program. The amount of time taken by an algorithm can be calculated by finding the number of steps the algorithm executes, while the space refers to the number of units it requires for memory storage.