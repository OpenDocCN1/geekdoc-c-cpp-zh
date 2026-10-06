# 7
Understanding Concurrent Code Design

In this chapter, we will cover the following topics:

+   * How to design parallel applications
* Understanding parallelism in code design
* Turning on to a parallel approach
* Improving the performance factors

# Introduction

Even though synchronization and time are significant factors in developing parallel applications, adding concurrency to programs brings many additional concerns.

Parallel programming can be a sword with two edges: you can do great things with it, such as scaling a program to be executed over up-to-date modern multicore processors. Furthermore, parallelism presents great software capabilities you can develop a responsive and rich user interface in GUI applications. However, you must still be aware of the fact that if parallelism is used incorrectly, it can cause serious performance issues.

Poorly designed parallel programs have worse performance compared to sequential programs because of the overhead that occurs on the CPU while it reschedules the threads for execution, fetches the memory blocks, sets the signaled state on a synchronization object, maintains protection, and so on.