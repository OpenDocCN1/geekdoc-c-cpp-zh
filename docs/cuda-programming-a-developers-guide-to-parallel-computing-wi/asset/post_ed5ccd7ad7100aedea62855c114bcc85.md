
However, over this time, a couple of standards did evolve that we still have today. The OpenMP standard addresses parallelism within a single node and is designed for shared memory machines that contain multicore processors. It does not have any concept of anything outside a single node or box. Thus, you are limited to problems that fit within a single box in terms of processing power, memory capacity, and storage space. Programming, however, is relatively easy as most of the low-level threading code (otherwise written using Windows threads or POSIX threads) is taken care of for you by OpenMP.

The MPI (Message Passing Interface) standard addresses parallelism between nodes and is aimed at clusters of machines within well-defined networks. It is often used in supercomputer installations where there may be many thousands of individual nodes. Each node holds a small section of the problem. Thus, common resources (CPU, cache, memory, storage, etc.) are multiplied by the number of nodes in the network. The Achilles’ heel of any network is the various interconnects, the parts that connect the networked machines together. Internode communication is usually the dominating factor determining the maximum speed in any cluster-based solution.

Both OpenMP and MPI can be used together to exploit parallelism within nodes as well as across a network of machines. However, the APIs and the approaches used are entirely different, meaning they are often not used together. The OpenMP directives allow the programmer to take a high-level view of parallelism via specifying parallel regions. MPI by contrast uses an explicit interprocess communication model making the programmer do a lot more work.

Having invested the time to become familiar with one API, programmers are often loath to learn another. Thus, problems that fit within one computer are often implemented with OpenMP solutions, whereas really large problems are implemented with cluster-based solutions such as MPI.

CUDA, the GPU programming language we’ll explore in this text, can be used in conjunction with both OpenMP and MPI. There is also an OpenMP-like directive version of CUDA (OpenACC) that may be somewhat easier for those familiar with OpenMP to pick up. OpenMP, MPI, and CUDA are increasingly taught at undergraduate and graduate levels in many university computer courses.

However, the first experience most serial programmers had with parallel programming was the introduction of multicore CPUs. These, like the parallel environments before them, were largely ignored by all but a few enthusiasts. The primary use of multicore CPUs was for OS-based parallelism. This is a model based on task parallelism that we’ll look at a little later.

As it became obvious that technology was marching toward the multicore route, more and more programmers started to take notice of the multicore era. Almost all desktops ship today with either a dual- or quad-core processor. Thus, programmers started using threads to allow the multiple cores on the CPU to be exploited.

A thread is a separate execution flow within a program that may diverge and converge as and when required with the main execution flow. Typically, CPU programs will have no more than twice the number of threads active than the number of physical processor cores. As with single-core processors, typically each OS task is time-sliced, given a small amount of time in turn, to give the illusion of running more tasks than there are physical CPU cores.

However, as the number of threads grows, this becomes more obvious to the end user. In the background the OS is having to context switch (swap in and out a set of registers) every time it needs to switch between tasks. As context switching is an expensive operation, typically thousands of cycles, CPU applications tend to have a fairly low number of threads compared with GPUs.

## SERIAL/PARALLEL PROBLEMS

Threads brought with them many of the issues of parallel programming, such as sharing resources. Typically, this is done with a semaphore, which is simply a lock or token. Whoever has the token can use the resource and everyone else has to wait for the user of the token to release it. As long as there is only a single token, everything works fine.

Problems occur when there are two or more tokens that must be shared by the same threads. In such situations, thread 0 grabs token 0, while thread 1 grabs token 1. Thread 0 now tries to grab token 1, while thread 1 tries to grab token 0. As the tokens are unavailable, both thread 0 and thread 1 sleep until the token becomes available. As neither thread ever releases the one token they already own, all threads wait forever. This is known as a deadlock, and it is something that can and will happen without proper design.

The opposite also happens—sharing of resources by chance. With any sort of locking system, all parties to a resource must behave correctly. That is, they must request the token, wait if necessary, and, only when they have the token, perform the operation. This relies on the programmer to identify shared resources and specifically put in place mechanisms to coordinate updates by multiple threads. However, there are usually several programmers in any given team. If just one of them doesn't follow this convention, or simply does not know this is a shared resource, you may appear to have a working program, but only by chance.

One of the projects I worked on for a large company had exactly this problem. All threads requested a lock, waited, and updated the shared resource. Everything worked fine and the particular code passed quality assurance and all tests. However, in the field occasionally users would report the value of a certain field being reset to 0, seemingly randomly. Random bugs are always terrible to track down, because being able to consistently reproduce a problem is often the starting point of tracking down the error.

An intern who happened to be working for the company actually found the issue. In a completely unrelated section of the code a pointer was not initialized under certain conditions. Due to the way the program ran, some of the time, depending on the thread execution order, the pointer would point to our protected data. The other code would then initialize “its variable” by writing 0 to the pointer, thus eliminating the contents of our “protected” and thread-shared parameter.

This is one of the unfortunate areas of thread-based operations; they operate with a shared memory space. This can be both an advantage in terms of not having to formally exchange data via messages, and a disadvantage in the lack of protection of shared data.

The alternative to threads are processes. These are somewhat heavier in terms of OS load in that both code and data contexts must be maintained by the OS. A thread by contrast needs to only maintain a code context (the program/instruction counter plus a set of registers) and shares the same data space. Both threads and processes may be executing entirely different sections of a program at any point in time.

Processes by default operate in an independent memory area. This usually is enough to ensure one process is unable to affect the data of other processes. Thus, the stray pointer issue should result in an exception for out-of-bounds memory access, or at the very least localize the bug to the particular process. Data consequently has to be transferred by formally passing messages to or from processes.

In many respects the threading model sits well with OpenMP, while the process model sits well with MPI. In terms of GPUs, they map to a hybrid of both approaches. CUDA uses a grid of blocks. This can be thought of as a queue (or a grid) of processes (blocks) with no interprocess communication. Within each block there are many threads which operate cooperatively in batches called warps.

We will look at this further in the coming chapters.

## CONCURRENCY

The first aspect of concurrency is to think about the particular problem, without regard for any implementation, and consider what aspects of it could run in parallel.

If possible, try to think of a formula that represents each output point as some function of the input data.

This may be too cumbersome for some algorithms, for example, those that iterate over a large number of steps. For these, consider each step or iteration individually. Can the data points for the step be represented as a transformation of the input dataset? If so, then you simply have a set of kernels (steps) that run in sequence. These can simply be pushed into a queue (or stream) that the hardware will schedule sequentially.

A significant number of problems are known as “embarrassingly parallel,” a term that rather understates what is being achieved. If you can construct a formula where the output data points can be represented without relation to each other—for example, a matrix multiplication—be very happy. These types of problems can be implemented extremely well on GPUs and are easy to code.

If you or more steps of the algorithm can be represented in this way, but maybe one stage cannot, also be very happy. This single stage may turn out to be a bottleneck and may require a little thought, but the rest of the problem will usually be quite easy to code on a GPU.

If the problem requires every data point to know about the value of its surrounding neighbors then the speedup will ultimately be limited. In such cases, throwing more processors at the problem works up to a point. At this point the computation slows down due to the processors (or threads) spending more time sharing data than doing any useful work. The point at which you hit this will depend largely on the amount and cost of the communication overhead.

CUDA is ideal for an embarrassingly parallel problem, where little or no interthread or interblock communication is required. It supports interthread communication with explicit primitives using on-chip resources. Interblock communication is, however, only supported by invoking multiple kernels in series, communicating between kernels running on off-chip global memory. It can also be performed in a somewhat restricted way through atomic operations to or from global memory.

CUDA splits problems into grids of blocks, each containing multiple threads. The blocks may run in any order. Only a subset of the blocks will ever execute at any one point in time. A block must execute from start to completion and may be run on one of N SMs (symmetrical multiprocessors). Blocks are allocated from the grid of blocks to any SM that has free slots. Initially this is done on a round-robin basis so each SM gets an equal distribution of blocks. For most kernels, the number of blocks needs to be in the order of eight or more times the number of physical SMs on the GPU.

To use a military analogy, we have an army (a grid) of soldiers (threads). The army is split into a number of units (blocks), each commanded by a lieutenant. The unit is split into squads of 32 soldiers (a warp), each commanded by a sergeant (See Figure 2.1).
