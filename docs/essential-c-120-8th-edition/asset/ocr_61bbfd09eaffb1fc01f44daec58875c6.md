```
}
```

The output for Listing 21.2 is identical to Output 21.2; however, the execution time is significantly faster if you have multiple CPUs (and possibly slower if you do not). The Parallel.For() API is designed to look similar to a standard for loop. The first parameter is the fromInclusive value, the second is the toExclusive value, and the last is the Action() to perform as the loop body. When using an expression lambda for the action, the code looks similar to a for loop statement except that each iteration may execute in parallel. As with the loop, the call to Parallel.For() will not complete until all iterations are complete. In other words, by the time execution reaches the string.Join() statement, all sections of pi will have been calculated.

Note that the code for combining the various sections of pi no longer occurs inside the iteration (action) in Listing 21.2. As sections of the calculation will likely not complete sequentially, appending a section whenever an iteration completes will append them out of order. Even if sequence was not a problem, there is still a potential race condition because the += operator in Listing 21.1 is not atomic. To address both problems, each section of pi is stored into an array, and no two or more iterations will access a single element within the array simultaneously. Only once all sections of pi are calculated does string.Join() combine them. In other words, we postpone concatenating the sections until after the Parallel.For() has completed. This avoids any race condition caused by sections not yet calculated or concatenating out of order.

The TPL uses the same sorts of thread pooling techniques that it uses for task scheduling to ensure good performance of the parallel loop: It will try to ensure that CPUs are not overscheduled and so on.

# Guidelines

DO use parallel loops when the computations performed can be easily split up into many mutually independent processor-bound computations that can be executed in any order or on any thread.