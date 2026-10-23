of values into a single value. A good example is summing the values of a large array to produce a single value.

S11, Message Passing Paradigm: This is a ubiquitous paradigm and a key component in models of concurrency and object-oriented programming. Using messages is an alternative to shared data structures in combination with locks and semaphores in order to avoid race conditions. There is no shared data between tasks that exchange information using messages. In this case we speak of an isolated state. An example of a library using this paradigm is the Asynchronous Agents Library that we discuss in Chapters 30 and 32.

These 11 patterns represent proven ways of analysing and designing concurrent systems. In order to determine which pattern (or combination of patterns) to use, we can deploy data or task decomposition to find potential parallelism rather than using traditional object-oriented decomposition. We shall elaborate on these topics in later chapters, when we examine extended examples and applications. The examples highlight essential features and functionality before proceeding to more advanced topics.

# 29.11 SUMMARY AND CONCLUSIONS

In this chapter we have introduced multitasking and parallel programming using functionality from the C++ Concurrency library. In contrast to low-level threads (introduced in Chapter 28) we took a top-down approach by decomposing a problem into concurrent tasks with the help of data dependency graphs. We trace the full software problem from an initial data dependency graph to an implementation using C++ futures.

We continue in Chapter 30 with an introduction to Microsoft’s PPL, which supports multitasking. In Chapter 32 we show how to apply C++ Concurrency and PPL to improve the speedup of Monte Carlo applications.

# 29.12 QUIZZES, EXERCISES AND PROJECTS

+   1. (Concurrency versus Parallelism, Quiz)
+      Which of the following statements are applicable to concurrency or parallelism (or both)?
+      a) Use of shared resources.
+      b) Goals are correctness, performance (throughput) and robustness.
+      c) Reduce latency (latency is the fixed cost of servicing a request).
+      d) Prevent thread starvation (never allow a program to become idle).
+      e) Concurrency is an optimisation, parallelism is a functional requirement.

+   2. (Data Parallelism versus Task Parallelism, Quiz)
+      Which of the following statements accurately describe data parallelism best and which accurately describe task parallelism?
+      a) Synchronous/asynchronous computation.
+      b) Optimum load balancing/load balancing depending on hardware availability and scheduling algorithms.
+      c) Different operations performed on the same data.
+      d) Degree of parallelisation depends on number of independent tasks/input data size.
+      e) Fewer/more speedup use cases.