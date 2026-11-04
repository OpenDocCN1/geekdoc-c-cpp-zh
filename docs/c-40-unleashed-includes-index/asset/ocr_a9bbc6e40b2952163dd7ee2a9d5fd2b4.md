+   - Merge options, controlling query result buffering because the parallel producers and the query consumer can move at their own paces
+   - Use of a cancellation token, allowing the executing query to be canceled without waiting for all input to be consumed

Because those operations are meant for advanced users who thoroughly understand the way the PLINQ query engine works, we forego a detailed discussion—refer to the MSDN documentation for further information. The defaults that are used when all of those options are omitted are reasonably tuned for the common PLINQ use scenarios.

# Parallel Enumeration with ForAll

So far, we’ve been using a classic foreach loop in conjunction with a PLINQ-based query. Although this is the most obvious and natural way to consume results of a query, we can do better when we’re facing concurrency. Maybe the results of the query can be consumed in parallel as well, which will allow for a higher throughput. You can see why this is the case in Figure 20.17.

![](bbox=[0.1, 0.68, 0.75, 0.88])

FIGURE 20.17 Buffering involved with one consumer and multiple producers.

After the input sequence is partitioned (possibly in a dynamic manner), parallel workers start executing the query (which by itself can have further decomposition in tasks). To present all information to a foreach loop, the results from the various workers need to be put together again in some producer-consumer collection so that the intrinsically single-thread foreach loop can read the results one at a time.