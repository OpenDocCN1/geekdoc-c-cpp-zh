
```fortran
!$OMP PARALLEL DO PRIVATE(J,K,...)
      DO J = 1, NGPTOT, NPROMA
         !(calculate offsets, start & end pts. etc.)
         ...
         K = OML_MY_THREAD   ! Includes 1 for MPI-only
         CALL CPG_GP(J, K, ARRAY(1,1,K),...)
         ...
      ENDDO
```

**FIGURE 17.7**

Schematic of a very high-level OpenMP loop in a weather model, which is highly parallel (in the partial coarse-grained sense) but profligate with memory (i.e., not fully coarse-grained) since working array sizes are proportional to thread count.

block simultaneously. This is highly efficient in the parallel sense, but extremely demanding of memory, since memory allocation increases almost in proportion to thread count.

Any “industrial-strength” application that is coded like this invariably runs out of memory before running out of threads on highly parallel, limited-memory platforms such as the Intel Xeon Phi coprocessor. Ideally, such codes should be rewritten to be fully coarse-grained (in the sense used throughout this chapter), in order to fully exploit multi-threaded parallelism within a fixed amount of memory.

One option to restructure the working arrays above would be to drop the third dimension completely (i.e., the OMP_NUM_THREADS dimension, which makes memory consumption directly proportional to thread count), and reorder the first two dimensions so that the declaration looks like:

```
REAL*8 :: ARRAY(NLEV,NPROMA2)
```

Here, NPROMA2 could be optionally much larger than NPROMA, since the OpenMP parallelism will be applied to this dimension. The key point is that once chosen, NPROMA2 is fixed, and does not change with thread count. The OpenMP multi-threading could then “decompose” along this dimension, much as MPI can decompose all the grid-points along a meridian into N subdomains of size NGPTOT.

The main reason to switch the order of the NLEV and NPROMA dimensions is because it is (usually) easier to parallelize over the horizontal NPROMA (or larger NPROMA2) points than over the vertical NLEV points. Physical processes such as radiation and convection, at any given level in the vertical, typically involve interactions with variables at levels immediately above and below. Those interactions introduce dependencies that inhibit parallelization along the vertical dimension.

By the way, the final contents of the working arrays as declared above are ultimately saved to a large pointer-based state structure, which spans all NGPTOT points—but that is not a problem from the multi-threading point of view.

### SUMMARY

This chapter illustrates, with the help of a simple program that performs repeated stencil-type operations, how the performance of simple loop-level or “fine-grained” OpenMP directives can be significantly improved by merging and expanding the OpenMP parallel regions into a single large “coarse-grained” parallel region that spans as much of the code as possible. The technique is not particularly novel, or particularly difficult, but the need for efficient multi-threaded parallelism nested in high-level distributed-memory parallelism (e.g., MPI) is becoming ever more urgent, as high-performance computing platforms evolve more and more into heterogeneous systems with massively parallel hardware components.

As OpenMP directives are moved higher up the call-tree to become more coarse-grained, an important consideration that arises (especially on devices like the Intel Xeon Phi coprocessor where memory is limited) is to avoid excessive memory blow-up due to each thread having its own copy of large private arrays. Such memory blow-up can be prevented by introducing a second-level domain decomposition, whereby each MPI subdomain is further decomposed into a set of “thread-local” sections. While this effectively saves memory, it comes at the price of extra coding complexity and can give rise to inefficiencies such as each thread (within an MPI process) sending its own MPI messages.

Performance tests with the stencil code on both a standard host-node and a coprocessor demonstrate the value of coarse-grained over fine-grained OpenMP and also show the penalty paid (often negligible, but it can be significant) by making the multi-threading fully coarse-grained and introducing the second-level domain decomposition. This effect will vary from application to application, but developers (especially for limited-memory devices such as the coprocessor) should be aware of the propensity of OpenMP to be profligate with memory, and also be aware of the trade-offs involved in managing this.

We can be reasonably confident that the practice of using memory in proportion to thread count must soon come to an end, even though future generations of coprocessors will undoubtedly have a lot more memory (indeed, as much memory as can fit on a host node). The more natural, and more sensible, approach is to select a problem size that fits in available memory, and then independently decompose that among an arbitrary number of threads. In other words, it will be worthwhile for future weather models to use truly coarse-grained OpenMP.

### FOR MORE INFORMATION

Here are some additional reading materials we recommend related to this chapter.

- Herb Sutter’s 2004 article “The Free Lunch Is Over: A Fundamental Turn Towards Concurrency in Software,” http://www.gotw.ca/publications/concurrency-ddj.htm.
- For a nice example of a small coarse-grained OpenMP program, only without MPI, see: http://faculty.washington.edu/rjl/classes/am583s2014/notes/jacobi1d_omp2.html. There is a link to an MPI version on that page too, but no “hybrid” (mixed MPI/OpenMP) version.
- Stencil Code, http://wikipedia.org/wiki/Stencil_code.
- Stencil computation optimization and auto-tuning on state-of-the-art multicore architectures, http://dl.acm.org/citation.cfm?id=1413375
- Download the code from this, and other chapters, http://lotsofcores.com

## EXPLOITING MULTILEVEL PARALLELISM IN QUANTUM SIMULATIONS

Jeongnim Kim, Lawrence Meadows
Intel Corporation, USA

Proper considerations of how to express and use nested parallelism can have a profound impact on performance. This chapter segments this challenge into two parts: nesting of OpenMP within a message passing interface (MPI) program, and then use of nesting within OpenMP itself. This logical decomposition of a program is quite approachable once the concepts are explained in the course of discussing real-world examples.

Using OpenMP within an MPI program has become common. It is especially important when the amount of parallelism at a node level becomes very high. The presence of Intel® Xeon Phi™ coprocessor(s) on a node definitely qualifies as a very high level of parallelism. The coprocessor can be exploited with a handful of MPI ranks, each rank made up of a number of cores from the coprocessor, and each using OpenMP within the rank.

Within an MPI rank, we can utilize OpenMP including its nesting capabilities. OpenMP nesting is turned off by default by most implementations, and is generally considered unsafe by typical users due to concerns of oversubscription and the resulting poor application performance. This chapter shows how properly using nested parallelism can boost performance.

One difference between nested parallelism as defined by OpenMP, and other similar solutions such as Intel Threading Building Blocks (TBB), is that OpenMP truly creates nested teams of threads. TBB (and OpenMP tasking) can have nested tasks, but the tasks themselves are executed by a single team of threads. The use of nested OpenMP thread teams is particularly valuable for modern SMP machines that have hierarchical (e.g., multilevel caches) memory systems. Outer teams can be created at higher levels of the hierarchy (e.g., cores) and inner teams can be created at lower levels of the hierarchy (e.g., hardware thread contexts). This chapter shows how exploiting nested parallelism can also take better advantage of hierarchical machine organization.

### SCIENCE: BETTER APPROXIMATE SOLUTIONS

> “The underlying physical laws necessary for a large part of physics and the whole of chemistry are thus completely known, and the difficulty is only that the exact applications of these laws lead to equations much too complicated to be soluble.”—Dirac, P., 1929. Proc. R. Soc. Lond. 123 (792).
