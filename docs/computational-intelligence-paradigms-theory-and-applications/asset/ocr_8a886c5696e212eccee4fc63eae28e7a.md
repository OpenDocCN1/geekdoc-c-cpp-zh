+   - A hypothesis that a genetic algorithm performs adaptation by implicitly and efficiently implementing this abstract adaptive mechanism.

According to Goldberg the abstract adaptive mechanism is defined as: “short, low order, and highly fit schemata are sampled, recombined [crossed over], and resampled to form strings of potentially higher fitness. In a way, by working with these particular schemata [the building blocks], instead of building high-performance strings by trying every conceivable combination, better and better strings can be constructed from the best partial solutions of past samplings.”

Just as a child creates magnificent fortresses through the arrangement of simple blocks of wood (building blocks), so does a genetic algorithm seek near optimal performance through the juxtaposition of short, low-order, high-performance schemata, or building blocks.

# 13.8.2  The Dynamics of a Schema

The Schema Theorem only shows how schemas dynamically change, and how short, low-order schemas whose fitness remain above the average mean receive exponentially growing increases in the number of samples. It cannot make more direct predictions about the population composition, distribution of fitness, and other statistics more directly related to the genetic algorithm itself. The pseudocode of the general algorithm is as follows:

```
Initialize population
While not end of population do
    Calculate Fitness
    Choose two parents selection methods
    Choose one of the offspring by single
        -point crossover
    Mutate each bit with probability pm,
    Place each bit in population.
End While
```

The method of approximating the dynamics can be calculated through the following method. Let S be a schema with at least one instance in the given population at the time t. Let the function n(S,t) be the number of instances of S at time t, and let the function f(S,t) be the observed average of S at time t. Now, it is required to calculate the expected number of instances of schema S during the next time interval. Assuming that E(x) is the expected value of x, to determine E(n(S,t+1)), the number of instances at t+1 is equivalent to the number of offspring