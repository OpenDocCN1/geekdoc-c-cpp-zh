As a little exercise, try to rewrite the process-filtering example in terms of typical loop constructs. I'm sure you'll come to realize the intent of the code gets buried underneath the imperative style of code. And we're not yet doing more fancy query operations like sorting, grouping, and so on.

# Loops in the Age of Concurrency

Looked at from a different perspective, loop constructors are essentially a source of tasks. If every iteration of a loop is independent from another iteration's state, there's no reason the individual iterations can't be run in parallel. In the age of multicore processors on every desk, better ways to unleash the hardware's power are a much-sought-for treasure. The new System.Threading namespace additions in .NET 4.0 provide for this in various ways, one of which is the concept of parallel loop constructs. We look at this in more detail in Chapter 30, "Task Parallelism and Data Parallelism." Figure 7.23 shows the Parallel class's static methods.

![](bbox=[0.1, 0.58, 0.7, 0.7])

FIGURE 7.23 The System.Threading.Parallel type's parallel loop constructs.

It's important to realize that those constructs are provided by libraries as opposed to any of the managed code languages. This is a huge advantage because all languages immediately benefit from this addition while not committing to new language syntax just yet. They may slip into the language at some point, however, but only if those constructs become popular. However, because C# has become expressive enough due to the introduction of lambda expressions in version 3.0, the use of those constructs feels quite natural:

```
Parallel.For(1, 100, i =>
{
    // Loop body code goes here.
});
```

To make parallel loops worthwhile, the work they do inside their loop bodies should be sufficiently heavy to exceed the overhead of setting up the multithreaded infrastructure required. One place where those conditions are met is when dealing with data-intensive operations, as in LINQ. For example, when filtering a huge set of data, it's possible to