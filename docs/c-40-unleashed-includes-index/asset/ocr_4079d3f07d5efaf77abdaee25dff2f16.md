```
var lst = new List<int>();
foreach (var x in Enumerable.Range(0, 10000))
    foreach (var y in Enumerable.Range(0, 10000))
        if (x > y)
            lst.Add(x + y);
```

Besides not being lazily evaluated, lots of issues with this code will prevent easy parallelization. Let's take a look.

One possible opportunity for parallelization is to split the input into separate partitions and run the filtering operation in parallel. On a dual-core machine, your core could process the first 5,000 values for x, while another could take care of the last half. This requires applying some partitioning policy depending on the machine capabilities. If you run the same code on a quad core, you likely want to create four partitions. Although this seems easy using Environment.ProcessorCount, a static partitioning with equal-size partitions might not be the right choice in general. It could be the case that the cost of applying querying operators varies from input to input, so that one partition is processed much faster than another one. In that case, the core assigned to the partition with the least cost will sit idle after a while.

Even if we come up with a good partitioning strategy, other remaining issues lurk around the corner. In the preceding code, we're adding results to an in-memory collection object, which is generally not safe for concurrency and multithreading in particular. So we need to use locks, which puts us in an error-prone situation and can cause adverse effects on our intended performance optimization. I'll leave the exercise of parallelizing this imperative piece of code to the concurrency-savvy reader. Suffice to say, things get messy immediately, and the intent of our code gets more blurry by the minute. With PLINQ, we can simply write the following:

```
var res = from x in Enumerable.Range(0, 10000).AsParallel()
          from y in Enumerable.Range(0, 10000)
          where x > y
          select x + y;
```

Now both cores are being put to work (as shown in Figure 20.15), and the total execution time went down to 10 seconds, about half of the original time. All we did to achieve this was to put the AsParallel call on the topmost (or outermost, depending on your mental model) data source in the query.

![](bbox=[0.08, 0.82, 0.55, 0.97])

FIGURE 20.15 PLINQ puts both cores to work.