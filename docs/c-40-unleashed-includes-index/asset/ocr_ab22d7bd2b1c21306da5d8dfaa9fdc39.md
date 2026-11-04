```
subtotal => Interlocked.Add(ref total, subtotal)
});

Console.WriteLine($"The total is {0}", total);
```

Here we're iterating over the enumerable sequence with parallel loop body executions. Again, we're using a long-valued thread-local state to compute subtotals of the sum of the sequence's elements, which get aggregated into the final sum.

# The Role of Partitioners

To run operations on the elements of a sequence in parallel, the sequence needs to be partitioned into chunks of work. This is where the concept of partitioners enters the picture. They play a crucial role in the PLINQ implementation, too (see the section "Parallel LINQ" in Chapter 20).

The idea of a partitioner is to let the workers that execute the loop body process more than just individual elements one at a time. For example, if you have 100 elements and four cores, it makes sense to have each core take care of the work for 25 elements. Such a common partitioning scheme is called range partitioning, where the input sequence size has to be known upfront to create index-based ranges for each worker. This scheme has a disadvantage, though: If one worker completes way before other workers are done with their part of the work, the idle worker cannot steal work.

Another way to partition a sequence is chunk partitioning, where chunks of a given size are processed by workers. This differs from range partitioning in that the split-up of the work is not statically based on the number of workers. For example, given 100 elements and a chunk size of 5, we get 20 units of work. If there are, say, four cores with a worker allocated for each core, they will on average execute five chunks each. This isn't static allocation of chunks to workers, though; if a worker is presented with a chunk, it can process much faster than another worker can process its chunk, and it can readily move on to the next chunk. Overall, the throughput of the system is higher. Load-balancing partitioning is another name for the use of dynamic chunk-based partitioning.

You can create a partitioner by using the Partitioner.Create factory methods. A set of overloads is based on from and to bounds, combined with range sizes, creating a partitioner that employs range partitioning. Other overloads can take in an array or an IList<> object, whose length is known immediately. Depending on a Boolean flag named loadBalance, the resulting partitioner uses range partitioning or load-balancing chunk partitioning.

For more information about the use of partitioners and the creation of custom partitioners, refer to the MSDN documentation about the subject.