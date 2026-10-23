
so the current matrix can be safely changed.) The columns with index j for which v_j = 0 in the previous exercise should be dropped using the "maskItems(v)" function of Chapter 3, Section 3.7 (applied to each row). Then, the column indices should be renumbered according to their number in c, using the "renumberColumns(v)" function in Chapter 16, Section 3. The "createTransfer" function also returns the matrix R = P^t as output. The solution can be found in Section A.18 of the Appendix.

7. Modify the "createTransfer" function of the previous exercise so that it constructs the matrix P of the AMG algorithm in Section 17.9 and returns its transpose R = P^t. The solution can be found in Section A.18 of the Appendix.

8. Implement the PCG algorithm to accelerate the basic multigrid iteration. Use the "sparseMatrix" and "dynamicVector" classes. The solution can be found in Section A.19 of the Appendix.

9. Show that, for every real matrix A, A^t A is SPD. Conclude that PCG is applicable to the normal equations provided that an SPD preconditioner is used.

10. Modify your PCG code to apply to complex systems as well by making sure that the inner product of two complex vectors v and w is defined by

(v, w) ≡ v^t \bar{w}

in the '*' operator in the "dynamicVector" class.

11. Rewrite your PCG code as a template function that is also suitable for systems with a complex coefficient matrix of type "sparseMatrix<complex>". The solution can be found in Section A.19 of the Appendix.

12. Show that, for a complex matrix A, A* A is the Hermitian adjoint of itself and is also positive definite. Conclude that PCG is applicable to the normal equation

A* A x = A* f,

provided that the preconditioner is also the Hermitian adjoint of itself and positive definite.

## Chapter 18

## Towards Parallelism

In this chapter, we describe parallel computers and parallelizable algorithms. In particular, we consider parallel architectures with distributed memory and a hypercube communication network. We also introduce a fair method of comparing parallel and sequential computers for a particular computational problem. We illustrate how this comparison method works for the numerical solution of SPD large sparse linear systems. Finally, we explain how the parallel implementation should take place in the low-level C++ code.

### 18.1 Parallel vs. Sequential Computers

When the digital computer was first invented in the 1950s, there seemed to be no computational task it couldn’t do: from data management, through arithmetic calculations, to numerical modeling of real physical phenomena. The computational problems in those days, however complicated for the human mind, were easy enough for the machine. The scale of a problem (number of degrees of freedom or unknowns) used to be a few thousand at most. Such small-scale problems were no challenge even for the early computer, which could perform thousands of arithmetic operations per second.

As time went by, the computational power of the digital computer increased. Modern computers can perform millions of arithmetic operations per second, and supercomputers can perform even billions of arithmetic operations per second. However, the scale of computational problems has increased as well. Modern problems in numerical modeling, from weather forecasting to nuclear simulations, may contain millions of degrees of freedom. However efficient the algorithms that solve these problems may be, their complexity (operation count) still grows superlinearly with the scale of the problem. This means that even modern computers may not be sufficiently powerful to solve them in acceptable time.

The traditional computer is sequential in the sense that it can perform only one operation at a time. This is why its computational power, however large, may still be insufficient for solving large-scale problems. This drawback motivated the introduction of the parallel computer, which can perform more than one operation at a time.

The main difference between sequential and parallel computers is in terms of the number of processors available to carry out computations. The sequential computer contains

three basic elements: memory to store data, a single processor to carry out calculations, and input/output devices to communicate with other sources of data. One processor can only do one thing at a time, be it data fetching, arithmetic operation, or data update. The parallel computer, on the other hand, contains more than one processor, so it may perform several operations at a time. Each processor must have access to the memory and input/output (I/O) devices. Thus, the parallel computer has a better chance of solving the original problem in acceptable time.

### 18.2 Parallelizable Algorithms

Computational problems are solved by an algorithm: a list of instructions that should be completed one by one. This list of instructions is often so long that it could never be completed by a human; a digital computer must be used.

Thus, the algorithm must be written in context-free formal language, which can be understood by the computer with no ambiguity. For this purpose, it must be written in a high-level programming language. This is called implementation. On parallel computers, however, the implementation may be different from that used on sequential ones, to exploit better the extra computational power they offer.

In order to have good parallel implementation, the nature of the algorithm must first be studied and well understood. In particular, some instructions in the algorithm are independent of each other and can be carried out concurrently. We then say that the algorithm is parallelizable: it can benefit from parallel implementation, in which different processors work on different instructions at the same time [56]. We say that an algorithm is well parallelizable if the most time-consuming instructions in it are indeed independent of each other and can be completed in parallel.

### 18.3 Inherently Sequential Algorithms

Some algorithms, however, are inherently sequential in that the most time-consuming instructions cannot be carried out at the same time. For example, if each instruction uses data computed in the previous one, then the original, sequential order of the instructions must be kept. Such algorithms cannot benefit from parallel computers. In fact, the traditional sequential computer may complete them as rapidly as the parallel computer, thanks to its straightforward and efficient architecture.

### 18.4 Architecture

The architecture of a computer is the way basic elements are organized in it and connected to each other. Obviously, the three basic elements in the computer must be connected to each other: the processor must be connected to the memory to fetch and update data and, most importantly, obtain instructions from the file containing the executable program. Furthermore, the processor must also be connected to the I/O devices to exchange data with the user. The memory, however, doesn’t have to be connected directly to the I/O devices, because all required communication can be carried out through the processor.

Actually, the memory is split into two parts: primary memory and secondary memory. The primary memory is small but easily accessed, so data that are used often are better stored

in it. The secondary memory, on the other hand, is big but not easily accessed, so it should contain files and other data that are not frequently used. When a process is executed, data are stored temporarily in the primary memory, where they are available for further use. Once the process terminates, its output is placed in its permanent address in the secondary memory.

It is thus advisable to access the secondary memory only when necessary. Data that have already been placed in the primary memory should be exploited as much as possible before being returned to the secondary memory.

The primary memory is sometimes called the cache, because data are stored in it as in an easily accessed cache. Actually, the cache may be divided into several levels, from the most easily accessed cache in the highest level to the least easily accessed cache at the lowest level. It is advisable to store data in the cache according to the number of times they are expected to be used: often-used data should be stored in the highest level, whereas rarely used data should be stored in the lowest level.

### 18.5 Cache-Oriented Relaxation

The following algorithms are designed with cache in mind; that is, they exploit the cache fully and avoid accessing the secondary memory, if possible.

A cache-oriented algorithm is an algorithm that is specifically designed to exploit the cache in full and minimize access to the secondary memory. The principle is to carry out as many useful calculations as possible with data that are already available in the cache before returning them to their permanent location in the secondary memory. In what follows, we describe a cache-oriented version of the Gauss–Seidel relaxation method in [28].

The standard Gauss–Seidel relaxation is not cache oriented in the sense that it cannot be implemented efficiently in terms of cache use. Indeed, the unknowns are relaxed one by one in the order in which they are stored in the vector of unknowns. The relaxation of each particular unknown uses the values calculated before in the relaxation of previous unknowns. The value calculated at the relaxation of a particular unknown cannot be stored in the primary memory for long: it must be transferred to the secondary memory to make room for the unknowns to be relaxed next. The result is too many accesses to the secondary memory, without fully exploiting values that are calculated in the current relaxation sweep and are available in the cache.

The cache-oriented version of the Gauss–Seidel relaxation, which fully uses data that are already in the cache, is as follows. First, divide the vector of unknowns into chunks that fit in the cache. For example, if the number of unknowns is 1000 and the cache can contain the data required to relax 256 unknowns, then divide the vector of unknowns into four chunks of 250 unknowns each. Then, transfer from the secondary memory to the cache the data required to relax the unknowns in the first chunk. Then, do as many relaxations as possible on the unknowns in this chunk (or at least most of them), to make full use of their updated values, which are already in the cache. In each of these relaxations, use the newest values available from the previous relaxation in this chunk. Then, place the newest values calculated for the unknowns in this chunk back in the secondary memory, and repeat the same procedure in the next chunk (containing the next 250 unknowns). Then, because there are probably unknowns at the interface between chunks that have not yet been relaxed enough times, repeat the same procedure in the intermediate chunk that contains the 250 unknowns from the 126th unknown to the 375th unknown. The procedure is repeated in
