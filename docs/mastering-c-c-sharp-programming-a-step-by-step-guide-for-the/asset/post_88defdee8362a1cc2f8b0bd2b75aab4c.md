
There will be cases where the query performance can be improved and that is done by writing a custom partitioner that will take full advantage of a source data characteristic. Inside the query, the enumerable object that is queried is the custom partitioner:

```
int[] arr = new int[9999];
Partitioner<int> partitioner = new MyArrayPartitioner<int>(arr);
var query = partitioner.AsParallel().Select(x => SomeFunction(x));
```

PLINQ has support for a set number of partitions, although, during run time, there is the chance that the data can be dynamically assigned to the partitions for the sake of load balancing. The for and foreach statements only support dynamic partitioning and this means that, at run time, the number of partitions will change.

## Measuring PLINQ Performance

Sometimes we can parallelize a query but there are costs to this – setting up parallel queries has overheads that far outweigh what benefit is gained in terms of performance. If a query doesn’t need to do a lot of computation or if there is a small data source, PLINQ queries can still be slower than sequential LINQ to Objects queries. The Parallel Performance Analyzer can be used in Visual Studio Team System to find any bottlenecks in processing, to compare how various queries perform, and to work out whether sequential or parallel processing is being used.

## Understanding PLINQ Speedup

The primary purpose of PLINQ is to speed up LINQ to Objects query execution. It does this through parallel execution of query delegates on multicore systems. PLINQ works the best when elements in source collections are processed independently of one another and there is no shared state among the individual delegates.

Operations like this are common in both PLINQ and LINQ to Objects queries and these operations are sometimes called “delightfully parallel” and this is because they easily lend themselves to being scheduled on several threads. However, not every query has these “delightfully parallel” operations; most of the time, queries involve certain operators that will slow parallel execution down or simply can’t be parallelized at all. Even if a query is “delightfully parallel”, the data source still has to be partitioned by PLINQ and work still has to be scheduled on the threads. This usually ends in the results being merged on completion of the query.

All of these kinds of operations cause the cost of parallelization to rise in terms of computation and these costs are known as overheads. For the best performance to be achieved in PLINQ queries, the “delightfully parallel” parts need to be maximized and the parts that need the overhead should be minimized. To finish this section on PLINQ, we are going to look at writing PLINQ queries that are as efficient as they can be while still providing the right results.

## What Can Impact PLINQ Query Performance?

What we are going to look at now are some of the very important factors that can have an impact on the performance of parallel queries. These are general and, on their own, are simply not enough for a prediction on the performance of a query in all cases. As with everything, you should measure the real performance of a query on computers that offer a series of representative loads and configurations.

- Computational cost – overall work

To be speeded up, PLINQ queries need to have sufficient “delightfully parallel” work in order for the overhead to be offset. That work can be expressed in terms of the computational cost of each individual delegate multiplied by how many elements there are in the source collections. Assuming that parallelization is possible on an operation then the more expensive it is in computational terms and that means there is more opportunity for it to be sped up.

For example, let’s say that a specific function will execute in one millisecond. If you have a sequential query that goes over a thousand elements, the operation will take one second to perform. On the other hand, a parallel query done on a computer that has four cores could be done inside of 250 milliseconds. The speedup gained here is 750 milliseconds. If the elements in the function needed one second each to execute, the speedup would equate to 750 seconds. If the delegate works out to be significantly expensive, PLINQ could offer sufficient speedup when the source collection only has a few items. On the other hand, collections with little source data and trivial delegates generally don’t make very good PLINQ candidates.

In the example below, you can see that queryA is a good PLINQ candidate assuming that there is a lot of work involved in the Select function. However, queryB probably isn’t a great candidate because the Select statement has insufficient work and the parallelization overhead cost will offset most, if not all, of any speedup gained:

```
var queryA = from num in numberList.AsParallel()
    select ExpensiveFunction(num); //a great candidate for PLINQ
```

```
var queryB = from num in numberList.AsParallel()
    where num % 2 > 0
    select num; //not such a good candidate for PLINQ
```

- Degree Of Parallelism

In simple terms, determine how many logical cores the system has. This is an obvious follow-on because a “delightfully parallel” query will clearly run faster on a system that has more cores simply because the work can be broken down into chunks and run concurrently on separate threads. How much speedup is gained will depend on the percentage of the query work that is parallelizable. However, what you should not do is assume that every query is going to run at twice the speed on a computer with eight cores than on a computer with four cores. When queries are tuned for the best performance, you must measure the real results on computer systems with varying numbers of cores. In relation to the previous factor, if you have large computing resources, you need large datasets to take full advantage of it.

## Type and Number of Operations

The AsOrdered operator is provided by PLINQ when the element order inside the source sequence needs to be maintained. Ordering comes with a cost but this isn’t usually too much. The operations of Join and GroupBy also incur a cost. PLINQ works the best when you let it process the source collection elements in any order it wants to, and pass them to another operator when they are ready.

## Query Execution Form

If the results of a query are being stored, usually by calling ToList or ToArray, the results from every parallel thread have to merge into one data structure. To do this incurs an overhead that simply cannot be avoided. In the same way, if the results are iterated over with a foreach loop, the worker thread results must be serialized on to the enumerator thread. However, if you only want an action performed based on each thread result, the ForAll method can be used to do this on multiple threads.

## Merger Option Types

There are two ways to configure PLINQ – to buffer its own output and produce it in small chunks or in one go once the entire set of results has been produced, or to stream the results as they come in individually. With the first way, execution time is shorter and, with the second, latency in between the elements that result is reduced. While the merger options don’t always impact significantly on the overall performance of the query, they can have an impact on the perceived performance because they are in control of the length of time a user waits before they see the results.

## Partitioning

Sometimes, PLINQ queries over source collections that are indexable can result in a workload that isn’t very balanced. When this happens, you can create custom partitioners to try to increase the performance of the query.

## When Sequential Mode is Chosen

PLINQ always tries to execute queries at a speed that is as fast or faster than sequential execution. PLINQ doesn’t look to see the computational cost of the user delegates and it doesn’t look to see the size of the input source, but it will look for specific shapes in the queries. More specifically, it will look to see if operators or combinations of operators are in use that tends to slow down query execution when in parallel mode. When it sees them, by default, PLINQ will go back to sequential mode.

However, if you measure the performance of a specific query and determine that parallel mode would be far better and quicker, you can make use of the flag called ParallelExecutionMode.ForceParallelism by using the method called WithExecutionMode, thus telling PLINQ that you want the query run in parallel mode.

The next list describes each of the query shapes that will be executed sequentially by PLINQ:

- Queries with an indexed Where, Select, ElementAt or indexed SelectMany clause once the filtering or ordering operator has either rearranged or removed altogether the original indices
