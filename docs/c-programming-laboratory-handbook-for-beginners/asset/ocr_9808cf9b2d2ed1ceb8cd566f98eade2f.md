# # Term-Work 14

# ## Problem Definition

Design, develop and execute a parallel program in C to determine and print prime numbers which are less than 100 making use of the algorithm of the Sieve of Eratosthenes.

# ## Objectives

+   - To learn the concept of parallel programming and functions.
+   - To understand the underlying logic to find prime numbers using Sieve of Eratosthenes of algorithm and write a program for the same.

# ## Prerequisites for Coding

# ### OpenMP (Open Multi-Processing)

**OpenMP** (Open Multi-Processing) is an API (application programming interface) that supports multi-platform shared memory multiprocessing programming in C, C++, and Fortran, on most processor architectures and operating systems, including Linux, Unix, AIX, Solaris, Mac OS X, and Microsoft Windows platforms. It consists of a set of compiler directives, library routines, and environment variables that influence run-time behavior. OpenMP uses a portable, scalable model that gives programmers a simple and flexible interface for developing parallel applications for platforms ranging from the standard desktop computer to the supercomputer.

# ### Directives

+   - `#pragma omp parallel for`
+   - The parallel construct forms a team of threads and starts parallel execution.
+   - `#pragma omp parallel for [clause[[,] clause] ...]` new-line
+   - for-loop

An OpenMP executable directive applies to the succeeding structured block or an OpenMP Construct. A “structured block” is a single statement or a compound statement with a single entry at the top and a single exit at the bottom.