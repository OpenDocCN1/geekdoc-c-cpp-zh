to obtain application speedup in the modern programming world. In most cases, multiple independent chains of dependent tasks offer the best opportunity for parallelization.

# Parallel execution

![](bbox=[0.09, 0.19, 0.53, 0.41])

FIGURE 1-3

# Parallelism

Nowadays, parallelism is becoming ubiquitous, and parallel programming is becoming mainstream in the programming world. Parallelism at multiple levels is the driving force of architecture design. There are two fundamental types of parallelism in applications:

+   - Task parallelism
- Data parallelism

Task parallelism arises when there are many tasks or functions that can be operated independently and largely in parallel. Task parallelism focuses on distributing functions across multiple cores.

Data parallelism arises when there are many data items that can be operated on the same time. Data parallelism focuses on distributing the data across multiple cores.

CUDA programming is especially well-suited to address problems that can be expressed as data-parallel computations. The major focus of this book is how to solve a data-parallel problem with CUDA programming. Many applications that process large data sets use a data-parallel model to speed up the computations. Data-parallel processing maps data elements to threads.

The first step in designing a data parallel program is to partition data across threads, with thread working on a portion of the data. In general, there are two approaches to partitioning: block partitioning and cyclic partitioning. In block partitioning, consecutive elements of data are chunked. Each chunk is assigned to a single thread in order, and threads generally process only one chunk at a time. In cyclic partitioning, fewer data elements are chunked together. Neighboring threads receive neighboring chunks, and each thread can handle more than one chunk. Selecting a new chunk for a thread to process implies jumping ahead as many chunks as there threads.