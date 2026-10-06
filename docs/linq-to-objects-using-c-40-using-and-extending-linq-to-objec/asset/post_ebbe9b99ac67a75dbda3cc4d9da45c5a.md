
# LINQ DATA PARALLEL 275

is much more balanced and even throughout the query's execution, not perfectly even but far superior to the sequential version. Although the query didn't run twice as fast (as might be expected on a dual-core machine), the speed improvement is significant and was solely achieved by adding .AsParallel() to the sequential query.

Failing short of the perfect doubling of performance in this case is due to the constraints spoken about earlier (Amdahl's Law, ordering, and so on); there is overhead in managing the parallelization process and sorting and is to a large degree limited by the disk access speed. It is important to realize that if this same test had been run on a quad-core processor, the results would have been closer to a four times increase in performance with no additional code changes. (Although never exceeding, and who knows when your hard-drive access speed limits improvement, the key point is no code changes are required to take advantage of more cores).

Having seen this example, understanding what actually occurred behind the scenes to parallelize a LINQ helps you realize what queries will be substantially improved by adding the AsParallel extension to a data source and what queries will actually degrade in performance.

# What Happens During a Parallel LINQ Query?

The general parallelization process for a query is to partition the work, hand off the work to worker processes running on different threads, and merge the results on completion. To achieve this general process, a query marked to execute as parallel goes through the following (much simplified here for clarity) process by the Parallel LINQ runtime:

- 1. Query analysis (Will parallelism help?)
2. Partitioning
3. Parallel execution
4. Merging the parallel results

Each of these steps is covered briefly here in order to help you understand how queries might be structured for best parallel performance.

# Query Analysis

The first step when a LINQ query is passed to the Parallel LINQ execution engine is query analysis. The query pattern is examined to determine if it is a candidate for parallelization improvement with respect to time and memory resources. If it isn't, then the query will be executed sequentially.

The runtime doesn't look at the size of the data or how much code is in the delegate functions; it simply examines (at this time, but who knows in future updates) the shape of the query and determines if it is worth the parallel overhead. The query can be forced to execute in parallel (or not) if the conservative nature of the run-time decision process isn't acceptable for a given case. To force a query to execute in parallel, add a WithExecutionMode extension to the ParallelQuery source. There are two values for the enumeration, default and ForceParallelism, which should not need further description.

```
.AsParallel())
.WithExecutionMode(
    ParallelExecutionMode.ForceParallelism)
```

There can be at most a single WithExecutionMode per query, even if that query is composed using the result of a previous query. WithExecutionMode extensions will cause a System.InvalidOperationException at runtime with the message:

The WithExecutionMode operator may be used at most once in a query.

Microsoft has said that they will continue to evolve the query assessment over time and devise new algorithms for improving the parallel performance of different query patterns that currently would fall back to sequential execution. Once the framework decides that a query is a candidate for parallelization, it moves onto partitioning the data, which is simply splitting the input data for efficient execution in chunks.

# Partitioning Data

Parallel LINQ has a number of data partitioning schemes it uses to segment the data for different worker processes. For example, if an input source has one hundred elements, when this query run on a dual-core machine, the Parallel LINQ execution engine might break the data into two partitions of 50 elements for parallel execution. This is a simplistic case, and in practice, partitioning the data is more complex, and the actual partitioning scheme depends on the operators used in the query, among other factors.

The built-in partition schemes at the time of writing are called chunk, striped, and hash. Each of these data partitioning schemes visits a certain set of source data types and operator scenarios; the parallel runtime chooses the appropriate one and partitions the data for execution when a worker process asks for more work.

You are not limited to the partitioners Microsoft has built-in. They have allowed for custom partitioners to be written for a specific purpose; this topic is beyond the scope of this book, but search online for Partitioner-ConfigSource for details. To understand each of the built-in partitioners and to understand their relative strengths and weaknesses, each one briefly explained.

**Range Partitioning** The range partitioning scheme breaks an input data set into equal-sized ranges optimized for the number of threads available (best case: equal to the number of cores available). Range partitioning is chosen when the data source is indexable (IList<T> and arrays). For indexable sources like these, the length is known when enumerating the data source (to determine the count), and the number of elements per partition for parallel execution is simply calculated upfront.

This partitioning scheme offers great parallel efficiency, largely from not needing any synchronization between participating threads. Threads get a range of data assigned to them and can process data without any interaction (incoming or outgoing) with other threads. The downside of this thread isolation is that other threads cannot help out if one thread gets behind in processing due to uneven utilization; on balance though, this partitioning scheme is efficient.

**Chunk Partitioning** Chunk partitioning is used when a data source isn't indexed (IEnumerable<T>) where the elements can be accessed by index and the count property cannot be ascertained without an enumeration of the entire data source.

Microsoft has optimized this partitioning scheme for a wide variety of queries, and although the exact algorithm isn't known, the responsible team's blog posts indicate that the number of elements per partition is doubled after a certain number of requests and so on. This allows this partitioning scheme to be adaptable from sources with only a few elements to sources with many elements, keeping each core filled with work, while still balancing the load to ensure the greatest chance of each core finishing at the same time. As mentioned previously, this partitioning algorithm can't be as exact as range partitioning, and you should strive for using indexable collection for your data sources whenever possible.

**Hash Partitioning** This partitioning scheme is for queries that need to compare data. The following operators execute: Join, GroupJoin, GroupBy, Distinct, Union, and Intersect. The intention of partitioning scheme is that elements that share the same hash code will be partitioned into the same thread. The alternative options of partitioning elements would require extensive and complex inter-thread synchronization and data sharing. This partitioning scheme reduces overhead and enhances parallel performance for queries using these operators.

The downside however is that hash partitioning is complex and has a higher overhead than the partitioning schemes so far. However, it is the most efficient and viable option for query operators that need to compare hash codes to do their work.

# HASH-CODE DISTRIBUTION CONCERNS WHEN USING HASH PARTITIONING Stephen Toub from Microsoft's Parallel Framework team made the following note on this subject during a quick review. I couldn't have written this better, so didn't even try:

> "The system makes an assumption that hash codes for elements are equally spread across all elements, such that the partitions will end up having many numbers of items, resulting in a load-balanced system. If, however, too many of one hash code exist (such as if the same string appeared in a list of strings a disproportionate number of times, or if a poor hash function was used on a custom type), load balance issues can result."

**Striped Partitioning** Striped partitioning is used for standard query operators that process and evaluate from the front of a data source. SkipWhile and TakeWhile are the operators that use this partitioning scheme. Striped partitioning is only available when the data source is indexable (List-T and arrays, T[]) and assumes that each element needs to be processed sequentially in order to avoid launching off a significant amount of work that has to be thrown away at merge time. It achieves this by taking very small ranges at a time, processing these in parallel to gain some optimization, and then merging carefully based on the result of the while predicate.
