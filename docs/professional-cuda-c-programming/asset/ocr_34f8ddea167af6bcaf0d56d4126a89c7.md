# IS CUDA C PROGRAMMING DIFFICULT?

The main difference between CPU programming and GPU programming is the level of programmer exposure to GPU architectural features. Thinking in parallel and having a basic understanding of GPU architecture enables you to write parallel programs that scale to hundreds of cores as easily as you write a sequential program.

If you want to write efficient code as a parallel programmer, you need a basic knowledge of CPU architectures. For example, locality is a very important concept in parallel programming. Locality refers to the reuse of data and/or to reduce memory latency. There are two basic types of reference locality. Temporal locality refers to the reuse of data within relatively small time durations. Modern GPU architectures use large caches to optimize for applications with good spatial and temporal locality. It is the programmer's responsibility to design their algorithm to efficiently use CPU cache. Programs must handle low-level cache optimizations, but no introspection into how threads are scheduled on the underlying architecture because the CPU does not expose that.

CUDA exposes you to the concepts of both memory hierarchy and thread hierarchy, extending your ability to control execution and scheduling to a greater degree, using:

+   - Memory hierarchy structure
- Thread hierarchy structure

For example, a special memory, shared memory, is exposed by the CUDA programming model. Shared memory can be thought of as a software-managed cache, which provides great speed by conserving bandwidth to main memory. With shared memory, you can control the locality of your code.

When writing a program in ANSI C, you need to explicitly organize your threads with either pthreads or OpenMP, two well-known techniques to support parallel programming on most processor architectures and operating systems. When writing a program in CUDA, you actually just a piece of serial code to be called by only one thread. The GPU makes it parallel by launching thousands of threads, all performing that computation. The CUDA programming model provides you with a way to organize your threads hierarchy. Managing this organization directly affects the order in which threads are executed on the GPU. Because CUDA is an extension of C, it is often straightforward to port C programs to CUDA C. Conceptually, peeling off the loops of your code yields the kernel code for a CUDA C implementation.

CUDA abstracts the hardware details and does not require applications to be mapped to traditional graphics APIs. At its core are three abstractions: a hierarchy of thread groups, a hierarchy