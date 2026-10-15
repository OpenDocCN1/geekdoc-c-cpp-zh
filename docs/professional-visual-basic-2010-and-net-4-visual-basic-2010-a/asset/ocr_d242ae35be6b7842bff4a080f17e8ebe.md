![](bbox=[0.125, 0.09, 0.62, 0.63])

# FIGURE 33-6

# Parallel.ForEach

Sometimes, refactoring an existing For loop as previously explained can be a very complex task, and the changes to the code could generate too much overhead for each iteration, reducing the overall performance. Another useful alternative is to partition all the data to be processed into parts that can be run as smaller loops in parallel, defining a custom partitioner, a mechanism tailored to split the input data into specific pieces that overrides the default partitioning mechanism. It is possible to use a Parallel.ForEach loop with a override partitioner in order to create new versions of the sequential loops with a simpler refactoring process.

Listing 33-5 shows the new code with the refactored loops using the imperative syntax to implement data parallelism offered by Parallel.ForEach, combined with a sequential For loop and a custom partitioner created with System.Collections.Concurrent.Partitioner. The new methods, ParallelPartitionGenerateAESKeys and ParallelPartitionGenerateMD5Hashes, also try to take advantage of all the cores available, relying on the work done under the hood by Parallel.ForEach and the range partitioning performed to distribute smaller sequential loops inside as many parallel loops as available cores. The code also optimizes its behavior according to the existing hardware at runtime.