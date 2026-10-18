
![](img/16cb41208935c5f22dd1044f03f2e31b_270_0.png)

## FIGURE 12.9

Parallel RF simulation with OpenMP. Tracing RF propagation paths is an embarrassingly parallel operation; however, careful attention to the expression of task-level parallelism in this context is required to maximize performance. These results depict scalar simulation performance, measured in terms of millions of rays per second, on two Intel Xeon E5-2699 processors using each of the three OpenMP parallelization strategies we explore.

As can be seen, when implemented in this way, simulator performance does not scale well with thread count. In fact, this version requires at least 16 threads before even a modest increase in performance is evident. This somewhat surprising behavior is a result of an implied barrier imposed at the end of the loop imposed by the parallel for construct. Each path segment will likely have a different computational cost due to variations in complexity of ray/object interactions or termination of the current path. Unfortunately, the barrier prevents other threads from making forward progress if any one segment is expensive to trace or if any one thread must create a new path. This parallelization strategy, though straightforward, induces unnecessary synchronization.

There are two approaches we examine to eliminate this unnecessary synchronization. One is to specify “nowait” which says that we do not want the implied barrier imposed at the end of the for loop. Another is to use the very flexible “task” capability of OpenMP.

First, we find that more careful use of OpenMP directives, by including the “nowait” clause, alleviates this issue (Figure 12.10). As before, this implementation spawns some number of threads using the omp parallel construct, but does so at the level of the while loop—not the nested for loop—so that

```
#pragma omp parallel num_threads(nthreads)
{
    while (running)
    {
        #pragma omp for nowait
        for (auto i = 0; i < npaths; ++i)
        {
            Path& path = livePaths[i];

            // Trace next segment in path... if current path completes,
            //     create a new one
            if (path.traceNextRay(scene))
            {
                // Create a new path
                ...
            }
        } // End for
    } // End while
} // End omp parallel

// Simulation has been stopped, finish in-flight paths and
//     terminate
for (auto i = 0; i < npaths; ++i)
{
    // Finish tracing path
}
```

## FIGURE 12.10

Using OpenMP `parallel` and `for nowait` to express path-level parallelism. The first approach to parallel RF path propagation induces unnecessary synchronization among threads and hinders parallel performance. This version more carefully expresses the available parallelism using a combination of `omp parallel` and `omp for`, together with the `nowait` clause, to maximize performance. (Code snippet from StingRay/Simulation.cpp:498–537.)

each thread now executes the entire loop. Note that there is an implied barrier at the end of the `omp parallel` construct.

Within the `while` loop, the `omp for` construct indicates that the current team of threads works together to execute the iterations of the corresponding `for` loop. However, the `nowait` clause at the end of the `omp for` construct indicates that threads executing the `for` loop do not need to wait on other threads before moving on. This clause removes the unnecessary synchronization point that was implied by the `omp parallel for` construct in the first OpenMP parallelization strategy. As before, threads run until the simulator is stopped, at which point threads complete their current path and the simulator terminates.

This approach improves performance by as much as 6.9× relative to single-threaded RF path propagation and recovers a factor of 3.07× (on average) relative to the first OpenMP parallelization strategy (Figure 12.9). In this case, each thread actually executes independently of every other thread—without synchronization—and performance scales nicely with thread count, as expected.

An alternative expression of path-level parallelism—using OpenMP tasks—can also be used to avoid unnecessary synchronization (Figure 12.11). Here, the implementation spawns threads using the `omp parallel` construct, but creates `npaths` tasks, one for each live path, using a single thread from

```
#pragma omp parallel num_threads(nthreads)
{
    #pragma omp single
    {
        for (auto i = 0; i < npaths; ++i)
        {
            #pragma omp task
            {
                Path& path = livePaths[i];

                while (running)
                {
                    // Trace next segment in path... if current path completes,
                    // create a new one
                    if (path.traceNextRay(scene))
                    {
                        // Create a new path
                        ...
                    }
                } // end while

                // Simulation has been stopped, trace each path to
                // completion
                while (!path.traceNextRay(scene))
                    ;
            } // End omp task
        } // End for
    } // End omp single
} // End omp parallel
```

## FIGURE 12.11

Using OpenMP tasks to express path-level parallelism. A third approach to parallel RF path propagation generates tasks using a single thread, expressed by the OpenMP `omp single` construct, and defers synchronization until the end of the surrounding `omp parallel` construct. As in the second OpenMP parallelization strategy, each path-trace task actually executes independently of every other task, and performance scales nicely. However, the task generation loop imposes unnecessary serialization in the RF path propagation loop, so absolute performance is generally not as high as with the second approach. (Code snippet from `StingRay/Simulation.cpp:549–593.`)

the pool. This arrangement is expressed by embedding the `omp single` construct immediately within the `omp parallel` construct. In this case, the first thread that arrives at the `omp single` construct executes the task creation loop. A task created in this manner can be executed immediately by any thread in the pool. Finally, once task creation is complete, the corresponding thread joins the other threads in executing the newly created tasks. As before, threads run until the simulator is stopped, at which point threads complete their current path and the simulator terminates.

This approach improves performance by as much as 6.5× relative to single-threaded RF path propagation and recovers a factor of 3.47× (on average) relative to the first OpenMP parallelization strategy (Figure 12.9). As in the second OpenMP parallelization strategy, each task actually executes

independently of every other task—without synchronization—and performance scales nicely with thread count. However, the task generation loop imposes unnecessary serialization in the RF path propagation loop, so absolute performance is generally not as high as with the second approach.

![](img/16cb41208935c5f22dd1044f03f2e31b_273_0.png)

## FIGURE 12.12

Parallel RF simulation on an Intel Xeon Phi 7120X coprocessor. These results depict scalar simulation performance, measured in terms of thousands of rays per second, on an Intel Xeon Phi 7120X coprocessor using task-level parallelism with 1-128 threads. Behavior of these codes is similar to that of the corresponding CPU versions; however, absolute performance suffers due to scalar code paths and memory bandwidth bottlenecks. Vectorized RF path propagation is an important area of future work, but is beyond the scope of this chapter.

Task-level parallelism also improves performance of RF path propagation on Intel Xeon Phi coprocessors (Figure 12.12). Behavior of these codes on Intel Xeon Phi coprocessors is similar to that of the corresponding codes on Intel Xeon processors: the second and third OpenMP parallelization strategies best express the available parallelism and generally achieve the best performance among the strategies we explore. However, absolute performance suffers due to scalar code paths and memory bandwidth bottlenecks. As noted above, vectorization of RF path propagation is particularly difficult, due to lack of coherence, even in primary rays. Vectorization in this context is an important area of future work, but is beyond the scope of this chapter.
