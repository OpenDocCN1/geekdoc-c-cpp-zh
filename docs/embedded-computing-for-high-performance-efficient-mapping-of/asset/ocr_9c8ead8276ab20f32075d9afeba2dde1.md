![](bbox=[0.22, 0.11, 0.83, 0.25])

# FIG. 6.4 The OpenMP fork-join execution model.

To allow applications to adjust to available resources, OpenMP uses the _fork-join_ execution model [14] (see Fig. 6.4). All OpenMP programs start execution within the master thread which runs the code sequentially. When a parallel region is found, the master thread creates a team of threads of a given number, with the master thread also part of this team of threads. The operating system will then schedule these threads, assigning them to available processor cores. As thread management incurs an overhead, developers must adjust the number of threads so that the workload distribution is properly balanced and each thread maximizes core utilization. When a thread in the parallel region completes execution, it waits for all other threads to complete. At this point, sequential execution resumes within the master thread. In OpenMP, developers are required to specify the parallel regions of their programs explicitly and may control the number of threads associated in each parallel region. The OpenMP runtime and the operating system coordinate the parallel execution.

Developers identify parallel regions with OpenMP code directives. In C/C++, compiler directives are controlled by source code `#pragma` annotations to identify: (i) concurrency, (ii) how work can be distributed between threads, and (iii) synchronization points. An OpenMP directive has the following syntax format in C/C++:

```
#pragma omp <comp-directive-name> [clause, ...] <statement>
```

An OpenMP directive typically annotates the statement that directly follows it, including a code block `{ ... }`. In addition to OpenMP directives, developers can use a set of OpenMP library routines to control and query the underlying execution platform about its available resources, including: (i) getting the number of threads operating on a particular program execution point, the executing thread _id_ and nested level; (ii) setting the number of threads; (iii) setting and terminating locks and nested locks. Note that if the platform is not configured explicitly in the program, such as setting the number of threads, then the default behavior can be overridden by environment variables.