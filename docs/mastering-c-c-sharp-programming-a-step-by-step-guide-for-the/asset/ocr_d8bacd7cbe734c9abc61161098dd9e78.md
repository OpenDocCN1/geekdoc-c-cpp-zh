Also by default, PLINQ will make use of every processor on the host system. Again, you can tell PLINQ that you only want a specific number of processors used and you do this by using the method called WithDegreeOfParallelism. This is another useful method to use when you need to ensure that all of the other processes on the system will still get a specified amount of CPU time. The following code shows you how to use the method to limit the query to using no more than two processors:

```
var query = from item in
source.AsParallel().WithDegreeOfParallelism(2)
    where Compute(item) > 42
    select item;
```

Where a query may be doing a lot of work that is classed as non-compute-bound, like File I/O, it may be more advantageous to specify that the degree of parallelism should be more than the number of processor cores on the system.

# Ordered vs. Unordered Parallel Queries

In certain queries, in order for results to be produced that keep the source sequence ordering preserved, a specific query operator must be used. With PLINQ, you get the AsOrdered operator and this is not the same as the AsSequential operator. The AsOrdered sequence still is processed in parallel but the results will be buffered and then sorted. Preserving errors is time-consuming because of the extra work involved, and because of this, AsOrdered sequences may be slower in processing than an AsUnordered sequence, which is the default option. There are several factors that determine whether a parallel operation that is ordered is going to be faster than the sequential version.

In the example below, you can see how you can opt into order preservation:

```
var evenNums = from num in numbers.AsParallel().AsOrdered()
    where num % 2 == 0
```