# 8

# Basics of Parallel Programming

Today, almost all computer systems, including embedded and mobile systems, are equipped with multicore microprocessors – not to mention graphics programming units (GPUs), which are equipped with thousands of cores. However, all the programs we have written and analyzed until now perform sequentially. That is, although we have multiple functions and calls between them, a microprocessor sequentially processes only one instruction at a time. This does not seem like the most efficient way to use the available hardware resources. Before we go into detail, let’s summarize the main topics we will learn about in this chapter:

+   - Basic concepts of parallel computations
+   - What concurrent multitasking and threads are
+   - The risk of using shared objects, and how to protect their access
+   - How to make standard algorithms like `std::transform`, `std::sort`, and `std::transform_reduce` operate in a parallel mode
+   - Programming asynchronous tasks with `std::future`
+   - Basic construction of the OpenMP library – e.g. how to launch and synchronize multiple tasks, and how to make `for` operate in parallel to significantly speed up matrix multiplication

# 8.1  Basic Concepts of Parallel Computations

Since an example is better than a hundred words, let’s start by analyzing the behavior of a simple function `Task_0` run simultaneously on two threads (later, we will show what a thread is and how to make code run on multiple threads). Let’s also assume that `Task_0` accesses a global variable x. The situation is outlined in Figure 8.1.

After launching the two threads, each running the same `Task_0`, the output may look like the following

```
0, 10
5, 10
```